# jsh

JSH - Write HTML in JavaScript

NOTE - this is just a quick draft. Implement this one day!

# Summary

JSH is to JSX what HTML is to XML.

JSH looks exactly the same as the generated HTML (or the HTML representation of the generated DOM elements) would look like, without discrepancies introduced by JSX.

## Void elements (elements with no closing tag) and optional closing tags

	function Component() {
 		return (
   			<>
	   			<p>This is a paragraph
		  		<p>Another one
		 		<form>
			 		<input name="username">
		 			<input type="submit">
		 		</form>
			</>
   		)
	}

## Proper HTML comments

In JSX you must comment out code with `{/* ... */}`. JSH allows regular `<!-- HTML comments -->`.

## More lenient syntax

	<textarea rows=6>        <!-- instead of rows={6} -->
 	<input type=submit>      <!-- instead of type="submit" -->
    
	<!-- Maybe we could also allow a shortcut for string interpolation -->
 	<h1 style=`color: ${headingColor}`>Users></h1>

## Identifiers are like in HTML

    <label for="name">Name:</label>         <!-- instead of htmlFor -->
	<p class="important"></p>               <!-- instead of className -->
	<button onclick={}>Click me</button>    <!-- instead of onClick -->

## Whitespace treated as in HTML (no need for {" "})

	function Heading() {
		return (
  			<>
				<span class="name">${firstName} ${lastName}</span>
		 		<Favorite value={favorited} />
		  	</>
	 	)
	}

Since this behavior is not always required, we should have a way to avoid it - maybe something like:

	<Component !nospace> <!-- ignore whitespace from this component --> 
 		<Title />
   		<UserDetails />
	 	<More />
   	</Component>
	<span>{name}</span> <Icon i={...}/> <!-- here whitespace counts again -->
 
## As a bonus, components could also accept an array instead of an object

	// @jsx h

	<!-- Object props, as supported by JSX -->
 	<Component x="one" y="two" /> <!-- h(Component, { x: "one", y: "two" }) -->
    <!-- Array props would be like this: -->
	<Vector 1 2 3 />              <!-- h(Vector, [1, 2, 3]) -->
 	<Wordlist "hello" "world" />  <!-- h(WordList, ["hello", "world"])

This might enable some patterns that would require a superfluous prop in JSX, such as: 

	<If {path == "/"}>
 		<Then>Then do this</Then>
   		<Else>Or else</Else>
	</If>
 	<!-- h(If, [path == "/"], h(Then, null, "Then do this"), h(Else, null, "or else")) -->
  
