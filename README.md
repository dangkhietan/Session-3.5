# Topic 1: Which products contribute the most to carbon emissions?
## Explore data
###Table 'Product_emissions'
```SQL
SELECT *
FROM product_emissions
LIMIT 5;
```
| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf | operations_percent_total_pcf | downstream_percent_total_pcf | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -------------------------: | ---------------------------: | ---------------------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                      | 17.36                        | 2.01                         | 
| 10261-1-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1488                 | 30.65                      | 5.51                         | 63.84                        | 
| 10261-2-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1818                 | 25.08                      | 4.51                         | 70.41                        | 
### So sanh AVG cac muc do Carbon_emissions theo san pham:
```SQL
SELECT product_name, ROUND (AVG(carbon_footprint_pcf),2) AS 'Average_PCF'
FROM product_emissions
GROUP BY product_name
ORDER BY Average_PCF DESC
LIMIT 10;
```
| product_name                                                                                                                       | Average_PCF | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ----------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00  | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00  | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00  | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00  | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00   | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00   | 
| TCDE                                                                                                                               | 99075.00    | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00    | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00    | 
| Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00    | 

# Topic 2:  What are the industry groups of these products?
## Tìm top 10 industry_group_id sản xuất các product_name có lượng khí phát thải cao:
```SQL
SELECT product_name,
	    industry_group_id,
	    ROUND (AVG(carbon_footprint_pcf),2) AS 'Average_PCF'
FROM product_emissions
GROUP BY product_name
ORDER BY Average_PCF DESC
LIMIT 10;
```
| product_name                                                                                                                       | industry_group_id | Average_PCF | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ----------------: | ----------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 13                | 3718044.00  | 
| Wind Turbine G132 5 Megawats                                                                                                       | 13                | 3276187.00  | 
| Wind Turbine G114 2 Megawats                                                                                                       | 13                | 1532608.00  | 
| Wind Turbine G90 2 Megawats                                                                                                        | 13                | 1251625.00  | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 7                 | 191687.00   | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 19                | 167000.00   | 
| TCDE                                                                                                                               | 19                | 99075.00    | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 7                 | 91000.00    | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 7                 | 85000.00    | 
| Mercedes-Benz SL (SL 350)                                                                                                          | 7                 | 72000.00    | 
## Tìm tên top 10 ngành công nghiệp sản xuất các product_name có lượng khí phát thải cao:
```SQL
SELECT ig.industry_group, 
		pe.product_name, 
		ROUND(AVG(carbon_footprint_pcf),2) AS 'Average_PCF'
FROM product_emissions AS pe
JOIN industry_groups AS ig on pe.industry_group_id =ig.id
GROUP BY ig.industry_group, pe.product_name
ORDER BY Average_PCF DESC
LIMIT 10;
```
| industry_group                     | product_name                                                                                                                       | Average_PCF | 
| ---------------------------------: | ---------------------------------------------------------------------------------------------------------------------------------: | ----------: | 
| Electrical Equipment and Machinery | Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00  | 
| Electrical Equipment and Machinery | Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00  | 
| Electrical Equipment and Machinery | Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00  | 
| Electrical Equipment and Machinery | Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00  | 
| Automobiles & Components           | Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00   | 
| Materials                          | Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00   | 
| Materials                          | TCDE                                                                                                                               | 99075.00    | 
| Automobiles & Components           | Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00    | 
| Automobiles & Components           | Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00    | 
| Automobiles & Components           | Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00    | 

# Topic 3: What are the industries with the highest contribution to carbon emissions?
## Sắp xếp tên industry_group sản xuất có lượng khí phát thải theo thứ tự giảm dần:
```SQL
SELECT ig.industry_group,  
		ROUND(AVG(carbon_footprint_pcf),2) AS 'Average_PCF'
FROM product_emissions AS pe
JOIN industry_groups AS ig on pe.industry_group_id =ig.id
GROUP BY ig.industry_group
ORDER BY Average_PCF DESC;
```
| industry_group                                   | Average_PCF | 
| -----------------------------------------------: | ----------: | 
| Electrical Equipment and Machinery               | 891050.73   | 
| Automobiles & Components                         | 35373.48    | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 24162.00    | 
| Capital Goods                                    | 7391.77     | 
| Materials                                        | 3208.86     | 
| "Mining - Iron, Aluminum, Other Metals"          | 2727.00     | 
| Energy                                           | 2154.80     | 
| Chemicals                                        | 1949.03     | 
| Media                                            | 1534.47     | 
| Software & Services                              | 1368.94     | 

## Truy xuất tên industry_group sản xuất có sản phẩm có lượng khí phát thải CAO nhất:
```SQL
SELECT ig.industry_group,  
		ROUND(AVG(carbon_footprint_pcf),2) AS 'Average_PCF'
FROM product_emissions AS pe
JOIN industry_groups AS ig on pe.industry_group_id =ig.id
GROUP BY ig.industry_group
ORDER BY Average_PCF DESC
LIMIT 1;
```
| industry_group                     | Average_PCF | 
| ---------------------------------: | ----------: | 
| Electrical Equipment and Machinery | 891050.73   | 
