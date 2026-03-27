# Team10_2026SpringB_CSE540_Freight_Supply_Chain_Provenance_System
Blockchain-based freight supply chain system with Django backend, Ethereum smart contracts, Stripe payments, Ganache, Remix, MetaMask, PostgreeDB and real-time shipment tracking

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

  ## Setup Instructions
1. Clone the repository
   ```bash
   git clone <repository_url>

## Create and activate a virtual environment
python -m venv venv
source venv/bin/activate   # Linux/Mac
venv\Scripts\activate      # Windows

## Install dependencies
pip install -r requirements.txt

## Setup PostgreSQL database and update
Locate File: Team10_2026SpringB_CSE540_Freight_Supply_Chain_Provenance_System/Jenik_freight_crm/local_settings.py
Note: File with settings and configurations are always hidden for security reasons but for the case of the project, group10 will be providing a clear path to the files

## Run Django migrations
Open Command Line. you can either use cmd or windows power shell and do the following
- locate your django instalation example: cd C:\Django_installation\django_activation\Scripts
   - then: .\activate  #This will activate you django enviroment,
   - After, Locate your django folder for  example: cd C:\Team10_2026SpringB_CSE540_Freight_Supply_Chain_Provenance_System
   - Run below commands
      - python manage.py makemigrations #this will create your tables ready to be uploaded on postgreeDB (the files run are in models.py)
      - python manage.py migrate #this will upload create a database and your table schemas on postgreeDB
      - python runserver # this will run your settings.py and provide a link to your application for your browser  



