# Dataset-Exploration

You are given a dataset that contains information about cars and their selling prices in a known period of time. The dataset is in csv format, you can download it directly from Kaggle. Make sure to download the file train.csv, then import the data inside the file to a database of your creation. After importing the data, make the following queries on it and provide the results: 

* Find the average price of cars in the dataset.
    ~~~sql
    SELECT AVG(PRICE) FROM Cars;
    ~~~
    +-------------------+   
    | AVG(PRICE)        |   
    +-------------------+   
    | 18555.92722357956 |   
    +-------------------+

* Calculate the number of cars with leather interior that are cheaper than $1400.
    ~~~sql
    SELECT COUNT(id) FROM Cars WHERE LeatherInterior='Yes' AND PRICE>1400;
    ~~~
    +-----------+   
    | COUNT(id) |   
    +-----------+   
    |     11422 |   
    +-----------+   

* Get the maximum price of Toyota cars produced in 2011.
   ~~~sql
    SELECT MAX(PRICE) FROM Cars WHERE Manufacturer='TOYOTA' AND ProdYear='2011';
    ~~~ 
    +------------+  
    | MAX(PRICE) |  
    +------------+  
    | 9408       |  
    +------------+  

* Sort the car manufacturers according to the average price of their cars descendingly.
    ~~~sql
    SELECT Manufacturer, AVG(PRICE) AS AVERAGE_PRICE  FROM Cars GROUP BY Manufacturer;
    ~~~
    +---------------+--------------------+  
    | Manufacturer  | AVERAGE_PRICE      |  
    +---------------+--------------------+  
    | LEXUS         |  19191.27698574338 |  
    | CHEVROLET     | 14926.368568755846 |  
    | HONDA         | 14291.335721596724 |  
    | FORD          |  15573.98199819982 |  
    | HYUNDAI       | 22338.447864154947 |  
    | TOYOTA        | 14248.982250136538 |  
    | MERCEDES-BENZ |  18609.38294797688 |  
    | OPEL          |  73305.61712846348 |  
    | PORSCHE       |  47106.03703703704 |  
    | BMW           |  20876.79218303146 |  
    | JEEP          | 25409.427536231884 |  
    | VOLKSWAGEN    | 11640.421416234887 |  
    | AUDI          | 14106.545098039216 |  
    | RENAULT       | 11464.351351351352 |  
    | NISSAN        | 10032.327272727272 |  
    | SUBARU        |  9998.698181818181 |  
    | DAEWOO        |  6973.142857142857 |  
    | KIA           | 15251.477434679335 |  
    | MITSUBISHI    | 13146.975778546714 |  
    | SSANGYONG     | 30894.637188208617 |  
    | MAZDA         |  9533.245901639344 |  
    | GMC           |             6831.4 |  
    | FIAT          | 11186.064102564103 |  
    | INFINITI      |            19774.8 |  
    | ALFA ROMEO    |            9890.25 |  
    | SUZUKI        | 11833.105263157895 |  
    | ACURA         |  5910.933333333333 |  
    | LINCOLN       |            13651.6 |  
    | VAZ           |  4613.583333333333 |  
    | GAZ           | 10481.666666666666 |  
    | CITROEN       | 10640.444444444445 |  
    | LAND ROVER    | 54053.489795918365 |  
    | MINI          | 17135.520833333332 |  
    | DODGE         |   8458.45054945055 |  
    | CHRYSLER      |  8631.538461538461 |  
    | JAGUAR        |  34408.78571428572 |  
    | ISUZU         |             9643.5 |  
    | SKODA         |            15079.8 |  
    | DAIHATSU      | 5402.7692307692305 |  
    | BUICK         |          11074.375 |  
    | TESLA         |              53941 |  
    | CADILLAC      |            13514.5 |
    | PEUGEOT       | 13470.117647058823 |  
    | BENTLEY       |           197574.5 |  
    | VOLVO         | 10278.894736842105 |  
    | სხვა          |            17248.5 |
    | HAVAL         |              15053 |  
    | HUMMER        |            31210.6 |  
    | SCION         |              16173 |
    | UAZ           |            5290.75 |  
    | MERCURY       |            12544.5 |  
    | ZAZ           |             3822.5 |
    | ROVER         | 2433.3333333333335 |  
    | SEAT          |             4829.5 |  
    | LANCIA        |              12231 |
    | MOSKVICH      |               4609 |  
    | MASERATI      |            20149.5 |  
    | FERRARI       |            66955.5 |
    | SAAB          |               6920 |  
    | LAMBORGHINI   |             872946 |  
    | ROLLS-ROYCE   |              178.5 |  
    | PONTIAC       |               6600 |
    | SATURN        |              13799 |  
    | ASTON MARTIN  |              54000 |  
    | GREATWALL     |              10036 |  
    +---------------+--------------------+  

* Calculate the percentage of cars that use petrol fuel only among cars with category Jeep.
    ~~~sql
    SELECT      ROUND(100.0 *          SUM(CASE WHEN FuelType = 'Petrol' THEN 1 ELSE 0 END) /          COUNT(*),2) AS petrol_percentage FROM cars WHERE category = 'Jeep';
    ~~~
    +-------------------+   
    | petrol_percentage |   
    +-------------------+   
    |             47.91 |   
    +-------------------+   

* Find the cheapest car(s) in the dataset. (If multiple cars have the same lowest price, return all of them.)
    ~~~sql
    SELECT Manufacuturer, PRICE
    FROM cars
    WHERE price = (
        SELECT MIN(price)
        FROM cars
    );
    ~~~
    +--------------+---------+-------+  
    | Manufacturer | Model   | PRICE |  
    +--------------+---------+-------+  
    | OPEL         | Astra   | 1     |  
    | CHEVROLET    | Lacetti | 1     |  
    +--------------+---------+-------+ 

*  Find the percentage of Toyota cars that are above the average price of all cars.
    ~~~sql
    SELECT
        ROUND(100.0 * COUNT(*) / (
            SELECT COUNT(*)
            FROM cars
            WHERE Manufacturer = 'Toyota'
        ), 2) AS percentage_above_average
    FROM cars
    WHERE Manufacturer = 'Toyota'
    AND price > (
        SELECT AVG(price)
        FROM cars
      );
    ~~~

    +--------------------------+    
    | percentage_above_average |    
    +--------------------------+    
    |                    29.60 |    
    +--------------------------+    
