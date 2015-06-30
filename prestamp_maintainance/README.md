# Prestamp maintainance

## Format of code file

The prestamps are converted from the location codes in Millennium item records according to the attached chart. Each line is for a separate location code in this format:

"ucode,Prestamp text"

Use the pipe character ("|") to enter a linebreak in a prestamp (e.g., "udar,DAAP|Ref").

The code file is attached below. Please note that for libraries with more than one location (such as Chem-Bio), the location is pulled in from |f in the item record, not from the prestamp code file.

Please keep all previous versions, using iLib version control.

## Uploading changes

Cancel the current program running on the printer:

    1. Press cancel (down arrow).
    1. Press again and hold for three seconds to clear temporary memory.
    1. The printer should say "Ready".

From any workstation, log into the printer via FTP, as user "root", with password "9100". (The ip address can be found in the printer settings, or in notes elsewhere in this documentation.) Change directory to "/card", and copy the new file in that location, overwriting the previous version.

Reload the program:

    1. Press menu (Memory Card is displayed on the screen).
    1. Press down (Label from card (IFFS) is displayed).
    1. Press Enter.
    1. If "1" is listed, press Enter again.
    1. Should be good!
 

## Changelog

(no longer maintained, with move to github.com)

  * 2013-12-10, added ucrlc stamp for CECH Literary Center Reference - dsm
  * 2013-10-07, added ucrns stamp for CECH NASA - dsm
  * 2013-05-21, added uarh stamp for Historical Textbooks - JV
  * 2013-02-22, edited stamp for ulara from Ref to Ref|Atlas -dsm
  * 2012-08-30, edited stamp for ucres from CECH to CECH|ESL -JV
  * 2012-06-08, added ucrue (CECH|K-12|Electronic) -dsm
  * 2012-05-09, added udaec (DAAP|Eames) -JV
  * 2012-05-04, removed udabe (not longer in use) and changed prestamp on udab and udabo from "Rare Book" to "Spec Coll" - JV
  * 2012-04-10, added CECH K-12 Mixed Materials (ucruk CECH K-12 Miced Material) -JV
  * 2012-04-10, added CECH Librarian's office (ucrf,CECH) -JV
  * 2012-04-10, added CECH Prof Ed Media (ucrl,CECH|Prof Ed) -JV
  * 2012-04-03, added CEAS Ref Historical location (uenrh,CEAS|Ref|Historical) - dsm
  * 2012-03-30, added classics maps location (ucl2,class) - dsm
  * 2012-03-27, added Preservation Services location (ulal,Pres Serv) - dsm
  * 2012-02-08, removed "C.U." from all prestamps, to work with print template, which adds this -JV
  * 2012-01-24, added DAAP Elephant location -JV
  * 2012-01-11, added Ref OVERSIZE location -JV
  * 2011-11-16, added CECH K-12 electronic location (ucrue,CECH|K-12|Electr) - dsm
  * 2011-10-19, added cl-g prestamps -JV
  * 2011-10-13, added CECH NASA location (ucrns,CECH|NASA) - dsm
  * 2011-08-15, updated uclg codes to remove "cl-g" from prestamp, as they now use |fcl-g in the call number - dsm
  * 2011-08-08, updated ucres to read "CECH|ESL" and added ucruk "CECH|K-12 MM".
  * 2011-08-02, updated to include CEAS location: uenu
  * 2011-07-08, corrected classics elephant location (ucle, ucleo) - dsm
  * 2011-06-28, New loc code for GMP Folio: ugpe
  * 2011-06-28, changed location code for CHEMBIOL Rbk Cage from ucbbx to ucbrb
  * 2011-06-28, changed location code for Oesper textbooks from ucbry to ucbbt
  * 2011-06-27, changed location code for Oesper Journals from ucbjb to ucbbj
  * 2011-06-03, added CECH Prof Ed Media location (ucrl,CECH|Prof Ed|Media)
  * 2011-05-09, changed "Admin" to "Admin|Office" - jv
  * 2011-05-04, added DAAP Librarian office location (udaf,DAAP) -jv
  * 2011-05-04, corrected DAAP video location (udau,DAAP|video) -dsm
