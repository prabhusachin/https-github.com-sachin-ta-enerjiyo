<script>
	let items = [
		{ id: 'J---aiyznGQ', name: 'Badam',price:750,rate:750,qty:'1 Kg' },
		{ id: 'z_AbfPXTKms', name: 'Kaju',price:875,rate:875,qty:'1 Kg' },
		{ id: 'OUtn3pvWmpg', name: 'Pista',price:1250,rate:1250,qty:'1 Kg' },
		{ id: 'OUtn3pvWmpg', name: 'Walnut',price:1500,rate:1500,qty:'1 Kg' },
		{ id: 'OUtn3pvWmpg', name: 'Anjeer',price:1400,rate:1400,qty:'1 Kg' },
	];
	let categories = [
		{ id: 'J---aiyznGQ', name: 'Dryfruits' },
		{ id: 'z_AbfPXTKms', name: 'Fruits' },
		{ id: 'OUtn3pvWmpg', name: 'Vegetables' },
		{ id: 'OUtn3pvWmpg', name: 'Meals' },
	];
	let cartProducts = [];
	
let showItems = true;
let showPhotos = false;
let showCategories = false;
let showCart = false;
var removeByAttr = function(arr, attr, value){
    var i = arr.length;
    while(i--){
       if( arr[i] 
           && arr[i].hasOwnProperty(attr) 
           && (arguments.length > 2 && arr[i][attr] === value ) ){ 

           arr.splice(i,1);

       }
    }
    return arr;
}
function handleItemsClick() {
		showItems = true;
		showPhotos = false;
		showCategories = false;
		showCart = false;
	}
function handlePhotosClick() {
		showItems = false;
		showPhotos = true;
		showCategories = false;
		showCart = false;
	}
function handleCategoriesClick() {
		showItems = false;
		showPhotos = false;
		showCategories = true;
		showCart = false;
	}
function handleCartClick() {
		showItems = false;
		showPhotos = false;
		showCategories = false;
		showCart = true;
		console.log (cartProducts);
	}	
function changeQuantity (qty,i)
{
	if (qty == '1 Kg')
	{
	items[i]["qty"] = '250 gm';
	items[i]["price"] = items[i]["price"] / 4;
	}
	if (qty == '250 gm')
	{  
	items[i]["qty"] = '500 gm';
	items[i]["price"] = items[i]["price"] * 2;
	}
	if (qty == '500 gm')
	{
	items[i]["qty"] = '1 Kg';
	items[i]["price"] = items[i]["price"] * 2;
	}
}	
function getPerKgPrice (name)
{
	console.log ("inside get per kg price");
	console.log (name);
	var i = items.length;
	while (i--)
	{
		console.log (items[i]["name"]);
		console.log (items[i]["name"] == name);
		if (items[i]["name"] == name)
		{
			console.log (items[i]["rate"]);
			return items[i]["rate"];
		}
	}
	return 0.00;
}
function getTotalPrice (name,prodlineitems)
{
var totalWeight = getTotalWeight (prodlineitems);
var totalPrice = totalWeight * getPerKgPrice (name);
console.log (totalWeight);
console.log (totalPrice);
return totalPrice ;

}
function getTotalWeight (prodlineitems)
{
console.log ("inside get total weight");
console.log (prodlineitems);
var j = prodlineitems.length;
var weight = 0;
var totalWeight = 0;
while (j--)
{
if (prodlineitems[j]["weight"].includes("gm"))	
{
	weight += parseInt(prodlineitems[j]["weight"].split(" ")[0]) * parseInt(prodlineitems[j]["qty"]);
}
if (prodlineitems[j]["weight"].includes("Kg"))	
{
	weight += parseInt(prodlineitems[j]["weight"].split(" ")[0]) * parseInt(prodlineitems[j]["qty"]) * 1000;	
}
console.log ("weight found for "+j);
console.log (weight);


console.log ("weight found for "+j);
console.log (weight);

}
weight = weight / 1000;
return weight;
}
function addToCart (name,weight){
	console.log ("weight is ");
	console.log (weight);
	var i = cartProducts.length;
	var productFound = false;
	var prodlineitems = [];
	while(i--){
       if(cartProducts[i]["name"] === name ){ 
		prodlineitems = cartProducts[i]["prodlineitems"];
		var j = prodlineitems.length;
		var weightFound = false;
		while (j--){
		if (prodlineitems[j]["weight"] == weight)
		{
			weightFound = true;
			prodlineitems[j]["qty"] += 1;
		}
		
		}
		if (!weightFound)
		{
			prodlineitems.push ({weight:weight,qty:1})
		}
		console.log (prodlineitems);
		cartProducts[i]["qty"] += 1;
		
		productFound = true;
		break;
	   }
	}
	if (!productFound){
	var prodlineitems = [];
    prodlineitems.push ({weight:weight,qty:1})
	cartProducts.push ({name: name,qty:1,prodlineitems:prodlineitems});
	console.log (cartProducts);
	console.log (cartProducts[0]["prodlineitems"]);
}

}
function removeFromCart (name){
	cartProducts = removeByAttr (cartProducts,"name",name);

}
</script>
<style>
body{
	width:90%;
	margin:0 auto;
	font-family: Arial, Helvetica, sans-serif;
	/*border:1px solid red;*/
}
button{
	padding:10px;
	background-color: #eee;
	border:1px solid #777;
	font-size: 16px;
	font-weight: bold;
}
.lineitemscontainer{
	float:left;
	/* border:1px solid red; */
	width:25%;
}
.logo{
	color:#00d500;
	float:left;
	/*border:1px solid red;*/
}
.headline{
	color:#777;
	margin-left: 60px;
margin-top: 32px;
float:left;
/*border:1px solid red;*/
}
hr{
	clear: both;
}
ul{
	list-style-type: none;
}
li{
	width:60%;
}
.left10{
	margin-left: 10%;
}

.left5{
	margin-left: 5%;
}
.width20{
width: 10%;
display:block;
float:left;
}
.width15{
	width:15%;
}
.left10px{
	margin-left: 10px;
}
.productname{
	width:15%;
	/*border:1px solid red;*/
	display:block;
	float:left;
	/* border:1px solid red; */
}
.productcontainer{
	padding: 10px;
	padding-bottom: 30px;
margin-bottom: 10px;
	border-bottom: 2px solid #aaa;
}
.col2{
	padding-bottom: 5px;
	font-size:18px;
	color:#000;
}
</style>
<!-- {#if show}

{/if} -->
<body>
<h1 class = "logo">
	Enerjio
</h1>	
<h2 class = "headline">
Buy Quality Dryfruits
</h2>
<hr/>

<button on:click={handleItemsClick} id = "menubutton" class = "selectcategory">
Items
</button>
<button on:click={handlePhotosClick} id = "photobutton" class = "selectcategory">
Photos
</button>
<button on:click={handleCategoriesClick} id = "categorybutton" class = "selectcategory">
Category
</button>
<button on:click={handleCartClick} id = "categorybutton" class = "selectcategory">
	Cart
</button>
<hr/>
{#if showItems}
<div id = "productmenu" class = "maincontainer">	
<ul>
{#each items as { id, name,price,qty }, i}
<li>
<span class = "productname">
{name}
</span>
<span class = "left10 width20">
	&#8377;&nbsp;{price}
	</span>
<button on:click={()=>changeQuantity(qty,i)} class = "left5 width15">
{qty} &#9660;
</button>
<button on:click={()=>addToCart(name,qty)}  class = "left10px">
Add
</button>
</li>
{/each}
</ul>
</div>
{/if}
{#if showPhotos}
<div id = "photolist" class = "maincontainer">
photolist
</div>	
{/if}
{#if showCategories}
<div id = "categorylist" class = "maincontainer">
<ul>
	{#each categories as { id, name }, i}
<li>
<span class = "productname">
{name}
</span>
<button on:click={handleItemsClick} class = "left10 selectcategorybutton">
Select
</button>
</li>	
{/each}
</ul>	
</div>	
{/if}
{#if showCart}
<div id = "cartlist" class = "maincontainer">
	<ul>
{#each cartProducts as {name,prodlineitems},i}
    <li class = "productcontainer">
		<span class = "productname">
			{name}
		</span>
		<ul class = "lineitemscontainer">
		{#each prodlineitems as {weight,qty},j}
		<li class = "col2">
			{weight} * {qty}
	    </li>
		{/each}
		</ul>
		<span>
			{getTotalWeight (prodlineitems)} &nbsp;Kg
		</span>
		<span class = "left10px">
			&#8377; {getTotalPrice (name,prodlineitems)}
		</span>
		<button on:click={()=>removeFromCart(name)} class = "left10px">
			Remove
			</button>
		</li>
		{/each}
</ul>
</div>	
{/if}
</body>