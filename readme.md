# Online Quiz


https://Quiz.in


## Features


User can see the sample question.


### Feature 1: Sample question.

```sql

create table Sample_Qus(Qus_id number ,Question varchar2(100) not null,
Choice_1 varchar2(100)  not null, Choice_2 varchar2(100) unique not null,
constraint Qus_id_pk primary key (Qus_id),constraint Che_1 unique(Choice_1),
constraint Che_2 unique(Choice_2));
create sequence seq1 start with 101 increment by 1
```

```sql
 insert into Sample_Qus(seq1.nextval,'How many years are there in a decade?','10','15')

select * from Sample_Qus;
```
