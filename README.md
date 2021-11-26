# CSC 4402 Introduction to Database Management System Project
This project is built in MySQL Workbench.

To run the db and run our sql queries we used sqlite. To run the db make sure all teh sqlite exe files are in a directory with our 5 csv files(clubs, students, players, sports, and teachers).

run sqlite3 after you cd to the directory

  >sqlite3.exe

Then build the project

.open 'project'
 
.mode csv
  
.import 'students.csv' students
  
.import 'teachers.csv' teachers
  
.import 'clubs.csv' clubs
 
.import 'sports.csv' sports
  
.import 'players.csv' players

Now the db is built, and you can run our queries by typing them into the cmd line.
