# Blockchain Freight Supplychain Project 
### CSE 540: Engineering Blockchain Application
This project implements a hybrid blockchain-Django solution for freight supply chain management. It enables secure shipment tracking, booking confirmations, and payments using Ethereum smart contracts, while providing a user-friendly interface with Django and Stripe integration. Key features include immutable payment records, shipment provenance, and automated reporting for admins and users.
## Overview
This project tracks freight shipments, booking confirmations, and payments using a hybrid architecture:
- **Django backend** for authentication, quotes, bookings, and system configuration (PostgreSQL DB)
- **Ethereum blockchain** for immutable storage of payments, shipment records, and status reports
- **Stripe** for fiat payments (credit/debit)
- **MetaMask + Remix** for Ethereum testnet interactions (optional ETH payments)

## 🚀 Dependencies

### 🖥️ Backend & Core
- **Python 3.11+** – Core programming language  
- **Django 4.x** – Backend web framework  
- **PostgreSQL** – Database for storing application data  

### ⛓️ Blockchain
- **Web3.py** – Interaction with Ethereum blockchain  
- **Ganache** – Local Ethereum blockchain for testing  
- **MetaMask Wallet** – User wallet for blockchain transactions  
- **Remix IDE** – Smart contract development and deployment  

### 💳 Payments & Integrations
- **Stripe API** – Payment processing integration  
- **Ngrok** – Exposes local server via a temporary public URL for Stripe webhooks, demos, and remote testing  

### 📄 Reporting & Email
- **requirements.txt packages**:
  - `docx`, `docx2pdf`, `reportlab==4.4.3` – Generate invoices and convert reports to PDF (from Blockchain & PostgreSQL data)  
  - `django-anymail` – Sending email notifications from the system  

### 🎨 Frontend
- **Bootstrap** – Responsive UI design  
- **Vue.js** – Dynamic frontend interactions  

## Locate Settings.py and local_settings.py
Note: File with settings and configurations are always hidden for security reasons but for the case of the project, group10 will be providing a clear path to the files
 - files Location : Blockchain-Freight-SupplyChain/Jenik_freight_crm/**

## Project Folder and File structure
This section describes the main folders and files in the project and their purposes.<br>
Figure 1: Overview of the project folder structure showing all main apps, blockchain folder, and supporting Django files.
<br><br><img width="822" height="734" alt="image" src="https://github.com/user-attachments/assets/9169d850-e02f-4b95-b46b-12462cbe304e" />


## Setup Instructions

1. **Setup PostgreSQL database and update**
   - Update/edit settings.py file
   - PostgreSQL database will be handling off-Chain services like Bookings,Quoting,Documentation,User Accounts Settings
     
2. **Clone the repository**
   ```bash
   git clone <repository_url>

3. **Install python Python 3.11+**

4. **Create and activate a virtual environment**
    python -m venv venv
    source venv/bin/activate   # Linux/Mac
    venv\Scripts\activate      # Windows

5. **Install dependencies pip install -r requirements.txt**
   - requirements.txt contains, django,docx,docx2pdf,reportlab==4.4.3,stripe
     
6. **Run Django and it's migrations**
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
          - python runserver # this will run your settings.py and provide a link to your application for your browser <br><br> 
            <img width="1247" height="211" alt="image" src="https://github.com/user-attachments/assets/3d41ec8e-60ce-4eac-a674-ed54c30ff719" />

7. **Use Ngrok**<br>
Ngrok creates a secure public URL for your local server, allowing external services like Stripe to access your application during development.
Instead of using http://127.0.0.1:8000/, use the Ngrok-generated public link and update your settings.py with this URL. This ensures Stripe can reach your application for testing webhooks and payments locally <br><br>
<img width="1000" height="402" alt="image" src="https://github.com/user-attachments/assets/444df54f-5c9d-4ef5-bfeb-e992765d4009" />


8. **Setup Stripe for payments**
   - Stripe will be handling Payments using Debit/Credit cards and sends a webhook through django using web3.py and stores payment transactions into on-chain(blockchain) service
   - create an account with stripe : https://stripe.com/en-ca #based on region
   - Go to dashboard -> developer and get API Keys and cpoy Publishable key and Secret key and update them in settings.py
   - Download stripe.exe if you are using windows and run it using command line enter stripe listen http: <port> #This Listens for webhook events and generates  secret key with whsec_......... copy the key and update your settings.py #python page<br><br>
     <img width="1103" height="143" alt="image" src="https://github.com/user-attachments/assets/004eafe9-db6b-4479-86c8-6aed38e492ea" />
    
9.  **Install**
     - Web3.py via virtual Python environment. so as to open up communication between our appliactaion and blockchain service(Ganache)
     - Vscode: To edit and write your python codes
     - Remix IDE : is a browser-based development environment used to write, edit, compile, run, and deploy smart contracts written in Solidity. It provides built-in tools for testing, debugging, and interacting with contracts, making it especially useful for beginners and rapid prototyping. Remix supports deployment to local blockchains, test networks, and the Ethereum mainnet, and integrates easily with wallets like MetaMask for transaction signing
     - MetaMask Wallet : is a popular crypto wallet and browser extension that allows users to store, send, and receive cryptocurrencies like Ethereum. It also acts as a gateway to decentralized applications, enabling secure interaction with blockchain networks directly from a web browser or mobile device.
     - Ganache : is a local blockchain simulator used for testing smart contracts.
  
 10. **Deploy smart contracts via Remix connected to Ganache or Polygon Amoy Testnet**

## Usage
- Clients,Finance,Sales team can manage quoting, documentations, bookings, shipments, payments,their own account and reports
- Users can view shipment status, confirm bookings,payments using debit and credit cards and optionally pay with ETH via MetaMask
- All payments and shipment status updates are recorded on blockchain for traceability
- Account settings,quoting, documentations, bookings are stored on postgre database as off-chain service
  
## Notes
- ETH payments are optional; Stripe payments are fully functional
- Smart contract logic is stored in blockchain/contracts/

## Smart Contract Structure & Interfaces
Our project uses two smart contracts on Ethereum to handle payments and shipments securely:<br><br>
### Payment.sol
  - Manages all payment transactions for freight bookings.
  - Tracks each payment with details such as sessionId, transactionId, amount, currency, and status (success/failed).
  - Emits events like PaymentCreated and EmailMarkedSent to notify the system when a payment occurs or a confirmation email is sent.
  - Only the contract owner can create and update payments, ensuring controlled and secure management.<br>
  *Figure 1: Flow of Payment.sol showing payment creation, status updates, and email notification.*
  <img width="891" height="465" alt="image" src="https://github.com/user-attachments/assets/82416b32-1095-416c-8647-db29af68acb9" /><br><br>
### Shipment.sol
  - Handles creation, tracking, and status updates of shipments.
  - Stores shipment information like shipmentId, origin, destination, containerType, weight, status, and delivery confirmation.
  - Emits events such as ShipmentCreated, ShipmentStatusUpdated, and DeliveryConfirmed for real-time monitoring.
  - Only the contract owner can create or update shipments, maintaining integrity of shipment data.<br><br>
  *Figure 2: Flow of Shipment.sol showing shipment creation, status updates, and delivery confirmation.*
  <img width="903" height="505" alt="image" src="https://github.com/user-attachments/assets/f11f6204-c083-4251-8442-ec6180d43f3b" /><br><br>
### How Payment.sol and Shipment.sol work together:
- When a customer makes a payment (Payment.sol), it is linked to a freight quote.
- Once the payment is confirmed, a shipment record (Shipment.sol) is created and tracked until delivery.
- Events from both contracts allow the frontend to update the UI in real-time.

## Code Documentation & Comments
Each Django model and smart contract function should have comments explaining:
- Purpose
- Parameters
- Returns or effects
- Example usage
  <br>**Example in Django model:**<br>
  <img width="1150" height="331" alt="image" src="https://github.com/user-attachments/assets/fdb6356f-32ff-4390-849e-bfd02cc609c6" />


        



