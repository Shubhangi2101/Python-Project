# Python-Project
It includes DVD Rental Database connected in Python to create Data visualization.

Query 1. 
CREATE VIEW Revenue_of_countries AS
WITH Customerandcountry AS
(
Select AddressWithCityandCountry.city_id, AddressWithCityandCountry.country, AddressWithCityandCountry.address_id, customer.customer_id from (
WITH cityandcountry AS (select city.city_id, city.city, country.country_id, country.country from city 
inner join country  on city.country_id=country.country_id
order by country.country_id)
select cityandcountry.city_id, cityandcountry.country, address.address_id from cityandcountry
inner join address on cityandcountry.city_id=address.city_id
order by city_id) AS AddressWithCityandCountry
inner join customer on AddressWithCityandCountry.address_id=customer.address_id
)
select Customerandcountry.country, Customerandcountry.customer_id,(payment.amount)  from Customerandcountry
inner join payment on Customerandcountry.customer_id=payment.customer_id;

select sum(amount),country from Revenue_of_countries 
group by country


![Movie Revenue from Diff Countries](https://github.com/Shubhangi2101/Python-Project/assets/46973898/e8d6de20-8514-429b-ba13-0b46fb2ccef9)


Query2. 
CREATE VIEW FILM_REVENUE AS
WITH RENTED_INVENTORY_AMOUNT AS (
SELECT RENTAL.RENTAL_ID,RENTAL.INVENTORY_ID,PAYMENT.AMOUNT FROM PAYMENT 
INNER JOIN RENTAL ON PAYMENT.RENTAL_ID=RENTAL.RENTAL_ID)
SELECT RENTED_INVENTORY_AMOUNT.RENTAL_ID,RENTED_INVENTORY_AMOUNT.INVENTORY_ID, RENTED_INVENTORY_AMOUNT.AMOUNT,INVENTORY.FILM_ID FROM RENTED_INVENTORY_AMOUNT
INNER JOIN INVENTORY ON RENTED_INVENTORY_AMOUNT.INVENTORY_ID=INVENTORY.INVENTORY_ID
ORDER BY INVENTORY.FILM_ID

SELECT CONCAT(FIRST_NAME,' ', LAST_NAME) AS FULL_NAME FROM ACTOR WHERE ACTOR_ID IN(SELECT ACTOR_ID FROM (
WITH TOP_TEN_REVENUE_GENERATING_FILMS AS
( SELECT FILM_ID, SUM(AMOUNT) FROM FILM_REVENUE 
 GROUP BY FILM_ID 
 ORDER BY FILM_ID DESC 
 LIMIT 10
) 
SELECT FILM_ACTOR.ACTOR_ID,TOP_TEN_REVENUE_GENERATING_FILMS.FILM_ID  FROM FILM_ACTOR 
INNER JOIN TOP_TEN_REVENUE_GENERATING_FILMS ON FILM_ACTOR.FILM_ID=TOP_TEN_REVENUE_GENERATING_FILMS.FILM_ID
ORDER BY FILM_ID DESC
LIMIT 10
	) AS SUBQUERY )


![Top Ten Revenue generating Countries](https://github.com/Shubhangi2101/Python-Project/assets/46973898/92a6d609-4c37-4a07-a47a-dbdce51e5b9e)


 
