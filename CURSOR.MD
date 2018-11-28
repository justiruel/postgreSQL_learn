http://www.postgresqltutorial.com/plpgsql-cursor/
https://dba.stackexchange.com/questions/186257/how-can-i-return-multiple-rows-of-records-in-pl-pgsql
https://stackoverflow.com/a/6085167
-----------------------------------------
````
select * from parking_lot

drop function if exists test_function();
create or replace function test_function()
    returns table (id int, name character varying)
    language plpgsql as $$
begin
    return query
        select  a.id,a.name from parking_lot a;
    -- you can use return query multiple times
    -- or assign values to columns
    -- and return the row:
	id = 100;
    name = 'naruto';	
    return next; -- without a parameter
	
	id = 900;
    name = 'boruto';	
    return next; -- without a parameter
	
end $$

select * from test_function();









--DROP FUNCTION get_film_titles(integer) 
CREATE OR REPLACE FUNCTION get_film_titles(p_year INTEGER)
   --RETURNS text AS $$
   RETURNS table (_id int, _name character varying) AS $$
DECLARE 
 titles TEXT DEFAULT '';
 rec_film   RECORD;
 cur_films CURSOR FOR SELECT * FROM parking_lot; --WHERE id = p_year;
BEGIN
   -- Open the cursor
   OPEN cur_films;
 
   LOOP
    -- fetch row into the film
      FETCH cur_films INTO rec_film;
    -- exit when no more row to fetch
      EXIT WHEN NOT FOUND;
 
 	_id = rec_film.id;
	_name = 'ini, '||rec_film.name;
	return next;
    -- build the output
	 --titles := titles || ',' || rec_film.name || ':' || rec_film.name;
   END LOOP;
  
   -- Close the cursor
   CLOSE cur_films;
 
   --RETURN titles;
END; $$
 
LANGUAGE plpgsql;

select * from get_film_titles(7)

DROP FUNCTION get_film_titles(integer)
select * from parking_lot
````
