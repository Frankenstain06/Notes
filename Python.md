
### FUNCTION
>1. `type(name)` -> Output the data type of the variable.
>2. `len(str)` -> Output the length of a string.
>3. `input()` -> This function takes input.
>4. `str.endswith("er")` -> This method checks if a string ends with 'er' or not. If yes then output is true and if not then then the output is false.
>5. `str.capitalize()` -> This method capitalize the first character of a string.
>6. `str.replace('old_value' , 'new_value')` -> This method replace the old value with a new value in a string.
>7. `str.find(word)` -> This method find a word in a string and gives the first index of that word in a string as output.
>8. `str.count()` -> This method count the string. If you write `str.count[o]` it will count the number of 'o' in the string.


## Common knowledge
>1. `#` -> This symbol is the comment in python.
>2. `**` -> This symbol is the power operator in python.
>3. `and` = `&&` , `not` = `!` , `or` = `||` -> python = `c++` comparison.
>4. `int("Refat")` -> This is type cast. There is a risk of data loss.
>5. `"hello" + "world"` => `"helloworld"` -> here, the + sign concatenate strings in python.
>6. `int(input(Enter Input: ))` -> input function always output in string. That is why we              typecast it into a desirable datatype. We can also print string when using input method.
>7. `str[2:4]` -> This means it will access index from 2 to 4 from the string index. For example : `hello` will give `llo`. Negative indexing is also possible in python `str[-5`: -2]`. This is called string slicing.
>8. `List = [10, 20, 30]` -> This is list in python. It is kind of array and it has also index. List is same as string but there is a big difference. String can't be changed through indexing but list can be changed. For example: `str = "hello"` then `str[3] = 'z'` but it will an error because we can not change the value of string through indexing but we can change the value of list through indexing.
>9. `Tuple = (10, 20, 30)` -> This is kind of list but the difference is we can not change the    value of tuple just like string. We can have empty tuple like `tup = ()` and it will output `()` this. If we want to add only single value in a tuple then we need add a comma after it otherwise they will not count the datatype as tuple. For example: `tup = (10,)`.
>   
>10. In python, there are something called dictionary. In the dictionary, there are keys and every key has values.
>    
```python
>    dict = {
> 	   "name" : "Fahim",
> 	   "age"  : 35,
> 	   "relationship"  : {
> 		   "FN" : "Rownak",
> 		   "MN" : "Fatema", #nested dictionary
> 		}
> 		"subjects" : ["phy", "che", "math"]
>    }
>    ```
> The way we access the value from dictionary is, `dict["relationship"]["FN"]`. We can also change the value of dictionary key. `dict["name"] = "Refat"` 

>11. `Set = {1, 2, 3, "word", "day"}` -> This is set. We can add items from different data type in this collection. Set is unchangeable like Tuple. We can not add duplicate value in the set because set will auto ignore the duplicate value. In set, there is no indexing unlike array. If we print the set then every time it will give different order.
>12. 
>    
``` python
fruits = ["apple", "banana", "cherry"]  #For loop
for x in fruits:  
  print(x)
  ```