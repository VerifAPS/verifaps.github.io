---
title: Library functions
---

# PCLOpenXML support




# AST and Parsing  

Parser and AST for StructuredText, Sequential Function Charts and Function Blocks.


* License: GPL v3
* Author
  * Alexander Weigl <weigl@kit.edu>
  * Contributions from @matheus23


# Sequential Function Chart Syntax

This is not a standard language.


## Example:

```
SFC example

    VAR_OUTPUT
        o : bool;
    END_VAR

    STEP A
        on active action
            o := true;
        end_action
    END_STEP

    STEP B
       on active action
            o := false;
       end_action
    END_STEP

    GOTO true :: A -> B
    GOTO true :: B -> A
END_SFC
```

## EBNF

```
<SFC>  :==  SFC <identifier>
                <elements>*
            END_SFC

<entry>   :== <var_decl> | <step_decl> | <transition>
<step_decl> :== STEP <identifier>
                  on <event> (action <statement>* end_action
                             | <function-identifier> )
                END_STEP
<transition> :== GOTO <guard> :: <identifier>* -> <identifier>*
```

`<event>` can be either `active`, `exit` or `entry`. `<statement>` refers to
valid Structured Text statements. `<var_decl>` responses to classical variable
declearation in IEC61131-3.

 
