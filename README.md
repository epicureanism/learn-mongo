# learn-mongo
## Overview
RDBMS | MongoDB
------------ | -------------
Database |	Database
Table |	Collection
Tuple/Row |	Document
column | Field
Table Join | Embedded Documents
Primary Key	| Primary Key (Default key _id provided by MongoDB itself)

- A Collection is a group of MongoDB documents.
- A Document is a set of key-value pairs.

### Advantages of MongoDB over RDBMS
- Schema less 
  − MongoDB is a document database in which one collection holds different documents. Number of fields, content and size of the document can differ from one document to another.
- Structure of a single object is clear.
- No complex joins.
- Deep query-ability
  - MongoDB supports dynamic queries on documents using a document-based query language that's nearly as powerful as SQL.
- Easier ORM
  - Conversion/mapping of application objects to database objects not needed.
- Faster
  - Uses internal memory for storing the (windowed) working set, enabling faster access of data.
  
## Data Model Desgin
### Embedded Data Model
All the related data in a single document.
```js
{
	_id: ,
	Emp_ID: "10025AE336"
	Personal_details:{
		First_Name: "Radhika",
		Last_Name: "Sharma",
		Date_Of_Birth: "1995-09-26"
	}
}
```
### Normalized Data Model
Refer the sub documents in the original document, using references.
```js
{
	_id: <ObjectId101>,
	Emp_ID: "10025AE336"
}
```
```js
{
	_id: <ObjectId102>,
	empDocID: " ObjectId101",
	First_Name: "Radhika",
	Last_Name: "Sharma",
	Date_Of_Birth: "1995-09-26"
}
```

### Considerations while designing Schema in MongoDB
- Combine objects into one document if you will use them together. Otherwise separate them (but make sure there should not be need of joins).
- Duplicate the data (but limited) **because disk space is cheap as compare to compute time**.
- **Do joins while write, not on read**.
- Optimize your schema for **most frequent use cases**.
- Do complex aggregation in the schema.

## Query
The following equivalent SQL where clause is 'select title from mycollections where viewed>=10 AND (by = 'tutorials point' OR title = 'MongoDB Overview')'
```js
db.mycollections.find(
	{
	  "viewed": {$gte:10}, 
	  $or: [
		{"by": "tutorials point"},
   		{"title": "MongoDB Overview"}]},
	{ title: 1}) //1 for show; 0 for hide
```
