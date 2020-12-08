# 数据库第五次作业

<center>第三章课后练习</center>



> written by panzy25, 18372046
>
> Typora used
>
> Based on Markdown

[TOC]

## 1. Overview

Create queries in SQL to answer the requests in Exercise 2.5 (a) through (u), at the end of Chapter 2.

Firstly, we import the SQL Script `use dataBase` to use the database in SQL Sever.

## 2. Details

**Q.(a)** Find all (cid, adi, pid) triples for customer,agent,product combinations that are all in the same city. Nothing about orders is involved in this selection.

**A.(a)** 

```sql
select distinct customers.cid, agents.aid, products.pid
from customers, agents, products
where customers.city = agents.city and agents.city = products.city
order by 1, 2, 3
```

Result:

![2020-12-06-21.44.59.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-06-21.44.59.png)

**Q.(b)** Find all (cid,adi,pid) triples for customer,agent,product combinations that are not all in the same city(any two may be).

**A.(b)** 

```sql
select distinct customers.cid, agents.aid, products.pid
from customers, agents, products
where NOT (customers.city = agents.city and agents.city = products.city)
order by 1, 2, 3
```

Or we can use the other expression:

```sql
select distinct customers.cid, agents.aid, products.pid
from customers, agents, products
where customers.city <> agents.city or agents.city <> products.city or customers.city <> products.city
order by 1, 2, 3
```

Result:

![2020-12-07-13.04.43.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-13.04.43.png)

There are 200 rows matching to the SQL query.

**Q.(c)** Find all (cid,adi,pid) triples for customer,agent,product combinations, no two of which are in the same city.

**A.(c)** 

```sql
select distinct customers.cid, agents.aid, products.pid
from customers, agents, products
where customers.city <> agents.city and agents.city <> products.city and products.city <> customers.city
order by 1, 2, 3
```

Result:

![2020-12-07-13.08.21.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-13.08.21.png)

There are 107 rows matching to the SQL query.

**Q.(d)** Get cities of agents booking an order from customer c002.

**A.(d)** 

```sql
select distinct agents.city
from agents 
where aid in (select aid from orders where cid = 'c002')
```

Result:

![2020-12-07-14.34.07.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.34.07.png)

**Q.(e)** Get product names ordered by at least one customer based in Dallas through an agent based in Tokyo.

**A.(e)** 

```sql
select distinct pname
from products, customers, agents, orders
where customers.cid = orders.cid and agents.aid = orders.aid and products.pid = orders.pid and customers.city = 'Dallas' and agents.city = 'Tokyo'
```

Result:

![2020-12-07-14.36.08.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.36.08.png)

**Q.(f)** Get pid of products ordered through any agent who makes at least one order for a customer in Kyoto. NOTE: The request posed here is not the same as asking for pids of products ordered by a customer in Kyoto.

**A.(f)** 

```sql
select distinct pid from orders
where aid in 
	(select aid from orders where cid in 
		(select cid from customers where customers.city = 'Kyoto'))
```

Result:

![2020-12-07-14.36.58.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.36.58.png)

**Q.(g)** Display all pairs of aids for agents who live in the same city. A:=AGENTS. B:=AGENTS.

**A.(g)** 

```sql
select a1.aid, a2.aid
from agents a1, agents a2
where a1.city = a2.city and a1.aid < a2.aid
```

Result:

![2020-12-07-14.40.08.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.40.08.png)

**Q.(h)** Find cids of customers who did not place an order through agent a03.

**A.(h)** 

```sql
select cid from customers
where cid not in 
	(select cid from orders where aid = 'a03')
```

Result:

![2020-12-07-14.47.52.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.47.52.png)

**Q.(i)** Find cids of customers who have the largests discount; separately, find those who have the smallest discount. NOTE: This is quite hard with the operations provided in relational algebra.

**A.(i)** 

```sql
-- MAX
select distinct cid from customers
where discnt = (select MAX(discnt) from customers)
-- MIN
select distinct cid from customers
where discnt = (select MIN(discnt) from customers)
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.48.40.png" alt="2020-12-07-14.48.40.png" style="zoom:110%;" />

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.49.18.png" alt="2020-12-07-14.49.18.png" style="zoom:130%;" />

**Q.(j)** Find cids of customers who order all products.

**A.(j)** 

```sql
select c.cid from customers c where not exists
(
  select p.pid from products p where not exists
(select * from orders o where c.cid = o.cid and o.pid = p.pid)
)
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.50.46.png" alt="2020-12-07-14.50.46.png" style="zoom:150%;" />

**Q.(k)** Find pids of products ordered through agent a03 but not through agent a06.

**A.(k)** 

```sql
select distinct pid from orders
where aid = 'a03' and pid not in
(select distinct pid from orders where aid = 'a06')
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.51.58.png" alt="2020-12-07-14.51.58.png" style="zoom:130%;" />

**Q.(l)** Get pnames and pids of products that are stored in the same city as one of the agents who sold these products.

**A.(l)** 

```sql
select distinct products.pname, products.pid from orders, agents, products
where products.pid = orders.pid and agents.aid = orders.aid and products.city = agents.city
```

Result:

![2020-12-07-14.52.45.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.52.45.png)

**Q.(m)** Get aids and anames of agents with aname beginning with the
letter “N” who do not place orders for any product in Newark.

**A.(m)** 

```sql
select aid, aname from agents
where aname like 'N%' and aid not in
(select aid from orders where pid not in
(select pid from products where city  = 'Newark')
)
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.53.19.png" alt="2020-12-07-14.53.19.png" style="zoom:150%;" />

**Q.(n)** Get cids of customers who order both product p01 and product p07.

**A.(n)** 

```sql
select distinct cid from orders
where pid = 'p01' and cid in
(select cid from orders where pid = 'p07')
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.54.12.png" alt="2020-12-07-14.54.12.png" style="zoom:150%;" />

**Q.(o)** Get names of agents who place orders for all products ordered by
customer c002.

**A.(o)** 

```sql
select aname from agents
where aid in
(select distinct aid from agents where not exists
(select pid from orders o1 where cid = 'c002' and not exists
(select * from orders o2 where agents.aid = o2.aid and o1.pid = o2.pid)))
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.55.59.png" alt="2020-12-07-14.55.59.png" style="zoom:150%;" />

**Q.(p)** Get names of agents who place orders for all products that are
ordered by any customers at all.(Hint: The phrase “any customers at
all means the same as “some customer.”

**A.(p)** 

```sql
select distinct aname from agents
where aid in
(select aid from agents where not exists
(select pid from orders o1 where not exists
(select * from orders o2 where agents.aid = o2.aid and o1.pid = o2.pid)))
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.56.38.png" alt="2020-12-07-14.56.38.png" style="zoom:150%;" />

**Q.(q)** Get(cid, aid, pid) triples for customer, agent, product combinations
so that at most two of them are in the same city.(Is this equivalent
to any of the first three queries of this exercise,(a),(b),or(c)?)

**A.(q)** 

```sql
select distinct cid, aid, pid from customers, agents, products
where 
(customers.cid = products.city) or (customers.city = agents.city) or (agents.city = products.city)
```

Result:

![2020-12-07-14.57.35.png](http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.57.35.png)

**Q.(r)** Get pids of products ordered by all customers who place any order through agent a03.

**A.(r)** 

```sql
select pid from products
where not exists
(select cid from orders o1 where aid = 'a03' and not exists
(select * from orders o2 where o1.cid = o2.cid and products.pid = o2.pid))
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.58.17.png" alt="2020-12-07-14.58.17.png" style="zoom:150%;" />

**Q.(s)** Get aids of agents who place individual orders in dollar value greater than $500 for customers living in Kyoto.

**A.(s)** 

```sql
select distinct aid from orders
where dollars > 500.00 and cid in
(select cid from customers where city = 'Kyoto')
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.58.50.png" alt="2020-12-07-14.58.50.png" style="zoom:150%;" />

**Q.(t)** Give all (cname, aname) pairs where the customers places an order
through the agent.

**A.(t)** 

```sql
select distinct cname, aname from customers, agents, orders
where customers.cid = orders.cid and agents.aid = orders.aid
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-14.59.26.png" alt="2020-12-07-14.59.26.png" style="zoom:150%;" />

**Q.(u)** Get cids of customers who order all their products through only
one agent.

**A.(u)** 

```sql
select distinct cid from orders
where cid not in
(select distinct o1.cid from orders o1, orders o2 where o1.cid = o2.cid and o1.aid <> o2.aid)
```

Result:

<img src="http://panzy25.ticp.io:4000/images/2020/12/07/2020-12-07-15.00.17.png" alt="2020-12-07-15.00.17.png" style="zoom:150%;" />