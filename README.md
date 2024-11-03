## Urban Taxi - Sprint 6
## Consola y Base de Datos
### Axel Van Dyck, Grupo 14

## Ejercicios para consultas en bases de datos y manejo de consola

### Consola

#### Ejercicio 1
El comando o secuencia de comandos que te proporcionó los registros necesarios:

    $ grep -R "^233.201" ~/logs/2019/12


#### Ejercicio 2
Comandos que crean los directorios `bug1` y `events`:

    $ mkdir ~/bug1 $ mkdir ~/bug1/events $ cd ~/bug1/events $ touch 400.txt 500.txt

El comando que usas para seleccionar las solicitudes para un periodo especificado. Estas son las solicitudes que usas para obtener registros en el archivo `main.txt`:

    $ grep ~/logs/2019/12/apache_2019-12-30.txt > ~/bug1/main.txt

Los comandos que usas para colocar los registros en los archivos `400.txt` y `500.txt` del `main.txt`:
    
    $ grep " 400 " ~/bug1/main.txt > ~/bug1/events/400.txt $ grep " 500 " ~/bug1/main.txt > ~/bug1/events/500.txt


- **400.txt**: 172 líneas encontradas  
- **500.txt**: 156 líneas encontradas

### Base de datos

#### Ejercicio 1
Número de automóviles:
5500

La solicitud que utilizaste para resolver la tarea:
```sql
SELECT COUNT(DISTINCT vehicle_id) FROM cabs;
```


Ejercicio 2
Lista de las compañías con menos de 100 automóviles. La solicitud que te ayudó a resolver la tarea:

    SELECT COUNT(DISTINCT vehicle_id) AS cnt, company_name 
    FROM cabs 
    GROUP BY company_name 
    HAVING COUNT(DISTINCT cab_id) < 100 
    ORDER BY cnt DESC;


Ejercicio 3
La tabla con los datos para el periodo especificado. Poner una estampa en las fechas de acuerdo a su clima registrado, en un periodo específico. La solicitud que utilizaste para resolver la tarea:

    SELECT ts, CASE
        WHEN description LIKE '%rain%' THEN 'Bad' 
        WHEN description LIKE '%storm%' THEN 'Bad' 
        ELSE 'Good' 
    END AS Weather_Conditions  
    FROM weather_records 
    WHERE ts BETWEEN '2017-11-05 00:00:00' AND '2017-11-06 00:00:00';


Ejercicio 4
La tabla con datos para contar los viajes de una compañía en un período específico. La solicitud que utilizaste para resolver la tarea:
    
    SELECT cabs.company_name, COUNT(DISTINCT trips.trip_id) AS trips_amount 
    FROM trips 
    JOIN cabs ON cabs.cab_id = trips.cab_id 
    WHERE CAST(trips.start_ts AS date) BETWEEN '2017-11-15' AND '2017-11-16' 
    GROUP BY cabs.company_name 
    ORDER BY trips_amount DESC;
