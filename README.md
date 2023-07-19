# CSV-to-MongoDB Importer

## Introduction

This script imports data from a CSV file to a MongoDB database. It creates a new document in MongoDB for each row in the CSV file. The keys are the column headers in the first row, and the values are the corresponding cells.

## Prerequisites

- Node.js and npm installed.
- Access to a MongoDB database.
- A CSV file with the data to import.

## Installation

This script depends on several npm packages:

- `fs-extra`
- `csv-parser`
- `mongodb`
- `commander`

To install these dependencies, navigate to the directory containing this script and run:

```bash
npm install fs-extra csv-parser mongodb commander
```

## Usage

```bash
node scripts/csv-to-mongo.mjs -u <db_url> -d <db_name> -c <csv_file_path> -n <collection_name>
```

Here are the details of the command-line arguments:

- `-u, --url <type>`: The MongoDB URL. Default is 'mongodb://localhost:27017'.
- `-d, --dbName <type>`: The name of the MongoDB database. Default is 'test'.
- `-c, --csv <type>`: The path of the CSV file. Default is 'file.csv'.
- `-n, --collectionName <type>`: The name of the MongoDB collection to import to. Default is 'data'.

## Example

```bash
node scripts/csv-to-mongo.mjs -u "mongodb://localhost:27017" -d testDB -c "data.csv" -n testData
```

This command will connect to a MongoDB database at "mongodb://localhost:27017", select a database named "testDB", read a CSV file "data.csv" and import each row as a document to a collection named "testData".

After the script is executed, it will print the number of documents inserted and then close the connection to the MongoDB server.

## Limitations

The script currently doesn't support handling nested data in CSV format. All data is considered as flat key-value pairs.

## Troubleshooting

If you encounter an error `MongoNotConnectedError: Client must be connected before running operations`, it's most likely caused by the MongoDB client being closed before all operations are complete. The updated version of the script addresses this issue by closing the client after all data is inserted.

If the issue persists, please check your MongoDB server status and the connection URL.

## Further Improvements

- Error handling: The script currently simply logs errors and continues processing. Depending on your use case, you might want to stop processing on certain errors, or take other actions such as retrying the operation, etc.
- Performance: For large CSV files, inserting the documents one at a time might be slow. Depending on your use case and the capabilities of your MongoDB server, you might be able to improve performance by inserting documents in batches.
