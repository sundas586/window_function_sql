# window_function_sql

What are window functions used for?<br/>
What are Window Functions? Window functions enable users to perform calculations against partitions (i.e. subgroups or sections) of a result set, typically a table or the results from another query.

![1](https://user-images.githubusercontent.com/33677647/204666035-adbfeb09-d328-4867-b921-b4be1dbacd69.JPG)
![2](https://user-images.githubusercontent.com/33677647/204666044-d6a835ce-a21d-422b-acc0-8e77fdd51542.JPG)
![3](https://user-images.githubusercontent.com/33677647/204666063-62806e54-2614-4645-baa2-fd3bf623baec.JPG)

when we use OVER() function with an agrigate function like max().
the sql does not take max() as an agrigate function but like a window function , and over() tell sql to create window for each row/record. <br/>
if I donnot put any thing in-between VIEW() then one window for each row.
and the result of that max() will be put in that window. <br/>
but if we put any thing in between VIEW( partition by dpt) then sql will group all the departments together and find max salary for each dpt, separatly.

![1](https://user-images.githubusercontent.com/33677647/204666268-c5087296-8a0b-410b-b589-f85acf5a15fd.JPG)
![2](https://user-images.githubusercontent.com/33677647/204666274-ae3819d0-b6c8-4b20-8e5c-237b56726a36.JPG)


## ROW_NUMBER 

asigns unique value to each record in a table

![4](https://user-images.githubusercontent.com/33677647/204671687-b57d2d6b-a142-49fe-a3a7-86409cd32ad3.JPG)
![5](https://user-images.githubusercontent.com/33677647/204671691-27732399-e855-41cb-bc07-c55710bb4970.JPG)
![6](https://user-images.githubusercontent.com/33677647/204671706-1604fb34-2195-4a43-b985-18fd1a2f0233.JPG)

but there is no proper order between the groups, as you see the empolyee with earlier id are put after employee with later id : 118, 116, 106, 104
- Now suppose we want to the the names of 2 senior most employees from each dpt, hence for that the id of all should have been arranged in asending order.

![1](https://user-images.githubusercontent.com/33677647/204672102-b59ad4a7-c605-46cd-acfb-7af0913182ad.JPG)

now data is sorted by employee id for each dpt.

- now to fetch only 2 senior most employye from each dpt :

![1](https://user-images.githubusercontent.com/33677647/204675609-369b3add-99d7-421b-9c3f-5a5d48d89704.JPG)

here x is an alias.

## RANK()

![11](https://user-images.githubusercontent.com/33677647/204677727-1ef3e60f-d3f5-478b-9759-6196dbbd7ed9.JPG)
![12](https://user-images.githubusercontent.com/33677647/204677733-cd6c10b3-ecbe-421f-97b8-891f4d0615c3.JPG)

## RANK() VS DENSE_RANK()

rank() will skip a rank value for duplicated values, whereas dense_rank() will not skip a rank value after duplicated rows.

![1](https://user-images.githubusercontent.com/33677647/204682206-557123f7-24cd-4239-b528-29d4d16f99fb.JPG)

here in rank() window the duplicated rows as they had same salary, both are given rank 2 but after that in next row rank() skips 3 and directly gives 4, but this is not tha case with dense rank.

## LEAD() vs LAG()

![1](https://user-images.githubusercontent.com/33677647/204777145-1c8aad75-ac0b-434c-bbaa-f1b4193a3ce4.JPG)
![2](https://user-images.githubusercontent.com/33677647/204777160-8ba5f6fe-1120-4e21-a28f-3c0c3c2ec9ac.JPG)
![3](https://user-images.githubusercontent.com/33677647/204777172-2090d87d-1ac8-45ab-8ba1-91ce6c02ae0e.JPG)
![4](https://user-images.githubusercontent.com/33677647/204777194-60789c45-e67b-4885-bda1-f3747ebabe90.JPG)

**LAG(any_columnName , 2, 0)** --> here 2 tell to return the value from previous of previous row, and 0 tell that when ever the return value is 'null' replace null with zero.

## first_value()

The FIRST_VALUE() is a window function that returns the first value in an ordered set of values.

![1](https://user-images.githubusercontent.com/33677647/204864019-0520b02f-e24e-4d22-9b32-33e23a58fb4e.JPG)

## last_view()

![2](https://user-images.githubusercontent.com/33677647/204864121-572cd1ef-892f-48c1-a7f9-d2004c413933.JPG)

as we see that the last values are not fetched correctly

- sql is not fetching last_row() properly due to by-default **Frame clause** used by sql.

![1](https://user-images.githubusercontent.com/33677647/204865468-c269b215-215d-4889-ab63-2c9c71d994f9.JPG)

the **Frame clause** is mentiones inside OVER() clause at the end, i.e after group by clause = over(partition by A order by B FrameClauseHere)
- ByDefault Frame clause : "range between unbounded preceding and current row"
![4](https://user-images.githubusercontent.com/33677647/204866950-6a5aa763-2f00-4c34-858b-363a9d9ecbcd.JPG)
- as the above frame clause is by default, so it is not necessary for us to mention it.

- UNBOUNDED PRECEDING indicates that the window starts at the first row of the partition;
- UNBOUNDED PRECEDING : The bound is the first partition row.
- UNBOUNDED FOLLOWING : The bound is the last partition row. 

![1](https://user-images.githubusercontent.com/33677647/204928871-098b1d5a-7a4c-464c-97c8-4b726df0aca8.jpeg)
![2](https://user-images.githubusercontent.com/33677647/204928656-302e13a9-5579-4eb0-9854-bf9ae77afff2.jpeg)
![3](https://user-images.githubusercontent.com/33677647/204928672-88931a0e-9671-4eb7-bdb9-d266492c487f.jpeg)
![4](https://user-images.githubusercontent.com/33677647/204928683-90942087-106e-42a5-a002-d99c91e7b2ea.jpeg)
![5](https://user-images.githubusercontent.com/33677647/204928714-b7e92edc-eea0-4895-bd9c-733cdfa29975.JPG)
![6](https://user-images.githubusercontent.com/33677647/204928748-8e63d916-2c9e-4e71-9a54-81488b88193d.JPG)
![7](https://user-images.githubusercontent.com/33677647/204928763-342b815a-b704-4c39-abac-16905c1f2198.jpeg)






