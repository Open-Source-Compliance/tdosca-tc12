# How to semi-automatically get an OSCF starting with a normalized BOM


## 1. create a normalized BOM by using the csv format_

The normalized BOM (nbom.csv) contains information necessary to create the compliance artifacts which a developer can and must manually gather from his work. It contains 5 columns separated  by a ';':

* $1 = CNAME = component name
* $2 = RelNr = release number
* $3 = CType =
  - app,
  - dll [= dynamically linked library ]
  - sll [= statically linked library ]
  - isf [= included source file ]
* $4 = PStat =
  - rap [= required as preinstalled component],
  - unm [= unmodified foss component becomes part of the distributable package]
  - mod [= modified foss component becomes part of the distributable package]
* $5 = SPDX License ID

## 2. create and complete the prefilled specified bom markdown file file

`./create.oscf/nbom.csv-2-sbom.md.sh nbom.csv > pre.sbom.md`

The derived file contains a partially prefilled markdown table. The empty colums must manually be filled by gathering the required information from the web.

Please name the finally filled file your `sbom.md`. The colums, it requires are these:

* NR : current number
* CNAME : component name = $1
* MpUrl : Main Project Url
* RelNr : release number = $2
* CTYPE : see above
* PSTAT : see above
* RepoUrl: Url of the repository containing the license info
* SpdxId : Spdx Identifier of the license
* LSTUrl : Url of the file containing the license / licensing statement
* LSTType :
  - stal [ stand alone license text file ]
  - embl [ license text embedded into a file header ]
  - olst [ only a licensing statement without a license text]

## 3. derive the processable sbom.csv file

The OSCF generator is a php file, taking the necessary information as csv file. This sbom.csv ist derived from the sbom.md file via

`./create.oscf/sbom.md-2-sbom.csv.sh > sbom.csv`

## 4. let the OSCF core snippet and the reports be derived

by using `./create.oscf/sbom.csv-2-oscf.snippets.php sbom.csv > oscf.core.md`

Note: The script `sbom.csv-2-oscf.snippets.php` contains applies the license knowledge to the gathered information. It is something like an expert system. It creates

* the `oscf.core.md`
* the `oscf.index.md` which links the index to the chapters
* the `oscf.report.sh` which collects the names of the multiply used licenses

## 5. let the final task tagged OSCF be compiled

by using the command `./create.oscf/link.oscf.md.sh oscf.core.md`

This script uses the file from step 4 together with some files / data stored in  `./create.oscf/snippets`, as the general oscf-header, the written offer text, and the license text in md format.
