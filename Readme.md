# This program demonstarte working with json server
# Building the backend
## install server
    npm install json-server

##  Create a db.json  file

    db.json:
    {
    "cars": [
      { "id": "1", "color": "red", "brand": "kia" },
      { "id": "2", "color": "green", "brand": "tsla" },
      { "id": "3", "color": "blue", "brand": "mazda" }
    ]
  }

# run the server
    npx json-server db.json

# result :
    Index:
    http://localhost:3000/

    Static files:
    Serving ./public directory if it exists

    Endpoints:
    http://localhost:3000/posts   
    http://localhost:3000/comments
    http://localhost:3000/profile 


# Building the frontend

## install axios
    <!DOCTYPE html>
    <html lang="en">
    <head>
        ...
        <script src="https://cdn.jsdelivr.net/npm/axios@1.6.7/dist/axios.min.js"></script>
    </head>
    <body>
        
    </body>
    </html>

## CRUD
    get - read
    put - update
    post - add new 
    delete - delete

## GET example
    <body>
        <script>
            const SERVER = "http://127.0.0.1:3000/cars"
            axios(SERVER).then(res => console.log(res.data))
        </script>
    </body>


## GET , POST (create new )
        <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        <script src="https://cdn.jsdelivr.net/npm/axios@1.6.7/dist/axios.min.js"></script>
    </head>

    <body>
        Color:<input id="carColor">
        brand:<input id="carbrand">
        <button onclick="add()"> Add</button>
        <script>
            const SERVER = "http://127.0.0.1:3000/cars"
            axios(SERVER).then(res => console.log(res.data))

            // const add = () => axios.post(SERVER, data).then(res => console.log(res))
            const add = () => axios.post(SERVER, { "color": carColor.value, "brand": carbrand.value }).then(res => console.log(res))
        </script>
    </body>

    </html>

# complete CRUD
    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        <script src="https://cdn.jsdelivr.net/npm/axios@1.6.7/dist/axios.min.js"></script>
    </head>

    <body>
        Color:<input id="carColor">
        brand:<input id="carbrand">
        <button onclick="add()"> Add</button>
        <hr>
        <div id="display"></div>
        <script>
            const SERVER = "http://127.0.0.1:3000/cars/"
            axios(SERVER).then(res => display.innerHTML = res.data.map(car => `
            <div>
                <button onclick="del('${car.id}')"> del</button>
                <button onclick="upd('${car.id}')"> upd</button>
                color:${car.color},
                brand:${car.brand}
            
            </div>
            `).join(""))

            // const add = () => axios.post(SERVER, data).then(res => console.log(res))
            const add = () => axios.post(SERVER, { "color": carColor.value, "brand": carbrand.value }).then(res => console.log(res))

            const del=(id)=>{
                console.log(id);
                axios.delete(SERVER  + id)
            }

            const upd=(id)=>{
                console.log(id);
                axios.put(SERVER  + id,{ "color": carColor.value, "brand": carbrand.value })
            }
        </script>
    </body>

    </html>