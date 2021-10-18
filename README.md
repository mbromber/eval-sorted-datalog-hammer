# Evaluation data and software

This repository contains auxiliary resources for the following research work:

**A Sorted Datalog Hammer for Supervisor Verification Conditions Modulo Simple Linear Arithmetic**
by Martin Bromberger, Irina Dragoste, Rasha Faqeh, Christof Fetzer, Larry González, Markus Krötzsch, Maximilian Marx, Harish K Murali, and Christoph Weidenbach. 2021.


## SPASS-SPL (v0.7)

[SPASS-SPL (v0.7)](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) can be used as a decision procedure for the first-order fragment of pure approximately grounded Horn Bernays-Schoenfinkel modulo simple linear (mixed real-integer) arithmetic (HBS(SLR)AP). To solve an HBS(SLR)AP problem encoded in the [FTCNF language](#ftcnf-language), execute [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) with the option `-d`:

    ./bin/SPASS-SPL -d <file>.ftcnf

[SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) will then apply the sorted Datalog Hammer to transform the HBS(SLR)AP clause set (modulo a universal conjecture) into an equisatisfiable Datalog program. After that is done, [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) solves the Datalog program with the Datalog reasoner [VLog](https://github.com/karmaresearch/vlog) that has been integrated into [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) via an API.

[SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) returns `Conjecture proven!` if the universal conjecture is entailed by the clause set and otherwise `Conjecture refuted!`.

If the input file `<file>.ftcnf` contains no universal conjecture, then [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) will assume `false` as the universal conjecture. In this case, [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) returns `Conjecture proven!` if the clause set is unsatisfiable (because "false" can only be entailed by an unsatisfiable clause set) and `Conjecture refuted!` if the clause set is satisfiable.

### Transformation of FTCNF problems into other input languages

[SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) can transform FTCNF problems into the SMT-LIB 2.6 and into the CHC competition format. The respective options to do so are `-S -p` and `-C -p`.

[SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL) can also be used to transform FTCNF problems after the application of the sorted Hammer into the DFG language of SPASS (with the options `-d -D -p`) and from DFG with the tool [dfg2tptp](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/dfg2tptp) in the `bin` folder into the tptp format.

We already transformed all problems into the various formats. They can be found in the `Benchmarks` folder under the folder named after the respective file ending. For instance, `Benchmarks/smt2/ecu_u1.smt2` is the output of `./bin/SPASS-SPL -S -p Benchmarks/ftcnf/ecu_u1.ftcnf`

### Additional Options

* Option `-h`: hammer statistics, prints statistics of the DATALOG hammer. (The size of largest test point set and the size of hammered universal conjecture.)
* Option `-q <query>`: returns all derivable facts over our test points matching the given query. (Only applicable in combination with -d). E.g. <query> := "P(X0,X1)" returns all facts derivable for the predicate P.
* Option `-qall`: returns all derivable facts over our test points. (Only applicable in combination with -d).
* Option `-m`: if the input contains a universal conjecture that SPASS-SPL refutes, then this option prints all facts over the test point set and the conjecture predicate that could not be derived. (If the test point scheme is not total over the query, we can still refute it but not return any facts here.)

## SPASS-SPL (v0.6)

[SPASS-SPL (v0.6)](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL-0_6) can solve clause sets modulo conjectures over the first-order fragment of pure positively grounded Horn Bernays-Schoenfinkel modulo simple linear real arithmetic (HBS(SLR)PP). To determine whether an HBS(SLR)PP clause set entails a universal conjecture (both encoded in one file in the [FTCNF language](#ftcnf-language)), execute [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL-0_6) with the options `-d -n`:

    ./bin/SPASS-SPL-v0_6 -d -n <file>.ftcnf

To determine whether a HBS(SLR)PP clause set is satisfiable (encoded in the [FTCNF language](#ftcnf-language)), execute [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL-0_6) with the options `-d`:

    ./bin/SPASS-SPL-v0_6 -d <file>.ftcnf

In both cases, [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL-0_6) will then apply the original Datalog Hammer to transform the HBS(SLR)PP clause set (modulo a universal conjecture) into an equisatisfiable Datalog program. After that is done, [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL-0_6) solves the Datalog program with the Datalog reasoner [VLog](SPASS-SPL solves the Datalog program with the Datalog reasoner VLog that has been integrated into SPASS-SPL via an API.) that has been integrated into [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL-0_6) via an API.

SPASS-SPL returns `Conjecture proven!` if the universal conjecture is entailed by the clause set and otherwise `Conjecture refuted!`.

If the input file `<file>.ftcnf` contains no universal conjecture, then SPASS-SPL will assume `false` as the universal conjecture. In this case, [SPASS-SPL](https://github.com/mbromber/eval-sorted-datalog-hammer/blob/main/bin/SPASS-SPL-0_6) returns `Conjecture proven!` if the clause set is unsatisfiable (because "false" can only be entailed by an unsatisfiable clause set) and `Conjecture refuted!` if the clause set is satisfiable.

## FTCNF Language
FTCNF is the input language of SPASS-SPL. It is possible to express any BS(LA) formula in this language. SPASS-SPL has 3 sorts: "R" for Real, "I" for Integer, and "F", which stands for a finite set whose elements are exactly the constants of the sort. (This means that we SPASS-SPL supports only one first-order sort at the moment!) Default sort for all variables and constants is "R". Default sort for all predicates with an argument of sort "R" or "I" is "R". Default sort for all predicates with an argument of sort "F" is "F". In order to change the sort of a variable/constant, it has to be declared in the <preamble> of the input file. For instance `p(x:I),p(y:F)` declares the variable x as an integer variable and the variable y as a variable over F.

A clause written in the language looks as follows:

    <(+(-(*(3,x),*(x,e(y,2))),6),5),  =(y,z) || P(x,y), Q(z,w) -> R(a,w), Q(z,z).

The full grammar of the language is defined below:

    <preamble>   ::= [["p("<var>":"<RIF>")" | "p("<const>":"<RIF>")"] [","["p("<var>":"<RIF>")" | "p("<const>":"<RIF>")"]]*]
    <comment>    ::= "%" <anystring until EOL>
    
    <clause>     ::= [<constraint> "||"] <atoms> "->" <atoms> "."
    <gclause>    ::= g [<constraint> "||"] "->" <atom> "."
    <tclause>    ::= t <catom> "||" -> <atom> "."
    <constraint> ::= <catom> ["," <catom>]*
    <atoms>      ::= [<atom> ["," <atom>]*]
    <atom>       ::= <upercaseletter>[<number> | <letter>]*"("[<terms>]")"
    <terms>      ::= <term> ["," <term>]*
    <term>       ::= <var> | <const>
    <RIF>        ::= "R" | "I" | "F" 
    <const>      ::= <abcd>[[<lowercasestring>] | [<RIF>] | [<number>]]*
    <var>        ::= <xyzuvw>[[<lowercasestring>] | [<RIF>] | [<number>]]*
    <abcd>       ::= "a" | "b" | "c" | "d" 
    <xyzuvw>     ::= "x" | "y" | "z" | "u" | "v" | "w" 
    <catom>      ::= <crel>"("<cterm>,<cterm>")"
    <crel>       ::= "<" | ">" | "=" | "<=" | ">=" | "!="
    <cterm>      ::= "+("<cterm>,<cterm>[,<cterm>]*")" | "*("<cterm>,<cterm>[,<cterm>]*")" | "-("<cterm>,<cterm>")" | "-"<number> | <number> | <var>
    <number>     ::= ["0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"]+
    
    <SUPLOGin>   ::= <comment>* <preamble> <clause>* <tclause>* [<gclause>]

All variables in a `<clause>` are assumed to be universally quantified.

The optional `<gclause>` defines a universal conjecture that is supposed to be verified for our set of clauses `<clause>*`. More complex positive universal conjectures have to be manually flattened to this format according to the process outlined in https://arxiv.org/abs/2107.03189.

Existential conjectures cannot be encoded directly into the FTCNF format. However, an existential conjecture can be added by manually flattening it according to the process outlined in https://arxiv.org/abs/2107.03189 until the conjecture consists only of a conjunction of atoms <atoms>*, which can then be added as a clause "<atoms>* || -> .". The existential conjecture is entailed by the original clause set if the new clause set is unsatisfiable.

### Restrictions

* The strings "Goal", "Missing", and "Oa" cannot be used as predicate symbols because they are reserved for our Datalog hammer.
* The sorted/original Datalog hammer only works for the horn fragment, i.e., at most one atom is allowed on the right side of the implication arrow `->`.
* Any variable in the theory `<constraint>` of a clause `<constraint> || <premisses> -> <head> .` must also appear in the first-order part `<premisses> -> <head>`. If this is not the case for a variable `x`, then we can easily fix this by
first introducing a fresh unary predicate `Q`, adding the literal `Q(x)` to `<premisses>`, and finally by adding a clause `-> Q(x).` to our clause set.
* The sorted Datalog hammer only works for simple bounds and approximately grounded inequalities whose finiteness can be approximated over non-recursive clauses. This includes all positively grounded inequalities.
* The previous version of SPASS-SPL (v0.6) was not yet able to recognize and handle theory constraints beyond simple bounds, unless they are positvely grounded variable comparisons (i.e., $x \LAOP y$ with $\LAOP \in \{\leq, <, \neq, =, >, \geq\}$). As a provisional workaround, it was also possible to "highlight" positively grounded theory atoms `<catom>` manually. To do so, the theory atom had to be replaced by a first-order `<atom>` over a fresh predicate and the same variables as <catom>. The interpretation of `<atom>` can then be fixed to `<catom>` with the help of a theory pattern clause `<tclause> ::= <catom> || -> <atom>`. The Datalog hammer will then treat `<catom>` as if it were a positively grounded theory atom that always simplifies to true or false in elim(S,N). The user has to check themselves if this is actually the case or the result is no longer guaranteed to be sound. Although the current version of SPASS-SPL (v0.7) can recognize all approximately grounded (and therefore the subsumed positively grounded) inequalities automatically, we still kept the theory pattern feature so old input files can still be executed by SPASS-SPL (v0.7).

# Acknowledgements

This work is partly supported by Deutsche Forschungsgemeinschaft (DFG, German Research Foundation)
in project number 389792660 (TRR 248, [Center for Perspicuous Systems](https://www.perspicuous-computing.science/)), and by the Bundesministerium für Bildung und Forschung (BMBF, Federal Ministry of Education and Research) in the [Center for Scalable Data Analytics and Artificial Intelligence](https://www.scads.de) (ScaDS.AI).
