<script>
let shopNo="",productImageName = "",itemCategory = "Fruits",shopName="New Open Mart",shopCat="1",sid="",sname="",oname="Sachin Prabhu",omob="9833163255",oaddr="336-356 Shree Bunglow RSC37 Gorai2 Pragati Borivali West",shopmob="9833163255",s1="",s2="",s3="",s4="";
let cartProducts = [],allitemsbycat = [],categoriesbyshop=[],items = [],categories = [],itemsbycat = [],shpnm = [];
let showShops=true,showOrder=false,showallItemsbycat=false,showItems=false,showCategories=false,showCart=false,ordena=true;
let i=0,carttotalprice=0;
var removeByAttr = function(arr, attr, value){
    var i = arr.length;
    while(i--){
       if(arr[i] && arr[i].hasOwnProperty(attr) && (arguments.length > 2 && arr[i][attr] === value ) ) 
           arr.splice(i,1);       
    }
    carttotalprice = getcarttotalprice();
    return arr;
}
async function getitemsfromserver() {    
  const res = await fetch("https://enerjiyo.pythonanywhere.com/getItemInfo")
  .then(response => response.json())
  .then(data => {
	items=data.entries;
	categories=data.entries1;
	shpnm=data.entries2;
	var i=0;
	while (i<categories.length) {
		if(categories[i]["cat"]==shopCat) {  
			categoriesbyshop.push ({id: categories[i]["id"],name: categories[i]["name"] , cat: categories[i]["cat"]})
			allitemsbycat.push ({id: categories[i]["id"],idname: categories[i]["name"], val: getitemsbyid(categories[i]["id"])})
		}
		i++;
	}
	sid=categoriesbyshop[0]["id"];
	sname=categoriesbyshop[0]["name"];		    
	s1=shpnm[0]["shopname"];
	s2=shpnm[1]["shopname"];
	s3=shpnm[2]["shopname"];
	s4=shpnm[3]["shopname"];
  }).catch(error => {
	console.log(error);
	return [];
  });	
}
function getitemsbyid(idcat) {    
	let sitemsbycat = [];
	let bFlag = false;
	var i=0;
	while (i<items.length) 	{
		if (items[i]["id"] == idcat) {
			bFlag = false;
		    if(items[i]["qty"]=="1 Pcs")
				bFlag = true;
			sitemsbycat.push ({id: items[i]["id"], name: items[i]["name"],price:items[i]["price"],rate:items[i]["rate"],qty:items[i]["qty"],qtype:bFlag});
		}
		i++;
	}
	return sitemsbycat;
}
function handleallItemsbycatClick() {
	disableTabSel();
	showallItemsbycat = true;
	allitemsbycat = [];
	var i=0;
	while (i<categories.length) {
		if(categories[i]["cat"]==shopCat)  
			allitemsbycat.push ({id: categories[i]["id"],idname: categories[i]["name"], val: getitemsbyid(categories[i]["id"])})
		i++;
	}
}
function handleItemsClick1() {
	handleItemsClick(sid,sname);
}
async function handleOrderItemsClick() {
	var x1=document.forms["orderform"]["pname"].value;
	var x2=document.forms["orderform"]["pmob"].value;
	var x3=document.forms["orderform"]["paddr"].value;
	if ((x1 == "")) 
		document.getElementById("ordmsg").innerHTML = "Enter name";
	else if ((x2 == ""))
		document.getElementById("ordmsg").innerHTML = "Enter mobile";
	else if ((x3 == ""))
		document.getElementById("ordmsg").innerHTML = "Enter address";
	else {
		document.getElementById("ordmsg").innerHTML = "";
		var dt = new Date().toLocaleDateString();
		var ordstr = "https://wa.me/91"+shopmob+"?text=Date:%20"+dt+"%0aName:%20"+x1.replaceAll(' ','%20')+"%0aMobile:%20"+x2.replaceAll(' ','%20')+"%0aAddress:%20"+x3.replaceAll(' ','%20')+"%0aItems:%0a";
		var i = cartProducts.length;
		var itmstr = "", strqty = "";
		while(i--) {
			ordstr = ordstr+cartProducts[i]["name"].replaceAll(' ','%20')+"%20"+getTotalWeight (cartProducts[i]["prodlineitems"])+"%20Kg%0a";
			itmstr = itmstr+cartProducts[i]["name"]+"|";
			strqty = strqty+getTotalWeight (cartProducts[i]["prodlineitems"])+" Kg|";
		}
		var win = window.open(ordstr,'_blank');		
		const res = await fetch('https://enerjiyo.pythonanywhere.com/addOrdInfo', {
			method: 'POST',
			headers: {
				'Accept': 'application/json',
				'Content-Type': 'application/json'
			  },
			body: JSON.stringify({"dt":dt,"name":x1,"mob":x2,"addr":x3,"item":itmstr,"qty":strqty,"shopNo":shopNo})
		});					
	}
}
function handleItemsClick(id,nm) {
	disableTabSel();
	showItems = true;
	itemsbycat = getitemsbyid(id);
	itemCategory = nm;		
}
function handleShopCat(itemcat) {
    if(shopNo != itemcat) {
	    cartProducts=[];
		carttotalprice=0;
		ordena=true;
	}
	shopNo=itemcat;
    if(itemcat=='1') {
		shopName=shpnm[0]["shopname"];
		shopmob=shpnm[0]["smob"];
	}
	else if(itemcat=='2') {
		shopName=shpnm[1]["shopname"];
		shopmob=shpnm[1]["smob"];
	}
	else if(itemcat=='3') {		
		shopName=shpnm[2]["shopname"];
		shopmob=shpnm[2]["smob"];
	}
	else if(itemcat=='4') {
		shopName=shpnm[3]["shopname"];	
		shopmob=shpnm[3]["smob"];
	}
	shopCat=itemcat;
	handleCategoriesClick();
	handleItemsClick1();
}
function handleClearOrderClick() {
	oname=omob=oaddr="";	
}
function handleCategoriesClick() {
	disableTabSel();
	showCategories = true;		
	let i=0;
	categoriesbyshop=[];
	while (i<categories.length) {
		if(categories[i]["cat"]==shopCat)   
			categoriesbyshop.push ({id: categories[i]["id"],name: categories[i]["name"] , cat: categories[i]["cat"]})
		i++;
	}
	sid=categoriesbyshop[0]["id"];
	sname=categoriesbyshop[0]["name"];
}
function disableTabSel() {
	showallItemsbycat = false;
	showItems = false;
	showCategories = false;
	showCart = false;
	showShops = false;
	showOrder = false;
}	
function handleCartClick() {
	disableTabSel();
	showCart = true;		
}
function handleallShopsClick() {
	disableTabSel();
	showShops = true;		
}	
function handleOrderClick() {
	disableTabSel();
	showOrder = true;			
}	
function changeQuantity (qty,i) {
	if (qty == '1 Kg') 	{
		itemsbycat[i]["qty"] = '1 Kg';
		itemsbycat[i]["price"] = items[i]["price"];
	}
	if (qty == '250 gm') {  
		itemsbycat[i]["qty"] = '250 gm';
		itemsbycat[i]["price"] = items[i]["price"] / 4;
	}
	if (qty == '500 gm') {
		itemsbycat[i]["qty"] = '500 gm';
		itemsbycat[i]["price"] = items[i]["price"] / 2;
	}	
}	
function getPerKgPrice (name) {
	var i = items.length;
	while (i--) {
		if (items[i]["name"] == name) 
			return items[i]["rate"];		
	}
	return 0.00;
}
function getTotalPrice (name,prodlineitems) {
	return (getTotalWeight (prodlineitems) * getPerKgPrice (name)) ;
}
function getTotalWeight (prodlineitems) {
	var j = prodlineitems.length;
	var weight = 0,totalWeight = 0;
	while (j--) {
		if (prodlineitems[j]["weight"].includes("gm")) 
			weight += parseInt(prodlineitems[j]["weight"].split(" ")[0]) * parseInt(prodlineitems[j]["qty"]);
		if (prodlineitems[j]["weight"].includes("Kg")) 
			weight += parseInt(prodlineitems[j]["weight"].split(" ")[0]) * parseInt(prodlineitems[j]["qty"]) * 1000;	
	}
	return (weight / 1000);
}
function getcarttotalprice() {
    var i = cartProducts.length;
    var totprice = 0;
    var prodlineitems = [];
    while(i--){
        prodlineitems = cartProducts[i]["prodlineitems"];
        var j = prodlineitems.length;
        while (j--)
			totprice = totprice + (getTotalWeight (cartProducts[i]["prodlineitems"]) * getPerKgPrice (cartProducts[i]["name"]));
    }
	ordena=true;
    if (cartProducts.length	> 0)
	    ordena=false;
    return totprice;
}
function addToCart (name,weight,oper) {
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
                if(oper == 1) 
                    prodlineitems[j]["qty"] += 1;                
                else {
                    if(prodlineitems[j]["qty"] > 1)
                        prodlineitems[j]["qty"] -= 1;
                }
                prodlineitems[j]["itemprice"] = getTotalPrice (name,[{weight:weight,qty:prodlineitems[j]["qty"]}]);
            }
		}
		if (!weightFound) 
		    prodlineitems.push ({weight:weight,qty:1,itemprice:newitemprice});
		if(oper == 1) 
		    cartProducts[i]["qty"] += 1;
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
}
button{
	padding:10px;
	background-color: #c2c2c2;
	border:1px solid #777;
	font-size: 16px;
	font-weight: bold;
}
.lineitemscontainer{
	float:left;
	width:11%;
}
.logo{
	color:#00d500;
	float:left;	
}
.headline{
	color:#777;
	margin-left: 60px;
	margin-top: 32px;
	float:left;
}
.catheader{
	color:#777;
	padding:5px;
	font-size: 16px;
	font-weight: bold;
}
.prodtitle{
	color:#777;
	padding:5px;
	font-size: 16px;	
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
	width: 15%;
	display:block;
	float:left;
}
.width15{
	display:block;
	float:left;
	width:10%;
}	
.left10px{
	margin-left: 10px;	
	display:block;
	float:left;
	width:5%;
}
.left101px{
	margin-left: 10px;	
	width:5%;
}
.productname{
	width:25%;
	display:block;
	float:left;
	cursor:pointer;
}
.productcontainer{
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
<svelte:window on:load={getitemsfromserver}/>
<body>
<table width="425"><tr><td><h1 class = "logo">	Enerjio</h1></td>
<td><h2 class = "headline">Buy Quality Dryfruits</h2></td></tr></table>		
<hr/>
<table width="560">
<tr><td width="80">	
<button on:click={handleallShopsClick} id = "menubutton" class = "selectcategory">Shops</button>
</td><td width="80">	
<button on:click={handleallItemsbycatClick} id = "menubutton" class = "selectcategory">ItemsByCategory</button>
</td><td width="80">	
<button on:click={handleItemsClick1} id = "menubutton" class = "selectcategory">Items</button>
</td><td width="80">	
<button on:click={handleCategoriesClick} id = "categorybutton" class = "selectcategory">Category</button>
</td><td width="80">	
<button on:click={handleCartClick} id = "categorybutton" class = "selectcategory">	Cart</button>
</td><td width="80">	
<button on:click={handleOrderClick} id = "orderbutton" disabled='{ordena}' class = "selectcategory">Order</button>
</td></tr></table>	
<hr/>
{#if showItems}
<div id="cathdr" class = "catheader"><bold>Category:</bold> {itemCategory}</div>
<hr/>
{/if}
{#if showShops}
<table width="500">
<tr><td width="250">	
<button on:click={()=>handleShopCat('1')} id = "menubutton" class = "selectcategory">{s1}</button>
</td><td width="250">	
<button on:click={()=>handleShopCat('2')} id = "menubutton" class = "selectcategory">{s2}</button>
</td></tr>
<tr><td width="250">	
<button on:click={()=>handleShopCat('3')} id = "menubutton" class = "selectcategory">{s3}</button>
</td><td width="250">	
<button on:click={()=>handleShopCat('4')} id = "menubutton" class = "selectcategory">{s4}</button>
</td></tr>
<tr><td colspan="2" align="center"><div id="shopname" class = "prodtitle">{shopName}</div></td></tr>
</table>
{/if}
{#if showallItemsbycat}
<table border="solid 1px #777" style="background: #777;" width="500">
{#each allitemsbycat as { id, idname, val }, j}
<tr><td colspan="2" style="background: #fff;"><b><div class = "prodtitle">{idname}</div></b></td><td colspan="8" style="background: #fff;"><button on:click={()=>handleItemsClick(id,idname)} class = "left10 selectcategorybutton">Select</button></td></tr>
<tr>
{#each val as { id, name,price,qty }, i}
 	<td style="background: #fff;"><div id="prodhdr" class = "prodtitle">{name}</div></td>
{/each}
</tr>
{/each}
</table>
{/if}
{#if showItems}
<table border="0" width="600">	
{#each itemsbycat as { id, name,price,qty,qtype }, i}
<tr><td><span class = "productname"><b><div id="prodhdr" class = "prodtitle">{name}</div></b></span></td>
<td><div class = "width20 prodtitle">&#8377;&nbsp;{price}</div></td>
<td width="90"><button disabled='{qtype}' on:click={()=>changeQuantity("250 gm",i)}>250 gm </button></td>
<td width="90"><button disabled='{qtype}' on:click={()=>changeQuantity("500 gm",i)}>500 gm </button></td>	
<td width="90"><button disabled='{qtype}' on:click={()=>changeQuantity("1 Kg",i)}>1 Kg </button></td>
<td><button on:click={()=>addToCart(name,qty,1)}>+</button></td>
<td><button on:click={()=>addToCart(name,qty,0)}>-</button></td>
<td width="80"><b><div class = "prodtitle">{qty}</div></b></td></tr>
{/each}
</table>
{/if}
{#if showCategories}
<div id = "categorylist" class = "maincontainer">
<ul>
{#each categoriesbyshop as { id, name }, i}
<li><span class = "productname prodtitle">{name}</span><button on:click={()=>handleItemsClick(id,name)} class = "left10 selectcategorybutton">Select</button></li>	
{/each}
</ul>	
</div>	
{/if}
{#if showCart}
<table border="0" width="600">
	<tr><td><b><div class = "prodtitle">Name</div></b></td><td><b><div class = "prodtitle">Weight*Qty</div></b></td><td><b><div class = "prodtitle">TotalWeight</div></b></td><td><b><div class = "prodtitle">Price</div></b></td><td><b><div class = "prodtitle">Subtotal</div></b></td></tr>
{#each cartProducts as {name,prodlineitems,price},i}
	<tr><td><b><div class = "prodtitle">{name}</div></b></td><td><div class = "prodtitle">{#each prodlineitems as {weight,qty},j}{weight} * {qty}{/each}</div></td><td><div class = "prodtitle">{getTotalWeight (prodlineitems)} &nbsp;Kg</div></td><td><div class = "prodtitle">&#8377; {price}</div></td>
		<td><div class = "prodtitle">&#8377; {getTotalPrice (name,prodlineitems)}</div></td><td><button class = "" on:click={()=>removeFromCart(name)}>Remove</button></td></tr>
{/each}
   <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td><b><div class = "prodtitle">Total Price</div></b></td><td><div class = "prodtitle">&#8377; <b>{carttotalprice}</b></div></td></tr>		
</table>	
{/if}
{#if showOrder}
<form name="orderform">
<table width="500">
<tr><td><div class = "prodtitle">Name</div></td><td><input type="text" id="pname" name="pname" value="{oname}"></td></tr>
<tr><td><div class = "prodtitle">Mobile</div></td><td><input type="text" id="pmob" name="pmob" value="{omob}"></td></tr>
<tr><td><div class = "prodtitle">Address</div></td><td><input type="text" id="paddr" name="paddr" value="{oaddr}" style="width: 480px;"></td></tr>
<tr><td align="center"><button on:click={()=>handleOrderItemsClick()} id = "ordbutton" class = "selectcategory">Order</button>
</td><td align="center"><button on:click={()=>handleClearOrderClick()} id = "clrbutton" class = "selectcategory">Reset</button></td></tr>	
<tr><td colspan="2" align="center"><b><div id="ordmsg" class = "prodtitle"></div></b></td></tr>	
</table>
</form>
{/if}
</body>
