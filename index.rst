CyberResidencesOCL
==================

This case study provides a UML model dealing with long-stay “Residences”
such as university residences or so. The text of the case study is
available at http://cyberresidencesocl.readthedocs.io
A few modifications have been made. For instance:

* the package named 'Rents' is now named 'Residents',
* an attribute 'description' has been added 'Residence'.

The specification and the corresponding states used for validation
are written using USE OCL.
See http://scribetools.readthedocs.org/en/latest/useocl

Content of the directory
------------------------

The directory is structured as following ::

    index.rst                   This file

    Classes/                    The class model
        classes.cls             The specification written in USE OCL
        Diagrams/               Provided Class diagrams
            classes.cld.png     The full class diagram
            buildings.cld.png   Class diagram for the Buildings package
            residents.cld.png   Class diagram for the Residents package
            rates.cld.png       Class diagram for the rates package

    States/                     State files used for invariant validation.
        index.rst               Information about testing invariants
        OK/                     Positive states (satisfy all invariants)
        KO/                     Negative states (invariants must fail)

    check-all                   A script to check invariants


Batch mode
----------

To compile the specification::

    use -c Classes/classes.cls

To check the class model using the positive state 1::

    use -qv Classes/classes.cls States/OK/1/states.sts   # -> OK OK OK ...

To check a particular invariant using a negative test::

    use -qv Classes/classes.cls States/KO/<PACKAGE>/<CLASS>/<INV>__KO.soil

Integrated command
------------------

To avoid typing complex commands as above you can complete the
file below and execute it::

    check-all