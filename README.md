# One To One

<!-- -->
>     CREATE TABLE accounts (
>         id SERIAL PRIMARY KEY,
>         username VARCHAR(32) UNIQUE NOT NULL,
>         full_name VARCHAR(32) NOT NULL
>     );
> 


<!-- -->
>     CREATE TABLE profiles(
>         id SERIAL PRIMARY KEY,
>         account_id INT UNIQUE NOT NULL,
>         bio TEXT,
>         age INT,
>         CONSTRAINT fk_account FOREIGN KEY(account_id) REFERENCES accounts(id) ON DELETE CASCADE
>     );
> 


<!-- -->
>     INSERT INTO accounts(username,full_name)
>     VALUES
>         ('younes','younes mirmohammdi'),
>         ('amin','amin valipour');
> 


<!-- -->
>     INSERT INTO profiles(account_id,bio,age)
>     VALUES 
>         (1,'I am Computer enginner',20),
>         (2,'I am electrical engineer',20);
> 


<!-- -->
>     SELECT username,full_name,bio,age
>     FROM accounts 
>     INNER JOIN profiles
>     ON profiles.account_id = accounts.id;
> 
> <pre>
> username | full_name          | bio                      | age
> :------- | :----------------- | :----------------------- | --:
> younes   | younes mirmohammdi | I am Computer enginner   |  20
> amin     | amin valipour      | I am electrical engineer |  20
> </pre>


# One To Many

<!-- -->
>     CREATE TABLE accounts (
>         id SERIAL PRIMARY KEY,
>         username VARCHAR(32) UNIQUE NOT NULL,
>         full_name VARCHAR(32) NOT NULL
>     );
> 


<!-- -->
>     CREATE TABLE posts(
>         id SERIAL PRIMARY KEY,
>         account_id INT NOT NULL,
>         body TEXT,
>         CONSTRAINT fk_account FOREIGN KEY(account_id) REFERENCES accounts(id) ON DELETE CASCADE
>     );
> 


<!-- -->
>     INSERT INTO accounts(username,full_name)
>     VALUES
>         ('younes','younes mirmohammdi'),
>         ('amin','amin valipour');
> 


<!-- -->
>     INSERT INTO posts(account_id,body)
>     VALUES 
>         (1,'today is great day'),
>         (2,'hello'),
>         (2,'im very busy today');
> 


<!-- -->
>     SELECT username,full_name,body
>     FROM accounts 
>     INNER JOIN posts
>     ON posts.account_id = accounts.id;
> 
> <pre>
> username | full_name          | body              
> :------- | :----------------- | :-----------------
> younes   | younes mirmohammdi | today is great day
> amin     | amin valipour      | hello             
> amin     | amin valipour      | im very busy today
> </pre>


# Many To Many


<!-- -->
>     CREATE TABLE products (
>         id SERIAL PRIMARY KEY,
>         title VARCHAR(32) NOT NULL,
>         price INT NOT NULL
>     );
> 

<!-- -->
>     CREATE TABLE colors(
>         id SERIAL PRIMARY KEY,
>         name VARCHAR(32) UNIQUE NOT NULL
>     );
> 


<!-- -->
>     CREATE TABLE product_color(
>         id SERIAL PRIMARY KEY,
>         product_id INT,
>         color_id INT,
>         CONSTRAINT fk_product FOREIGN KEY(product_id) REFERENCES products(id),
>         CONSTRAINT fk_color FOREIGN KEY(color_id) REFERENCES colors(id)
>     )
> 


<!-- -->
>     INSERT INTO products(title,price)
>     VALUES
>         ('iphone 13',800),
>         ('mi 11 ultra',500);
> 

<!-- -->
>     INSERT INTO colors(name)
>     VALUES 
>         ('red'),
>         ('black'),
>         ('blue');
> 


<!-- -->
>     INSERT INTO product_color(product_id,color_id)
>     VALUES
>         (1,1),
>         (1,3),
>         (2,1),
>         (2,3)
> 


<!-- -->
>     SELECT title,price,name
>     FROM products
>     INNER JOIN product_color ON product_color.product_id = products.id
>     INNER JOIN colors ON product_color.color_id = colors.id;
> 
> <pre>
> title       | price | name
> :---------- | ----: | :---
> iphone 13   |   800 | red 
> iphone 13   |   800 | blue
> mi 11 ultra |   500 | red 
> mi 11 ultra |   500 | blue
> </pre>
