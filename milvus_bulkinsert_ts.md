---

copyright:
  years: 2017, 2025
lastupdated: "2025-04-15"

keywords: watsonx.data, milvus, bulk insert
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Resolving bulk insert issues in Milvus
{: #milvus_bulkinsert_ts}

## What’s happening
{: #milvus_bulkinsert_ts_1}

Inserting large data sets by using the bulk insert API in Milvus might fail.

## Why it’s happening
{: #milvus_bulkinsert_ts_2}

Bulk insert operations are time-consuming because it involves transferring large volumes of data into a storage system. Failures can occur due to the following common issues, leading to incomplete or failed inserts:
* Network connectivity problems
* Request throttling
* Storage bucket issues

## How to fix it
{: #milvus_bulkinsert_ts_3}

**Verify task status**: When you initiate a bulk insert operation, the asynchronous API returns a task ID. Use the task ID to query the status of the insert operation.
**Handle failures**: If the bulk insert operation fails, check the failure reason. If the failure is due to network-related issues, retry the bulk insert. For other failures, analyse the error message and take appropriate action.

Example

   ```bash
   from pymilvus import connections, utility

connections.connect()

task_ids = {}  # Dictionary to track task_id -> filenames mapping

files = ["data/id.npy", "data/vector.npy"]
# Bulk-insert data
task_id = utility.do_bulk_insert(collection_name="test_collection", files=files)
task_ids[task_id] = files  # Store task ID with corresponding files

# Get bulk-insert task state
# Milvus removes completed or failed tasks after the task retention period.
# Please ensure that you do not call get_bulk_insert_state for tasks that have already been completed.

wait_ids = task_ids
while True:
    time.sleep(2)
    temp_ids = {}
    for id, files in wait_ids.items():
        state = utility.get_bulk_insert_state(task_id=id)
        if state.state == BulkInsertState.ImportFailed or state.state == BulkInsertState.ImportFailedAndCleaned:
            print(state)
            print("The task", state.task_id, "failed, reason:", state.failed_reason)
            print(f"Failed filenames: {files}")
            continue
        if state.state >= BulkInsertState.ImportCompleted:
            print(state)
            continue

        temp_ids[id] = files

    wait_ids = temp_ids
    if len(wait_ids) == 0:
        break;

# <Bulk insert state:
#     - taskID          : 446781855410077319,
#     - state           : Completed,
#     - row_count       : 10000,
#     - infos           : {'files': 'data/id.npy,data/vector.npy', 'collection': 'test_collection_2', 'partition': '_default', 'failed_reason': '', 'progress_percent': '100', 'persist_cost': '0.34'},
#     - id_ranges       : [],
#     - create_ts       : 2024-01-06 22:24:07
# >

   ```
   {: screen}
