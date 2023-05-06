---
title: Data Modelling
---

Aims of data modelling
* describe what information is contained in the database
* describe relationships between data items
* describe constraints on data

Data modelling is a design process
* converts requirements into a data model

Kinds of data models:
* logical: abstract, for conceptual design (e.g. ER, UML)
* physical: record-based, for implementation (e.g. relational, SQL)  
<img src="imgs/img1.png" width="500"/>

The most important aspects of a design:
* correctness
* completeness
* consistency

Potential inadquencies in a design:
* omits information that needs to be included
* contains redundant information
* leads to an inefficient implementation
* violate syntatic or semantic rules of a data model

## **ER Models**

An entity-relationship model has three major constructs:
* attribute
* entity
* relationship

An ER diagram consists of:
* a collection of entity set ("entity") definitions
* a collection of relationship set ("relationship") definitions
* attributes associated with entity and relationship sets
* connections between entity and relationship sets

<img src="imgs/img2.png" width="500"/>  

Attributes

<img src="imgs/img7.png" width="300"/>  

Keys
* Primary key: unique attribute in an entity set
* Candidate key: potential key
* Discriminator: weak key

<img src="imgs/img4.png" width="300"/>  

Degree
* Number of entities involved in a relationship

<img src="imgs/img5.png" width="500"/>  

Cardinality
* Number of associated entities on each side of relationship

<img src="imgs/img6.png" width="500"/> 

Participation
* partial: entity may or may not be involved in relationship
* total (bold): entity must be involved in relationship

<img src="imgs/img3.png" width="500"/>

Subclasses and inheritance

<img src="imgs/img9.png" width="500"/>

<img src="imgs/img10.png" width="500"/>

Weak entities
* Weak entities results in weak relationships (?)

<img src="imgs/img8.png" width="500"/>

## **Relational Model**

A relational data model describes the world as a collection of inter-connected relations (or tables). Each relation has:
* a name
* a set of attributes, each having:
    * a name
    * a domain (set of allowed values)
        * which are atomic values (e.g. integer, string, date)
        * may be `NULL`
* a key

Consider relation R:
* Relation schema of R: `R(a_1:D_1, a_2:D_2, ..., a_n:D_n`
* Tuple of R: an element of `D_1 * D_2 * ... * D_n` (a list of values or a row in the table)
* Instance of R: subset of `D_1 * D_2 * ... * D_n` (a set of tuples)

Example of a relation: `Account(branchName, accountNo, balance)`
* Instance of this relation:
```
{
  (Sydney, A-101, 500),
  (Coogee, A-215, 700),
  (Parramatta, A-102, 400),
  (Rouse Hill, A-305, 350),
  (Brighton, A-201, 900),
  (Kingsford, A-222, 700)
  (Brighton, A-217, 750)
}
```
* As a table:

<img src="imgs/img11.png" width="400"/> 

Constraints
* Constraints are logical statements:
    * domain constraints: limit the set of values that attributes can take
        * e.g. age must be `0 <= age <= 100`
    * key constraints: identify attributes that uniquely identify tuples
        * e.g. `Student(id, ...)` is guaranteed unique
    * entity integrity constraints: require keys to be fully-defined
        * e.g. `Class(Mon, 2pm, Lyre, ...)` is well defined, but `Class(NULL, 2pm, Lyre, ...)` is not well defined
    * referential integrity constraints: require references to other tables to be valid
        * e.g.  
<img src="imgs/img12.png" width="500"/> 

## **ER Model -> Relational Model**

Correspondences between relational and ER data models:
* entity set (ER) = relation (Rel) 
* relationship (ER) = relation (Rel)
* entity (ER) = tuple (Rel)
* attribute (ER) = attribute (Rel)

Differences between relational and ER models:
* Relation model uses relations to model entities and relationships
* Relation model has no composite or multi-valued attributes (only atomic)
* Relation model has no object-oriented notions (e.g. subclasses, inheritance)

Example:  
<img src="imgs/img13.png" width="500"/> 

Weak entity example:  
<img src="imgs/img14.png" width="500"/> 

1:N Relationship example:  
<img src="imgs/img15.png" width="500"/> 

1:1 Relationship example:
* Any relation may be chosen to house the foreign key  
<img src="imgs/img16.png" width="500"/> 

Multi-valued entities example:  
<img src="imgs/img17.png" width="500"/>

Mapping subclasses example:  
<img src="imgs/img18.png" width="500"/>
<img src="imgs/img19.png" width="500"/>
