![Working-with-Realtional-Data](https://www.yiiframework.com/doc/guide/2.0/en/db-active-record#declaring-relations)

### Working with Relational Data


Besides working with individual database tables, Active Record is also capable of bringing together related data, making them readily accessible through the primary data.

For example, the customer data is related with the order data because one customer may have placed one or multiple orders.


With appropriate declaration of this relation, you'll be able to access a customer's order information using the expression **$customer->orders** which gives back the customer's order information in terms of an array of ***Order* Active Record instance.


