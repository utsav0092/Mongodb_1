 <h1>MongoDB Shell Commands</h1>

  <h2>Connecting to MongoDB</h2>
    <p>To connect to the MongoDB shell:</p>
    <pre><code>mongosh</code></pre>
    <p>Press <code>Enter</code> to initiate the connection.</p>

  <h2>Database Operations</h2>

  <h3>Show Databases</h3>
    <p>To list all databases:</p>
    <pre><code>show dbs</code></pre>

  <h3>Use a Database</h3>
    <p>To switch to a specific database:</p>
    <pre><code>use "database_name"</code></pre>

  <h3>Create a New Database</h3>
    <p>To create a new database (this command also switches to it):</p>
    <pre><code>use "database_name_you_want_to_create"</code></pre>

  <h3>Drop a Database</h3>
    <p>To delete the current database:</p>
    <pre><code>db.dropDatabase()</code></pre>
    <p><strong>Output:</strong></p>
    <pre><code>{ ok: 1, dropped: "collection_name" }</code></pre>

  <h2>Collection Operations</h2>

  <h3>Add a Collection</h3>
    <p>To create a new collection in the current database:</p>
    <pre><code>db.createCollection("collection_name")</code></pre>
    <p><strong>Output:</strong></p>
    <pre><code>{ ok: 1 }</code></pre>

   <h3>Insert One Document</h3>
    <p>To insert a single document into a collection:</p>
    <pre><code>db."collection_name".insertOne({"key":"value"})</code></pre>
    <p><strong>Output:</strong></p>
    <pre><code>{
  acknowledged: true,
  insertedId: ObjectId('ID')
}</code></pre>

  <h3>Insert Many Documents</h3>
    <p>To insert multiple documents into a collection:</p>
    <pre><code>db."collection_name".insertMany([{"key":"value"}, {"key":"value"}, {"key":"value"}])</code></pre>
    <p><strong>Output:</strong></p>
    <pre><code>{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('ID'),
    '1': ObjectId('ID'),
    '2': ObjectId('ID')
  }
}</code></pre>

  <h2>Query Operations</h2>

  <h3>Find Documents</h3>
    <p>To retrieve all documents from a collection:</p>
    <pre><code>db."collection_name".find()</code></pre>
    <p><strong>Output:</strong></p>
    <pre><code>[
  {
    _id: ObjectId('ID'),
    name: 'Spongebob',
    age: 30,
    gpa: 3.2
  }
]</code></pre>

  <h3>Sort Documents</h3>
    <p>To sort documents by a specific key:</p>
    <pre><code>db.students.find().sort({"key": 1})  // 1 for ascending, -1 for descending</code></pre>

  <h3>Limit Number of Documents</h3>
    <p>To limit the number of documents returned:</p>
    <pre><code>db.students.find().limit(10)</code></pre>
    <p><strong>With sorting:</strong></p>
    <pre><code>db.students.find().sort({"key": 1}).limit(1)</code></pre>

  <h2>Data Types in MongoDB</h2>

  <h3>Example Document with Various Data Types</h3>
    <pre><code>db.students.insertOne({
  name: "string goes here",                 // String
  age: 30,                                  // Integer
  fullTime: false,                          // Boolean
  registerDate: new Date(),                 // Date Object
  graduateDate: null,                       // Null
  courses: ["maths", "science", "bio"],     // Array
  address: {                                // Nested Document
    street: "123 Fake St.",
    city: "don't know",
    name: "also don't know"
  }
})</code></pre>

  <h2>MongoDB Compass</h2>

  <h3>Insert Documents Using Compass</h3>
    <ol>
        <li>Open MongoDB Compass.</li>
        <li>Select the database and collection.</li>
        <li>Use the GUI to insert documents.</li>
    </ol>

  <h2>Query and Update Operations</h2>

  <h3>Query Documents</h3>
    <pre><code>db.students.find({query},{projection})</code></pre>
    <p>Example:</p>
    <pre><code>db.students.find({}, {name: true})</code></pre>

  <h3>Update Documents</h3>
    <pre><code>db.students.updateOne({query},{$set:{update}})  // Update one document
db.students.updateMany({},{$set:{update}})      // Update many documents
</code></pre>
    <p>If there are documents with the same name, use:</p>
    <pre><code>db.students.updateOne({_id:ObjectId("")},{$set:{updated query}})</code></pre>

  <h3>Unset a Field</h3>
    <pre><code>db.students.updateOne({query},{$unset:{field:1}})  // 1 to delete</code></pre>

  <h3>Check if Field Exists and Set</h3>
    <p>If a field doesn't exist, you can set it:</p>
    <pre><code>db.students.updateMany({fullTime:{$exists:false}}, {$set:{fullTime:true}})</code></pre>

  <h3>Delete Documents</h3>
    <p>To delete one document:</p>
    <pre><code>db.students.deleteOne({query})</code></pre>
    <p>To delete many documents:</p>
    <pre><code>db.students.deleteMany({query})</code></pre>

  <h2>Comparison Operators</h2>

  <ul>
        <li><code>$eq</code> - equal to</li>
        <li><code>$ne</code> - not equal to</li>
        <li><code>$gt</code> - greater than</li>
        <li><code>$lt</code> - less than</li>
        <li><code>$gte</code> - greater than or equal to</li>
        <li><code>$lte</code> - less than or equal to</li>
    </ul>

  <p>Example:</p>
    <pre><code>db.students.find({gpa:{$lte:3, $gte:4}})</code></pre>

  <ul>
        <li><code>$in</code> - in array:</li>
    </ul>
    <pre><code>db.students.find({name:{$in:["first_name", "second_name"]}})</code></pre>

  <ul>
        <li><code>$nin</code> - not in array</li>
        <li><code>$mod</code> - modulus</li>
        <li><code>$regex</code> - regular expression</li>
    </ul>

  <h2>Logical Operators</h2>

  <ul>
        <li><code>$and</code> - and</li>
    </ul>
    <pre><code>db.students.find({$and: [{fullTime: true}, {age:{$lte:22}}]})</code></pre>

  <ul>
        <li><code>$or</code> - or</li>
        <li><code>$nor</code> - nor (both should be false)</li>
        <li><code>$not</code> - not</li>
    </ul>

  <h2>Indexes</h2>

  <p>Indexes help improve query performance but can take more memory and slow down inserts. Data is stored in a B-tree format.</p>

  <p>Without applying an index:</p>
    <pre><code>db.students.find({name:"Larry"}).explain("executionStats")</code></pre>

  <p>Create an index:</p>
    <pre><code>db.students.createIndex({name: 1})</code></pre>

  <p>To get the indexes:</p>
    <pre><code>db.students.getIndexes()</code></pre>

  <p>To drop an index:</p>
    <pre><code>db.students.dropIndex("name_1")</code></pre>

  <h2>Collections</h2>

  <p>A database is a group of collections, and a collection is a group of documents.</p>

  <p>To show collections:</p>
    <pre><code>show collections</code></pre>

  <h3>Create a New Collection</h3>
    <pre><code>db.createCollection("teacher", {capped:true, size:1024000, max:100}, {autoIndexId: false})</code></pre>

  <p><strong>Output:</strong></p>
    <pre><code>{ ok: 1 }</code></pre>

  <h3>Drop a Collection</h3>
    <pre><code>db.courses.drop()</code></pre>

  <h2>Other Commands</h2>

  <h3>Clear the Screen</h3>
    <p>To clear the terminal screen:</p>
    <pre><code>cls</code></pre>

  <h3>Exit the Shell</h3>
    <p>To exit the MongoDB shell:</p>
    <pre><code>exit</code></pre>
