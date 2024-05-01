### Node MongoDB Postman API Testing

Initialize a new Node.js project
```
npm init -y
```

Install MongoDB for project
```
npm install mongodb
```

Install express 
```
npm install express
```

Install Body Parser
```
npm install body-parser
```

Add server.js in Root Directory
``` js
const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');

const app = express();
const port = 3000;

// Middleware
app.use(bodyParser.json());

// Connect to MongoDB
// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/mydb')
    .then(() => {
        console.log('Connected to MongoDB');
    })
    .catch((err) => {
        console.error('Error connecting to MongoDB:', err);
    });

mongoose.connection.on('error', console.error.bind(console, 'MongoDB connection error:'));

// Define routes
app.use('/api', require('./routes'));

// Start the server
app.listen(port, () => {
    console.log(`Server is listening at http://localhost:${port}`);
});
```

Add code in item.js in models folder

``` js
const mongoose = require('mongoose');

const itemSchema = new mongoose.Schema({
    name: String,
    description: String,
    price: Number
});

module.exports = mongoose.model('Item', itemSchema);

```

Add code in index.js in routes folder

``` js
const express = require('express');
const router = express.Router();
const Item = require('../models/item');

// Create an item
router.post('/items', async (req, res) => {
    try {
        const item = new Item(req.body);
        await item.save();
        res.status(201).send(item);
    } catch (err) {
        res.status(400).send(err);
    }
});

// Read all items
router.get('/items', async (req, res) => {
    try {
        const items = await Item.find();
        res.send(items);
    } catch (err) {
        res.status(500).send(err);
    }
});

// Update an item
router.patch('/items/:id', async (req, res) => {
    try {
        const item = await Item.findByIdAndUpdate(req.params.id, req.body, { new: true });
        if (!item) {
            return res.status(404).send();
        }
        res.send(item);
    } catch (err) {
        res.status(400).send(err);
    }
});

// Delete an item
router.delete('/items/:id', async (req, res) => {
    try {
        const item = await Item.findByIdAndDelete(req.params.id);
        if (!item) {
            return res.status(404).send();
        }
        res.send(item);
    } catch (err) {
        res.status(500).send(err);
    }
});

module.exports = router;

```


Run command for project
```
node server.js
```



Use POSTMAN to test API 
1. Insert Data using POST method
     ```
     http://localhost:3000/api/items
     ```
    Go to Body>raw>json
    ``` json
    {
    "name" : "Ice Cream",
    "Description" : "Creamed Ice cream",
    "price" : 20
    }
    ```

2. Read Data using GET method
   ```
   http://localhost:3000/items
   ```

3. Update Data using PATCH method
   ```
   http://localhost:3000/items/{id}
   ```

4. Update Data using PATCH method
   ```
   http://localhost:3000/items/{id}
   ```

Also See, the updated Infomation in MongoDB Compass at time of API TESTING

</br>
