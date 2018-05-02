```
do $$
declare num integer = 1;
declare x char varying = (select name from visionet where age = 23);

begin
if x = 'randy' then
raise notice 'Value: %', x;
end if;
end$$
```
