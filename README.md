# Homework 3

* Assigned: 3/11
* Due: 4/1 @ 10AM ET
* worth 3.75% of your grade

In this assignment it's time to get real!  You'll first flex your SQL
muscles by
writing SQL and reflecting on the experience.  
You will then perform some normalizations.


# 1. SQL, the sequel

* [Click here to open the HW3 notebook in google colab](https://drive.google.com/file/d/19405dMQzrKoHMnasybrIeYyX2I_JefRD/view?usp=sharing)
* Click "ctrl + s" and save a copy to your own Google Drive
* Follow the instructions in the notebook to complete and submit Part 1


# 2. (14 pts) Normalization

Click here [to open the Overleaf latex template](https://www.overleaf.com/read/rmfpnzcdsfxq) where you will write your answers.   Clone the template and edit it.   Hand writing or alternative submission formats are NOT accecptable.

### Warmup questions:

(2 points) **Q2.1**: You have a relation `R(A,B,C)` and functional dependencies 
  `C->A, A->B`

  * What are all the non-trivial functional dependencies in the closure
    that have  only one attribute on the right side?
  * What are all the keys of `R`?

(3 points) **Q2.2**: You have a relation `S(A, B, C, D)` and functional dependencies 
  `AB->C, BC->D, CD->A, and AD->B`

  * What are all the non-trivial functional dependencies in the closure
    that have  only one attribute on the right side?
  * What are all the keys of `S`?

### Real application. 

The Iowa dataset has the following un-normalized schema:


        CREATE TABLE iowa (
            address char(256),
            bottle_volume_ml integer,
            category char(256),
            category_name char(256),
            city char(256),
            county char(256),
            county_number char(256),
            date date,
            im_desc char(256),
            invoice_line_no char(256),
            itemno integer,
            name char(256),
            pack integer,
            sale_bottles integer,
            sale_dollars double precision,
            sale_gallons double precision,
            sale_liters double precision,
            state_bottle_cost double precision,
            state_bottle_retail double precision,
            store integer,
            store_location char(256),
            store_location_address char(256),
            store_location_city char(256),
            store_location_zip char(256),
            vendor_name char(256),
            vendor_no integer,
            zipcode text
        );

Suppose we have the functional dependencies:

        store -> address, name, city, zipcode, store_location, store_location_adress,
                county_number, county, store_location_zip, store_location_city
        vendor_no -> vendor_name
        category -> category_name
        itemno -> category, bottle_volume_ml, im_desc, state_bottle_cost, state_bottle_retail
        date, store, vendor_no, itemno, invoice_line_no -> pack, sale_bottles, sale_dollars, sale_gallons, sale_liters


(2 points) **Q2.3**: What are the keys in 'iowa'?

(3 points) **Q2.4**: Decompose `iowa` into 3NF (Third Normal Form).  Write a few sentences to justify
  why you chose the tables you did.  

(2 points) **Q2.5**: Is your schema redundancy and anomaly free?  Justify your answer in
   a few sentences.

(2 points) **Q2.6**: We want to ensure that an order cannot purchase more than 10
   bottles (`bottle_qty`).  Can you enforce this using functional 
   dependencies?  Justify your answer

(1 point) **Q2.7**: Let's verify whether `store` indeed determines the store name.   How many distinct `name` values 
   exist for `store` number `2508` in the `iowa` dataset?  Solve this by running a SQL query.

(1 point) **Q2.8**: In class, we discussed that functional dependencies (and constraints in general) cannot be
  determined just by looking at data in the database.  
  Argue in one or two sentences whether or not `store -> name` is should actually be a functional dependency and why.  





# Submission

[Gradescope](https://www.gradescope.com/)
