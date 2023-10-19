

## Mongo DB

- No Sql Design considerations

   - 16 MB limit for per document
   - There's no rules for no sql DB to store data in a certain way

- Schema approach

   1. Schema less
   2. Flexible Schema
   3. Strict Schema

- MongoDB Datatypes

   - Text
   - Boolean
   - Number
      - NumberInt
      - NumberLong
      - NumberDecimal

   - ObjectId
   - ISODate
   - EmbeddedObject
   - Array

- Relationship in MongoDB

   - Your default preference should always be embedded if you have valid reason then you should go for the reference approach

   1. Embedded
      - Pros
         - Performance
         - Simplicity
         - Atomic Operations
         - Get all Data in one query (Avoids expensive joins and $lookups )

      - Cons
         - Size limitation
         - Unbound Growth will leads to size limitations

      - When to choose Referenced
         - If Data is not frequently updated
         - When you want to access that data together (Read)
         - When you need better performance
         - When you know the limit

      - Ex:
         - one to one relationships
         - User and his addresses , credit card

   2. Referenced
      - Pros
         - smaller documents
         - No duplication data
         - Scalability
         - Data Normalization
         - More structured schema

      - Cons
         - Performance as you have to do two queries or $lookup
         - Complexity

      - When to choose Referenced
         - If There are frequent Write operations
         - When you can not predict the size of the array
         - You need Normalization on your data

      - Ex:
         - One to Many relationship
         - User and it's posts (where there's no limit on how many numbers of post a user can post)
         - One to trillions (Unbounded data)
         - system logs schema

- Schema Validations

   - DataTypes
   - Required field
   - Field Length Constraints (maxLength)
   - Field Value Constraints (minimum maximum)
   - Pattern Matching
   - Enumeration
   - Nested Document Validation
   - Array Validation
   - Custom Validation

- Considerations (Suggested by mongoDB)

   - The main consideration depends on your project's specification
   - Embed unless there's a compelling reason not to
   - Avoid joins if they can be avoided but don't be afraid of using them if they provide better schema design.
   - Array should not grow without bound
   - You should use indexes since without it MongoDb will scan the whole collection one by one

- Schema Design Anti-pattern (Suggested by mongoDB)

   1. Massive array
      - it can reach upto limit of 16 mb document size
      - index perfomance decreases when the array size is increased

   2. Massive numbers of collections
      - Since every collection has it's own index storage
      - (MongoDB suggested Limit) is 10,000 collection per replica

   3. Do remove empty or unused collections
   4. Unnecessary indexes
      - indexes takes up the space and resources
      - It can impact the storage engine performance
      - It can impact on write performance
      - Two types of indexes you should remove
         1. Rarely used indexes
         2. Redundant indexes

      - (MongoDB suggested Limit) 50 index per each collection

   5. Bloated Documents :
      - Don't store all related data together instead store only that data together which is accessed together

   6. Create caseinsensitive indexes wherever needed
   7. Don't separate data which is accessed together unless it's required
      - $lookup can be slow and resource intensive
      - getting data from multiple collections is slow and resource intensive than getting data from single document