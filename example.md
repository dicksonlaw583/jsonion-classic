# JSOnion Examples

------------

## Encoding a Basic Map
```
//Build a map of fruits to prices
fruit_map = jso_new_map();
jso_map_add_real(fruit_map, "Apple", 4.49);
jso_map_add_real(fruit_map, "Banana", 4.99);
jso_map_add_real(fruit_map, "Cherry", 2.75);

//Encode
json = jso_encode_map(fruit_map);
```
------------

## Encoding a Nested Map
```
//Build a map of supermarkets to inventories
supermarket_map = jso_new_map();

//Build the inventory of a supermarket
gamegeisha_fruit_map = jso_new_map();
jso_map_add_real(gamegeisha_fruit_map, "Apple", 3.49);
jso_map_add_real(gamegeisha_fruit_map, "Banana", 6.99);
jso_map_add_real(gamegeisha_fruit_map, "Cherry", 1.99);

//Build the inventory of a competing supermarket
codedanna_fruit_map = jso_new_map();
jso_map_add_real(codedanna_fruit_map, "Apple", 4.49);
jso_map_add_real(codedanna_fruit_map, "Banana", 4.99);
jso_map_add_real(codedanna_fruit_map, "Cherry", 2.75);

//Add the supermarkets
jso_map_add_submap(supermarket_map, "gamegeisha", gamegeisha_fruit_map);
jso_map_add_submap(supermarket_map, "codedanna", codedanna_fruit_map);

//Encode
json = jso_encode_map(supermarket_map);
```
------------

## Encoding a Basic List
```
//Build a list of strings
client_list = jso_new_list();
jso_list_add_string(client_list, "Arnold Anderson");
jso_list_add_string(client_list, "Brian Brown");
jso_list_add_string(client_list, "Catherine Capulet");

//Encode
json = jso_encode_list(client_list);
```
------------

## Encoding a Nested List
```
//Build a list of floors in an office building
floor_list = jso_new_list();

//Build a sublist consisting of companies on the ground floor
ground_floor_list = jso_new_list();
jso_list_add_string(ground_floor_list, "Blue Skies Travel Agency");
jso_list_add_string(ground_floor_list, "Starbucks");
jso_list_add_string(ground_floor_list, "Hikari Sushi and Teriyaki");

//Build a sublist consisting of companies on the second floor
second_floor_list = jso_new_list();
jso_list_add_string(second_floor_list, "GameGeisha Interactive");
jso_list_add_string(second_floor_list, "Polaris Tax Return Services");
jso_list_add_string(second_floor_list, "ABC Law Firm");

//Put the floors together
jso_list_add_sublist(floor_list, ground_floor_list);
jso_list_add_sublist(floor_list, second_floor_list);

//Encode
json = jso_encode_list(floor_list);
```
------------

## Decoding a Map
```
//Start with a JSON string
json = '{ "Apple":4.49, "Banana":4.99, "Cherry":2.75 }';

//Decode
fruit_map = jso_decode_map(json);
```
------------

## Decoding a List
```
//Start with a JSON string
json = '["Arnold Anderson", "Brian Brown", "Catherine Capulet"]';

//Decode
client_list = jso_decode_list(json);
```
------------

## Discarding a Map
```
//Throw away a map
throw_away_map = jso_new_map();
jso_cleanup_map(throw_away_map);
```
------------

## Discarding a List
```
//Throw away a list
throw_away_list = jso_new_list();
jso_cleanup_list(throw_away_list);
```
------------

## Referencing from a Basic Map
```
//Get a basic map from a JSON string
fruit_map = jso_decode_map('{ "Apple":4.49, "Banana":4.99, "Cherry":2.75 }');

//Retrieving a value
apple_price = jso_map_get(fruit_map, "Apple");
```
------------

## Referencing from a Nested Map
```
//Get a nested map from a JSON string
supermarket_map = jso_decode_map('{ "gamegeisha" : { "Apple":3.49, "Banana":6.99, "Cherry":1.99 }, "codedanna" : { "Apple":4.49, "Banana":4.99, "Cherry":2.75 } }');

//Retrieving a value (with safety check)
if (jso_map_check(supermarket_map, "gamegeisha", "Apple")) {
	apple_price_at_gamegeisha = jso_map_lookup(supermarket_map, "gamegeisha", "Apple");
}
```
------------

## Referencing from a Basic List
```
//Get a basic list from a JSON string
client_list = jso_decode_list('["Arnold Anderson", "Brian Brown", "Catherine Capulet"]');

//Retrieving a value
first_client_name = jso_list_get(client_list, 0);
```
------------

## Referencing from a Nested List
```
//Get a basic list from a JSON string
floor_list = jso_decode_list('[["Blue Skies Travel Agency", "Starbucks", "Hikari Sushi and Teriyaki"], ["GameGeisha Interactive", "Polaris Tax Return Services", "ABC Law Firm"]]');

//Retrieving a value (with safety check)
if (jso_list_check(floor_list, 0, 2)) { 
	ground_floor_third_shop = jso_list_lookup(floor_list, 0, 2);
}
```
------------

## Comparing two Maps
```
//Get two maps from JSON strings
gamegeisha_shop = jso_decode_map('{ "Apple":3.49, "Banana":6.99, "Cherry":1.99 }');
codedanna_shop = jso_decode_map('{ "Apple":4.49, "Banana":4.99, "Cherry":2.75 }');

//Compare the two lists
if (jso_compare_maps(gamegeisha_shop, codedanna_shop)) {
	show_message("These shops sell the same fruits at the same price.");
} else {
	show_message("These shops sell different fruits, or the same fruits at different prices.");
}
```
------------

Comparing two Lists
```
//Get two lists from JSON strings
correct_sequence = jso_decode_list('["D", "A", "C", "B"]');
entered_sequence = jso_decode_list('["D", "A", "C", "B"]');

//Compare the two lists
if (jso_compare_lists(correct_sequence, entered_sequence)) {
	show_message("You entered the correct sequence.");
} else {
	show_message("Try again.");
}
```
