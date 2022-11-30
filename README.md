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



