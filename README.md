#### /workers

**GET**

_List worker IDs._

    # Example

    curl http://host:8000/worker-registry/workers
    [
        "004894dc-bb03-4649-92c4-6b184c30c594",
        "9a84f6ad-2ba6-49b3-b931-b7629c34be9c",
        "1567e155-51c6-4f0b-a898-842c737f1b34"
    ]

**POST**

_Add new worker._

    # Example

    cat worker_data.json
    {
        "name": "Trim column from csv",
        "description": null,
        "image": "trim-csv-worker",
        "data_cache_path": "/data_cache",
        "input": {
            "type": "single",
            "fields": [
                {
                    "name": "input_csv",
                    "media_type": "text/csv",
                    "is_file": true
                }
            ]
        },
        "output": {
            "type": "single",
            "fields": [
                {
                    "name": "output_csv",
                    "media_type": "text/csv",
                    "is_file": true
                }
            ]
        },
        "configs": {
            "delimiter": null,
            "column_num": null
        }
    }

    curl \
    -d @worker_data.json \
    -H 'Content-Type: application/json' \
    -X POST http://host:8000/worker-registry/workers
    {
        "resource": "04e6b617-fff1-41bb-a50c-8c2a2c0413e5"
    }

----

#### /workers/{worker-id}

**GET**

_Retrieve worker data._

    # Example

    curl http://host:8000/worker-registry/workers/004894dc-bb03-4649-92c4-6b184c30c594
    {
        "name": "Split on unique",
        "description": null,
        "image": "split-on-unique-worker",
        "data_cache_path": "/data_cache",
        "input": {
            "type": "single",
            "fields": [
                {
                    "name": "source_table",
                    "media_type": "text/csv",
                    "is_file": true
                }
            ]
        },
        "output": {
            "type": "multiple",
            "fields": [
                {
                    "name": "unique_id",
                    "media_type": "text/plain",
                    "is_file": false
                },
                {
                    "name": "result_table",
                    "media_type": "text/csv",
                    "is_file": true
                }
            ]
        },
        "configs": {
            "column": null,
            "delimiter": null
        }
    }

**PUT**

_Update a worker._

    # Example

    cat worker_data.json
    {
        "name": "Upload to platform",
        "description": null,
        "image": "platform-upload-worker",
        "data_cache_path": "/data_cache",
        "input": {
            "type": "single",
            "fields": [
                {
                    "name": "service_id",
                    "media_type": "text/plain",
                    "is_file": false
                },
                {
                    "name": "source_table",
                    "media_type": "text/csv",
                    "is_file": true
                }
            ]
        },
        "output": null,
        "configs": {
            "user": null,
            "password": null,
            "machine_id": null
        }
    }

    curl \
    -d @worker_data.json \
    -H 'Content-Type: application/json' \
    -X PUT http://host:8000/worker-registry/workers/9a84f6ad-2ba6-49b3-b931-b7629c34be9c

**DELETE**

_Remove a worker_

    # Example

    curl -X DELETE http://host:8000/worker-registry/workers/9a84f6ad-2ba6-49b3-b931-b7629c34be9c
