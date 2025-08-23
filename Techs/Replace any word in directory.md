# Info

Change 

```
perl -pi -e '
s/(WORD_TO_CHANGE)/
   $1 eq lc($1)   ? "change_with_lowercase" :           # all lowercase
   $1 eq uc($1)   ? "CHANGE_WITH_UPPERCASE" :           # all uppercase
   ucfirst(lc($1)) eq $1 ? "Change_with_capitalizrd" :    # capitalized
   "change_with"
/gei
' $(grep -ril "WORD_TO_FIND" .)
```
