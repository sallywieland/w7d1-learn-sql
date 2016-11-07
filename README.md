## Questions: Explorer Mode

### How many users are there? 
Answer: 50
* select count(*) from users;

### What are the 5 most expensive items?
Answer: 
* 9984|Small Cotton Gloves
* 9859|Small Wooden Computer
* 9790|Awesome Granite Pants
* 9390|Sleek Wooden Hat
* 9341|Ergonomic Steel Car 
* select price, title from items order by price desc;

### What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
Answer: 1496|Ergonomic Granite Chair|Books
* select price, title, category  from items where category like '%book%' order by price;
* select price, title, category  from items where category like 'book' order by price; --> no matches.


### Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
Answer: 40|Corrine|Little / Yes
* select addresses.user_id, users.first_name, users.last_name from addresses inner join users on addresses.user_id=users.id where street like '%6439%';
* select * from addresses where user_id like '40'

### Correct Virginie Mitchell's address to "New York, NY, 10108".
Answer: 
* select addresses.id, addresses.city, addresses.state, users.first_name, users.last_name from addresses inner join users on addresses.user_id=users.id where first_name like '%Virginie%';
* select * from addresses where user_id like '39';
* update addresses set city='New York', state='NY', zip='10108' where id=41;

### How much would it cost to buy one of each tool?
Answer: 46477 / 7383
* select sum(price) from items where category like '%tools%' order by price;
* select sum(price) from items where category like 'tools' order by price;

### How many total items did we sell?
Answer: 2125
* select sum(quantity) from orders;

### How much was spent on books?
Answer: 420566
* select items.category, sum(orders.quantity*items.price) from orders inner join items on orders.item_id=items.id where items.category like '%books%'; 

### Simulate buying an item by inserting a User for yourself and an Order for that User.
Answer:
* insert into users (id, first_name, last_name, email) values (51, 'Sally', 'Wieland', 'sallybwieland@gmail.com');
* insert into orders (id, user_id, item_id, quantity, created_at) values (378, 51, 66, 2, datetime());

