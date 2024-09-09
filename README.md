# Installation

1. Clone repo
2. Install dependency: npm i
3. Create env file in root folder and add following:

PORT=3000
DB_HOST=your_hostname
DB_USER= your_username
DB_PASSWORD=your_password
DB_NAME=your_db_name
ADMIN_API_KEY=your_admin_api_key
JWT_SECRET=your_jwt_secret

Note: add DBname and other as per your setup in workbench mySQL 

4. Run project using node app.js

Race condition handling: Mutual exclusion is implemented using transaction. Prevent multiple writer to write same variable at once. 

# TABLE SS
## user table
This table help us to maintain which user is admin or normal user. Also, secret key is used to sign the password and same secret key is used to decrypt the password.
![image](https://github.com/user-attachments/assets/895f55f6-b8d0-4f5e-885f-dafa0c587ae3)

## Train table
This table is used to maintain the present train, their route, id and number of seats, etc. No. of seats per train is tracked using this table.
![image](https://github.com/user-attachments/assets/4153989f-6780-4861-82f0-742aa7d1120c)

## Booking table
This table is used to store bookings, it store train id and the booking id for each seat. Multiple seats can be booked at once and race condition handled.
![image](https://github.com/user-attachments/assets/26927fc0-fe94-4a3b-b213-a8a4e9b745fc)

# Working 
## 1. Register a User
### http://localhost:3000/api/users/register

![image](https://github.com/user-attachments/assets/aa367c5b-2e84-42c4-994c-630b5dd5655c)
![image](https://github.com/user-attachments/assets/89990120-dd3a-4f08-90e5-536843b4c91c)


## 2. Login User
### http://localhost:3000/api/users/login
Login via non admin user
![image](https://github.com/user-attachments/assets/74f19ee5-9bf6-4c4c-965c-da893110f001)

Login via admin user
![image](https://github.com/user-attachments/assets/9b18419d-e73a-473d-b6ad-62f37a2782c2)

## 3. Add a New Train
###
both organisation api key and authorization key of admin login is neeeded to add new train.
![image](https://github.com/user-attachments/assets/b06b8c89-4b3d-4c09-bfe3-887407706b2c)

only admin can add train so need admin data/auth token. 
![image](https://github.com/user-attachments/assets/adcb8837-e8ab-47f4-830d-f359afa31e19)
![image](https://github.com/user-attachments/assets/7178f209-cd05-4b28-991b-1d1b11e2410a)

## 4. Edit train details

![image](https://github.com/user-attachments/assets/0b3d60e8-9782-4eb7-b6e2-6efda00470c6)


## 5. Get Seat Availability
###
![image](https://github.com/user-attachments/assets/c6e0d014-f435-4249-9f9d-0a85d2685d48)


## 6. Book a Seat
### http://localhost:3000/api/bookings/book
Booking multiple/single seat at once.
### For getting booking seats, Authorization Token received in the login endpoint is required.
![image](https://github.com/user-attachments/assets/4a555171-c9a2-473d-9283-298b266ac912)
If try to book more than capacity 
![image](https://github.com/user-attachments/assets/821f39cd-1e54-4e8c-99d4-631643cc0741)
If try to book invalid number of seats
![image](https://github.com/user-attachments/assets/a5bdda2c-e9ff-4749-b7d1-0aff589ef255)


## 7. Get Specific Booking Details
### For getting specific booking details, Authorization Token received in the login endpoint is required.
### http://localhost:3000/api/bookings/<--booking id-->
getting details based on booking id.
![image](https://github.com/user-attachments/assets/437d2b75-ddb5-44b8-a437-703b8e1f7ddb)

## 8. Authorization is implemented and Signing of key using secret key is done.

## 9. Admin api endpoints are protected using the ADMIN API KEY
