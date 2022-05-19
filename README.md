# iProtekt - Operator File Transfer README

## Prerequisites
- A way to export a table or set of data to a CSV file (see **CSV File Format** section below for information on the columns and data types you will need to provide, along with the order these columns need to be in).  
- An SFTP client application or command line tool (e.g. WinSCP, Cyberduck, PuTTY PSFTP, OpenSSH, etc.).
- A generated SSH public/private key pair (be sure to send us your public key, otherwise you won't be able to connect to our server).
- A username and password provided to you by iProtekt to access our server.

## CSV File Format

See the chart below for the accepted order and data types of your CSV columns (if the order of columns or data type is incorrect, a log file will generate in your SFTP directory outlining the error(s) in your CSV): 

|                |user_id |transaction_datetime  |transaction_type | transaction_amount |account_bal (optional) |
|----------------|--------|----------------------|-----------------|--------------------------|-----------------------|
|**Data Type**   |`STRING`|`DATETIME`            |`STRING`            |`NUMBER`          |`NUMBER`               | 
- **user_id**: the encrypted string of a user (from their email, phone number, username, etc.)
- **transaction_datetime**: the date and time a transaction was made (e.g. mm/dd/yyyy hh:mm:ss or yyyy-mm-dd hh:mm:ss)
- **transaction_type**: the type of transaction made (can either be 'Deposit', 'Wager', 'Win', or 'Withdraw')
- **transaction_amount**: the dollar amount of the transaction
- **account_bal**: the dollar balance of that user's account after that transaction

### SFTP Requirements
You will be required to send (via SFTP) **one CSV file with transaction data going back one full year (historical data)**. After the historical data is transferred, **subsequent CSV files should be sent (via SFTP) once a day with all the transaction data for the current day**.
The CSV files must follow the CSV File Format above.

## How to Send A File

Once the CSV file format is correct, you can now send your file via SFTP. Follow the steps below to successfully send a file:
- First, open a connection using your SFTP client application or command line tool.
- Be sure to include the Server URL, Username and Password, and SSH private key inputs with the correct information.
- Once a connection with the server has been established, upload your CSV
- After the CSV is uploaded, be sure no errors were found. Refresh your SFTP connection to verify this (if there is an error, the file you just sent will be deleted and an error log will generate in the directory you are currently in. You will be able to download this file.
