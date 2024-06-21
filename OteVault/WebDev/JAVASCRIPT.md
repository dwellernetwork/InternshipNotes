### Javascript useful commands.

If you want a prompt for the user to input something into, do
x = prompt("my prompt's text and guides for the user")

If you want a way to "default" values in javascript, there's the ?? operator.
Assume this:

	x = null
	alert ( x ?? "my default text)
	This will throw a pop up with "my default text" since x is Null;. 
	This is called a "Nullish coalescing operator"
	
	x=5
	y = null
	alert(x ?? y)
	This will return 5. 

The operator has low precedence. Use parenthesis when applying.

Three ways to write the same function:
function checkAge(age) {	      
  if (age > 18) {
	
	return true;

} else {

	return confirm('Did parents allow you?');

}
}

function checkMaAge(age) {

	return (age > 18 ) ? true : confirm('Did parents allow you?');

}

function checkMyNut(age) {

	return (age >18) || confirm("Did your parents allow you?");

}

### Javascript shenanigans and intricacies.

Inputting an empty input in a prompt returns an empty string " "
Pressing Esc during a prompt returns Null.

If we do (alert || 3 && 5 || 2), what will be returned? 
	The answer is 5. the & operator takes precedence, and returns the first truthy value after. 
	Even if there was no OR operators with other values, 5 would take precedence yet again.

If we do (alert(1) || 2 || alert(3)):
	First, we will get an alert with 1, and then an alert saying 2. 

If we do (alert(1) && alert(2))
	First, we will get an alert with 1, and then an undefined error because there is no actual value in alert(1)

If we do (alert(1) || alert(2))
	We get both alert(1) and alert(2) as prompts.


if (-1 || 0) alert( 'first' );}
	This will return -1.
	Why:
	-1 is a truthy value. 0 is a falsy value. Falsy values in Javascript are:
		False
		0
		Null
		Undefined
		Null
		"" //NOT " "!!!!!!!. A space between quotation marks is a character that IS TRUTHY

if (-1 && 0) alert( 'second' );
	This won't do anything
	Why:
	 0 is faulty. If just one value is faulty with the && operand, then byebye.

if (null || -1 && 1) alert( 'third' );
