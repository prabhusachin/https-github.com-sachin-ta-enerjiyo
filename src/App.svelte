<script>
	let items = [
		{ id: 'J---aiyznGQ', name: 'Badam',price:750,rate:750,qty:'1 Kg' },
		{ id: 'J---aiyznGQ', name: 'Kaju',price:875,rate:875,qty:'1 Kg' },
		{ id: 'J---aiyznGQ', name: 'Pista',price:1250,rate:1250,qty:'1 Kg' },
		{ id: 'J---aiyznGQ', name: 'Walnut',price:1500,rate:1500,qty:'1 Kg' },
		{ id: 'J---aiyznGQ', name: 'Anjeer',price:1400,rate:1400,qty:'1 Kg' },
		{ id: 'z_AbfPXTKms', name: 'Apple',price:200,rate:200,qty:'1 Kg' },
		{ id: 'z_AbfPXTKms', name: 'Grapes',price:175,rate:175,qty:'1 Kg' },
		{ id: 'z_AbfPXTKms', name: 'Watermelon',price:250,rate:250,qty:'1 Kg' },
		{ id: 'z_AbfPXTKms', name: 'Chickoo',price:150,rate:150,qty:'1 Kg' },
		{ id: 'z_AbfPXTKms', name: 'Pineapple',price:120,rate:120,qty:'1 Kg' },
		{ id: 'OUtn3pvWmpg', name: 'Flower',price:100,rate:100,qty:'1 Kg' },
		{ id: 'OUtn3pvWmpg', name: 'Brinjal',price:75,rate:75,qty:'1 Kg' },
		{ id: 'OUtn3pvWmpg', name: 'Drumsticks',price:25,rate:25,qty:'1 Kg' },
		{ id: 'OUtn3pvWmpg', name: 'Gobi',price:95,rate:95,qty:'1 Kg' },
		{ id: 'OUtn3pvWmpg', name: 'Potato',price:110,rate:110,qty:'1 Kg' },
		{ id: 'Pm_0058xmkz', name: 'Veg',price:400,rate:400,qty:'1 Kg' },
		{ id: 'Pm_0058xmkz', name: 'NonVeg',price:675,rate:675,qty:'1 Kg' },
		{ id: 'Pm_0058xmkz', name: 'Chinese',price:425,rate:425,qty:'1 Kg' },
		{ id: 'Pm_0058xmkz', name: 'Punjabi',price:595,rate:595,qty:'1 Kg' },
		{ id: 'Pm_0058xmkz', name: 'Persian',price:710,rate:710,qty:'1 Kg' },
	];
    let categories = [
		{ id: 'J---aiyznGQ', name: 'Dryfruits' },
		{ id: 'z_AbfPXTKms', name: 'Fruits' },
		{ id: 'OUtn3pvWmpg', name: 'Vegetables' },
		{ id: 'Pm_0058xmkz', name: 'Meals' },
	];
	let itemsbycat = [
		{ id: 'J---aiyznGQ', name: 'Badam',price:750,rate:750,qty:'1 Kg' },
		{ id: 'J---aiyznGQ', name: 'Kaju',price:875,rate:875,qty:'1 Kg' },
		{ id: 'J---aiyznGQ', name: 'Pista',price:1250,rate:1250,qty:'1 Kg' },
		{ id: 'J---aiyznGQ', name: 'Walnut',price:1500,rate:1500,qty:'1 Kg' },
		{ id: 'J---aiyznGQ', name: 'Anjeer',price:1400,rate:1400,qty:'1 Kg' },
	];
let productImageName = "";
let itemCategory = "Dryfruits";
let cartProducts = [];
let showPic = false;
let showallItemsbycat = true;
let showItems = false;
let showPhotos = false;
let showCategories = false;
let showCart = false;
let allitemsbycat = [];
let i=0;
let carttotalprice=0;
while (i<categories.length)
{
    let itemsbycat = [];
    let j=0;
    while (j<items.length)
    {
        if (items[j]["id"] == categories[i]["id"])
        {
            itemsbycat.push ({ id: items[j]["id"], name: items[j]["name"],price:items[j]["price"],rate:items[j]["rate"],qty:items[j]["qty"] });
        }
        j++;
    }
    allitemsbycat.push ({id: categories[i]["id"],idname: categories[i]["name"], val: itemsbycat})
    i++;
}

var removeByAttr = function(arr, attr, value){
    var i = arr.length;
    while(i--){
       if( arr[i] 
           && arr[i].hasOwnProperty(attr) 
           && (arguments.length > 2 && arr[i][attr] === value ) ){ 
           arr.splice(i,1);

       }
    }
    carttotalprice = getcarttotalprice();
    return arr;
}
function handleallItemsbycatClick() {
        showallItemsbycat = true;
		showItems = false;
		showPhotos = false;
		showCategories = false;
		showCart = false;
		showPic = false;
		allitemsbycat = [];
        var i=0;
        while (i<categories.length)
        {
            itemsbycat = [];
            var j=0;
            while (j<items.length)
            {
                if (items[j]["id"] == categories[i]["id"])
                {
                    itemsbycat.push ({ id: items[j]["id"], name: items[j]["name"],price:items[j]["price"],rate:items[j]["rate"],qty:items[j]["qty"] });
                }
                j++;
            }
            allitemsbycat.push ({id: categories[i]["id"],idname: categories[i]["name"], val: itemsbycat})
            i++;
        }
	}
	function handleItemsClick1() {
        showallItemsbycat = false;
		showItems = true;
		showPhotos = false;
		showCategories = false;
		showCart = false;
		showPic = false;
		itemsbycat = [];
		var i=0;
        while (i<items.length)
        {
            if (items[i]["id"] == 'J---aiyznGQ')
            {
                itemsbycat.push ({ id: items[i]["id"], name: items[i]["name"],price:items[i]["price"],rate:items[i]["rate"],qty:items[i]["qty"] });
            }
            i++;
		}
		itemCategory = "Dryfruits";
	}
function handleItemsClick(id) {
        showallItemsbycat = false;
		showItems = true;
		showPhotos = false;
		showCategories = false;
		showCart = false;
		showPic = false;
		itemsbycat = [];
		var i=0;
        while (i<items.length)
        {
            if (items[i]["id"] == id)
            {
                itemsbycat.push ({ id: items[i]["id"], name: items[i]["name"],price:items[i]["price"],rate:items[i]["rate"],qty:items[i]["qty"] });
            }
            i++;
		}
		i=0;
		while (i<categories.length)
		{
		    if (categories[i]["id"] == id)
		    {
		         itemCategory = categories[i]["name"];
		    }
		    i++;
		}
	}
function handlePhotosClick() {
        showallItemsbycat = false;
		showItems = false;
		showPhotos = true;
		showCategories = false;
		showCart = false;
		showPic = false;
	}
function handleCategoriesClick() {
        showallItemsbycat = false;
		showItems = false;
		showPhotos = false;
		showCategories = true;
		showCart = false;
		showPic = false;
	}
function handleCartClick() {
        showallItemsbycat = false;
		showItems = false;
		showPhotos = false;
		showCategories = false;
		showCart = true;
		console.log (cartProducts);
		showPic = false;
	}	
function handleShowPicClick (name)
{
    showallItemsbycat = false;
	showItems = false;
	showPic = true;
	productImageName = name.toLowerCase ();
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
function getcarttotalprice() {
    var i = cartProducts.length;
    var totprice = 0;
    var prodlineitems = [];
    while(i--){
        prodlineitems = cartProducts[i]["prodlineitems"];
        var j = prodlineitems.length;
        while (j--) {
            totprice = totprice + prodlineitems[j]["itemprice"];
        }
    }
    return totprice;
}

function addToCart (name,weight,oper){
	console.log ("weight is ");
	console.log (weight);
	var i = cartProducts.length;
	var productFound = false;
	var prodlineitems = [];
	var newitemprice = getPerKgPrice (name);
	while(i--){
       if(cartProducts[i]["name"] === name ){ 
		prodlineitems = cartProducts[i]["prodlineitems"];
		var j = prodlineitems.length;
		var weightFound = false;
		while (j--){
            if (prodlineitems[j]["weight"] == weight) {
                weightFound = true;
                if(oper == 1) {
                    prodlineitems[j]["qty"] += 1;
                }
                else {
                    if(prodlineitems[j]["qty"] > 1)
                        prodlineitems[j]["qty"] -= 1;
                }
                prodlineitems[j]["itemprice"] = getTotalPrice (name,[{weight:weight,qty:prodlineitems[j]["qty"]}]);
            }
		}
		if (!weightFound) {
		    prodlineitems.push ({weight:weight,qty:1,itemprice:newitemprice});
		}
		console.log (prodlineitems);
		if(oper == 1) {
		    cartProducts[i]["qty"] += 1;
		}
		else {
            if(cartProducts[i]["qty"] > 1)
                cartProducts[i]["qty"] -= 1;
        }
		cartProducts[i]["prodlineitems"] = prodlineitems;
		productFound = true;
		break;
	   }
	}
	if (!productFound){
	prodlineitems.push ({weight:weight,qty:1,itemprice:newitemprice});
	cartProducts.push ({name: name,qty:1,prodlineitems:prodlineitems,price:newitemprice});
	console.log (cartProducts);
	console.log (cartProducts[0]["prodlineitems"]);
    }
    carttotalprice = getcarttotalprice();
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
	width:11%;
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
.catheader{
	color:#777;
	padding:5px;
	font-size: 16px;
	font-weight: bold;
}
.productimage{
	width:540px;
	
}
hr{
	clear: both;
}
ul{
	list-style-type: none;
	padding:0px;
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
	display:block;
	float:left;
	width:10%;
	/* border:2px solid red; */
}
.left10px{
	margin-left: 10px;	
}
.productname{
	width:11%;
	/*border:1px solid red;*/
	display:block;
	float:left;
	/* border:1px solid red; */
	cursor:pointer;
}
.productcontainer{
	/* padding: 10px; */
	padding-top: 10px;
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
<button on:click={handleallItemsbycatClick} id = "menubutton" class = "selectcategory">
ItemsByCategory
</button>
<button on:click={handleItemsClick1} id = "menubutton" class = "selectcategory">
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
<div id="cathdr" class = "catheader"><bold>Category:</bold> {itemCategory}</div>
<hr/>
{/if}
{#if showPic}
<img class = "productimage" alt = "Enerjio - {productImageName}"src = "{productImageName}.jpg" />
{/if}

{#if showallItemsbycat}
<table border="1" bordercolor="#777" width="500">
{#each allitemsbycat as { id, idname, val }, j}
<tr><td colspan="2"><b><span class = "productname">{idname}</span></b></td><td colspan="8"><button on:click={()=>handleItemsClick(id)} class = "left10 selectcategorybutton">Select</button></td></tr>
<tr>
{#each val as { id, name,price,qty }, i}
<td>{name}</td>
{/each}
</tr>
{/each}
</table>
{/if}
{#if showItems}
<div id = "productmenu" class = "maincontainer">	
<ul>
{#each itemsbycat as { id, name,price,qty }, i}
<li>
<span on:click={()=>handleShowPicClick(name)} class = "productname">
{name}
</span>
<span class = "width20">
	&#8377;&nbsp;{price}
	</span>
<button on:click={()=>changeQuantity(qty,i)} class = "width15">
{qty} &#9660;
</button>
<button on:click={()=>addToCart(name,qty,1)}  class = "left10px">
+
</button>
<button on:click={()=>addToCart(name,qty,0)}  class = "left10px">
-
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
<button on:click={()=>handleItemsClick(id)} class = "left10 selectcategorybutton">
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
	<li class = "productcontainer">
		<span class = "productname">Name</span>
		<ul class = "lineitemscontainer">
		    <li class = "col2">Weight*Qty</li>
		</ul>
		<span class = "width15">TotalWeight</span>
		<span class = "width15">Price</span>
		<span class = "width15">Subtotal</span>
		</li>
{#each cartProducts as {name,prodlineitems,price},i}
    <li class = "productcontainer">
		<span class = "productname">
			{name}
		</span>
		<ul class = "lineitemscontainer">
		{#each prodlineitems as {weight,qty},j}
		<li class = "col2">{weight} * {qty}</li>
		{/each}
		</ul>
		<span class = "width15">
			{getTotalWeight (prodlineitems)} &nbsp;Kg
		</span>
		<span class = "width15">
			&#8377; {price}
		</span>
		<span class = "width15">
			&#8377; {getTotalPrice (name,prodlineitems)}
		</span>
		<button class = "" on:click={()=>removeFromCart(name)}>
			Remove
			</button>
		</li>
		{/each}
		 <li class = "productcontainer">
		<span class = "productname">&nbsp;</span>
		<ul class = "lineitemscontainer">
		    <li class = "col2">&nbsp;</li>
		</ul>
		<span class = "width15">&nbsp;</span>
		<span class = "width15">Total Price = </span>
		<span class = "width15">&#8377; {carttotalprice}</span>
		</li>
</ul>
</div>	
{/if}
</body>
