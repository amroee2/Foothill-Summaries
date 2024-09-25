# Entity Relationship Diagrams

An Entity-Relationship Diagram (ERD) is a visual representation of the data model of a system, depicting entities, attributes, and the relationships between them. ERDs are widely used in database design and serve as a blueprint for creating the structure of a relational database.

**Components of an ERD**

- Entities:

Represent objects or concepts that have distinct and independent existence in the domain being modeled. For example, in a university database, entities could be Student, Course, Instructor, etc.
Notation: Typically represented as rectangles.

- Attributes:

Characteristics or properties of an entity. For example, for the Student entity, attributes could include StudentID, Name, DateOfBirth, etc.
Notation: Usually represented as ovals connected to their entity.

- Primary Key:

A unique attribute (or a combination of attributes) that uniquely identifies each record in an entity. For example, StudentID in the Student entity.

- Relationships:

Represent associations between two or more entities. For example, a Student enrolls in a Course.
Notation: Depicted as diamonds or lines connecting entities. Labeled with relationship names.

- Cardinality:

Describes the number of instances of one entity that can be associated with an instance of another entity. The common types of cardinality include:

- One-to-One (1:1): A single entity instance in one entity is related to a single entity instance in another. For example, each Person has exactly one Passport.
  
- One-to-Many (1:M): A single entity instance in one entity is related to many instances in another. For example, one Instructor teaches many Courses.
  
- Many-to-Many (M:M): Many instances in one entity are related to many instances in another. For example, many Students can enroll in many Courses.
