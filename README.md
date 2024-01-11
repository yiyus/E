Text editing with structural regular expressions
===============================================

Match functions
---------------

    {a}∆ w   returns 1 if the regex a (default '.') matches w
    {a}⍙ w   returns 1 if the regex a (default '.') does not match w

Replacements and selections
--------------------------

    {a}(aa x ww)w   substitute each match of ww in w for the result of (a aa match)
                    ww = is equivalent to '^.*$' (select lines)
                    ww | is equivalent to '\S+' (whitespace separated fields)
                    ww < the file named w is opened, or listed if w is a directory
                    ww > the file named w is opened and edited in place
                    aa < the results are written to file named a or stdout
                    aa list of namespaces returned by A to execute them in order
                    aa string is used as transformation string (see ⎕R)
    {a}(aa X ww)w   like x, but returns substitutions
    {a}(aa y ww)w   like x, but inverted selection (split at)
    {a}(aa Y ww)w   is to y like X is to x
    {a}(aa g ww)w   equivalent to (aa x '^.*$' ⍣ (⍵⍵ ∆ w) w)
    {a}(aa v ww)w   equivalent to (aa x '^.*$' ⍣ (⍵⍵ ⍙ w) w)
    {a}(aa G ww)w   select elements of w that match ww
    {a}(aa V ww)w   select elements of w that do not match ww
       (aa A ww)w   return action ww for condition aa, copying objects w
    {a}(aa j ww)w   join result of (a aa w) using ww as separator
    {a}    J    w   join elements of w using a (default space) as separator

Examples
--------

        E.('<&>'g't'X|)'one two three'
    ┌───┬─────┬───────┐
    │one│<two>│<three>│
    └───┴─────┴───────┘
        E.('\u0'v'o'x|)'foo bar foobar barbar'
    foo BAR foobar BARBAR
        '#'⎕NS E.Unix
        'E_.apln'get(¯1∘tail cat('^⍝'sed'^   'grep'E/README.md')cat 1∘tail)_'E/E.apln'

See also `Test` function and `Unix` namespace

References
----------

- https://doc.cat-v.org/bell_labs/structural_regexps/se.pdf
- https://doc.cat-v.org/bell_labs/sam_lang_tutorial/sam_tut.pdf
- https://linux.die.net/man/1/ed
- https://linux.die.net/man/1/sed
- https://linux.die.net/man/1/awk
