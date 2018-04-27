# Having
having digunakan sebagai pengganti where sesudah query di group by

## contoh

table
```
name      address     age salary
"alde"    "tuban"     20  3000000
"afkar"   "kediri"    20  2500000
"anang"   "nganjuk"   26  4000000
"jimmy"   "tangerang" 27  10000000
"randy"   "tuban"     23  5000000
"aefin"   "tuban"     24  7000000
```

query group by
```
select address, count(salary), max(salary) from visionet where salary > 4000000 group by address
```

hasil grouping
```
address		  count	max
"tuban"		  "2"		7000000
"tangerang"	"1"		10000000
```
ini artinya record di group berdasarkan address

dari hasil grouping tersebut bagaimana jika saya ingin mendapatkan record where address = tuban? karena query sudah di grouping kita tidak dapat menggunakan where, 
sebagai gantinya kita gunakan having

contoh :

```
select address, count(salary), max(salary) from visionet where salary > 4000000 group by address having address = 'tuban'

hasil : 

address		count	max
"tuban"		"2"		7000000
```

```
select address, count(salary), max(salary) from visionet where salary > 4000000 group by address having count(salary) < 2

hasil : 

address		  count	max
"tangerang"	"1"		10000000
```

```
select address, count(salary), max(salary) from visionet where salary > 4000000 group by address having max(salary) > 9000000

hasil : 

address		  count	max
"tangerang"	"1"		10000000
```

Dapat juga digunakan untuk semua fungsi aggregate lain yang tidak ikut ke select 
```
select address, count(salary), max(salary) from visionet where salary > 4000000 group by address having avg(salary) = 10000000
hasil : 

address		  count	max
"tangerang"	"1"		10000000
```
ini maksudnya : tampilkan record yang salary > 4000000, lalu hasilnya di group by address, lalu salary yang punya address yang sama dihitung rata-rata nya



