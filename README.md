# Field-Aliases-Calculated-Fields

### Field-Aliases
A field alias is an alternate name that can be assigned to a field. Field aliases can be used to normalize data from multiple sources, and to assign different extracted field names to a single field name.

Example see the below data, which is having the common field 

![raw_data](https://github.com/Tejaswini-Meka/Field-Aliases-Calculated-Fields-/blob/main/Raw%20data.png)

### Calculated-Fields

![data1](https://github.com/user-attachments/assets/b8dcdba8-7ae9-46fe-a05a-cb44d4c46a46)

The above query is having the calculated fields.
Same results i want it in each and every results without writing the qurey everytime.
In this scenario, calculated fields comes to the picture.

In above query calculated fields are</br>
```
| eval discount_in_number = MRP - 'Selling Price'
| eval discount_in_perc = round((discount_in_number/MRP)*100)
```
If you see the above query, field **discount_in_perc** rely on **discount_in_number**
it can give the results in search time but same cannot be applicable in props.conf - calculated field cannot reliably depend on another is due to Splunk’s independent and non-sequential calculation of fields in props.conf. Each calculated field should rely on raw data, not on the results of other calculated fields

Now we have to mentioned them in **props.conf** file of the respective application and sourcetype.
Below is the configuration we have to do it in props.conf
```
EVAL-discount_in_number = MRP - 'Selling Price'
EVAL-discount_in_perc = round((MRP - 'Selling Price')*100)
```
![Data2](https://github.com/user-attachments/assets/b612c520-0d0f-4202-8421-b6a7f744dd3e)

Now without mentioning the *eval* command in the query directly we can get the results of our calculated fields **"discount_in_number"** & **"discount_in_perc"**

![data3](https://github.com/user-attachments/assets/8cc40498-dd74-462f-9912-b9f73ebaee82)






