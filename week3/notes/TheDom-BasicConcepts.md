### The Dom - Basic Concepts
Whitespace nodes are text nodes that contain characters you can't see such as spacing or line breaks

### Node Releationships
#### Example of how to determine nodePath in javascript
	function handleClick (event) {
		<!-- Make sure the event only happens once -->
		event.stopPropogation();

		var node = event.target;
		var thisPath = node.nodeName;

		while(node.parentNode) {
			node = node.parentNode;
			thisPath = node.nodeName + ' > ' + thisPath;
		}

		alert (thisPath);
	}

	<!-- Register the Click handler for all nodes -->
	function attachHandler(node) {
		if (node === null) {
			return;
		}

		node.onclick = handleClick;

		for (var i = 0; i < node.childNodes.length; ++i) {
			attachHandler(node.childNodes[i]);
		}
	}

### Locating Nodes
#### By Using Type
	getElementsByTagName()

Gets nodes by html tag. h2, h3, p, etc
Need to know the exact node, ex

	document.getElementsByName('h2')[0].style.color="yellow";

#### By Using Name
	getElementsById()

Gets nodes by searching for id of element

	document.getElementById("some_id").style.color="blue";

Alternate syntax
	
	var thisNode = document.getElementById("some_id");
		thisNode.setAttribute('color', 'blue');

### Creating and Adding Nodes to the DOM Structure
#### Creating Nodes
##### Creating Elements
	var newDiv = document.createElement('div');

##### Creating Text Nodes
	var newText = document.createTextNode("Hello world");

#### Adding Nodes to the DOM Structure
##### Insert Before
	var newDiv = document.createElement('div');
	var destinationParent = document.getElementsByTagName('body')[0];
		<!-- Insert element before the first child of the body element -->
		destinationParent.insertBefore(newItem, destination.firstChild);

#### Deleting a Node from the Dom Structure
##### Remove Child
	<!-- Three examples of the same thing -->
	var toBeDeleted = document.getElementById("firstParagraph");
		toBeDeleted.parentNode.removeChild(toBeDeleted);

	var toBeDeleted = document.getElementsByTagName("p")[0];
		toBeDeleted.parentNode.removeChild(toBeDeleted);

	var toBeDeletedParent = document.getElementById("theBody");
		toBeDeletedParent.removeChild(toBeDeletedParent.firstChild);

##### Remove All Children
	var theBody = document.getElementByid("theBody");
	<!-- While the first child exists -->
	while (theBody.firstChild) {
		theBody.removeChild(theBody.firstChild);
	}

#### Cloning Nodes
##### cloneNode

	function cloneLastChildInList () {
		var lastChild = document.getElementById("someList").lastChild;
		<!-- Won't actually clone it -->
		var lastChildClone = lastChild.cloneNode(); // Same as cloneNode(false); Won't clone a text child node, just the list item element
		var lastChildClone = lastChild.cloneNode(true); // Will clone the entire branch
		var theList = document.getElementById("someList");
			theList.appendChild(lastChildClone);
	}	
