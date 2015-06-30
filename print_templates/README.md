# Sierra Print Templates

The spine label print template is a JasperReport file, which is a combination of XML and Java. It picks up pre-defined variables from the item record and allows us to format them for output.

The variables that our template uses are:

## callSubf

Data Element 8: subfield f, from c-tagged varfld Purpose: call number prestamp

## itemFix79

Data Element 12: ff79 from item record Purpose: item location

## callAlphaStart

Data Element 1: subfield a/h (1st occurrence only of subfield a), alpha content until first number; from c-tagged varfld Purpose: call number

## callNumericStart

Data Element 2: subfield a/h (1st occurrence only of subfield a), numerical content until decimal point, from c-tagged varfld Purpose: call number

## callNumericAfterDec

Data Element 3: subfield a/h (1st occurrence only of subfield a), numerical content following decimal point, from c-tagged varfld (assume that customer may interpolate the decimal point as desired) Purpose: call number

## callEndCR

Data Element 4: subfield a/h (1st occurrence only of subfield a), all remaining content following 1-3 (with carriage returns for spaces), from c-tagged varfld Purpose: call number

## callSubb

Data Element 7: subfield b/I (1st occurrence only of subfield b), content (without carriage returns for spaces), from c-tagged varfld Purpose: call number for pocket labels

## itemv

Data Element 40: 1st instance each of 'v' tagged field from item record Purpose: varfld from item
 
## Formatting

These elements are arranged to output on multiple lines, as follows:

```
subfield f
location code
call number
volume
```

LC call numbers are formatted as:

```
$F{callSubf} + "\n"
+ $F{itemFix79} + "\n"
+ $F{callAlphaStart} + $F{callNumericStart}
+ $F{callNumericAfterDec} + " ." + $F{callEndCR}
+ " " + $F{callSubb}
+ "\n" + $F{itemv}
```

The " ." is necessary for Computype's code to properly parse Cutter numbers.

Dewey call numbers are formatted as:

```
$F{callSubf} + "\n"
+ $F{itemFix79} + "\n\n"
+ $F{callAlphaStart} + $F{callNumericStart}
+ $F{callNumericAfterDec} + ":"
+ $F{callEndCR} + " "
+ $F{callSubb} + $F{itemv}
```

The call number is moved to the "volume" line, and an extra ":" is inserted to force a line break after the call number.

CECH TEXT call numbers are formatted as:

```
($F{callSubf} + "\n"
+ $F{itemFix79} + "\n\n"
+ $F{callEntireCR}.replace(" ", "("))
```

The spaces are replaced with "(", to force linebreaks.

History (No longer maintained after change to github):

`_spine_computype11.jrxml` : Updated to support label queues:

columnCount changed from "8" to "1"

`_spine_computype10.jrxml` : Updated to support |b in C.U. call numbers:

`<textFieldExpression class="java.lang.String"><![CDATA[(($F{callEntire}.substring(0,4)).equals("C.U.")) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace("C.U.", "C.U. ").replace(" ", "(")) : (Pattern.matches("cl-g", $F{callSubf})) ? ("\n" + ($F{itemFix79} + $F{callSubf}).replace(" ", "") + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv}) : (Pattern.matches("(M|m)icroprint.*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : (Pattern.matches("j?[0-9][0-9][0-9].*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : ($F{callEntire}.substring(0,4)).equals("TEXT") ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace(" ", "(") + "(" + $F{itemv}) : ($F{callSubf} + "\n" + $F{itemFix79} + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv})]]></textFieldExpression>`

`_spine_computype9.jrxml` : Updated to support volume field in CECH TEXT call numbers:

`<textFieldExpression class="java.lang.String"><![CDATA[(($F{callEntire}.substring(0,4)).equals("C.U.")) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callField}.replace("C.U.", "C.U. ").replace(" ", "(")) : (Pattern.matches("cl-g", $F{callSubf})) ? ("\n" + ($F{itemFix79} + $F{callSubf}).replace(" ", "") + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv}) : (Pattern.matches("(M|m)icroprint.*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : (Pattern.matches("j?[0-9][0-9][0-9].*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : ($F{callEntire}.substring(0,4)).equals("TEXT") ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace(" ", "(") + "(" + $F{itemv}) : ($F{callSubf} + "\n" + $F{itemFix79} + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv})]]></textFieldExpression>`

`_spine_computype8.jrxml` : Updated to support C.U. call numbers:

`<textFieldExpression class="java.lang.String"><![CDATA[(($F{callEntire}.substring(0,4)).equals("C.U.")) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callField}.replace("C.U.", "C.U. ").replace(" ", "(")) : (Pattern.matches("cl-g", $F{callSubf})) ? ("\n" + ($F{itemFix79} + $F{callSubf}).replace(" ", "") + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv}) : (Pattern.matches("(M|m)icroprint.*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : (Pattern.matches("j?[0-9][0-9][0-9].*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : ($F{callEntire}.substring(0,4)).equals("TEXT") ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace(" ", "(")) : ($F{callSubf} + "\n" + $F{itemFix79} + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv})]]></textFieldExpression>`

`_spine_computype7.jrxml` : Updated to support cl-g call number changes. This detects the presence of |fcl-g, and adds it to the item record location, to work with an updated spine label prefix list that handles this |f seperately from the others:

`<textFieldExpression class="java.lang.String"><![CDATA[((Pattern.matches("cl-g", $F{callSubf})) ? ("\n" + ($F{itemFix79} + $F{callSubf}).replace(" ", "") + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv}) : (Pattern.matches("(M|m)icroprint.*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : (Pattern.matches("j?[0-9][0-9][0-9].*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : ($F{callEntire}.substring(0,4)).equals("TEXT") ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace(" ", "(")) : ($F{callSubf} + "\n" + $F{itemFix79} + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv}))]]></textFieldExpression>`

`_spine_computype6.jrxml` : Updated to expand support for Dewey numbers, whether or not they start with "j", using regular expressions:

`<textFieldExpression class="java.lang.String"><![CDATA[(Pattern.matches("(M|m)icroprint.*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : (Pattern.matches("j?[0-9][0-9][0-9].*", $F{itemc})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : ((($F{callEntire}.substring(0,4)).equals("TEXT")) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace(" ", "(")) : ($F{callSubf} + "\n" + $F{itemFix79} + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv}))]]></textFieldExpression>`

`_spine_computype5.jrxml` : Updated to add support for Microprint, using regular expressions:

`<textFieldExpression   class="java.lang.String"><![CDATA[(Pattern.matches("(M|m)icroprint.*", $F{callAlphaStart})) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{itemc}.replace(" ", "(")) : ($F{callEntire}.substring(0,1).equals("j")) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace(" ", "(")) : ((($F{callEntire}.substring(0,4)).equals("TEXT")) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace(" ", "(")) : ($F{callSubf} + "\n" + $F{itemFix79} + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv}))]]></textFieldExpression>`

added line neat beginning to import regular expression matching:

`<import value="java.util.regex.Pattern"/>`

`_spine_computype4.jrxml` : Updated to improve support for CECH TEXT numbers and for CECH juv. Dewey numbers:

`<textFieldExpression   class="java.lang.String"><![CDATA[($F{callEntire}.substring(0,1).equals("j")) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace(" ", "(")) : ((($F{callEntire}.substring(0,4)).equals("TEXT")) ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntire}.replace(" ", "(")) : ($F{callSubf} + "\n" + $F{itemFix79} + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv}))]]></textFieldExpression>`

`_spine_computype3.jrxml` : updated to include support for CECH TEXT numbers with the following expression in the textFieldExpression field:

`<textFieldExpression   class="java.lang.String"><![CDATA[($F{callAlphaStart}.substring(0,1)).equals("j") ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + ":" + $F{callEndCR} + " " + $F{callSubb} + $F{itemv}) : ($F{callField}.substring(0,4)).equals("TEXT") ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callEntireCR}.replace(" ", "(")) : ($F{callSubf} + "\n" + $F{itemFix79} + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv})]]></textFieldExpression>`

`_spine_computype2.jrxml` : updated to include support for CECH juv. Dewey numbers with the following expression in the textFieldExpression field:

`<textFieldExpression   class="java.lang.String"><![CDATA[($F{callAlphaStart}.substring(0,1)).equals("j") ? ($F{callSubf} + "\n" + $F{itemFix79} + "\n\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + ":" + $F{callEndCR} + " " + $F{callSubb} + $F{itemv}) : ($F{callSubf} + "\n" + $F{itemFix79} + "\n" + $F{callAlphaStart} + $F{callNumericStart} + $F{callNumericAfterDec} + " ." + $F{callEndCR} + " " + $F{callSubb} + "\n" + $F{itemv})]]></textFieldExpression>`

`_spine_computype.jrxml` : original template.
