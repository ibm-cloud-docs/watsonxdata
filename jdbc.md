---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-13"

keywords: lakehouse, watsonx.data, presto, cli

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# JDBC pushdown
{: #jdbc_publicpreview}

IBM Presto can push down the processing of join queries or part of join queries into the connected JDBC data source.

## Join operation
{: #join_publicpreview}

Presto transforms join queries into a specific internal representation (join operation) called a 'PlanNode'. By effectively using join operation and query optimization techniques, Presto performs complex join queries efficiently.

### Join pushdown
{: #joinpush_publicpreview}

Presto allows the connector to delegate the 'Join operation (PlanNode)' to the underlying JDBC data source. The connector should be able to process the join predicate at the data source level. This process, which is known as 'join pushdown', significantly improves query performance.

### Query optimization
{: #queryop_publicpreview}

Presto analyzes join queries to create an optimal 'Join operation (PlanNode)'. This optimisation process involves inferencing and restructuring the query to improve performance.

The following are some examples for Presto inferencing which makes structural difference in join query:

| Presto inferencing           | User provided query        | Result of query inferencing        |
 |------------------|--------------------|--------------------|
 | Inferencing to remove join condition    | select * from postgresql.pg.mypg_table1 t1 \n join postgresql.pg.mypg_table2 t2 on \n t1.pgfirsttablecolumn=t2.pgsecondtablecolumn \n where t1.pgfirsttablecolumn=100 | select * from postgresql.pg.mypg_table1 \n t1,postgresql.pg.mypg_table2 t2 where \n t1.pgfirsttablecolumn=100 and \n t2.pgfirsttablecolumn=100  |
 | Inferencing to create inner join from right, left or cross join            | SELECT e.first_name_varchar, \n p.project_name_varchar, p.risk_level_tinyint \n FROM mysql.tm_lakehouse_engine_db_1.employee \n e CROSS JOIN \n mysql.tm_lakehouse_engine_db_1.projects p \n WHERE e.age_tinyint > p.risk_level_tinyint;  | SELECT e.first_name_varchar, \n p.project_name_varchar, \n p.risk_level_tinyint FROM \n mysql.tm_lakehouse_engine_db_1.employee \n e , \n mysql.tm_lakehouse_engine_db_1.projects \n p WHERE e.age_tinyint > \n p.risk_level_tinyint; |
 {: caption="Presto inferencing" caption-side="bottom"}

The left joins and right joins may be internally converted into inner joins and may get pushed down toward a specific connector. Also, there exists a case where the inner joins may not get pushed down toward a specific connector due to some conditions.
{: note}

## Key considerations for Join query pushdown in Presto JDBC data source
{: #keycons_publicpreview}

Presto validates 'join operation(PlanNode)' specifications to perform 'join pushdown'. These specifications vary for each data source and connector. However, the following are some generic conditions to be met for a `join` to be pushed down in a JDBC connector.

* Connector Support: The JDBC connector must be able to process the join operation. Complex operations involving Presto functions or operators may prevent pushdown.
* Join Type and Conditions: The join should typically be an inner join with at least one common column between the tables. The join conditions should involve compatible data types and operators.
* Database Compatibility: The underlying database must support the specific join operation and data types involved. For more information, see Data types and operators that support join pushdown feature.
* Table Grouping: Tables from the same connector and meeting the required criteria can be grouped for pushdown.
* Configuration: Join pushdown is typically enabled through a global configuration flag. The flag for global setting is tech preview specific and the default value is enable-join-query-pushdown=false. You can set the global flag as enable-join-query-pushdown=true in custom-config.properties through the backend and restart the Presto server. After enabling the flag, you can pushdown equi-join and non-equi-join queries.
* Configuration: Join pushdown is controlled using a combination of session-level properties.

To enable join pushdown, set the following session flags:

Enables pushdown to eligible data sources but will only work for equi-joins (joins with equality conditions)

   ```bash
SET SESSION optimizer_inner_join_pushdown_enabled = true;
   ```
   {: codeblock}

Enables pushdown for non-equi joins (joins with inequality or range-based conditions) to eligible data sources. Needs to be set to true along with the above flag.

   ```bash
SET SESSION optimizer_inequality_join_pushdown_enabled = true;
   ```
   {: codeblock}

Enables partial predicate pushdown at the catalog level. This allows pushing down applicable filter conditions to the data source along with join clauses.

   ```bash
SET SESSION <catalogName>.partial_predicate_push_down = true;
   ```
   {: codeblock}

For example,
   ```bash
SET SESSION postgresql.partial_predicate_push_down = true;
   ```
   {: screen}

While this is not mandatory, it is recommended, as certain queries rely on this flag for pushdown to be effective.

For example, when you use some aggregate, math operation or data type conversion along with join query, it is converted to Presto functions and applied to 'join' operation. For any 'join' query that creates intermediate Presto function, that query cannot be handled by the connector and hence push down is not performed.

| Example           | Query        |
 |------------------|--------------------|
 | For query which creates Presto function    | `abs(int_clumn)=int_column2;` \n `int_sum_column=int_value1_column1+int_value1_column2` \n `cast(varchar_20_column, varchar(100) )=varchar100_column` |
 {: caption="Query example" caption-side="bottom"}

## Verifying join pushdown
{: #keycons_publicpreview}

To check whether a join query has been pushed down to the underlying data source, you can examine the query's EXPLAIN plan.

Consider the following points to verify whether a join query has been pushed down to the underlying data source:
* If the plan does not show a 'join' operator, it means that a complete pushdown happened.
* If there is less number of join operators than original join query, it means that partial pushdown happened.
* If the number of join operators is same as original query, it means that no pushdown happened.

The following example explains the verifying join pushdown results:

**Join query:**
   ```bash
SELECT order_id, c_customer_id FROM postgresql.public.orders o INNER JOIN postgresql.public.customer c ON c.c_customer_id=o.customer_id;
   ```
   {: codeblock}

**Original Presto plan:**
   ```bash
- Output[PlanNodeId 9][order_id, c_customer_id] => [order_id:integer, c_customer_id:char(16)]
    - RemoteStreamingExchange[PlanNodeId 266][GATHER] => [order_id:integer, c_customer_id:char(16)]
        - InnerJoin[PlanNodeId 4][(""customer_id"" = ""c_customer_id"")][$hashvalue, $hashvalue_11] => [order_id:integer, c_customer_id:char(16)]
                Distribution: PARTITIONED
            - RemoteStreamingExchange[PlanNodeId 264][REPARTITION][$hashvalue] => [customer_id:char(16), order_id:integer, $hashvalue:bigint]
                    Estimates: {source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: ?}
                - ScanProject[PlanNodeId 0,326][table = TableHandle {connectorId='postgresql', connectorHandle='JdbcTableHandle{connectorId=postgresql, schemaTableName=public.orders, catalogName=null, schemaName=public, tableName=orders, joinTables=Optional.empty}', layout='Optional[{domains=ALL, additionalPredicate={}}]'}, projectLocality = LOCAL] => [customer_id:char(16), order_id:integer, $hashvalue_10:bigint]
                        Estimates: {source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: 0.00}/{source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: 0.00}
                        $hashvalue_10 := combine_hash(BIGINT'0', COALESCE($operator$hash_code(customer_id), BIGINT'0')) (3:6)
                        LAYOUT: {domains=ALL, additionalPredicate={}}
                        order_id := JdbcColumnHandle{connectorId=postgresql, columnName=order_id, jdbcTypeHandle=JdbcTypeHandle{jdbcType=4, jdbcTypeName=int4, columnSize=10, decimalDigits=0, arrayDimensions=null}, columnType=integer, nullable=true, comment=Optional.empty} (3:6)
                        customer_id := JdbcColumnHandle{connectorId=postgresql, columnName=customer_id, jdbcTypeHandle=JdbcTypeHandle{jdbcType=1, jdbcTypeName=bpchar, columnSize=16, decimalDigits=0, arrayDimensions=null}, columnType=char(16), nullable=true, comment=Optional.empty} (3:6)
            - LocalExchange[PlanNodeId 297][HASH][$hashvalue_11] (c_customer_id) => [c_customer_id:char(16), $hashvalue_11:bigint]
                    Estimates: {source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: ?}
                - RemoteStreamingExchange[PlanNodeId 265][REPARTITION][$hashvalue_12] => [c_customer_id:char(16), $hashvalue_12:bigint]
                        Estimates: {source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: ?}
                    - ScanProject[PlanNodeId 1,327][table = TableHandle {connectorId='postgresql', connectorHandle='JdbcTableHandle{connectorId=postgresql, schemaTableName=public.customer, catalogName=null, schemaName=public, tableName=customer, joinTables=Optional.empty}', layout='Optional[{domains=ALL, additionalPredicate={}}]'}, projectLocality = LOCAL] => [c_customer_id:char(16), $hashvalue_13:bigint]
                            Estimates: {source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: 0.00}/{source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: 0.00}
                            $hashvalue_13 := combine_hash(BIGINT'0', COALESCE($operator$hash_code(c_customer_id), BIGINT'0')) (4:12)
                            LAYOUT: {domains=ALL, additionalPredicate={}}
                            c_customer_id := JdbcColumnHandle{connectorId=postgresql, columnName=c_customer_id, jdbcTypeHandle=JdbcTypeHandle{jdbcType=1, jdbcTypeName=bpchar, columnSize=16, decimalDigits=0, arrayDimensions=null}, columnType=char(16), nullable=true, comment=Optional.empty} (4:12)
   ```
   {: codeblock}

**Pushdown Presto plan:**
   ```bash
- Output[PlanNodeId 9][order_id, c_customer_id] => [order_id:integer, c_customer_id:char(16)]
        Estimates: {source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: ?}
    - RemoteStreamingExchange[PlanNodeId 261][GATHER] => [order_id:integer, c_customer_id:char(16)]
            Estimates: {source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: ?}
        - TableScan[PlanNodeId 287][TableHandle {connectorId='postgresql', connectorHandle='JdbcTableHandle{connectorId=postgresql, schemaTableName=public.orders, catalogName=null, schemaName=public, tableName=orders, joinTables=Optional[[JdbcTableHandle{connectorId=postgresql, schemaTableName=public.orders, catalogName=null, schemaName=public, tableName=orders, joinTables=Optional.empty}, JdbcTableHandle{connectorId=postgresql, schemaTableName=public.customer, catalogName=null, schemaName=public, tableName=customer, joinTables=Optional.empty}]]}', layout='Optional[{domains=ALL, additionalPredicate={}}]'}] => [customer_id:char(16), order_id:integer, c_customer_id:char(16)]
                Estimates: {source: CostBasedSourceInfo, rows: ? (?), cpu: ?, memory: 0.00, network: 0.00}
                LAYOUT: {domains=ALL, additionalPredicate={}}
                c_customer_id := JdbcColumnHandle{connectorId=postgresql, columnName=c_customer_id, jdbcTypeHandle=JdbcTypeHandle{jdbcType=1, jdbcTypeName=bpchar, columnSize=16, decimalDigits=0, arrayDimensions=null}, columnType=char(16), nullable=true, comment=Optional.empty} (4:12)
                customer_id := JdbcColumnHandle{connectorId=postgresql, columnName=customer_id, jdbcTypeHandle=JdbcTypeHandle{jdbcType=1, jdbcTypeName=bpchar, columnSize=16, decimalDigits=0, arrayDimensions=null}, columnType=char(16), nullable=true, comment=Optional.empty} (3:6)
                order_id := JdbcColumnHandle{connectorId=postgresql, columnName=order_id, jdbcTypeHandle=JdbcTypeHandle{jdbcType=4, jdbcTypeName=int4, columnSize=10, decimalDigits=0, arrayDimensions=null}, columnType=integer, nullable=true, comment=Optional.empty} (3:6)
   ```
   {: codeblock}


## Conditions to enable JDBC join pushdown
{: #keycons_publicpreview}

JDBC join pushdown makes queries run faster, sometimes up to 10 times faster. However, it is important to use it carefully. If used incorrectly, it may slow down query processing.

The following are the key considerations to enable JDBC join pushdown:

* If you have only a limited number of records as the join operation results from huge tables:
   * The join should return a relatively small subset of records from large tables.
   * Ideal join conditions typically return less than 10% of the total records.

* Avoid Cross Joins:
   * If the join criteria lead to cross-join result, then you should not use join pushdown capabilities. Cross joins (which produce the Cartesian product of two tables) can degrade the performance.

* Database Optimization:
   * The database system should be optimized to handle join queries efficiently, especially non-equi-joins. Presto is able to perform join pushdown for equi-join condition (=) and for non-equi-join conditions (<, >, <=, >=, !=, <>). Almost every database is able to handle the equi-join effectively. But not all databases are optimized for non-equi-join conditions.

* Aggregation:
   * Only select queries are pushed down. A query which does aggregation (For example, select count()) is not pushed down and may affect the performance.

You can see performance gains as the number of rows of the table increase and the join result restrict to less than 10% of total records. See the following statistics to understand the behavior:

| Join query           | Join query        | Performance improvement        |
 |------------------|--------------------|--------------------|
 | SELECT A.ASSIGNMENT_ID, A.ROLE, \n A.IS_CURRENT, B.ASSIGNMENT_ID, \n B.DEFAULT_INT FROM \n DB2.DB2.ASSIGNMENTS A JOIN \n DB2.DB2.STUDENT B ON \n A.ASSIGNMENT_ID = B.ASSIGNMENT_ID;    | When Joining tables: \n ASSIGNMENTS with 10 million rows and \n STUDENT with 5000 rows \n Join Result is 50 rows. | 5x  |
 | SELECT A.ASSIGNMENT_ID, A.ROLE, \n A.IS_CURRENT, B.ASSIGNMENT_ID, \n B.DEFAULT_INT FROM \n DB2.DB2.ASSIGNMENTS A JOIN \n DB2.DB2.STUDENT B ON \n A.ASSIGNMENT_ID = B.ASSIGNMENT_ID;    | When Joining tables: \n ASSIGNMENTS with 20 million rows and \n STUDENT with 5000 rows \n Join Result is 50 rows. | 10x  |
 {: caption="Presto inferencing" caption-side="bottom"}

The statistics that are shown in the table is an approximate example, there is a chance of value variations based on the database and environment.
{: note}

## Data types and operators that support join pushdown
{: #datatypes_publicpreview}

The following data types and operators support join pushdown feature:

| Data types           | Operators        |
 |------------------|--------------------|
 | [BigInt](https://prestodb.io/docs/current/language/types.html#bigint)    | = , <, >, <=, >= , != and <> |
 | [Boolean](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.0.x?topic=presto-data-types#datatypes__boolean)            | =, !=, <>  |
 | [Integer](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.0.x?topic=presto-data-types#datatypes__integer)            | = , <, >, <=, >= , != and <>  |
 | [TINYINT](https://prestodb.io/docs/current/language/types.html#tinyint)            | = , <, >, <=, >= , != and <>  |
 | [SMALLINT](https://prestodb.io/docs/current/language/types.html#smallint)            | = , <, >, <=, >= , != and <>  |
 | [Floating-point](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.0.x?topic=presto-data-types#datatypes__float)            | = , <, >, <=, >= , != and <>  |
 | [REAL](https://prestodb.io/docs/current/language/types.html#real)            | = , <, >, <=, >= , != and <>  |
 | [DOUBLE](https://prestodb.io/docs/current/language/types.html#double)             | = , <, >, <=, >= , != and <> |
 | [DECIMAL](https://prestodb.io/docs/current/language/types.html#decimal)   | = , <, >, <=, >= , != and <> |
 | [VARCHAR](https://prestodb.io/docs/current/language/types.html#varchar)     | = , <, >, <=, >= , != and <> |
 | [CHAR](https://prestodb.io/docs/current/language/types.html#char) | = , <, >, <=, >= , != and <> |
 {: caption="Supported data types" caption-side="bottom"}

## Federated join pushdown
{: #federatedjoin_publicpreview}

A federated join is a join query which contains tables from multiple catalogs.

In a federated join, Presto groups tables based on their JDBC catalog to optimize pushdown. However, pushdown is only possible if:

* JDBC data source: The tables are from a JDBC data source.
* Pushdown specifications: The join operation meets the specific requirements for pushdown, such as compatible data types and operators. For more information, see Key considerations for Join query pushdown in Presto JDBC data source.

If a table doesn't meet these criteria, it is excluded from the pushdown and is processed by Presto directly. The following table shows an example for federated join:

| Federated join           |
|------------------|
| SELECT \n `i1.customer_last_name, A.ASSIGNMENT_ID, B.FIRST_NAME, t2.custkey` \n `FROMDB2_CATALOG.DB2.ASSIGNMENTS_10_MILLION A` \n `JOINDB2_CATALOG.DB2.CUSTOMER_10_MILLION BONA.EMPLOYEE_ID = B.CUST_ID` \n `JOINDB2_CATALOG.DB2.JOIN_TABLE_50_ROWS CONA.ASSIGNMENT_ID = C.ASSIGNMENT_ID` \n `JOINpostgres_catalog.pg.customer t1onB.CUST_ID = t1.custkey` \n `Joinpostgres_catalog.pg.orders t2ONt1.custkey = t2.orderkey` \n `Joinpostgres_catalog.pg.products t3ONt3.productkey = t2.productkey` \n `JOINiceberg_catalog.ice.customer i1ONi1.customer = B.CUST_ID`    |
| Here, the query has 3 catalogs namely db2_catalog, postgres_catalog and iceberg_catalog. \n db2_catalog (db2 catalog) has 3 tables \n postgres_catalog (postgres catalog) has 3 tables \n iceberg_catalog (iceberg catalog) has 1 table            |
 {: caption="Example" caption-side="bottom"}

For the preceding federated join query, join pushdown optimizer creates Join Operation for the catalogs db2_catalog and posgres_catalog as shown in the following table. As the iceberg_catalog is not a JDBC data source, it will skip and return back to Presto for processing.

| Field           | Description        |
 |------------------|--------------------|
 | Representation of `DB2_CATALOG` Join Operation that is created by join pushdown optimizer    | Select t2.custkey From \n DB2_CATALOG.DB2.ASSIGNMENTS_10_MILLION A, \n DB2_CATALOG.DB2.CUSTOMER_10_MILLION B, \n DB2_CATALOG.DB2.JOIN_TABLE_50_ROWS C where \n A.EMPLOYEE_ID = B.CUST_ID and A.ASSIGNMENT_ID = \n C.ASSIGNMENT_ID; |
 | Representation of `posgres_catalog` Join Operation join pushdown optimizer creates            | Select A.ASSIGNMENT_ID, B.FIRST_NAME From \n posgres_catalog.pg.customer t1, \n posgres_catalog.pg.orders t2, \n posgres_catalog.pg.products t3 where t1.custkey = \n t2.orderkey and t3.productkey = t2.productkey;  |
 {: caption="Example" caption-side="bottom"}

After the optimisation of join pushdown, the preceding federated query is processed by Presto as follows:

`select i1.customer_last_name, A.ASSIGNMENT_ID, B.FIRST_NAME, t2.custkey from (result of DB2_CATALOG Join pushdown) join ( result of posgres_catalog Join pushdown) on B.CUST_ID = t1.custkey join iceberg_catalog.ice.customer i1ONi1.customer = B.CUST_ID`

## List of data sources that support join pushdown
{: #datasources_publicpreview}

The following data sources support join pushdown feature:
* IBM Db2
* PostgreSQL
* Informix
* IBM Netezza
* MySQL
* Oracle
* SQL Server
* Teradata
* Amazon Redshift
* SingleStore
* Snowflake
* HANA
* Apache Phoenix

## Benefits of join pushdown
{: #benefits_publicpreview}

The following are the benefits of join pushdown feature:
* Improved overall query performance.
* Reduced network traffic between IBM presto and the data source.
* Reduced load on the remote data source.
* Significant cost reduction due to the limited number of databases hit.

## Limitations of join pushdown
{: #limitations_publicpreview}

The following are the limitations of join pushdown feature:
* Dependency on Filter Pushdown: Join pushdown relies on existing filter pushdown capabilities of the underlying database. Any limitations or inefficiencies in filter pushdown impact join pushdown performance.
* Database Compatibility: Join pushdown is limited to queries that the underlying database can understand. Complex queries involving filters, projections, conditions, or special keywords may not be pushed down.
* Self-Join Limitations: The current implementation of self-joins is not optimal and has dependencies on the table handle cache. By default, the table handle cache is turned off in Presto and if it is enabled, then self-join pushdown fails.
