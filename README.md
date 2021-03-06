# Context_Free_Grammars

### Context Free Grammars
[Context free grammars](https://en.wikipedia.org/wiki/Context-free_grammar) are a type of formal grammar. The production rules are of the form A -> α. Where A is a nonterminal character, and α is a string of terminal and or non-terminal characters. The grammar is defined by a tuple G = (V, Σ, R, S) in which V is a set of all nonterminal characters, Σ is a set of terminal characters, R describes the production rules of the grammar, and S is the start string. 

### The Parantheses Grammar
The following cfg generates well formed parentheses. Its production rules are:
```
S -> SS
S -> (S)
S -> ()
S -> ε
```

in which S is a non-terminal character.

A single run of the grammar, with the starting symbol "S" may generate any string in the set: {SS, (S), (), ε}. Multiple iterations can be executed, generating:
(((()))((((())())))), ()(()(()))()(()), (()), ()
All strings generated by the grammar are guranteed to be well-formed, meaning that no parantheses goes unclosed

#### The Grammar Object
The Grammar Object is comprised of a dictionary which stores the production rules for the grammar. 
To use the Grammar Object to simulate the Parantheses Grammar we can simply do:
```py
paran_productions = {
  'S' : ['SS', '(S)', '()', '']
}
G = Grammar(paran_productions)
```
To use the Grammar object to generate strings we specify the start string S, and the max number of iterations to allow for the generation:
```py
paran_productions = {
  'S' : ['SS', '(S)', '()', '']
}
G = Grammar(paran_productions)
generation = G.transform('S', 10)
```
### .grammar file format
The .grammar file format is a structured text based file format intended to encode the production rules of a context free grammar. The syntax is of the form:
```
non_terminal -> production_output
``` 
In which the empty string is written as "EMPTY"
Grammars can be serialized as .grammar files easily:
```py
paran_productions = {
  'S' : ['SS', '(S)', '()', '']
}
G = Grammar(paran_productions)
G.to_grammar('Parantheses.grammar')
```
Which generates a .grammar file:
```
S -> SS
S -> (S)
S -> ()
S -> EMPTY
```
To load the grammar, given its grammar file:
```py
G = Grammar()
G.from_grammar_file('Parantheses.grammar')
```
