# window_function_sql

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



