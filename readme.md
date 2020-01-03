# Online Quiz


https://Quiz.in


## Features


User can see the sample question.


### Feature 1: Sample question.


 ```sql
create table Sample_Qus(Qus_id number,Question varchar2(100) unique not null,constraint Sam_Qus_id_fk Foreign Key (Qus_id) References Question(Qus_id));
create table Choice(Choice_id number,Choice varchar2(100) not null,Qus_id number,Answer number not null,constraint Qus_id_fk Foreign Key (Qus_id) References question(Qus_id),constraint Che unique (Choice));
create table Catogary(Cat_id number,Catogary_name varchar2(25), constraint cat_pk primary key(Cat_id));
create table Question (Qus_id number,Question varchar2(100) unique not null,Cat_id number,Diff_id number,constraint Cat_id_fk Foreign Key (Cat_id) References catogary(Cat_id),constraint Qus_id_pk primary key (Qus_id),constraint Diff_id_fk Foreign Key (Diff_id) References Diff(Diff_id));
create table User_login (User_id number,User_name varchar2(20),constraint user_id_pk primary key (User_id));
create table Diff(Diff_id number,Diff_level varchar2(10),constraint Diff_id_pk primary key (Diff_id));
create table Ranks(Rank_id number,Rank_level varchar2(20),constraint Rank_id_pk primary key (Rank_id));
Create table Results(user_id number, Ranks number,Mark_Scored number);
create table Test_Attempt (Qus_id number,CHOICE_ID NUMBER,Answer_status varchar2(10) not null,Test_id number,user_id number,constraint qus_tst_id foreign key (qus_id) references Question(qus_id),constraint che_tst_id foreign key (CHOICE_ID) references CHOICE(CHOICE_ID),constraint tezst primary key (test_id),constraint usezr  foreign key (user_id) references user_login(user_id) );

create sequence seq5 start with 1 increment by 1;

 
create sequence seq1 start with 101 increment by 1;
create sequence seq2 start with 301 increment by 1;
create sequence seq3 start with 501 increment by 1;
create sequence seq4 start with 701 increment by 1;

```

```sql
 

select * from Sample_Qus;

select * from User_login;
select * from Diff;

insert into User_login values (seq5.nextval,'Bob');
insert into User_login values (seq5.nextval,'Max');
insert into User_login values (seq5.nextval,'Joy');


insert into Catogary  values (seq1.nextval,'Maths');
insert into Catogary  values (seq1.nextval,'English');
insert into Catogary  values (seq1.nextval,'Science');
select * from Catogary;

insert into Diff values (seq2.nextval,'Easy');
insert into Diff values (seq2.nextval,'Medium');
insert into Diff values (seq2.nextval,'Hard');
 select * from Question;
insert into Question values (SEQ3.nextval,'How many years are there in a decade?','101','301');
insert into Question values (SEQ3.nextval,'The highest mountain on earth is?','101','301');
insert into Question values (SEQ3.nextval,'What is the biggest planet in our solar system?','101','301');

--update Question set cat_id='103' where cat_id='102'

insert into Question values (SEQ3.nextval,'Jack ___________ English, Spanish and a bit of French.?','102','302');
insert into Question values (SEQ3.nextval,' ___________ to London on the train yesterday?','102','302');

insert into Question values (SEQ3.nextval,'Express the ten thousandths place in 1.7389','101','303');

```
```sql
insert into Sample_Qus values ('501',(select Question from Question where qus_id='501'));
insert into Sample_Qus values ('502',(select Question from Question where qus_id='502'));
insert into Sample_Qus values ('505',(select Question from Question where qus_id='505'));
insert into Sample_Qus values ('506',(select Question from Question where qus_id='506'));
select * from Sample_Qus;

select * from Question;
insert into Choice values (SEQ4.nextval,'10','501','1');
insert into Choice values (SEQ4.nextval,'15','501','0');
insert into Choice values (SEQ4.nextval,'Fuji','502','0');
insert into Choice values (SEQ4.nextval,'Everest','502','1');

insert into Test_Attempt values (502,703,0,1,1) ; 
insert into Test_Attempt values (501,701,1,1,1) ;
insert into Test_Attempt values (501,701,1,1,1) ;

select * from Choice

```
| User_id | User_name | 
|---------|-----------|
| 1       | bob       |
| 2       | max       |
| 3       | joy       |


| Cat_id | Catogary_name |   
|--------|---------------|
| 301    | Science       |
| 401    | Maths         |
|        |               |

   
| Diff_id | Diff_level |
|---------|------------|
| 501     | Easy       |
| 601     | Medium     |
|         |            |



| Qus_id | Question                              | Cat_id | Diff_id |
|--------|---------------------------------------|--------|---------|
| 101    | How many years are there in a decade? | 301    | 501     |
| 201    | The highest mountain on earth is?     | 301    | 501     |
|        |                                       |        |         |        


| Qus_id | Question                              |
|--------|---------------------------------------|
| 101    | How many years are there in a decade? |
| 201    | The highest mountain on earth is?     |
|        |                                       |


| Choice_id | Choice | Qus_id | Answer |
|-----------|--------|--------|--------|
|    101    |   10   |   101  |    1   |
|    101    |   15   |   101  |    0   |


| user_id | Marks_Scored | Ranks |
|---------|------------|---------|
|   101   |      10      | 2     |
|   101   |      15      | 1     |





