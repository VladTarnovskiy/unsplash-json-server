# JSON-server-api
Api for task "RS Clone".

## Setup and Running

- Use `node 14.x` or higher.
- Clone this repo: `$ git clone https://github.com/igormotorin/json-server-api.git`.
- Go to downloaded folder: `$ cd json-server-api`.
- Install dependencies: `$ npm install`.
- Start server: `$ npm start`.
- Now you can send requests to the address: `http://127.0.0.1:3000`.

## Usage


1. Чтобы начать работу с сервером нужно зарегестрировать пользователя

	Делаем запрос: POST  http://localhost:3000/register

	в Body запроса пишем JSON: 

    ```json
        {
            "email": "olivier2@mail.com", // свои данные
            "password": "bestPassw0rd"  // свои данные
        }
    ```
							

	Сервер в ответе пришлет id пользователя и accessToken (как в примере ниже)

	Response:
    ```json
        {
            "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im9saXZpZXIxQG1haWwuY29tIiwiaWF0IjoxNjc1NDM3MTE4LCJleHAiOjE2NzU0NDA3MTgsInN1YiI6IjQifQ.c6uMSTy8dwWRJzmH1g-sCXsXxxyHHoFQcQpdN7ovXf8",
            "user": {
                "email": "olivier1@mail.com",
                "id": 4
            }
        }
    ```

2. Дальше все последующие запросы делаем с 	accessToken, для этого необходимо в Headers запросов в поле Authorization установить тип авторизации Bearer и токен полученный при регистрации.

    ```json	
		Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im9saXZpZXJAbWFpbC5jb20iLCJpYXQiOjE2NzU0MzU5NjAsImV4cCI6MTY3NTQzOTU2MCwic3ViIjoiMyJ9.wkzZjoRZXzrMYjVFBdwuZwg_hxPGmyAEIr7rPi6cyZw
	```
		
3. Токен живет 1 час, по истечении часа необходимо получить новый токен. Для этого выполнить вход в систему Login.
	
	
	Делаем запрос: POST  http://localhost:3000/login

	в Body запроса пишем JSON:

    ```json
        {
            "email": "olivier12@mail.com",
            "password": "bestPassw0rd11"
        }
    ```

	Сервер в ответе пришлет id пользователя и обновленный accessToken

	Response:
    ```json
        {
            "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im9saXZpZXIxQG1haWwuY29tIiwiaWF0IjoxNjc1NDM3Njk3LCJleHAiOjE2NzU0NDEyOTcsInN1YiI6IjQifQ.Ca5h8xNzmfJzyiSxCayZzKN5ZxOlJm68Ib1uug720co",
            "user": {
                "email": "olivier1@mail.com",
                "id": 4
            }
        }
    ```

- **User**
    - [Register User](https://github.com/igormotorin/json-server-api#register-user)
    - [Login User](https://github.com/igormotorin/json-server-api#login-user)
    - [Get User](https://github.com/igormotorin/json-server-api#get-user)
    - [Update User](https://github.com/igormotorin/json-server-api#update-user)
    - [Delete User](https://github.com/igormotorin/json-server-api#delete-user)

**Register User**
----
Register a new user.

<details>

* **URL**

    /register

* **Method:**

    `POST`

* **Headers:**

    `'Content-Type': 'application/json'`

*  **URL Params**

    None

* **Query Params**

    None

* **Data Params**

    ```typescript
      {
        email: string,
        password: string
      }
    ```

* **Success Response:**

  * **Code:** 201 CREATED <br />
    **Content:** 
    ```json
      {
        "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im9saXZpZXJAbWFpbC5jb20iLCJpYXQiOjE2NzU0MDAyMDEsImV4cCI6MTY3NTQwMzgwMSwic3ViIjoiMyJ9.rb6HiOz3JLsY8JUNovCE6vTjtBBXBQiC80Ru7_ADcl4",
        "user": {
            "email": "olivier@mail.com",
            "id": 3
        }
    }
    ```
 
* **Error Response:**

   * **Code:** 400 Bad Request <br />
    **Content:** 
    `"Email and password are required"`

    * **Code:** 400 Bad Request <br />
    **Content:** 
    `"Email already exists"`



* **Notes:**

    None

</details>


**Login User**
----
Login user.

<details>

* **URL**

    /login

* **Method:**

    `POST`

* **Headers:**

    `'Content-Type': 'application/json'`

*  **URL Params**

    None

* **Query Params**

    None

* **Data Params**

    ```typescript
      {
        email: string,
        password: string
      }
    ```

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:** 
    ```json
      {
        "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im9saXZpZXJAbWFpbC5jb20iLCJpYXQiOjE2NzU0MDAyMDEsImV4cCI6MTY3NTQwMzgwMSwic3ViIjoiMyJ9.rb6HiOz3JLsY8JUNovCE6vTjtBBXBQiC80Ru7_ADcl4",
        "user": {
            "email": "olivier@mail.com",
            "id": 3
        }
    }
    ```
 
* **Error Response:**

   * **Code:** 400 Bad Request <br />
    **Content:** 
    `"Cannot find user"`

    * **Code:** 400 Bad Request <br />
    **Content:** 
    `"Incorrect password"`

    * **Code:** 400 Bad Request <br />
    **Content:** 
    `"Email and password are required"`


* **Notes:**

    None

</details>



**Get User**
----
Get user data

<details>

* **URL**

    /users/:id

* **Method:**

    `GET`

* **Headers:**
   
    `'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im9saXZpZXIxQG1haWwuY29tIiwiaWF0IjoxNjc1NDAyMjM1LCJleHAiOjE2NzU0MDU4MzUsInN1YiI6IjEifQ.V_lNh4EXi2DtVcOD7UDrZblxFFmYeoEufxshsLIJ_ik'`

*  **URL Params**

    **Required:**
 
    `id=[integer]`

* **Query Params**

    None

* **Data Params**

    None

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:** 
    ```json
      {
        "email": "olivier12@mail.com",
        "password": "$2a$10$dvRIbUcWuFkuY/gJsi5fAORBJ9DsHmSOLawKzT4Rzf7C6mon/cwWe",
        "id": 1
     }
    ```
 
* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** 
    `"Private resource replacement: request body must have a reference to the owner id"`

* **Notes:**

    None

</details>


**Update User**
----
Update user data

<details>

* **URL**

    /users/:id

* **Method:**

    `PUT`

* **Headers:**

    `'Content-Type': 'application/json'`
    `'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im9saXZpZXIxQG1haWwuY29tIiwiaWF0IjoxNjc1NDAyMjM1LCJleHAiOjE2NzU0MDU4MzUsInN1YiI6IjEifQ.V_lNh4EXi2DtVcOD7UDrZblxFFmYeoEufxshsLIJ_ik'`

*  **URL Params**

    **Required:**
 
    `id=[integer]`

* **Query Params**

    None

* **Data Params**

   ```typescript
      {
        email: string,
        password: string
      }
    ```

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:** 
    ```json
      {
        "email": "olivier12@mail.com",
        "password": "$2a$10$dvRIbUcWuFkuY/gJsi5fAORBJ9DsHmSOLawKzT4Rzf7C6mon/cwWe",
        "id": 1
     }
    ```
 
* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** 
    `"Private resource replacement: request body must have a reference to the owner id"`

* **Notes:**

    None

</details>



**Delete User**
----
Delete user

<details>

* **URL**

    /users/:id

* **Method:**

    `DELETE`

* **Headers:**
    
    `'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im9saXZpZXIxQG1haWwuY29tIiwiaWF0IjoxNjc1NDAyMjM1LCJleHAiOjE2NzU0MDU4MzUsInN1YiI6IjEifQ.V_lNh4EXi2DtVcOD7UDrZblxFFmYeoEufxshsLIJ_ik'`

*  **URL Params**

    **Required:**
 
    `id=[integer]`

* **Query Params**

    None

* **Data Params**

    None

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:** 
    ```json
      {}
    ```
 
* **Error Response:**

  * **Code:** 401 Unauthorized <br />
    **Content:** 
    `"Cannot read properties of undefined (reading 'id')"`

* **Notes:**

    None

</details>
