### Worker Data Structure

    {
        "name": <string>,
        "image": <string>,
        "data_cache_path": <string>,
        "description": <string>,
        "configs": {
            <string>: <string>,
            ...
        },
        "input": {
            "type": <string>("single" / "multiple"),
            "fields": [
                {
                    "name": <string>,
                    "media_type": <string>,
                    "is_file": <boolean>
                },
                ...
            ]
        },
        "output": {
            "type": <string>("single" / "multiple"),
            "fields": [
                {
                    "name": <string>,
                    "media_type": <string>,
                    "is_file": <boolean>
                },
                ...
            ]
        }
    }

### API

#### /workers

**GET**

_List workers._

    # Example

    curl http://<host>/workers
    {
        "9a84f6ad-2ba6-49b3-b931-b7629c34be9c": "{\"name\": \"Upload CSV to platform\", \"image\": \"platonam/lopco-upload-csv-worker:dev\", \"data_cache_path\": \"/data_cache\", \"description\": \"MQTT upload worker.\", \"configs\": {\"usr\": null, \"pw\": null, \"mqtt_server\": \"connector.platona-m.technology\", \"mqtt_port\": \"18883\", \"mqtt_keepalive\": \"15\", \"delimiter\": null}, \"input\": {\"type\": \"multiple\", \"fields\": [{\"name\": \"service_id\", \"media_type\": \"text/plain\", \"is_file\": false}, {\"name\": \"source_file\", \"media_type\": \"text/csv\", \"is_file\": true}]}, \"output\": {\"type\": \"multiple\", \"fields\": [{\"name\": \"service_id\", \"media_type\": \"text/plain\", \"is_file\": true}, {\"name\": \"sent_messages\", \"media_type\": \"text/plain\", \"is_file\": false}]}}",
        "1567e155-51c6-4f0b-a898-842c737f1b34": "{\"name\": \"XLSX to CSV\", \"image\": \"platonam/lopco-xlsx-to-csv-worker:dev\", \"data_cache_path\": \"/data_cache\", \"description\": \"Convert a Microsoft Excel Open XML Spreadsheet file to Comma-Separated Values.\", \"configs\": {\"delimiter\": null}, \"input\": {\"type\": \"single\", \"fields\": [{\"name\": \"xlsx_file\", \"media_type\": \"application/vnd.ms-excel\", \"is_file\": true}]}, \"output\": {\"type\": \"single\", \"fields\": [{\"name\": \"csv_file\", \"media_type\": \"text/csv\", \"is_file\": true}, {\"name\": \"line_count\", \"media_type\": \"text/plain\", \"is_file\": false}]}}",
        "04e6b617-fff1-41bb-a50c-8c2a2c0413e5": "{\"name\": \"Trim CSV\", \"image\": \"platonam/lopco-trim-csv-worker:dev\", \"data_cache_path\": \"/data_cache\", \"description\": \"Trim a column from a Comma-Separated Values file.\", \"configs\": {\"delimiter\": null, \"column_num\": null}, \"input\": {\"type\": \"single\", \"fields\": [{\"name\": \"input_csv\", \"media_type\": \"text/csv\", \"is_file\": true}]}, \"output\": {\"type\": \"single\", \"fields\": [{\"name\": \"output_csv\", \"media_type\": \"text/csv\", \"is_file\": true}, {\"name\": \"line_count\", \"media_type\": \"text/plain\", \"is_file\": false}]}}"
    }

**POST**

_Add new worker._

    # Example

    cat worker_data.json
    {
        "name": "Split CSV",
        "image": "platonam/lopco-split-csv-worker:dev",
        "data_cache_path": "/data_cache",
        "description": "Split a Comma-Separated Values file into multiple unique files.",
        "configs": {
            "column": null,
            "delimiter": null
        },
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
        }
    }

    curl \
    -d @worker_data.json \
    -H 'Content-Type: application/json' \
    -X POST http://<host>/workers
    {
        "resource": "004894dc-bb03-4649-92c4-6b184c30c594"
    }

----

#### /workers/{worker-id}

**GET**

_Retrieve worker data._

    # Example

    curl http://<host>/workers/004894dc-bb03-4649-92c4-6b184c30c594
    {
        "name": "Split CSV",
        "image": "platonam/lopco-split-csv-worker:dev",
        "data_cache_path": "/data_cache",
        "description": "Split a Comma-Separated Values file into multiple unique files.",
        "configs": {
            "column": null,
            "delimiter": null
        },
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
        }
    }

**PUT**

_Update a worker._

    # Example

    cat worker_data.json
    {
        "name": "Split CSV",
        "image": "platonam/lopco-split-csv-worker:dev",
        "data_cache_path": "/data_cache",
        "description": "Split a Comma-Separated Values file into multiple unique files.",
        "configs": {
            "column": null,
            "delimiter": null
        },
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
                },
                {
                    "name": "line_count",
                    "media_type": "text/plain",
                    "is_file": false
                }
            ]
        }
    }

    curl \
    -d @worker_data.json \
    -H 'Content-Type: application/json' \
    -X PUT http://<host>/workers/004894dc-bb03-4649-92c4-6b184c30c594

**DELETE**

_Remove a worker_

    # Example

    curl -X DELETE http://<host>/workers/004894dc-bb03-4649-92c4-6b184c30c594
