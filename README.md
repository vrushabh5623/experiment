Exp4:
create table dept1 (
dnum number (3),
dname varchar (12),
mgr number (4),
area char (1),
constraint chk1_dnum check (dnum > 100),
constraint chk2_mgr unique(mgr), 
constraint chk3_area check (area in ('N', 'S')),
constraint pk4_dnum primary key (dnum));


create table emp3 (
enum number (4),
name varchar (12) not null,
salary number (7,2) not null,
tax number (6,2) not null, 
mgr number (4) not null, 
dnum1 number (3) not null,
constraint chk_1enum check (enum >9200),
constraint Fk_2dnum foreign key (dnum1) references dept1(dnum));


create table supplier12 (
snum number (3),
name varchar (12) unique,
city char (3),
constraint ch_snum check (snum between 501 and 505),
constraint ch1_city check (city in ('NXP', 'DLH', 'UMK')),
constraint pk1_snum primary key (snum));


create table supply(
pnum number (4),
snum number (3),
dnum number (4),
constraint pk1_supply primary key (pnum, snum,dnum));


#exp 5
#inset table2:
alter table supply add QTY number(2);
INSERT INTO dept1 (dnum, dname, mgr, area) VALUES (101, 'CT', 1000, 'N');
INSERT INTO dept1 (dnum, dname, mgr, area) VALUES (102, 'IT', 2000, 'S');
INSERT INTO dept1 (dnum, dname, mgr, area) VALUES (103, 'EL', 3000, 'N');
INSERT INTO dept1 (dnum, dname, mgr, area) VALUES (104, 'EC', 4000, 'N');
INSERT INTO dept1 (dnum, dname, mgr, area) VALUES (105, 'ME', 5000, 'S');


INSERT INTO emp3 (enum, name, salary, tax, mgr, dnum1) VALUES (9201, 'ABC', 10000, 1000, 1000, 101);
INSERT INTO emp3 (enum, name, salary, tax, mgr, dnum1) VALUES (9202, 'DEF', 20000, 2000, 2000, 102);
INSERT INTO emp3 (enum, name, salary, tax, mgr, dnum1) VALUES (9203, 'PQR', 25000, 2500, 3000, 103);
INSERT INTO emp3 (enum, name, salary, tax, mgr, dnum1) VALUES (9204, 'UVW', 15000, 1500, 1000, 101);
INSERT INTO emp3 (enum, name, salary, tax, mgr, dnum1) VALUES (9205, 'XYZ', 12000, 1200, 2000, 102);
INSERT INTO emp3 (enum, name, salary, tax, mgr, dnum1) VALUES (9206, 'AVY', 20000, 2000, 4000, 104);
INSERT INTO emp3 (enum, name, salary, tax, mgr, dnum1) VALUES (9207, 'BPQ', 18000, 1800, 5000, 105);


INSERT INTO supplier12 (snum, name, city) VALUES (501, 'xputs', 'NXP');
INSERT INTO supplier12 (snum, name, city) VALUES (502, 'oputs', 'NXP');
INSERT INTO supplier12 (snum, name, city) VALUES (503, 'bputs', 'DLH');
INSERT INTO supplier12 (snum, name, city) VALUES (504, 'cputs', 'NXP');
INSERT INTO supplier12 (snum, name, city) VALUES (505, 'dputs', 'UMK');

INSERT INTO supply (pnum, snum, dnum, QTY) VALUES (201, 501, 101, 50);
INSERT INTO supply (pnum, snum, dnum, QTY) VALUES (201, 501, 102, 10);
INSERT INTO supply (pnum, snum, dnum, QTY) VALUES (202, 502, 105, 20);
INSERT INTO supply (pnum, snum, dnum, QTY) VALUES (203, 503, 102, 30);
INSERT INTO supply (pnum, snum, dnum, QTY) VALUES (204, 504, 103, 40);


#Queries:
SELECT name, salary FROM emp3 WHERE dnum1 = 102;
select supplier12.snum, supplier12.name, dept1.dnum, dept1.dname from supplier12, supply, dept1 where supplier12.snum = supply.snum and supply.dnum = dept1.dnum and dept1.dname =  'IT';
select supplier12.name from supplier12, dept1, supply where supplier12.city = 'NXP' and dept1.area = 'S';

