# Educase India Task

This is an assignment given to me by Educase India via Internshala

You can follow the steps given below to run this project, but first of all, you must have installed  
• Node JS  
• MySQL

## Installation

Open the terminal in any code editor and run the following command

```bash
git clone https://github.com/nipun-io/Educase_India_Task.git
```

This will clone the repository in your editor including all its files

Steps to configure the project

1. create a .env file in the root folder of the cloned project
   in the .env file enter these credentials

```env
DATABASE_URL= mysql://<YourUserName>:<YourPassword>@localhost:3306/educaseindia
PORT=3000
```

in place of **"YourUsername"** and **"YourPassword"** type the username and password of your MySQL server

Now open the terminal in the code editor and type down the following commands one by one

```bash
npm install
```

then, run the following command

```bash
npx prisma generate
```

this command will generate prisma in your project, then

```bash
npx prisma migrate dev --name init
```

Now rin this command

```bash
npm run dev
```

this command will start the server.

## Database Schema 📝

```prisma
model School {
  id        Int      @id @default(autoincrement())
  name      String
  address   String
  latitude  Float
  longitude Float
  createdAt DateTime @default(now()) @map("created_at")

  @@map("schools")
}
```

## API Reference 📚

### Add School

**Endpoint:** `POST /api/addSchool`

**Required Parameters:**

```javascript
{
  name: string,      // School name
  address: string,   // School address
  latitude: float,   // Geographical latitude
  longitude: float   // Geographical longitude
}
```

**Example Request:**

```bash
curl -X POST http://localhost:3000/api/addSchool \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Example School",
    "address": "123 Education Street",
    "latitude": 40.7128,
    "longitude": -74.0060
  }'
```

**Success Response:**

````javascript
{
  "status": "success",
  "message": "School added successfully",
  "data": {
    "id": 1,
    "name": "Example School",
    "address": "123 Education Street",
    "latitude": 40.7128,
    "longitude": -74.0060,
    "createdAt": "2023-01-01T00:00:00.000Z"
  }
}
### List Schools

**Endpoint:** `GET /api/listSchools`

**Query Parameters:**
```javascript
{
  latitude: float,   // User's current latitude
  longitude: float   // User's current longitude
}
````

**Example Request:**

```bash
curl "http://localhost:3000/api/listSchools?latitude=40.7128&longitude=-74.0060"
```

**Success Response:**

```javascript
{
  "status": "success",
  "data": [
    {
      "id": 1,
      "name": "Example School",
      "address": "123 Education Street",
      "latitude": 40.7128,
      "longitude": -74.0060,
      "distance": 1.5
    }
    // ... more schools
  ]
}
```

Error Handling 🚨  
The API uses standard HTTP response codes:

200: Success  
201: Created  
400: Bad Request  
404: Not Found  
500: Internal Server Error

## Example Postmen Collection link: [Educase India](https://api-testing-3299.postman.co/workspace/API-Testing-Workspace~1cf72d95-9a84-437e-83ea-d4dda42ff83d/collection/32127961-95978766-d126-46b6-b105-836701f64e79?action=share&creator=32127961)
