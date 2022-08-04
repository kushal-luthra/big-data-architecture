### Uber System Design Interview Questions
System Design competency. <br>

Below is Uber Schema -   <br>
```
rider - rider id, name, age, gender, dob, phone, current payment type , current payment account;

rider_bookmarks - bookmark id, rider_id, bookmark_tag('home','office' etc), bookmark_locn id;

driver - driver id, name, joined date, curr cab id; check if running multiple vehicle so have curr cab id;

cab - vehicle type, per_km, base_fare, etc; cab id, cab type, brand, reg no, year of make;

map_grid = locn in a map grid of 1x1km; id, latitude,longitude;

locn - human readable landmark locn - india gate, school, rly station etc; id, map_grid_id, is_landmark, related_locn_id, zip_code;

trip - trip_id, cab id,rider id,start time, end time,request time, is surge applied, surge %, rider rating, driver rating, start locn id, end locn id;

payment - id, type, base fare, surge fare, total fare, payment timestamp, card no, transaction id

```

Question – <br>
System Design to handle scenario wherein customers who used Uber app to take a ride but couldn’t subscribe to the ride. <br> 
That is ,they drop off at the final tunnel. <br>