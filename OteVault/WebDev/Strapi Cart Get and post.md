
We get the USER's id through the JWT token or through other means.

We then perform a GET request, that pulls all cart items that match the user's id.

If any are matched , though the relation product field, it will match the title, price,
and image of each product and add them to the user's cart. 

If item quantity is changed, we will make a post request to update the quantity change to the database.
If item quantity now equals zero, we will make a post request to delete the ordered item from the database.

If the user decides to proceed to check out: We will await for the user to complete an order form. When the order form is created, we will again pull the products from the database that match the user's id, and relate them to the order. The order will thus be posted to the database.


---------------------------------------------------------------------

Way number 2:  

cart items are not posted to the database at any point, till only the very end.
This means cart items are not saved, and will be deleted at any refresh or change of the page.

When the user decides to create an order , we will then post any item within the cart one by one to the database, and then we will post the order and we will relate the order to these items, and the order to the user.