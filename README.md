## DATABASE

**Type:** MySQL

### projectDB

#### Tables

- **users**
    - `id`: Int, Primary Key, Unique
    - `userID`: String(100), Unique, Not Null
    - `username`: String(100), Unique, Not Null
    - `email`: String(250), Unique, Not Null
    - `password`: String(1000), Unique, Not Null
    - `permission`: String(100), Default 'user', Not Null
    - `token`: String(1000), Unique, Not Null
    - `created_at`: Timestamp

- **messages**
    - `id`: Int, Primary Key, Unique
    - `messageID`: String(100), Unique, Not Null
    - `chatID`: String(100), Not Null
    - `userID`: String(100), Not Null
    - `content`: String(3000), Not Null
    - `replyed_to`: String(100), Default Null
    - `created_at`: Timestamp

- **companies**
    - `id`: Int, Primary Key, Unique
    - `companyID`: String(100), Unique, Not Null
    - `name`: String(500), Unique, Not Null
    - `email`: String(500), Unique, Not Null
    - `logo`: String(300), Unique, Default Null
    - `website`: String(300), Unique, Default Null
    - `created_at`: Timestamp

- **chats**
    - `id`: Int, Primary Key, Unique
    - `chatID`: String(100), Unique, Not Null
    - `members`: String(1000), Not Null
    - `created_at`: Timestamp

# BACK-END API
Framework: NestJS
Language: Typescript

Endpoints:
### Authentication
- **/api/users/authentication**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
    - **Response**
        - **Success**:
            - `status`: Int
            - `message`: String
            - **user**:
                - `username`: String
                - `email`: String
                - `permission`: String
                - `token`: String
        - **Failed**:
            - `status`: Int
            - `message`: String

### Access Management
- **/api/users/access**
    - **Request**
        - `action`: 'login' | 'register'
        - `method`: POST
        - **Body**:
            - `username`: String
            - `email`: String
            - `password`: String
    - **Response**
        - **Login/Registration Success**:
            - `status`: Int
            - `message`: String
            - `token`: String
        - **Login/Registration Failed**:
            - `status`: Int
            - `message`: String

### Users
- **/api/users/get**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `findUserData?`:
                - `id?`: Int
                - `userID?`: String
                - `username?`: String
                - `email?`: String
                - `password?`: String
                - `permission?`: String
                - `token?`: String
    - **Response**
        - **Request Success**:
            - `status`: Int
            - `message`: String
            - `users`: []
        - **Request Failed**:
            - `status`: Int
            - `message`: String

- **/api/users/update**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `updateUser`:
                - `id?`: Int
                - `userID?`: String
                - `username?`: String
                - `token?`: String
            - `updateUserData`:
                - `id?`: Int
                - `userID?`: String
                - `username?`: String
                - `email?`: String
                - `password?`: String
                - `permission?`: String
                - `token?`: String
    - **Response**
        - **Request Success**:
            - `status`: Int
            - `message`: String
            - `updateUser`: {}
        - **Request Failed**:
            - `status`: Int
            - `message`: String

- **/api/users/delete**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `deleteUser`:
                - `id?`: Int
                - `userID?`: String
                - `username?`: String
                - `token?`: String
    - **Response**
        - **Request Success**:
            - `status`: Int
            - `message`: String
        - **Request Failed**:
            - `status`: Int
            - `message`: String

### Messages
- **/api/messages/get**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `findMessageData?`:
                - `id?`: Int
                - `messageID?`: String
                - `chatID?`: String
                - `userID?`: String
                - `content?`: String
                - `replied_to?`: String
    - **Response**
        - **Request Success**:
            - `status`: Int
            - `message`: String
            - `messages`: []
        - **Request Failed**:
            - `status`: Int
            - `message`: String

- **/api/messages/update**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `updateMessage`:
                - `id?`: Int
                - `messageID?`: String
                - `chatID?`: String
            - `updateMessageData`:
                - `id?`: Int
                - `messageID?`: String
                - `chatID?`: String
                - `userID?`: String
                - `content?`: String
                - `replied_to?`: String
    - **Response**
        - **Request Success**:
            - `status`: Int
            - `message`: String
            - `updatedMessage`: {}
        - **Request Failed**:
            - `status`: Int
            - `message`: String

- **/api/messages/delete**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `deleteMessage`:
                - `id?`: Int
                - `messageID?`: String
                - `chatID?`: String
    - **Response**
        - **Request Success**:
            - `status`: Int
            - `message`: String

### Companies
- **/api/companies/get**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `findCompanyData?`:
                - `id?`: Int
                - `companyID?`: String
                - `name?`: String
                - `email?`: String
                - `logo?`: String
                - `website?`: String
    - **Response**
        - 
        - `status`: Int
        - `message`: String
        - `companies`: []

- **/api/companies/update**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `updateCompany`:
                - `id?`: Int
                - `companyID?`: String
                - `name?`: String
            - `updateCompanyData`:
                - `name?`: String
                - `email?`: String
                - `logo?`: String
                - `website?`: String
    - **Response**
        - **Request Success**:
            - `status`: Int
            - `message`: String
            - `companies`: []
        - **Request Failed**:
            - `status`: Int
            - `message`: String

- **/api/companies/delete**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `deleteCompany`:
                - `id?`: Int
                - `companyID?`: String
                - `name?`: String
    - **Response**
        - `status`: Int
        - `message`: String

### Chat
- **/api/chats/get**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `findChatData`:
                - `id?`: Int
                - `chatID?`: String
                - `members?`: String
    - **Response**
        - **Request Success**:
            - `status`: Int
            - `message`: String
            - `chats`: []
        - **Request Failed**:
            - `status`: Int
            - `message`: String

- **/api/chats/update**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `updateChat`:
                - `id?`: Int
                - `chatID?`: String
            - `updateChatData`:
                - `id?`: Int
                - `chatID?`: String
                - `members?`: String
    - **Response**
        - **Request Success**:
            - `status`: Int
            - `message`: String
            - `updatedChat`: []
        - **Request Failed**:
            - `status`: Int
            - `message`: String

- **/api/chats/delete**
    - **Request**
        - `method`: POST
        - **Body**:
            - `token`: String
            - `deleteChat`:
                - `id?`: Int
                - `chatID?`: String
    - **Response**
        - `status`: Int
        - `message`: String

# Socket Server
## Events
- **send_message**
    - **data**
        - `message`
            - `chatID`: String
            - `content`: String
            - `user`: String
            - `replied_to`: String
- **send_form_message**
    - **data**
        - `chatID`: 'general'
        - `user`: String
        - `content`: String
        - `image`: IMAGE
        - `subject`: String
        - `categories`: String[]
        - `companies`: String[]
- **delete_message**
    - **data**
        - `messageID`: String
        - `chatID`: String
        - `userID`: String
- **update_message**
    - **data**
        - `messageID`: String
        - `chatID`: String
        - `userID`: String
        - `content`: String
- **create_chat**
    - **data**
        - `userID`: String
        - `targetUserUsername`: String
- **delete_chat**
    - **data**
        - `chatID`: String
