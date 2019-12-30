# Online Quiz


https://Quiz.in


## Features


User can see the sample question.


### Feature 1: Sample question.

```sql

create table Sample_Qus(Qus_id number ,Question varchar2(100) unique not null,
Choice_1 varchar2(100) unique not null, Choice_2 varchar2(100)  unique not null,
constraint Qus_id_pk primary key (Qus_id));
create sequence seq1 start with 101 increment by 1
```

```sql
 insert into Sample_Qus(seq1.nextval,'How many years are there in a decade?','10','15')
 insert into Sample_Qus(seq1.nextval,'The highest mountain on earth is?','Everest','Fuji')

select * from Sample_Qus;
```
