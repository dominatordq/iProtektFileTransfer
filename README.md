# iProtekt - Operator File Transfer README

The Operator File Transfer Protocol will involve sending transactional betting data to iProtekt. There are two types of betting data required: **historical data** and **realtime data**. Each of these will be transferred via SFTP as a CSV file. The transfer of this data should follow these steps:
  1. Transfer of the historical data (all betting data that occurred over the previous YEAR)
  2. Transfer of the realtime data (all betting data that occurred on the current DAY)

The historical data will only be transferred **once**. The realtime data is expected be tranferred **once per day after the historical data is sent**.

## Prerequisites
- A way to export a table or set of data to a CSV file (see **CSV File Format** section below for information on the columns and data types you will need to provide, along with the order these columns need to be in).  
- An SFTP client application or command line tool (e.g. WinSCP, Cyberduck, PuTTY PSFTP, OpenSSH, etc.).
- A generated SSH public/private key pair **(be sure to send us your public key, otherwise you won't be able to connect to our server)**.
- A username and password provided to you by iProtekt to access our server.

## CSV File Format

See the chart below for the accepted order and data types of your CSV columns (if the order of columns or data type is incorrect, a log file will generate in your SFTP directory outlining the error(s) in your CSV): 

|                |user_id |transaction_datetime  |transaction_type | transaction_amount |account_bal (optional) |
|----------------|--------|----------------------|-----------------|--------------------------|-----------------------|
|**Data Type**   |`STRING`|`DATETIME`            |`STRING`            |`NUMBER`          |`NUMBER`               | 
- **user_id**: the encrypted string of a user (from their email, phone number, username, etc.)
- **transaction_datetime**: the date and time (in military time) a transaction was made (e.g. mm/dd/yyyy hh:mm:ss or yyyy-mm-dd hh:mm:ss)
- **transaction_type**: the type of transaction made (can either be 'Deposit', 'Wager', 'Win', or 'Withdraw')
- **transaction_amount**: the dollar amount of the transaction
- **account_bal**: the dollar balance of the user's account after the transaction

Click this link to view a sample CSV that follows this format: https://github.com/dominatordq/iProtektFileTransfer/blob/main/example_csv.CSV

### SFTP Requirements
You will be required to send (via SFTP) **one CSV file with transaction data going back one full year (historical data)**. After the historical data is transferred, subsequent CSV files will be sent (via SFTP) **once a day with all the transaction data for the most recent day (realtime data)**.
The CSV files must follow the CSV File Format above.

## Step-by-Step Guide
  (Historical data)
  1. Export transaction (betting) data to a CSV of your user-base spanning the previous year (YTD). Make sure to encrypt each 'user_id' for security purposes.
  (Realtime data)
  1. Export transaction (betting) data to a CSV of your user-base spanning the most recent day. Make sure to encrypt each 'user_id' for security purposes.
  2. Follow the steps outlined in **How to Send A File** below.
  3. Be sure to refresh your SFTP connection periodically over the next minute or so. If your file contains an error, an error log will appear in the current directory you are in. If your file contains no errors, a success log will appear.
  4. If the file contained an error, download the error log to view where the error(s) occurred. After the error(s) have been fixed, repeat steps 2-3. 

## How to Send A File

Once the CSV file format is correct, you can now send your file via SFTP. Follow the steps below to successfully send a file:
- First, open a connection using your SFTP client application or command line tool.
- Be sure to include the Server URL, Username and Password, and SSH private key inputs with the correct information.
- Once a connection with the server has been established, upload your CSV.
- After the CSV file is uploaded, make sure you 'refresh' your SFTP connection after a minute or two to ensure there were no errors (if there is an error, the CSV file that was just sent will be deleted and an error log will generate in the directory you are currently in. You will be able to download this file).
