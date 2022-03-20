# sql_tink

# Задание 1

select Пилоты.* from ( 

select second_pilot_id from Рейсы where destination = 'Шереметьево' 

group by second_pilot_id

having count(*)=3) ) t left join Пилоты  

on t.second_pilot_id = pilot_id

# Задание 2

select Пилоты.* from ( 

select first_pilot_id 

from Рейсы left join Самолеты 

on Рейсы.plane_id = Самолеты.plane_id 

where Самолеты.cargo_flg = 0 and Самолеты.capacity>30 group by first_pilot_id ) id 

left join Пилоты on Пилоты.pilot_id = id.first_pilot_id 

where Пилоты.age > 45

union

select Пилоты.* from ( 

select first_pilot_id 

from Рейсы left join Самолеты 

on Рейсы.plane_id = Самолеты.plane_id 

where Самолеты.cargo_flg = 0 and Самолеты.capacity>30 group by second_pilot_id ) id 

left join Пилоты on Пилоты.pilot_id = id.first_pilot_id 

where Пилоты.age > 45

# Задание 3

select top(10) p_id.passengers, Пилоты.* from ( 

select first_pilot_id, count(*) passengers 

from Рейсы left join Самолеты 

on Рейсы.plane_id = Самолеты.plane_id 

where cargo_flg = 1 group by first_pilot_id ) id left join Пилоты 

on id.first_pilot_id = Пилоты.pilot_id 

order by p_id.passengers desc
