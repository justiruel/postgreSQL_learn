````````
CREATE OR REPLACE FUNCTION public.fn_get_device_parking_lot(
	_id character varying,
 	OUT id_detail_zona integer,
 	OUT device_id character varying,
 	OUT name character varying,
 	OUT state character,
 	OUT up_down_state character,
 	OUT battery_state integer,
 	OUT status_flag character
)
    RETURNS SETOF record 
    LANGUAGE 'plpgsql'

    COST 100
    VOLATILE 
    ROWS 1000
AS $BODY$
	begin
		if $1 = '' then
			RETURN QUERY
			select a.id_detail_zona,a.device_id,a.name,a.state,a.up_down_state,a.battery_state,a.status_flag FROM device_parking_lot a WHERE a.status_flag = '1';
 		else
			RETURN QUERY
 			select a.id_detail_zona,a.device_id,a.name,a.state,a.up_down_state,a.battery_state,a.status_flag FROM device_parking_lot a WHERE a.status_flag = '1' AND a.id = $1::integer;
		end if;
	end;
	

$BODY$;

ALTER FUNCTION public.fn_get_device_parking_lot(character varying)
    OWNER TO postgres;
````````
