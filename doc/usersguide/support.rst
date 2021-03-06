=========================
Support File Descriptions 
=========================


**Introduction**

 This section discusses all the files which ALARA expects to
 find when running a problem:     

| :ref:`Element Library`
| :ref:`Material Library`
| :ref:`Waste Disposal/Clearance Index Limits`
| :ref:`Binary Reaction Library`

----------------------

.. _Element Library:

Element Library
===============

Description
-----------

 The element library allows the user to define the
 :term:`isotopic abundances`
 to be used for each element. While this library
 should normally include a  definition of the natural
 abundances for each element, an extension is available
 for defining enriched or isotopically tailored elements.

Format
------

 An element library can contain an arbitrary
 number of elemental definitions, each 
 represented by a block with the following
 format. Every block must start with the 
 following five entries: 

   * a string indicating the name/identifier,
   * a :term:`floating point value <floating point scalar normalization>` for the molar mass,
   * an integer value for the :term:`atomic number`,
   * a floating point value for the theoretical density, and
   * an integer value defining the number of :term:`isotopes <isotope>`.

 This is followed by two entries for each of these isotopes: 

   * an integer value for the mass number, and
   * a floating point value for the atomic abundance, in %.

Example
-------

Naming Elemental Definitions
----------------------------

 The names/identifiers for all elemental definitions must
 be derived from the :term:`chemical symbol`
 for that element, using the format ZZ[:AAA...], where ZZ
 represents the :term:`chemical symbol`,
 and [:AAA...] represents an optional modifier, separated by a
 colon, ':', from the chemical symbol. By  convention, entries
 without modifiers are used to define the :term:`natural
 abundances` of isotopes. The
 modifier must be a character string containing no
 :term:`whitespace`. [example: a
 definition for lithium enriched to 90% in the isotope
 6Li, might have the name 'Li:90'.] These names/identifiers
 can be  used both in a mixture block of the input file
 (when defining a constituent of type element) and in the
 material library.

-----------------------------

.. _Material Library:

Material Library
================

Description
-----------

 The material library is a mechanism for allowing users to
 save and re-use the definitons of a set of materials.
 Users are encouraged to develop their own material libraries,
 by adding material definitions to them as needed. Material
 libraries are all defined as lists of elemental definitions,
 each of which must occur in the :ref:`Element Library`.

Format
------

 A material library can contain an arbitrary number of
 material definitions, each represented by a block with the
 following format. Every block must start with the following
 three entries: 

   * a string indicating the name/identifier,
   * a floating point value for the theoretical density, and
   * an integer defining the number of elemental definitions.

 This is followed by three entries for each elemental definition: 

   * a string indicating the name/identifier,
   * a floating point value for the weight fraction in %, and
   * an integer for the :term:`atomic number`.

Example
-------

Naming Material Definitions
---------------------------

 The name of a material definition must be a character string
 with no :term:`whitespace`. The
 recommended practice is that material definitions never be
 deleted from a material library, ensuring the repeatability
 of results. It is expected, however, that many materials will
 undergo variations in their definition over time. It is
 therefore recommended that each material be named with a
 very specific identifier, perhaps containing dates, references,
 or project names. This will allow a single material library
 to be a growing and complete record of the material
 definitions used over time.

------------------------------------

.. _Waste Disposal/Clearance Index Limits:

Waste Disposal Rating/Clearance Index
=====================================

Description
-----------

 :term:`Waste disposal ratings <waste disposal rating>` and
 :term:`clearance indices` are used to
 provide a single metric for classifying the level of control
 required when disposing of used material. Each metric is
 based on a (possibly) unique list of isotopes and the
 allowable specific activities for those isotopes.

Format
------

 The WDR/CI files contain the disposal limit expressed as
 either a volumetric or specific activity. These files are
 simple text files containing one pair for each isotope for
 which a limit exists. The first entry of each pair identifies
 the isotope using either the standard :term:`chemical
 symbol` notation CC-AAAM (CC is
 the chemical symbol, AAA is the mass number, and M is the
 isomeric state: 'm' for the first isomeric state, 'n' for
 the second, and so on), or ALARA's kza notation ZZAAAM (ZZ
 is the :term:`atomic number`, AAA is
 the mass number, and M is the numerical isomeric state: '1'
 for the first state, '2' for the second, etc). The second
 entry is a specific activity in any combination of units
 supported by ALARA. The user is responsible for ensuring
 that the units chose in the output block match the units
 in the waste disposal limit file(s) used in that same block.

Example
-------

------------------------------

.. _Binary Reaction Library:

Binary Reaction Library
=======================

Description
-----------

 Because the reaction schemes/chains are created by a
 depth first search using the data from the transmutation
 and decay libraries, these libraries need to be accessed
 extensively and randomly. In the past, such random
 access was not possible due to limits on mass storage
 devices. Currently, in a text format, such random access
 would still be very tedious. To ensure that this random
 access does not create a drag on ALARA, it is necessary
 to either store the entire library in memory or use a
 binary file format. Because the libraries are often
 quite large (many MB) a simple binary format was designed.

Note
----

 For more information, see the section on binary reaction libraries in the Developers' Guide. 
