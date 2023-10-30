***** MONGODB QUERIES *****

1. Find all the information about each products
```
      db.products.find()
```
![All Products part-1](<day-3/Q01/1-5.PNG>)
![All Products part-2](day-3/Q01/6-10.PNG)
![All Products part-3](day-3/Q01/11-15.PNG)
![All Products part-4](day-3/Q01/16-20.PNG)
![All Products part-5](day-3/Q01/21-25.PNG)

2. Find the product price which are between 400 to 800

         db.products.find({product_price:{$gte:400,$lte:800}})

![Between 400to800](<day-3/Q02/btw_400-800.PNG>)       



3. Find the product price which are not between 400 to 600

         db.products.find({product_price:{$not:{$gte:400,$lte:600}}})

![Not Between 400to600 part-1](<day-3/Q03/till_id_8.PNG>)
![Not Between 400to600 part-2](day-3/Q03/till_id_13.PNG)
![Not Between 400to600 part-3](day-3/Q03/till_id_18.PNG)
![Not Between 400to600 part-4](day-3/Q03/till_id_23.PNG)
![Not Between 400to600 part-5](day-3/Q03/24-25.PNG)





4. List the four product which are grater than 500 in price

         db.products.find({product_price:{$gt:500}}).limit(4)

![Greater than 500 and limit 4](<day-3/Q04/gt500_Limit(4).PNG>)



5. Find the product name and product material of each products

         db.products.find().projection({product_name:1,product_material:1,_id:0})

![product name and material part-1](<day-3/Q05/part-1.PNG>)
![product name and material part-2](day-3/Q05/part-2.PNG)


6. Find the product with a row id of 10

         db.products.find({id:"10"})

![product detais of id=10](<day-3/Q06/part-1.PNG>)



7. Find only the product name and product material

         db.products.find().projection({product_name:1,product_material:1,_id:0})

![product name and material part-1](<day-3/Q05/part-1.PNG>)
![product name and material part-2](day-3/Q05/part-2.PNG)




8. Find all products which contain the value of soft in product material 

          db.products.find({product_material:'Soft'})

![Soft material](<day-3/Q08/part-1.PNG>)



9. Find products which contain product color indigo  and product price 492.00

         db.products.find({$or:[{product_color:'indigo'},{product_price:492}]})

![indigo or 492](<day-3/Q09/or.PNG>)

  ```
    db.products.find({$and:[{product_color:'indigo'},{product_price:492}]})
  ```

 **NO-OUTPUT** SInce there is no object that has both color and price as mentioned


10. Delete the products which product price value are same

         db.products.aggregate([
           { $group: { _id: "$product_price", count: { $sum: 1 } } },
           { $match: { count: { $gt: 1 } } },
        ])
        .forEach((doc) => {
           db.products.deleteMany({ product_price: doc._id });
        });

![products remaining after delete part-1](<day-3/Q10/part-1.PNG>)
![products remaining after delete part-2](day-3/Q10/part-2.PNG)
![products remaining after delete part-3](day-3/Q10/part-3.PNG)
![products remaining after delete part-4](day-3/Q10/part-4.PNG)
![products remaining after delete part-5](day-3/Q10/part-5.PNG)