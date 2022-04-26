# Summary Designing Data Intensive Applications
![Book Cover Data Intensive](./book-cover.jpg "Book Cover")

- [Summary Designing Data Intensive Applications](#summary-designing-data-intensive-applications)
- [Part 1: The fundamental ideas that underpin the design of data-intensive applications.](#part-1-the-fundamental-ideas-that-underpin-the-design-of-data-intensive-applications)
  - [Chapter 1. What is Reliability,Scalability and maintainability ?](#chapter-1-what-is-reliabilityscalability-and-maintainability-)
    - [Reliability:](#reliability)
    - [Describing Performance:](#describing-performance)
  - [Chapter 2. Data models and query languages](#chapter-2-data-models-and-query-languages)
    - [Normalize vs un-normalized data](#normalize-vs-un-normalized-data)
    - [Database Types](#database-types)
      - [Network Database AKA CODASYL model](#network-database-aka-codasyl-model)
      - [Relational Database](#relational-database)
- [Part 2: Move from data store on one machine to data that is distributed across machines. Often needed for scalability.](#part-2-move-from-data-store-on-one-machine-to-data-that-is-distributed-across-machines-often-needed-for-scalability)
- [Part 3: Discuss Systems that derive some datasets from other datasets. Derived data often occurs in heterogeneous systems(multiple system CPU, GPU) where one database can't do everything well. Potential example is a media website that use mySql for user account data and AWS S3 buckets for storing the media.](#part-3-discuss-systems-that-derive-some-datasets-from-other-datasets-derived-data-often-occurs-in-heterogeneous-systemsmultiple-system-cpu-gpu-where-one-database-cant-do-everything-well-potential-example-is-a-media-website-that-use-mysql-for-user-account-data-and-aws-s3-buckets-for-storing-the-media)



# Part 1: The fundamental ideas that underpin the design of data-intensive applications.

## Chapter 1. What is Reliability,Scalability and maintainability ?

### Reliability:
- Simple Definition: Continue to work correctly, even when things go wrong.  
- Things that can go wrong are faults. System anticipating faults are fault-tolerant or resilient.
- Fault is not the same as a failure. Fault is deviating from the spec of the system.
- Errors come from. Hardware Errors, Software Errors, Human Errors. One study found configuration errors by operators to be the leading cause of outages, where hardware faults (servers or network) 
### Describing Performance:
  - In a batch processing system such as hadoop, we usually care about _throughput_. **In online systems** service's response time is more important
  - **Response times** should be thought as a distributions of values.
  - Latency and Response Time are completely different. Latency is how long it takes for the service to start handle the request (think network path, queue waiting etc). 
  - Media is a good way to see how the average user experience, since 50% will be slower and 50% faster 
  - Outlines are catch better by p95, p99, p99.9
    - Amazon targets for internal service 99.9%. Even though it affects only 1 in 1000 request is because those with the slowest request are often the ones who have the most data on their account, because they have made many purchases--in short, they are the most valuable customers.
    - amazon has also observed 100ms increase in response time reduced sales by 1%, and other reports that 1 second slowdown reduces customer satisfaction metric by 16%.


## Chapter 2. Data models and query languages

### Normalize vs un-normalized data

| Normalize Data                                                                                                                                                                                                                         | Denormalized Data                                                                                                                                                                                                          |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Data is store using and ID and value                                                                                                                                                                                                   | Data is store directly as a string                                                                                                                                                                                         |
| Multiple request to join and get the values you need for a model                                                                                                                                                                       | In denormalized database data can be store directly as json                                                                                                                                                                |
| One source for things like cities. Less storage used and is easy to change if needed(example political changes)                                                                                                                        | A renaming would be very difficult if you allow people to enter any sort of string                                                                                                                                         |
| Queries are a lot more powerful as they can infer more about the data. <br/> For example you can count seattle being in Washington since is part of the data selected. <br/> This is less clear when user types 'Greater Seattle area' | Queries have to be done in application code. <br/> That means making multiple request and performing the operation in memory. <br/> For cities that is not too much memory but for certain models that can become an issue |

### Database Types
Relational database and noSql database are the most popular and heavily debate since 1970.  
One less know database that never got popular is the network database

#### Network Database AKA CODASYL model

How it worked: 
- In the tree structure of a hierarchical mode, every record has exactly one parent.    
- In the network model a record can have multiple parents.   
- Example 'Greater London Area' and every user who lived in that region could be linked to it. Allowing many to one and many-to-many relationships to be made.   
- The links between record were not foreign keys but rather pointers line in code. To access a record you need to follow a path from root along the chines of links.  

Cons:
- The code for querying and updating the database was difficult. 
- If you change the path you had to rewrite all the manually handcrafted queries traversing the path or else it will break

#### Relational Database
- SQL database are written as tuples and unlike Network database, they use complicated query analyser to determine the best path and index to use to query the data.  
- Main difference is that this is done automatic without developer input outside of maybe creating indexes.  



# Part 2: Move from data store on one machine to data that is distributed across machines. Often needed for scalability.  



# Part 3: Discuss Systems that derive some datasets from other datasets. Derived data often occurs in heterogeneous systems(multiple system CPU, GPU) where one database can't do everything well. Potential example is a media website that use mySql for user account data and AWS S3 buckets for storing the media. 
