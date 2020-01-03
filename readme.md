# Online Quiz


https://Quiz.in


## Features


User can see the sample question.


### Feature 1: User login.


 ```sql

create table User_login (
User_id number,
User_name varchar2(20),
constraint user_id_pk primary key (User_id));

create sequence seq5 start with 1 increment by 1;

insert into User_login values (seq5.nextval,'Bob');
insert into User_login values (seq5.nextval,'Max');
insert into User_login values (seq5.nextval,'Joy');

select * from User_login;

```

| User_id | User_name | 
|---------|-----------|
| 1       | bob       |
| 2       | max       |
| 3       | joy       |

### Feature 2: We can choose a particular Catogary .

```sql

create table Catogary(
Cat_id number,
Catogary_name varchar2(25),
constraint cat_pk primary key(Cat_id));

create sequence seq2 start with 301 increment by 1;

insert into Catogary  values (seq1.nextval,'Maths');
insert into Catogary  values (seq1.nextval,'English');
insert into Catogary  values (seq1.nextval,'Science');

select * from Catogary;

```
| Cat_id | Catogary_name |   
|--------|---------------|
| 301    | Science       |
| 302    | Maths         |
| 303    | English       |

### Feature 3: We can choose difficulty level.

```sql

create table Diff(
Diff_id number,
Diff_level varchar2(10),
constraint Diff_id_pk primary key (Diff_id));


create sequence seq4 start with 601 increment by 1;

insert into Diff values (seq2.nextval,'Easy');
insert into Diff values (seq2.nextval,'Medium');
insert into Diff values (seq2.nextval,'Hard');

select * from Diff;

```

| Diff_id | Diff_level |
|---------|------------|
| 601     | Easy       |
| 602     | Medium     |
| 603     | Hard       |

```sql

create table Question (
Qus_id number,
Question varchar2(100) unique not null,
Cat_id number,
Diff_id number,
constraint Cat_id_fk Foreign Key (Cat_id) References catogary(Cat_id),
constraint Qus_id_pk primary key (Qus_id),
constraint Diff_id_fk Foreign Key (Diff_id) References Diff(Diff_id));

select * from Question;

insert into Question values (SEQ3.nextval,'How many years are there in a decade?','101','301');
insert into Question values (SEQ3.nextval,'The highest mountain on earth is?','101','301');
insert into Question values (SEQ3.nextval,'What is the biggest planet in our solar system?','101','301');
insert into Question values (SEQ3.nextval,'Jack ___________ English, Spanish and a bit of French.?','102','302');
insert into Question values (SEQ3.nextval,' ___________ to London on the train yesterday?','102','302');
insert into Question values (SEQ3.nextval,'Express the ten thousandths place in 1.7389','101','303');

```

| Qus_id | Question                              | Cat_id | Diff_id | 
|--------|---------------------------------------|--------|---------|
| 501    | How many years are there in a decade? | 301    | 501     |   
| 502    | The highest mountain on earth is?     | 301    | 501     |  
|        |                                       |        |         |          

### Feature 4: According to user choice the Question will be given .

 ```sql
 create table Sample_Qus(
 Qus_id number,
 Question varchar2(100) unique not null,
 constraint Sam_Qus_id_fk Foreign Key (Qus_id) References Question(Qus_id));
 
 create sequence seq3 start with 501 increment by 1;

insert into Sample_Qus values ('501',(select Question from Question where qus_id='501'));
insert into Sample_Qus values ('502',(select Question from Question where qus_id='502'));
insert into Sample_Qus values ('505',(select Question from Question where qus_id='505'));
insert into Sample_Qus values ('506',(select Question from Question where qus_id='506'));

select * from Sample_Qus;


```

| Qus_id | Question                              |
|--------|---------------------------------------|
| 501    | How many years are there in a decade? |
| 502    | The highest mountain on earth is?     |
|        |                                       |

### Feature 5: According to the question the choice will be displayed.

```sql

create table Choice(Choice_id number,
Choice varchar2(100) not null,
Qus_id number,
Answer number not null,
constraint Qus_id_fk Foreign Key (Qus_id) References question(Qus_id),
constraint Che unique (Choice));

create sequence seq1 start with 101 increment by 1;

insert into Choice values (SEQ4.nextval,'10','501','1');
insert into Choice values (SEQ4.nextval,'15','501','0');
insert into Choice values (SEQ4.nextval,'Fuji','502','0');
insert into Choice values (SEQ4.nextval,'Everest','502','1');

select * from Choice;


```

| Choice_id | Choice | Qus_id | Answer |
|-----------|--------|--------|--------|
|    101    |   10   |   501  |    1   |
|    102    |   15   |   502  |    0   |

### Feature 6: After the test the result will be displayed .

```sql
create table overall_result (
test_id number,
marks number, 
test_status varchar2(10),
user_id number,
constraint useerd foreign key (user_id) references user_login(user_id));


select * from overall_result

```
```sql
create or replace PROCEDURE PROCEDURE1 (i_user_id number ,i_test_id number ) AS 
v_marks number;
v_count number;
BEGIN
    select count(*) into v_count from test_attempt where user_id =i_user_id  and test_id=i_test_id;
  select sum(answer_status) into v_marks  from test_attempt where user_id =i_user_id  and test_id=i_test_id;
  update overall_result set marks = v_marks where user_id =i_user_id  and test_id=i_test_id;
END PROCEDURE1;
```

| Test_id | Mark_scored | Test_result           | User_id |
|---------|-------------|-----------------------|---------|
| 1001    | 10          | Good                  | 1       |
| 1001    | 4           | Better luck next time | 2       |

### Feature 7: You can view which are question you have answered correct and wrong.

```sql

create table Test_Attempt(
Qus_id number,
CHOICE_ID NUMBER,
Answer_status varchar2(10) not null,
Test_id number,
user_id number,
constraint qus_tst_id foreign key (qus_id) references Question(qus_id),
constraint che_tst_id foreign key (CHOICE_ID) references CHOICE(CHOICE_ID),
constraint tezst primary key (test_id),
constraint usezr  foreign key (user_id) references user_login(user_id));

insert into Test_Attempt values (502,703,0,1,1) ; 
insert into Test_Attempt values (501,701,1,1,1) ;
insert into Test_Attempt values (501,701,1,1,1) ;

select * from Test_Attempt;
create or replace FUNCTION IS_CORRECT 
(
  i_qus_id IN number , i_choice_id IN NUMBER 
) RETURN number AS 
v_answer number;
BEGIN
select answer into v_answer from choice where qus_id=i_qus_id and choice_id= i_choice_id;
  return v_answer;
END IS_CORRECT;

```

| Qus_id | Choice_id | Answer_status | Test_id | User_id |
|--------|-----------|---------------|---------|---------|
|   501  |    101    | 0             | 1001    | 1       |
|   502  |    102    | 1             | 1001    | 1       |
