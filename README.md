# window_function_sql

![b](https://user-images.githubusercontent.com/33677647/205153034-0a1a2be7-8065-46a7-a88b-4f268f530c93.jpg)

What are window functions used for?<br/>
What are Window Functions? Window functions enable users to perform calculations against partitions (i.e. subgroups or sections) of a result set, typically a table or the results from another query.

![1](https://user-images.githubusercontent.com/33677647/204666035-adbfeb09-d328-4867-b921-b4be1dbacd69.JPG)
![2](https://user-images.githubusercontent.com/33677647/204666044-d6a835ce-a21d-422b-acc0-8e77fdd51542.JPG)
![3](https://user-images.githubusercontent.com/33677647/204666063-62806e54-2614-4645-baa2-fd3bf623baec.JPG)

when we use OVER() function with an agrigate function like max().
the sql does not take max() as an agrigate function but like a window function , and over() tell sql to create window for each row/record. <br/>
if I donnot put any thing in-between over() then one window for each row.
and the result of that max() will be put in that window. <br/>
but if we put any thing in between over( partition by dpt) then sql will group all the departments together and find max salary for each dpt, separatly.

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

![kk](https://user-images.githubusercontent.com/33677647/204942047-8817a4cc-515e-4f01-a98a-8cdbfe43af0b.png)

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

So,
- At first in each partitioned window, the Unbounded preceding and current row, both are on first row, so there is only 1 row (considers that there is only one row) at first in each partition, which is also last row because only one row.
- Then at 2nd time, unbounded-preceding stays at first row and current-row moves to next row, so there will be two rows now in each partition and the row at which current-row has moved is now last row.
- now in each window, current row moves to third row and unbounded-precedings remains at first row, so in each window, there are 3 rows now, and this new add row is now last row.
- goes on...


**BUT!!!!!**

this issue can be solved just by changing the "current row" to **unbounded following** 

![99](https://user-images.githubusercontent.com/33677647/204930722-ff97b479-1e25-47f3-9102-0745d280af1c.JPG)

### writing a window w function :

as most of the time the query inside over() is same, so intead of repeating that again and again and making the code look complex, we can store that query in a window function, make an alias "w", and use as many time as I want.

![1](https://user-images.githubusercontent.com/33677647/204934454-685b9f8b-a000-4684-a464-4df4ac2c2619.JPG)

## nth_value()

returns the nth row we ask for, here in this example, we put 2, because we want second most expensive product.

![2](https://user-images.githubusercontent.com/33677647/204935823-0cbcc6cc-850b-4426-9dc9-5baf028b6236.JPG)
![2](https://user-images.githubusercontent.com/33677647/204935957-d1c34f29-d755-4181-9522-bcd336feaac5.JPG)
 
```diff
- When ever we use last_value() or nth_value, we must specify the Frame clause in order to properly fetch the data
```

## NTILE()

when we want to group together a few records into some desired number of buckets.

![aa](https://user-images.githubusercontent.com/33677647/204943203-647786ed-6135-4815-a74d-4fd417d3febd.JPG)

we did not use partition here because we need only phone catagory.

![aa](https://user-images.githubusercontent.com/33677647/204943456-32a6666b-7321-4179-9ca8-eecdff9c91cb.JPG)

## cume_dist()

MySQL CUME_DIST() function to calculate cumulative distribution value.
Means it give each row a percentage-wise rank.
![aaa](https://user-images.githubusercontent.com/33677647/205168798-b42d5aff-0ef5-46d9-b9e0-bb95a0522ac9.JPG)


![99](https://user-images.githubusercontent.com/33677647/205147402-72030745-1753-455d-bde7-91265ff8c81f.JPG)

- The value of cume_dist() is always between 0 to 1.<br/>
- In dataset we give each row a row_nuber and then the cume_dist() value of each row will be like<br/>
- cume_dist value for 1st row = 1/ tota_number_of rows<br/>
- cume_dist value for 2nd row = 2/ tota_number_of rows<br/>
- cume_dist value for 3rd row = 3/ tota_number_of rows<br/>
.<br/>
.<br/>
.<br/>
- cume_dist value for nth row = n/ tota_number_of rows<br/>

```diff
- Alert!!!
- if two neighbouring rows (suppose 7th and 8t row ) contains same data with in them, then both rows will have the cume_dist() value :
- cume_dist value for both 7th & 8th rows = 8 / tota_number_of rows
```

![aa](https://user-images.githubusercontent.com/33677647/205152945-b1def205-cde1-4dbc-abde-6866532736f4.JPG)

**Do not pass any value inside cume_dist() window function.**

```diff
+ Now suppose I have a products company, I want to find that which 20% of products are having least sales out of all products.
```

For that I arrage the all products group by price desc, so that all the products are arranged in high to low sales order.
The we can use cume_dist() window function to fetch last 20% for row, as they all are least sale products.

SELECT *, <br/>
cume_dist() over (order by price desc) AS CumeDistValue<br/>
FROM products<br/>
WHERE CumeDistValue <= .2;<br/>

![99](https://user-images.githubusercontent.com/33677647/205152373-ee234e76-b5be-41b0-b3ff-efa84e86e78a.JPG)

Here "||" is used to concatination btw. the value and "%" sign

## percent_rank() --> percentage rank

 This function takes a column name as the argument and returns the number of rows with greater values than the sample value. <br/><br/>
 In other words, if you have a column with values 1, 2, 3, and 4, and your current row has a value of 3, the Percent_Rank() function would return 0.75, or 3/4.

```diff
@@ The first row in any set has a PERCENT_RANK of 0 @@
```

![aa](https://user-images.githubusercontent.com/33677647/205156474-e9d0fc44-7c23-4500-a8fe-2d7e8e189b3d.JPG)
![bb](https://user-images.githubusercontent.com/33677647/205171448-cb639c74-bb7f-480c-a7e6-d7b1bcb73d12.JPG)
![aaa](https://user-images.githubusercontent.com/33677647/205171467-e5af2a83-0a95-4487-8e8f-13bcb169f726.JPG)

## Rank() vs Cume_dist() vs Percent_rank()

These two functions are PERCENT_RANK and CUME_DIST.<br/>
They are similar to the RANK function but return a percent over the group instead of just a ranking number.

For a list of scores, PERCENT_RANK returns the percent of values less than the current score. CUME_DIST, which stands for cumulative distribution, returns the actual position of the score. <br/>
If there are 100 scores and the PERCENT_RANK is 90, that means that the score is 90% higher than other scores. If the CUME_DIST is 90, that means that the score is the 90th one in the list.

```diff
ALERT!!!<br/>
Two things to remember when using window functions:<br/>
1- you can't use group by in the same query with the window function.<br/>
2- You can't use the window function in the where clause to filter data.<br/>
```











