# EtherScanETLProject

Overview
This project is a Python script designed to extract, transform, and load (ETL) cryptocurrency transaction data from the Ethereum blockchain using the Etherscan API. It allows you to retrieve transaction data for various ERC-20 tokens, clean and format the data, and then load it into a SQL Server Management Studio (SSMS) database. The project demonstrates how to use Python libraries such as PrettyTable, requests, and pyodbc to accomplish this ETL process.

Prerequisites
Before running the script, make sure you have the following prerequisites installed:

Python 3.x
PrettyTable
Requests
pyodbc
SQL Server Management Studio (SSMS) for database storage
You can install the required Python packages using the following commands:

bash
Copy code
pip install PrettyTable
pip install requests
pip install pyodbc
Usage
Extract Data: The ExtractAPI function extracts transaction data from the Ethereum blockchain via the Etherscan RESTful API. To extract data for a specific ERC-20 token, provide its contract address as an argument to the function.

Transform Data: The TransformJSON function takes the extracted data and performs data transformation. It categorizes transaction amounts as "High," "Medium," or "Low" based on predefined criteria. Additionally, it converts values to float and formats timestamps.

Load Data: The loadSSMS function loads the transformed data into a SQL Server database using ODBC drivers. It creates a table named ERC_Tokens if it does not already exist and inserts the data into this table. Duplicate rows with the same timestamp, hash, value, and token symbol are removed to ensure data integrity.

Running the Code: The script is set up to run on ten different ERC-20 tokens, including Shiba Inu, Tether USD, BNB, stETH, TRON, Theta, Matic, ChainLink, Dai, and Uniswap Stablecoin. You can modify the script to include additional tokens or adjust the parameters as needed.

python
Copy code
# Example usage for Shiba Inu token
tokenName = 'SHIBA INU'
si_result = ExtractAPI('0x95aD61b0a150d79219dCF64E1E6Cc01f0B64C4cE')
si_result_transformed = TransformJSON(si_result)
loadSSMS(si_result_transformed, tokenName)
Database Schema
The script creates a table named ERC_Tokens with the following schema:

blockNumber (int)
hash (varchar(MAX))
nonce (int)
blockHash (varchar(MAX))
from (varchar(MAX))
contractAddress (varchar(MAX))
to (varchar(MAX))
value (float)
tokenName (varchar(MAX))
tokenSymbol (varchar(MAX))
tokenDecimal (int)
transactionIndex (int)
gas (float)
gasPrice (nvarchar(MAX))
gasUsed (float)
cumulativeGasUsed (float)
input (varchar(MAX))
confirmations (int)
dateTime (datetime)
amount_flag (varchar(MAX))
This schema is designed to store relevant transaction details for the extracted ERC-20 token data.

Running the Script
You can run the script for each token by providing the contract address and token name as shown in the example usage section. Ensure that you have configured SQL Server and the ODBC drivers correctly to enable data loading into SSMS.
