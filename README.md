# CSC 4402 Introduction to Database Management System Project
This project is built in MySQL Workbench.

To run the db and run our sql queries we used sqlite. To run the db, download sqlite3 and make sure all the sqlite exe files are in a directory with our 5 csv files(clubs, students, players, sports, and teachers).

CD to the directory that all the files are in then run sqlite.

  >sqlite3.exe

Then build the project

  >.open 'project'
 
  >.mode csv
  
  >.import 'students.csv' students
  
  >.import 'teachers.csv' teachers
  
  >.import 'clubs.csv' clubs
 
  >.import 'sports.csv' sports
  
  >.import 'players.csv' players

Now the db is built, and you can run our queries by typing them into the cmd line.


Find and order the salaries of teachers who head coach a sport that has at least 20 players:

>select tid, salary from teachers where tid in (select head_coach from sports s, players p where s.sport=p.sport group by p.sport having count(p.sid)>20) order by salary;

Purpose: Want to give a raise to the teachers who coach large sports teams as well as teaching



Find students who are on at least 2 sports team, in a club, and have a GPA > 3.5 and return their id, first and last name, number of teams, and GPA and order them by gpa in descending order:

>select s.sid, s.fname, s.lname, count(p.sport), s.gpa from students s, players p where s.sid=p.sid and gpa>3.5 and club not null group by s.sid having count(p.sport)>1 order by s.gpa desc;

Purpose: Want to give a special award to students who are active in extracurricular activities, while maintaining a high GPA




Find the sid, fname, and lname, all 2nd year or greater students in a sport and a club with a GPA < 2.0, sort in descending order by GPA

>select distinct(S.sid), S.fname, S.lname, S.GPA from Students as S, Players as P where S.sid = P.sid and S.year > 2 and S.GPA < 2.0 and S.club IS NOT NULL order by GPA desc;

Purpose: Need to meet with these students in order for them to focus on academics and graduate on time.


Find the average GPA of each sports team that has at least 20 students, order by average GPA in descending order: 

>select avg(S.GPA) as AVG_GPA, P.sport from Students as S, Players as P where S.sid = P.sid group by P.sport having count(P.sid) > 20 ORDER BY AVG_GPA desc;

Purpose: want to compare the academic achievements of the different sports teams at the school



Find all students with a last name between the letters A-E, sorted in alphabetical order

>select distinct(sid), lname, fname from Students where lname like 'A%' or lname like 'B%' or lname like 'C%' or lname like 'D%' or lname like 'E%' order by lname;

Purpose: Need to give a list of students to the advisor that handles students with a name between A-E.



Find the salary of all teachers who are head coaches and club sponsors

>select distinct(T.tid), T.fname, T.lname, T.salary from Teachers as T, Clubs as C where T.tid = C.sponsor INTERSECT select distinct(T.tid), fname, lname, salary from Teachers as T, Sports as A where T.tid = A.head_coach;

Purpose: want to give a raise to all teachers who are coaches and club sponsors as well as teaching



Find clubs with a budget of < 5000 and an average GPA of > 2.5

>select distinct(S.club), C.budget, avg(S.gpa) as avg_gpa from Clubs as C, Students as S where C.budget < 5000 group by S.club having avg_gpa > 2.5 Order by avg_gpa desc;

Purpose: want to raise the budget of clubs with a high GPA






List the number of students in each club and their budget, order by number of students

>select distinct(S.club), C.budget, count(S.sid) as num_students from Students as S, Clubs as C where C.name=S.club group by S.club Order by num_students desc;

Purpose: want to ensure that the clubs with the most students have appropriate budgets



Find all teachers in the Algebra or Calculus or Physics or Chemistry department that sponsor a club and a Sport

>select distinct(t.tid), T.fname, T.lname, C.name, A.sport from Teachers as T, Clubs as C, Sports as A where T.tid = C.sponsor and T.tid = A.head_coach and (T.subject='Algebra' or T.subject = 'Calculus' or T.subject = 'Physics' or T.subject = 'Chemistry');

Purpose: Find teachers that are eligible for STEM teacher of the year award.



Find students who are not in a club and do not play a sport:

>select fname, lname, sid from students where sid not in (select sid from players group by sid) and club='NULL';

Purpose: Send email Promotions of extracurriculars that the students might be interested in.



