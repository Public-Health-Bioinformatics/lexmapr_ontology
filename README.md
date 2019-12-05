# lexmapr.owl
[LexMapr](https://github.com/Public-Health-Bioinformatics/LexMapr), a free-text-to-ontology term matching software () produced by Hsiao Labs, can be given instructions to report term matches according to a given agency Biosample categorization scheme.  The lexmapr.owl ontology file contains various agency category schemes for this reporting which we have bundled together in an open-source format for easy comparison and update.

## Adding Rules
Agency reporting categories or "buckets" are listed under the "agency reporting buckets" class, so named to indicate that reports can be generated that show, for a given textual description of a Biosample say, which agency buckets its terms match to.  The match test is contained in a bucket entity's OWL "Equivalent To" expression which has the form of 

    "has member" some [logical expression]"

where the logical expression can be a disjunction ("or") of ontology terms, and may include negation ("not ...") and bracketed expressions.  A given term (e.g. 'Mammalia') in an expression is matcheable, and any of its subordinate terms (e.g. 'Felis catus') are too.

If you need to reference an OBOFoundry ontology term that lexmapr.owl doesn't currently have, then:

1) add that term as a line item in the *imports/obo_ontofetch.txt* configuration file in the appropriate ontology section.  
2) Then visit the [OntoFox tool](http://ontofox.hegroup.org/) and select that file in the "2. Data input using local text file:" section towards bottom of form.
3) Then press "Get OWL (RDF/XML) Output File" to manually generate the output file link
4) Follow that link to see the generated .owl content in your browser
5) Save that page to imports/obo_import.owl .

Then the next time you open lexmapr.owl, the new term should appear, along with any parent path terms that locate it within BFO.  For example say you wanted to define a bucket for "Companion Animals".  The bucket itself can be created as a lexmapr.owl class under whichever agency uses it, but its membership rule needs to reference NCBITaxon terms.

    'has member' some ('Canis lupus familiaris' or 'Felis catus')

To reference 'Canis lupus familiaris' in the rule you first have to enter it into lexmapr.owl by way of the imports/obo_import.owl file.  Since it is an NCBITaxon term, it is best to add its URI to the imports/obo_ontofetch.txt file, in the UBERON term import section; then regenerate obo_import.owl .  With it now referenced in lexmapr.owl, you can go back and compose the equivalency rule given above.
