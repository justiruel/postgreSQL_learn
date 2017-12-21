## return setof record
```
CREATE OR REPLACE FUNCTION semua(nama varchar) 
returns SETOF record as $$
    select * from company where name=$1
$$ language 'sql';
```
## cara panggil
```
select semua('joni')
```
//return table
CREATE OR REPLACE FUNCTION semua_row(nama varchar) 
returns table(name text, age integer) as $$
    select name,age from company where name=$1
$$ language 'sql';

//cara panggil
select * from semua_row('joni')


//return table with like statement
CREATE OR REPLACE FUNCTION semua_like(nama varchar) 
returns table(name text, age integer) as $$
    select name,age from company where name LIKE '%' || $1 || '%'
$$ language 'sql';

//cara panggil
select * from semua_like('han')


//return varchar 
CREATE OR REPLACE FUNCTION semua_varchar(nama varchar) 
returns varchar as $$
    select name from company where name=$1
$$ language 'sql';

//cara panggil
select * from semua_varchar('joni')

ref: http://www.postgresqlforbeginners.com/2010/12/create-function-return-types.html
