# pfam_terms
Search description of PFAM terms with [RESTful API](http://pfam.xfam.org/help#tabview=tab11)

```bash
# code in bash
# pfam_terms.tab contains a list of PFAM identifiers

cat pfam_terms.tab | while read  pfam; do
desc=$(curl http://pfam.xfam.org/family/"$pfam"/desc | head -1);
printf "$pfam\t";
printf "$desc\n";
done 2> /dev/null \
> pfam_terms.desc.tab

# Postprocessing of not found terms (since HTTP request returns always 200, even when the PFAM term was not found and an error is reported in HTML)

cat pfam_terms.desc.tab | sed 's#<\!DOCTYPE.*#NF#' > tmp && mv tmp pfam_terms.desc.tab

# END
```
