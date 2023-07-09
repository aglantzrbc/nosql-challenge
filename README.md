# NoSQL Challenge

## nosql-challenge
Glantz Adam Bootcamp RUT-VIRT-DATA-PT-04-2023-U-LOLC-MWTH - Module 12 NoSQL Challenge

## TABLE OF CONTENTS

1. Project Description
   - Task 1: Database and Jupyter Notebook Set Up
   - Task 2: Update the Database
   - Task 3: Exploratory Analysis
2. Installation
3. Contributing
4. Acknowledgements
5. Licenses

### 1. PROJECT DESCRIPTION

This project is designed to assess student skills using the [PyMongo](https://pypi.org/project/pymongo/) driver for the [MongoDC](https://en.wikipedia.org/wiki/MongoDB) database to manipulate non-relationtional, object-based [NoSQL](https://en.wikipedia.org/wiki/NoSQL) files and work with them in [Python](https://en.wikipedia.org/wiki/Python_(programming_language)). The advantage of this is that database information in the cloud can be prepackaged in the desired form using an "aggregation pipeline" of sequential *match*, *group*, and *sort* queries before being imported to a local machine, maintaining efficiency and saving memory space.

In the project scenario, the editors of a fictional United Kingdom (UK) food magazine, *Eat Safe, Love*, want the author to evaluate some of the ratings data issued by the UK [Food Standards Agency](https://en.wikipedia.org/wiki/Food_Standards_Agency) (which assesses various establishments across the UK and gives them each a food hygiene rating) in order to help the magazine's journalists and food critics decide where to focus future articles. *Coding was guided by the [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) ("don't repeat yourself") principle*, though with two similar coding files for different parts of the same project, there were inevitably some redundancies.

- [Task 1: Database and Jupyter Notebook Set Up](https://courses.bootcampspot.com/courses/3337/assignments/54004?module_item_id=961459)

**FILE:** NoSQL_setup_1-2.ipynb

The author installed the necessary Python libraries (including PyMongo). A connection was established to a MongoDB server using the PyMongo library; MongoDB was allowed to run on its default port 27017. The database containing a .json collection was imported into MongoDB using this code in Git Bash when in the vicinity of the file: **_mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json_**. See **Figure 1** for an illustration. Proof of the success of the import of the database and its collection are shown in **Figure 2**.

![image](https://github.com/aglantzrbc/nosql-challenge/assets/127694342/14531a75-7b34-423c-9f4d-dc92cee17854)

**Figure 1** | *Git code pulling the database* uk_food *with the collection* establishments.json *into MongoDB, making sure any preexisting .json file with that name is deleted first*

![image](https://github.com/aglantzrbc/nosql-challenge/assets/127694342/9b58541e-27bd-4cfa-b921-ef1cf8951260)

**Figure 2** | *A MongoDBCompass GUI app screen capture showing the existence of the database and its collection in MongoDB*

- [Task 2: Update the Database](https://courses.bootcampspot.com/courses/3337/assignments/54004?module_item_id=961459)

**FILE:** NoSQL_setup_1-2.ipynb

Using the same file from Task 1, a record for a fictional new halal restaurant in Greenwich, *Penang Flavours*, was inserted into the collection and manipulated. Establishments from the Dover Local Authority were identified (994) and deleted. `RatingValue` and the coordinates `latitude` and `longitude` were coerced from strings to numbers and non-numeric RatingValue data (e.g., "Pass") were nullified, all in prerparation for Task 3. See **Figure 3** for the outcome of this last process.

![image](https://github.com/aglantzrbc/nosql-challenge/assets/127694342/80570701-f4b2-4b48-a94f-65423f399484)

**Figure 3** | *Jupyter Notebook output showing the coercion of strings into numbers for useful key values*

- [Task 3: Exploratory Analysis](https://courses.bootcampspot.com/courses/3337/assignments/54004?module_item_id=961459)

**FILE:** NoSQL_analysis_3.ipynb

The scenario for Task 3 is to help the editors of the *Eat Safe, Love* magazine answer specific questions from the current data, which will putatively help them find the locations they wish to visit and avoid. After making sure the new NoSQL_analysis_3.ipynb coding file has the same important features as the previous coding file (e.g., installed libraries), the following questions were posed and answered, with sample output converted to [Pandas](https://en.wikipedia.org/wiki/Pandas_(software)) DataFrames:

1. *Which establishments have a hygiene score equal to 20?* (Note - the lower the hygiene score, the better an establishment's cleanliness.) **Answer: 41 establishments**.
   
2. *Which establishments in London have a `RatingValue` greater than or equal to 4?* (Note - the numeric part of the RatingValue scale has a 1-5 range, with higher values better than lower values.) **Answer: 33 establishments**.

3. *What are the top 5 establishments with a `RatingValue` rating value of 5, sorted by hygiene score from lowest to highest, nearest to the new London restaurant added,* "Penang Flavours"? Nearness was defined as within 0.01 degree of `latitude` and `longitude`, approximately 1.11 km. As one ilustration, the closest establishment to *Penang Flavours* with the lowest RatingValue (i.e., 0 in this case) is a bar/pub/nightclub called *Volunteer*. See **Table 1**.

![image](https://github.com/aglantzrbc/nosql-challenge/assets/127694342/83147dca-f18c-433e-b6d6-a74a450438e2)

**Table 1** | *Jupyter Notebook output showing part of a Pandas DataFrame of the top 5 establishments with a `RatingValue` rating value of 5, sorted by hygiene score from lowest to highest, nearest to the new London restaurant,* "Penang Flavours"

4. *How many establishments in each Local Authority area have a hygiene score of 0?* An aggregation pipeline was used to find the answer, with records *matched* on a hygiene score of 0, *grouped* by Local Authority, and the output "*sorted* in descending order. **Answer: 55 establishments**. The DataFrame was normalized to "flatten" nested keys before being printed. See **Table 2**.

![image](https://github.com/aglantzrbc/nosql-challenge/assets/127694342/4b8b5fdf-2f34-4f76-989a-2df92f628071)

**Table 2** | *Jupyter Notebook output showing the final DataFrame of the top 10 establishments in each Local Authority area, in descending count order, that have a hygiene score of 0, after normalization*

### 2. INSTALLATION

- The file for *Database and Jupyter Notebook Set Up* and *Update the Database* tasks 1 & 2: **NoSQL_setup_1-2.ipynb**
- The file for *Exploratory Analysis* task 3: **NoSQL_analysis_3.ipynb**

- The [GitHub repository](https://github.com/aglantzrbc/data-scraping-challenge) (version 2.9.1) containing all project files is publicly accessible.
- The *Resources* subdirectory contains the *establishments.json* source file requested by the instructions. It is located in the same place as the code files. **If this relative placement is altered, the code won't run**
- As mentioned above, before starting to run the code, the user needs to install recent versions of MongoDB and Mongo Database Tools, and then run this code in a Git Bash terminal in the same subdirectory as the .json source file: *mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json*. **If this isn't done, the code won't run**
- It is intended for the user to run all of the *NoSQL_setup_1-2.ipynb* code and then, without a new mongoimport attempt, run the *NoSQL_analysis_3.ipynb* code, because the latter file's processes build upon accomplishments from the former. **If this sequence isn't adhered to or a new mongoimport command intervenes between running the two code files, the user may get different outputs than shown here and/or encounter errors.**
- Since certain code blocks make changes to the collection, rerunning "before and after" scenario code may lose the dinstinction that makes these processes worthwhile as a check. **Only run the code once.**
- The assignment details and starter code are proprietary and located on the [Rutgers University](https://www.rutgers.edu/) [(edX)](https://www.edx.org/) Bootcamp Spot [Module 12 NoSQL Challenge](https://courses.bootcampspot.com/courses/3337/assignments/54004?module_item_id=961459) webpage.
- Both source files use Python version 3.10.9. The project was coded in [Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/stable/) version 6.5.2. The *mongoimport* command was run in [Git Bash](https://git-scm.com/downloads) version 2.40.0.windows.1. The latest stable version of [Git](https://en.wikipedia.org/wiki/Git) itself is 2.41.
- The NoSQL database used here is MongoDB 6.0. The author also used *mongoimport* from [Mongo Database Tools](https://www.mongodb.com/docs/database-tools/) for Windows x86_64-100.7.3, the [Mongosh](https://www.mongodb.com/docs/mongodb-shell/) Shell 1.10.1-win32-x64, and the GUI app [MongoDBCompass](https://www.mongodb.com/products/compass) 1.38.2.

### 3. CONTRIBUTING

- [Glantz, Adam](https://www.linkedin.com/in/adam-glantz/): Annapolis, Maryland, USA, July 2023, email: adamglantz@yahoo.com

### 4. ACKNOWLEDGEMENTS

In addition to using the resources listed above, the author acquired query responses in OpenAI's [ChatGPT](https://chat.openai.com/) 3.5 platform and the [VSCode GitHub Copilot](https://github.com/features/copilot) app.

The author also consulted code and results from similar projects publicly accessible in [GitHub](https://github.com/) repositories and recoverable through [Google](https://www.google.com/) and comparable search engines:

- [Bacza, Patrick](https://www.linkedin.com/in/patrick-bacza/): Newtown, Pennsylvania, USA, March 2022. [nosql-challenge](https://github.com/Patrick-Bacza/nosql-challenge)
- [Stegall-Rodriguez, Sarah](https://www.linkedin.com/in/sarsteg/): Brownsville, Texas, USA, June 2023. [nosql-challenge](https://github.com/sarsteg/nosql-challenge)
- [Wang, Yeyan](https://www.linkedin.com/in/yeyan-wang/): Seattle, Washington, USA, March 2023. [nosql-challenge](https://github.com/yeyanwang/nosql-challenge)


### 5. LICENSES

**N/A**


