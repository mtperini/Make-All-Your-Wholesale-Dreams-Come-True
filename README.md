# Make-All-Your-Wholesale-Dreams-Come-True
Shopify Wholesale Shop

<h2>Quantity Dropdowns</h2>

What if we need to sell in case packs and we don’t want people to be able to break up our wholesale inventory? Well you can force their selection by using a dropdown for quantity. 


First we make a new product template, we are calling this one case-packs-of-six:

You can make as many of these as you need/like. 

Then we copy over the original product liquid and we edit the quantity function. 

Here’s the original code: (This will vary based on your theme)


<div class="qty"> <a class="minus_btn" ></a>
                      <input type="text" id="quantity" name="quantity" class="txtbox" value="1" min="1">
                      <a class="plus_btn" ></a> 
                    </div>

 
Here’s our code to make a dropdown: 

 <div class="units_in_case_packs"> 
                          <p> Quantity (units in case pack increments)</p></div>
                          <div class="quantity_dropdown"><!--style class for the dropdown>-->
                     <label for="qty"></label>
					<select id="quantity" name="quantity">
						{% for i in (1..12) %} <!-- i is the interval value that we are going to multiplying. -->
                      <option value="{{ i | times:6}}">{{ i | times:6 }}</option> <!-- we use a multiple that corresponds to your case pack in this case we have packs of 6 but you can use any multiple. -->
							{% endfor %}
								</select></div>
                      <input type="submit" name="add" class="btn_c" id="addToCart" value="{{ 'products.product.add_to_cart' | t }}">


Now people can only pick quantities from 6-72 at a multiple of 6. 

Checkout Minimums 

What if your client wants a minimum order total? Well that’s a simple liquid fix. Let’s say we want at least a $200 dollar subtotal otherwise we don’t want them to be able to check out. 

If they don’t have a sufficient subtitle the checkout button isn’t visible. We can of course style this and make it more pronounced but this is the basics. 

If they have more than the minimum in their cart then they can checkout normally. 

Here’s the liquid update to the cart.liquid search for the “submit” input and put this liquid code above it and add the “{%endif%}” directly after. 

{% if customer.tags contains 'Wholesale' and cart.total_price < 20000 %}
        <p> Your wholesale total must be $200 or more.</p>
         {% else %}
          <input type="submit" name="update" class="btn--secondary update-cart" value="{{ 'cart.general.update' | t }}">
          <input type="submit" name="checkout" class="btn checkout" value="{{ 'cart.general.checkout' | t }}">
			{% endif %}
