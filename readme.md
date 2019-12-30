# Online Quiz


https://Quiz.in


## Features


User can see the sample question.


### Feature 1: Sample question.

```sql

create table Sample_Qus(Qus_id number ,Question varchar2(100) not null,
Choice_1 varchar2(100) unique not null, Choice_2 varchar2(100) unique not null
,constraint qes_id_pk primary key (Qes_id)
);

```

```sql
 insert into Sample_Qus(101,'How many years are there in a decade?','10','15')

select * from Sample_Qus;
```
