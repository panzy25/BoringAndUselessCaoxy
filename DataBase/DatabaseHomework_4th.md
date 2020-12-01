# 数据库第四次作业

<center>第二章课后练习</center>



> written by panzy25, 18372046
>
> on Typora
>
> Based on Markdown language 

[TOC]

## 1. Overview

Homework: 2.1(b); 2.2; 2.4; 2.5

## 2. T2.1(b)

![2020-12-01-16.08.54.png](http://panzy25.ticp.io:4000/images/2020/12/01/2020-12-01-16.08.54.png)

**Q**: Find the two candidate keys for this table.

**A**: Key1: A; Key2: (B,C,E)

## 3. T2.2

Consider a database for the telephone company that contains a table SUBSCRIBE-ERS, whose heading is

```sql
name ssn address city zip information-no
```

Assume that "information-no" is the unique 10-digit telephone number, including area code, provided for subscribers. Although one subscriber may have multiple phone numbers, such alternate numbers are carried in a separate table; the current table has a row for each distinct subscriber (but note that husband and wife, subscribing together, can occupy two rows and share an information number).The DBA has set up the following rules about the table, reflecting design  intensions for the data:

- No two subscribers (on separate rows) hava the same Social Security number.
- Two different subscribers can share the same infomation number (for example, husband and wife). They are listed separately in the SUBSCRIBERS table. However, two different subscribers with the *same name* cannot share the same address, city, *and* zip code and also the same information number. For example,  if Diane and David Issacs who live together and share the same information number wish to both be listed as D. Issacs, they will be asked to differentiate their two names, say, by spelling out at least one of them.

**Q.(a)** Identify all candidate keys for the SUBSCRIBERS table, based on the assumptions given above. Note that there are three such keys; one of them contains the infomation-no attribute and a different one contains the zip attribute.

**A.(a)** There are three candidate keys:

Key1: (SSN); Key2: (name, information-no); Key3: (name, address, city, zip)

**Q.(b)** Which of these candidate keys would you choose for a primary key? Explain why.

**A.(b)** Primary key requires that the meaning is concise and clear on the basis of not repeating and uniquely identifying tuples. Obviously, SSN is the best choice.

## 4. T2.4

Solve in relational algebra the following queries involving the CAP database. These problems are basic and meant as a warm-up for the following exercise.

**Q.(a)** Find all (ordno, pid) pairs for orders of quantity equal to 1000 or more.

**A.(a)** (ORDERS where qty $\ge$ 1000)[ordno, pid]

**Q.(b)** Find all product names of products priced between \$0.50 and \$1.00, inclusive.

**A.(b)** (PRODUCTS where (price $\ge$ 0.50 and price $\le$ 1.00))[pname]

**Q.(c)** Find all (ordno, cname) pairs for orders of dollar value less than \$500. Use one join here.

**A.(c)** (CUSTOMERS JOIN ORDERS where OREDERS.dollars $<$ 500)[ordno, cname]

**Q.(d)** Find all (ordno, aname) pairs for orders in March. Use one join here.

**A.(d)** (AGENTS JOIN ORDERS where ORDERS.month = 'mar')[ordno, aname]

**Q.(e)** Find all (ordno, cname, aname) triples for orders in March. Use two joins here.

**A.(e)** ((ORDERS where month = 'mar' JOIN OREDERS)[ordno, cname, aid] JOIN AGENTS)[ordno, cname, aname]

**Q.(f)** Find all the names of agents in New York who placed orders of individual dollar value less than \$500.

**A.(f)** ((AGENTS where city ='New York') JOIN (OREDERS where dollars $<$ 500))[aname]

**Q.(g)** Find all product names of products in Duluth ordered in March.

**A.(g)** ((PRODUCTS where city = 'Duluth') JOIN (OREDERS where month ='mar'))[pname]

## 5. T2.5

Solve in relational algebra the following queries involving the CAP database. (These requests will be used again in the next chapter to demonstrate capabilities of the computer-based query language SQL.) **NOTE**: In all requests that follow, you should pose the query as a single, self-cintained relational algebra expression that does not depend on any intermodiate results created by means of alias, except where absolutely necessary.

**Q.(a)** Find all (cid, adi, pid) triples for customer,agent,product combinations that are all in the same city. Nothing about orders is involved in this selection.

**A.(a)** ((CUSTOMERS Times AGENTS Times PRODUCTS) where CUSTOMERS.city = AGENTS.city and AGENTS.city = PRODUCTS.city)[cid, aid, pid]

**Q.(b)** Find all (cid,adi,pid) triples for customer,agent,product combinations that are not all in the same city(any two may be).

**A.(b)** Two possible expressions:

- ((CUSTOMERS Times AGENTS Times PRODUCTS) where NOT(CUSTOMERS.city = AGENTS.city and AGENTS.city = PRODUCTS.city))[cid, aid, pid]
- ((CUSTOMERS Times AGENTS Times PRODUCTS) where CUSTOMERS.city <> AGENTS.city or AGENTS.city <> PRODUCTS.city or CUSTOMERS.city <> PRODUCTS.city)[cid,aid,pid]

**Q.(c)** Find all (cid,adi,pid) triples for customer,agent,product combinations, no two of which are in the same city.

**A.(c)** ((CUSTOMERS Times AGENTS Times PRODUCTS) where CUSTOMERS.city <> AGENTS.city and AGENTS.city <> PRODUCTS.city and CUSTOMERS.city <> PRODUCTS.city)[cid,aid,pid]

**Q.(d)** Get cities of agents booking an order from customer c002.

**A.(d)** (OREDERS where cid = 'c002' JOIN AGENTS)[city]

**Q.(e)** Get product names ordered by at least one customer based in Dallas through an agent based in Tokyo.

**A.(e)** (OREDERS JOIN (CUSTOMER where city = 'Dallas')[cid] JOIN (AGENTS where city = 'Tokyo')[aid] JOIN PRODUCTS)[pname]

**Q.(f)** Get pid of products ordered through any agent who makes at least one order for a customer in Kyoto. NOTE: The request posed here is not the same as asking for pids of products ordered by a customer in Kyoto.

**A.(f)** (ORDERS JOIN ((ORDERS JOIN (CUSTOMERS where city = ’Kyoto’)[cid]) [aid]))[pid]

**Q.(g)** Display all pairs of aids for agents who live in the same city. A:=AGENTS. B:=AGENTS.

**A.(g)** ((A $\times$ B) where A.city = B.city and A.aid $<$ B.aid)[cid]

**Q.(h)** Find cids of customers who did not place an order through agent a03.

**A.(h)** CUSTOMERS[cid] - (OREDERS where aid = 'a03')[cid]

**Q.(i)** Find cids of customers who have the largests discount; separately, find those who have the smallest discount. NOTE: This is quite hard with the operations provided in relational algebra.

**A.(i)** 

C:=CUSTOMERS. D:=CUSTOMERS.
Largest:((C × D) where C.discnt $\ge$ D.discnt)[C.cid, D.cid] ÷ C[cid]                        Smallest:((C × D) where C.discnt $\le$ D.discnt)[C.cid, D.cid] ÷ C[cid]

**Q.(j)** Find cids of customers who order all products.

**A.(j)** ORDERS[cid, pid] ÷ PRODUCTS[pid]

**Q.(k)** Find pids of products ordered through agent a03 but not through agent a06.

**A.(k)** (ORDERS where aid = 'a03')[pid] - (ORDERS where aid = 'a06')[pid]

**Q.(l)** Get pnames and pids of products that are stored in the same city as one of the agents who sold these products.

**A.(l)** (((OREDERS[pid, aid] JOIN AGENTS) $\times$ PRODUCTS) where ORDERS.pid = PRODUCTS.pid and AGENTS.city = PRODUCTS.city)[pname, pid]

**Q.(m)** Get aids and anames of agents with aname beginning with the
letter “N” who do not place orders for any product in Newark.

**A.(m)** (AGENTS[aid] - (OREDERS JOIN PRODUCTS where city = 'Newark')[aid]) JOIN AGENTS)[aid, aname] where aname $\ge$ 'N'

**Q.(n)** Get cids of customers who order both product p01 and product p07.

**A.(n)** (ORDERS where pid = 'p01' and pid = 'p07')[cid]

**Q.(o)** Get names of agents who place orders for all products ordered by
customer c002.

**A.(o)** ((ORDERS[aid, pid] $÷$ (ORDERS where cid = 'c002')[pid]) JOIN AGENTS)[aname]

**Q.(p)** Get names of agents who place orders for all products that are
ordered by any customers at all.(Hint: The phrase “any customers at
all means the same as “some customer.”

**A.(p)** ((ORDERS[aid, pid] $÷$ ORDERS[pid]) JOIN AGENTS)[aname]

**Q.(q)** Get(cid, aid, pid) triples for customer, agent, product combinations
so that at most two of them are in the same city.(Is this equivalent
to any of the first three queries of this exercise,(a),(b),or(c)?)

**A.(q)** This is equivalent to (b):
((CUSTOMERS Times AGENTS Times PRODUCTS) where CUSTOMERS.city
<> AGENTS.city or AGENTS.city <> PRODUCTS.city or CUSTOMERS.city <>
PRODUCTS.city )[cid, aid, pid]

**Q.(r)** Get pids of products ordered by all customers who place any order through agent a03.

**A.(r)** OREDERS[cid, pid] $÷$ (ORDERS where aid = 'a03')[cid]

**Q.(s)** Get aids of agents who place individual orders in dollar value greater than $500 for customers living in Kyoto.

**A.(s)** ((ORDERS where dollar $>$ 500)[aid, cid] JOIN CUSTOMERS where city = 'Kyoto')[aid]

**Q.(t)** Give all (cname, aname) pairs where the customers places an order
through the agent.

**A.(t)** ((ORDERS $\times$ CUSTOMERS $\times$ AGENTS) where ORDERS.aid = AGENTS.aid and ORDERS.cid = CUSTOMERS.cid)[cname, aname]

**Q.(u)** Get cids of customers who order all their products through only
one agent.

**A.(u)** O1 := OREDERS; O2 := OREDERS

O1[cid] $-$ ((O1 $\times$ O2) where O1.cid = O2.cid and O1.aid <> O2.aid)[O1.cid]









