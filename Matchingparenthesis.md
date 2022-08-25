# Check if given Parentheses expression is balanced or not

Given a string str of length N, consisting of ‘(‘ and ‘)‘ only, the task is to check whether it is balanced or not.

```php

function pairedBrackets($strBrackets){
	$aBrackets = str_split($strBrackets);
	$counter = 0;
	$validCharacters = ['(', ')'];
	foreach($aBrackets as $character){
		if(!in_array($character, $validCharacters)){
			return 0;
		}
		if($character == '('){
			$counter++;		
		}
		if($character == ')'){
			$counter--;		
		}
		if($counter<0){
			return 0;
		}
	}
	if(!$counter){
		return 1;
	}
	return 0;
}

```
