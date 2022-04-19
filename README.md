# Designing_Data_Intensive_Applications
Summary for Book Data Intensive Applications
![Book Cover Data Intensive](./book-cover.jpg "Book Cover")

1. Part 1: The fundamental ideas that underpin the design of data-intesive applications.
    - Chapter 1. What is Reliability,Scalability and maintanability ?
        - Reliability:
            - Simple Definition: Continue to work correctly, even when things go wrong.  
            - Things that can go wrong are faults. System anticipating faults are fault-tolerant or resilient.
            - Fault is not the same as a failure. Fault is deviating from the spec of the system.
    - Chapter 2
    - Chapter 3 
    - Chapter 4
2. Part 2: Move from data store on one machone tp data that is distributed across machines. Often needed for scalability
3. Part 3: Discuss Systems that derive some datasets from other datasets. Derived data often occurs in heterogenerous systems(multiple system CPU, GPU) where one database can't do everything well. Potential example is a media website that use mySql for user account data and AWS S3 buckets for storing the media. 
