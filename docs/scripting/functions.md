## Why would a function be useful?

A function is mainly a chunk of code that either is used for multiple actions of the same item, or a simple way to check
the status of something. This eliminates lots of code from the main script and makes it a bit cleaner for you to see and
debug.

## Creating a Function

In order to create a function, you can do one of many things. Many scripters place their functions in 1 of 2 locations.
I, myself, place my functions in a functions.txt script file and load that independently. By doing this, you can
organize your functions and keep all your other scripts clean and free of clutter. Another method is to simply place
them inside the script itself, however, I find this to lengthen the script quite a bit, and makes it complicated to find
where the function is located in case another script file is calling it.

    function(TAB)script(TAB)name(TAB){
    	//  code
    }

## The RETURN Command

Sometimes it's necessary to send back information that you retrieved from your function. Such as a TRUE/FALSE 0/1
response, or sometimes even more. In order to do this, your function needs a return statement.

    return <Value>;
    return <Variable>;

## Calling a Function

There are a few ways to call functions, depends on what information you are retrieving.

    callfunc "MyFunction";

// Simply calls the function that does not use a RETURN command

### Using Arguments in a Function

Sometimes it's helpful to pass variables or values to a function in order to retrieve the information that you would
like. These values are called arguments. Many people use these in order to make calculations.

#### The Function

    function(TAB)script(TAB)calc(TAB){
    	set @a, getarg(0) + getarg(1);
    	return @a;
    }

#### Calling the Function

    set @a, callfunc("calc",1,2)
    mes @a;

#### The Result/Return

    3

#### Passing Arrays as Arguments

Calling the Function:

    callfunc "calc", MyArrayName;

The Function:

    function(TAB)script(TAB)calc(TAB){
      getelementofarray(getarg(0), 1);
    }

- Please note, that npc variable arrays will not function in the same manner (this will be updated at a later date)

#### Calling Function as a Script Command

    prontera,150,150,5<TAB>script<TAB>Calculator<TAB>999,{

        function<TAB>Add<TAB>{
            return (getarg(0)+getarg(1));
        }

        mes Add(1,2);
    }

### Special Notes

Variables are passed to functions by reference

This means that you can do normal variable operations on a variable reference returned by getarg.

Ex:

    function<tab>script<tab>F_Increment<tab>-1,{
        // getarg(0) returns a reference to the .@num variable in NPC_Test
        // NOTE: you can't use .@num directly, it's a different variable from the .@num in NPC_Test
        set getarg(0), getarg(0) + 1;
        return;
    }

    prontera,156,156,4<tab>script<tab>NPC_Test<tab>56,{
        // initial number
        set .@num, 123;
        mes .@num;
        
        // increment inside the function
        callfunc("F_Increment", .@num);
        mes .@num;
        
        close;
    }

Operators always return values, so this would provoke an error on the set inside F_Increment:

    callfunc("F_Increment", .@num + 1);

It's important to note the difference between the reference of the variable and the value of the variable:

- *reference* : the variable itself. It knows it's name, value and index. The type of variable is determined from the
  name.
- *value*: the value of the variable (string or number).
