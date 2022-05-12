# CouchDB Workshop

- Related concepts I learned about:
  - cluster: a computer cluster is a set of computers that work together so that they can be viewed as a single system. 
  - redundancy: data redundancy occurs when the same piece of data is stored in two or more separate places. 
  - latency: also called ping, refers to several kinds of delays typically incurred in the processing of network data. A low-latency network connection experiences small delay times, while a high-latency connection experiences long delays.
  
  
### What is CouchDB

CouchDB is an open-source NoSQL database, which store documents and implemented in Erlang. CouchDB is not a Relational Database Management System (RDBMS) and it doesn't use the Structured Query Language (SQL).

### When we should use it?

- General Purpose Data: we can use it in different kinds of applications, including data science, internet, financial, etc.
- Scalable big-data cluster:
  - store a lot of data: CouchDB allows us to create a _cluster_ that acts as a single database, but also it allows us to use the storage capacity of all the servers combined.
  - high availability: CouchDB clustering comes with _double redundancy_ built-in, that means if we have two server all the data will be duplicated with the intention of increasing reliability, so that if we lose a server, we can still access all of our data.
  - lot of requests: the clustering system allow us to spread the load across as many server we want and also we can add or remove servers to or from the cluster without any service interruption.
- Seamless Data Synchronisation: it's possible replicate data from one server to another located on another continent and now we have an up-to-date copy of our data here as well. And this works bi-directionally so it adds more fault tolerance, high availability and also lower latency as we can direct our user to the nearest server.

### Features:

- Schema Free (JSON): unlike a relational database, a CouchDB database doesn't store data and relationships in tables. Instead, each database is a **collection** of independent **documents**. What we are saving are JSON files because of that we don’t need any additional layer like an Object-Relational Mapping (ORM). But CouchDB will add them an `_id` (to identify them, it also acts as the primary key for the database that holds the document) and a `_rev` (to know the version of this file, when it was last modified, similar to git). Example:

```javascript
{
  "_id": "ja3kj23daa23nd34sas934",
  "_rev": "j323332end34sas934",
  "type": "text-document",
  "name": "Learning CouchDB",
  "author": {
    "firstName": "Mariano",
    "lastName": "Giménez",
  }
}
```

- Document Oriented NoSQL: document fields are **uniquely named**, contain values of varying types (text, number, boolean, lists, etc), and there is no set limit to text size or element count (CouchDB provides a RESTful HTTP API for reading and updating them). So, every time we want to group data we have to do it within a collection in a JSON format called documents. And we can treat them like in the real world because real-world data is managed as real-world-document, what does it mean? We can dump our data as it appears in our real-life document, we don't need all the documents in that collection to have the same fields or we don't have to think about adding more, so there is no need (like in SQL) to write in some fields 'none' or 'unknown', we can just ignore it. Think of a business card or an invoice, they are different from each other, and we just have to add them as we find them. So all the information we need from them, they already have, we call this **'self-contained'** data.


- RESTful HTTP API: we can communicate with a RESTful API to manipulate our documents. We can do it using `curl` and HTTP request, actually any and all communication from and to CouchDB is done over HTTP.
  Example, if I want to update my data (PUT - UPDATE):
  `curl -X PUT http://127.0.0.1:5984/marian-documents/01`
  `-d {`
  `"id":01`,
  `"type": "note"`
  `}`
  CouchDB will return

```javascript
{
  "ok": true,
  "id": "01",
  "rev": "2-sdasd",

}
```
