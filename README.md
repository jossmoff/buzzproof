# buzzproof
🐝 LaTeX style for Linear Style Natural Deduction proofs similar to way found in COMP1120 at UoM
## Contents
1. [Preamble](#preamble)
2. [Setup](#setup)
3. [Notation](#notation)
4. [Documentation](#documentation)
5. [Customization](#customization)

## Preamble
This style is based on the very popular [bussproofs](https://ctan.org/pkg/bussproofs?lang=en) package which allows for the construction of proof trees in the style of the sequent calculus and many other proof systems, however this package allows one to construction linear proofs.

## Setup

LaTeX style for Formal Grammars and operations

In order to load the package, use the following code:

```latex
\usepackage{buzzproof}
```

Once you have done this you can now create your proof by creating a linearproof enviroment and passing it asequence of inference rules

```latex 
\begin{linearproof}
    \axiom{p}{p}
    \implicationintro{}{p \rightarrow p}{1}
    \weakening{}{p \rightarrow p}{2}
    \conjunctionintro{}{p\land (p \rightarrow p)}{1,3}
\end{linearproof}
```

Will output as the following:
<p align="center"><img src="https://github.com/JossMoff/buzzproof/blob/main/images/linearproof.png" height="200"/></p>

## Notation
A *judgement* is a list of propositions called the *antecedents* followed by a single proposition known as the *consequent*. A judgement has the form, Γ⊢ϕ where everything to the left of the turnstile are the antecedents and to the left the consequent.
## Documentation
### Commands

#### \axiom
  - **Description**: Adds a proof line using the axiom rule.
  - **Usage**: `\axiom{antecedents}{consequent}`
  - **Example**: 
  ```latex 
  \axiom{p}{p}
  ```
#### \weakening
 - **Description**: Adds a proof line using the weakening rule.
 - **Usage**: `\weakening{antecedents}{consequent}{lines-infered-from}`
 - **Example**:
 ```latex
 \weakening{p,q}{p}{1}
 ```
#### \conjunctionintro
 - **Description**: Adds a proof line using the conjunction introduction rule.
 - **Usage**: `\conjunctionintro{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
 \conjunctionintro{p,q}{p \land q}{1,2}
 ```
 #### \disjunctionintro
 - **Description**: Adds a proof line using the disjunction introduction rule.
 - **Usage**: `\disjunctionintro{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
 \disjunctionintro{p}{p \lor q}{1}
 ```
 #### \implicationintro
 - **Description**: Adds a proof line using the implication introduction rule.
 - **Usage**: `\implicationintro{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
 \implicationintro{q}{p \rightarrow q}{2}
 ```
  #### \negationintro
 - **Description**: Adds a proof line using the negation introduction rule.
 - **Usage**: `\negationintro{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
  \negationintro{p}{p}{1}
 ```
  #### \doublenegationintro
 - **Description**: Adds a proof line using the double negation introduction rule.
 - **Usage**: `\doublenegationintro{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
  \doublenegationintro{p}{\neg\neg p}{1}
 ```
 #### \conjunctionelim
 - **Description**: Adds a proof line using the conjunction elimination rule.
 - **Usage**: `\conjunctionelim{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
 \conjunctionelim{p\landq}{p}{1}
 ```
 #### \disjunctionelim
 - **Description**: Adds a proof line using the disjunction elimination rule.
 - **Usage**: `\disjunctionelim{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
 \disjunctionelim{\Gamma}{\phi}{1,2,3}
 ```
 #### \implicationelim
 - **Description**: Adds a proof line using the implication elimination rule.
 - **Usage**: `\implicationelim{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
 \implicationelim{p, p \rightarrow q}{q}{1,2}
 ```
  #### \negationelim
 - **Description**: Adds a proof line using the negation elimination rule.
 - **Usage**: `\negationelim{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
  \negationelim{p, \neg p}{\bot}{1,2}
 ```
  #### \doublenegationelim
 - **Description**: Adds a proof line using the double negation elimination rule.
 - **Usage**: `\doublenegationelim{antecedents}{consequent}{lines-infered-from}`
 - **Example**: 
 ```latex
  \doublenegationelim{\neg\negp}{p}{1}
 ```

 
### Enviroments 

#### linearproof
 - **Description**: Enviroment for passing inference rules into to render a formatted proof
 - **Usage**: `\begin{linearproof}
                    {inferences}
               \end{linearproof}`
 - **Example**: 
 ```latex
    \begin{linearproof}
        \axiom{p}{p}
        \implicationintro{}{p \rightarrow p}{1}
        \weakening{}{p \rightarrow p}{2}
        \conjunctionintro{}{p\land (p \rightarrow p)}{1,3}
    \end{linearproof}
  ```

## Customization
You can easily define your own rules using the base functions:
- `baseRuleWithNoPremises`
- `baseRuleWithPremises`

Where if you have assumptions that have no premises (similar to the axiom) rule use `baseRuleWithNoPremises` and `baseRuleWithPremises` otherwise. However, if your functions are simply introduction or elimination rules which involve some premises, consider using the following for the appropriate usage:
- `introductionRule`
- `eliminationRule`

An example would be if we wanted to exnted to [FOL](https://en.wikipedia.org/wiki/First-order_logic) we would want the Universal Quantifier Introduction rule, which could be implemented as:

```latex
\newcommand{\universalquantifierintro}[3]{
    \baseRuleWithPremises{#1}{#2}{#3}{I_{\forall}}
}
% or
\newcommand{\universalquantifierintro}[3]{
    \introductionRule{#1}{#2}{#3}{\forall}
}
\begin{linearproof}
  ...
  \universalquantifierintro{\Gamma}{\forall{x}.A}{2}
\end{linearproof}
```
