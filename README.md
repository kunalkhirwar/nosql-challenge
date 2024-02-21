**Instructions**

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. I've been contracted by the editors of a food magazine, ***Eat Safe, Love***, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.


**Part 1: Database and Jupyter Notebook Set Up**

Used '*NoSQL_setup.ipynb*' for this section of the challenge.

1. Imported the data provided in the '*establishments.json*' file from the command promt. Named the database **uk_food** and the collection **establishments**.
2. Within my notebook, imported the libraries I needed: PyMongo and Pretty Print (pprint).
3. Created an instance of the Mongo Client.
4. Confirmed that I created the database and loaded the data properly:
   - Listed the databases I had in MongoDB. Confirmed that **uk_food** is listed.
   - Listed the collection(s) in the database to ensure that **establishments** is there.
   - Found and displayed one document in the **establishments** collection using **find_one** and displayed with pprint.
5. Assigned the **establishments** collection to a variable to prepare the collection for use.


**Part 2: Update the Database**

Used '*NoSQL_setup.ipynb*' for this section of the challenge.

The magazine editors have some requested modifications for the database before I could perform any queries or analysis for them. Made the following changes to the **establishments** collection:

1. An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine asked me to include it in my analysis.
2. Found the BusinessTypeID for "Restaurant/Cafe/Canteen" and returned only the *BusinessTypeID* and *BusinessType* fields.
3. Updated the new restaurant with the *BusinessTypeID* I found.
4. The magazine is not interested in any establishments in Dover, so checked how many documents contained the Dover Local Authority. Then, removed any establishments within the Dover Local Authority from the database, and checked the number of documents to ensure they were deleted.
5. Some of the number values were stored as strings, when they should be stored as numbers.
   - Used *update_many* to convert **latitude** and **longitude** to decimal numbers.
   - Used *update_many* to convert **RatingValue** to integer numbers.
  

**Part 3: Exploratory Analysis**

***Eat Safe, Love*** had specific questions they wanted me to answer, which would help them find the locations they wish to visit and avoid.

Used '*NoSQL_analysis.ipynb*' for this section of the challenge.

Some notes to be aware of while I was exploring the dataset:
  - **RatingValue** refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
      - **Note**: This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. I coerced non-numeric values to nulls during the database setup before converting ratings 
                     to integers.
  - The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.

Used the following questions to explore the database, and found the answers, so I could provide them to the magazine editors.

For each question, followed the process mentioned below:
  - Used *count_documents* to display the number of documents contained in the result.
  - Displayed the first document in the results using pprint.
  - Converted the result to a Pandas DataFrame, printed the number of rows in the DataFrame, and displayed the first 10 rows.

**Q1.** Which establishments have a hygiene score equal to 20?

**Q2.** Which establishments in London have a RatingValue greater than or equal to 4?

**Q3.** What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

**Q4.** How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.
