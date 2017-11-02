# Principles
* [Tell don't ask](https://martinfowler.com/bliki/TellDontAsk.html)
    * For example a function should be provided with all the data needed to perform processing. It should not be given a reference with which to retreive data from another system.
* [SOLID](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design))
    * _S_	- Single responsibility principle
        * a class should have only a single responsibility (i.e. changes to only one part of the software's specification should be able to affect the specification of the class)
    * _O_	- Open/closed principle
        * “software entities … should be open for extension, but closed for modification.”
    * _L_	- Liskov substitution principle
        * “objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.” See also design by contract.
    * _I_	- Interface segregation principle
        * “many client-specific interfaces are better than one general-purpose interface.”[8]
    * _D_	- Dependency inversion principle
        * one should “depend upon abstractions, [not] concretions.”
