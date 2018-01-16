States
======

This directory contains two kinds of states:

*   **positive tests**. With theses tests 
    invariants are expected to evaluate to True.
    Positive tests are in the directory OK.
*   **negative tests**. With theses tests
    invariants are expected to evaluate to False.
    negative tests can be found in the directory OK.

States are expressed with .soil actions prefixed by '!'.
The following assertions in the files are currently **not interpreted**.::

    -- @assert Residence__floorOrder OK

However this means that the invariant floorOrder (in Residence class)
is expected evaluate to true (KO means false). This can be check
using the OCL USE interpreter (e.g. ``use -qv``).


Positive tests
--------------

Positive tests can be found in the directory ``States/OK``.
These states are given : a priori you do not need to change them.
All invariants are expected to evaluate to true with these
tests. These states can also be used to provide a base to create negative
tests with some mutation code.

Negative tests
--------------

Negative tests can be found in the directory ``States/KO``. Two examples are
given:

*   the negative test floorOrder__KO
*   the negative test floorBetweenMinAndMax__KO

There is one
state file for each invariant, each file being classified according to the
class is defined in and to the corresponding package.

For instance ``Buildings/Residence/floorOrder__KO.soil``
provides a state that does *not* satisfy the ``floorOrder`` invariant.::

    -- @assert Residence__floorOrder KO     -- not interpreted yet

    -- context self : Residence inv floorOrder :
    -- Order between floorMin and floorMax attributes.

    ! condillac := new Residence('condillac')
    ! condillac.name := 'Residence Condillac'
    ! condillac.floorMin := 5
    ! condillac.floorMax := 1

Negative tests can be build from scratch just like above.
Otherwise it could easier to make a reference to a given state
and then to change a few elements to make ultimately the invariant fail.
The file ``Buildings/Residence/floorBetweenMinAndMax__KO.soil`` includes
the positive test 2 but add a statement that makes the invariant fail.::

    -- @assert Room__floorBetweenMinAndMax KO

    -- context self : Room inv floorBetweenMinAndMax :
    -- Floor between minimum and maximum floors.

    open -q ../../../OK/2/state.sts
    ! residence1.floorMax := 2

Mutation code can add instances, delete links, change the value
of attributes, and so on. Including a base make it possible to avoid copy
and paste across files.

All other strategies in between can be taken. One can define different
base files or indeed define arbitrary include structures as long as there
is no cycle.