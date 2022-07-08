# Data Engineering Track

Tasks implementation
1. Create two tables (if they don't exist) to store pipeline job information. Go to task 2.
2. Insert a new record into the two tables, respectively. Go to task 3.
3. Randomly generate a given number of digits (from 0 to 9) and get the count of digits found in a given string. There is a 30% chance that
this task will raise an exception. If an exception is raised, go to task 4. Otherwise, go to task 5.
4. (This task runs only when there is an exception in task 3) Update the records created in task 2 with values indicating that the job is unsuccessful. The pipeline ends after this task.
5. (This task runs only when there is no exception in task 3) If the count in task 3 is greater than a given threshold, go to task 6. Otherwise, go to task 7.
6. Update the records created in task 2 with the information that the count is greater than a given threshold. The pipeline ends after this task.
7. Update the records created in task 2 with the information that the count is less than or equal to a given threshold. The pipeline ends after this task.
