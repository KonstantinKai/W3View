# Compo.JS
Extremely light, fast and easy to understand tool, that 
provides painless Custom Elements technology.

14 kB of documented, not minified code.

## What Compo.JS does ?
Compo.JS generates DOM nodes from HTML based declarative definitions.

+ DOM nodes, generated by Compo.JS is still DOM nodes with lifecicle
methods mixed in, they also can contain the table of inner references,
that is DOM nodes too. 
+ The definition of component is just HTML markup, 
plus optional lifecicle handlers in the embedded script. 
+ Definition of Como.JS component is not template - it is data structure. 

Each instance of Compo.JS contains its own namespace and independed 
set of components. 
Therefore the number of independent applications can be mounted on the page.
Also one Compo app can use the number of mounting points on the page, 
and it can run the number of Compo apps inside one Compo app. 
This is the real power of Javascript, of old good Javascript.

## What Compo.JS is ?
* **Small (really small!) and well documented browser script, 
contains one constructor**
* **HTML based definition of components**
* **Small set of additional attributes**
* **Natural, manageble DOM Nodes as component instances**
* **Natural DOM events**
* **Only five new methods to use**
* **Up to five methods to implement**
* **API and lifecicle oriented on reactive programming**

## What Compo.JS is not?
* **MAGIC CARPET**
* **SILVER BULLET**
* **NUMBER OF NEW CONCEPTIONS**
* **COFFEE MAKER**

## What is main Conception, the Compo.JS provides?
The main conception of Compo.JS is - NO NEW CONCEPTIONS and the 
second conception is - NO NEW WORDS.

## Where can You use the Compo.JS ?
You can use Compo.JS as View layer of any kind of MVC.
Compo.JS is ready to Flux, reactive programming, 
and event driven programming. All what You can do with HTML and Javascript,
You can do with Compo.JS components.

## What You need to start using Compo.JS ?
You need just compo.js file, text editor and browser.
Any browser, including IE6.

## What You need to know to start using Compo.JS ?
You need to know HTML and Javascript, old good Javascript.
You also need to know basics of DOM API.

## How to create UI components with Compo.JS ?
Component definition - is the markup of one sample HTMLElement.
Just write some HTML markup and embedded constructor script,
like this:

		//"hallo-world" definition
		<div as="hallo-world">
			<input ref="input" placeholder="type your name here">
			<h1>Hallo <span ref="name">Anonimous</span>!</h1>
			<script>
				this.ref.input.onkeyup = function(e){
					this.setData(this.ref.input.value);
				}.bind(this);
				this.onSetData = function(data){
					this.ref.name.innerText = data || 'Anonimous';
				};
			</script>
		</div>
		//Here:
		//"this" - is the reference to DIV, that is instance of "hallo-world".
		//attribute "ref" - is some one like *id*, inside the component.
		//"this.ref" - is the table of references to corresponded elements.

Looks like web page, when web was young, is not it? 
Yes, but it is **reusable component**.
It can be used as simple application,
and it can be used as part of more complex app inside another component, 
for example:

		<div as="double-hallo-world">
			<hallo-world></hallo-world>
			<hr>
			<hallo-world></hallo-world>
		</div>

Okay, lets combine these examples, make complete HTML page and 
run "double-hallo-world" app:

	<!DOCTYPE html>
	<html>
		<head>
			<meta http-equiv="content-type" content="text/html;charset=utf-8">
			<title>Double Hallo</title>
		<head>
		<script src="compo.js"></script>
		<script type="text/compo" id="components">
			
			//any text can be placed between components definitions,
			//except HTML markup.
			
			//hallo-world component
			<div as="hallo-world">
				<h1 ref="content"></h1>
				<input ref="input" placeholder="type your name here">
				<h2>Hallo <span ref="name">Anonimous</span>!</h2>
				<constructor>
					//CONSTRUCTOR tag should be used inside SCRIPT tag
					this.ref.input.onkeyup = function(e){
						this.setData(this.ref.input.value);
					}.bind(this);
					this.onSetData = function(data){
						this.ref.name.innerText = data || 'Anonimous';
					};
				</constructor>
			</div>
			
			//root of app 
			<div as="double-hallo-world">
				<hallo-world>Hallo first</hallo-world>
				<hr>
				<hallo-world>Hallo second</hallo-world>
			</div>

		</script>

		<body style="margin:50px;">
			<script defer="defer">
				var compo = new Compo();
				compo.parse(components.textContent);
				compo.create('double-hallo-world').mount(document.body);
			</script>
		</body>
	</html>

You can find this example in ./examples folder of this repo.

More examples and descriptions You can find in 
the ./howto.md, detailed API - in the api-doc.md
