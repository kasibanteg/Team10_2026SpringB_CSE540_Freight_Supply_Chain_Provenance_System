# Blockchain Freight Supplychain Project 
### CSE 540: Engineering Blockchain Application
This project implements a hybrid blockchain-Django solution for freight supply chain management. It enables secure shipment tracking, booking confirmations, and payments using Ethereum smart contracts, while providing a user-friendly interface with Django and Stripe integration. Key features include immutable payment records, shipment provenance, and automated reporting for admins and users.
## Overview
This project tracks freight shipments, booking confirmations, and payments using a hybrid architecture:
- **Django backend** for authentication, quotes, bookings, and system configuration (PostgreSQL DB)
- **Ethereum blockchain** for immutable storage of payments, shipment records, and status reports
- **Stripe** for fiat payments (credit/debit)
- **MetaMask + Remix** for Ethereum testnet interactions (optional ETH payments)

## Dependencies
- Python 3.11+
- Django 4.x
- PostgreSQL
- Web3.py
- Stripe API
- Remix IDE
- MetaMask Wallet
- Ganache local blockchain (for testing)
- Ngrok creates a public link to your localhost which can be accessed over the web to connect your application with stripe(only for local production)

## Locate Settings.py and local_settings.py
Note: File with settings and configurations are always hidden for security reasons but for the case of the project, group10 will be providing a clear path to the files
 - files Location : Blockchain-Freight-SupplyChain/Jenik_freight_crm/**

## Project Folder and File structure
Blockchain-Freight-SupplyChain/
│
├─ apps/
│  ├─ Account_settings/
│  ├─ Bookings/
│  ├─ Documentations/
│  ├─ Home/
│  ├─ Login/
│  ├─ Payments/
│  ├─ Quotings/
│  ├─ Reports/
│  └─ Shipments/
│
├─ blockchain/
│  ├─ contracts/
│  │   ├─ Freight.sol
│  │   └─ Payment.sol
│  └─ migrations/ (optional for testnets)
│
├─ dependencies/
│  ├─ static/
│  ├─ templates/
│  └─ global_variables.py
│
├─ manage.py
├─ README.md
├─ requirements.txt
└─ .vscode/

## Setup Instructions

1. Setup PostgreSQL database and update
   - Update/edit settings.py file
   - PostgreSQL database will be handling off-Chain services like Bookings,Quoting,Documentation,User Accounts Settings
     
2. Clone the repository
   ```bash
   git clone <repository_url>

3. Install python Python 3.11+

4. Create and activate a virtual environment
    python -m venv venv
    source venv/bin/activate   # Linux/Mac
    venv\Scripts\activate      # Windows

5. Install dependencies
    pip install -r requirements.txt
   
7. Run Django and it's migrations
   Open Command Line. you can either use cmd or windows power shell and do the following
    - locate your django instalation example: cd C:\Django_installation\django_activation\Scripts
       - then: .\activate  #This will activate you django enviroment,
       - After, Locate your django folder for  example: cd C:\Blockchain-Freight-SupplyChain
       - Run below commands
          - python manage.py makemigrations #this will create your tables ready to be uploaded on postgreeDB (the files run are in models.py)
          - python manage.py migrate #this will upload create a database and your table schemas on postgreeDB
          - Create Admin Accounts:
             -  python manage.py createsuperuser #Run the createsuperuser command
             -  python manage.py createsuperuser --username admin --email admin@example.com #Enter the required info
          - python runserver # this will run your settings.py and provide a link to your application for your browser  
            <img width="1247" height="211" alt="image" src="https://github.com/user-attachments/assets/3d41ec8e-60ce-4eac-a674-ed54c30ff719" />

8. Use Ngrok : - Ngrok creates a public link to your localhost which can be accessed over the web to connect your application with stripe(only for local  production) so instead of using http://127.0.0.1:8000/ it will be converted to a secure public link so use that to access your application
- <img width="1000" height="402" alt="image" src="https://github.com/user-attachments/assets/444df54f-5c9d-4ef5-bfeb-e992765d4009" />
Update the generated public secure URL in settings.py

9. Setup Stripe for payments
   - Stripe will be handling Payments using Debit/Credit cards and sends a webhook through django using web3.py and stores payment transactions into on-chain(blockchain) service
   - create an account with stripe : https://stripe.com/en-ca #based on region
   - Go to dashboard -> developer and get API Keys and cpoy Publishable key and Secret key and update them in settings.py
   - Download stripe.exe if you are using windows and run it using command line enter stripe listen http: <port> #This Listens for webhook events and generates  secret key with whsec_......... copy the key and update your settings.py #python page
   - <img width="1103" height="143" alt="image" src="https://github.com/user-attachments/assets/004eafe9-db6b-4479-86c8-6aed38e492ea" />
10.  Install Web3.py via virtual Pyton environment
    
11.  Install
     - Vscode: To edit and write your python codes
     - Remix IDE : is a browser-based development environment used to write, edit, compile, run, and deploy smart contracts written in Solidity. It provides built-in tools for testing, debugging, and interacting with contracts, making it especially useful for beginners and rapid prototyping. Remix supports deployment to local blockchains, test networks, and the Ethereum mainnet, and integrates easily with wallets like MetaMask for transaction signing
     - MetaMask Wallet : is a popular crypto wallet and browser extension that allows users to store, send, and receive cryptocurrencies like Ethereum. It also acts as a gateway to decentralized applications, enabling secure interaction with blockchain networks directly from a web browser or mobile device.
     - Ganache : is a local blockchain simulator used for testing smart contracts.
  
 12. Deploy smart contracts via Remix connected to Ganache or Polygon Amoy Testnet

## Usage
- clients,Finance,Sales team can manage quoting, documentations, bookings, shipments, payments,their own account and reports
- Users can view shipment status, confirm bookings,payments using debit and credit cards and optionally pay with ETH via MetaMask
- All payments and shipment status updates are recorded on blockchain for traceability
- Account settings,quoting, documentations, bookings are stored on postgre database as off-chain service
  
## Notes
- ETH payments are optional; Stripe payments are fully functional
- Smart contract logic is stored in blockchain/contracts/
        
## Dependencies


