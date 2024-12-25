java c
CSC1034:   Lecture   3
Intro
•   This   weeks   programming   topics
•      Programming
–      Modules
–    Generators
–    Named   Tuples
–    Pizza   (next   weeks   lecture!)
•    Development
–   Testing
How   to   learn
•   Important to   read   and   to   play
•      Don’t   understand   Python
–      Python Tutorial   https://docs.python.org/3/tutorial/
•      Not   clear   on   commits   and   pushing
–      Progit   https://git-scm.com/book/en/v2
•      Markdown
–   https://www.markdownguide.org
Stuck   somewhere
•   If you   are   stuck   on   the   practials,   read   the   online   material
•   If you   are   stuck   on   the   online   material,   try   more   of the   practical
•   If   neither   make   sense,   use   the   internet!
On   the   Internet
•   Wikipedia   is   a   good   source
•    StackOverflow
•    Can   be   hard   to judge   whether   you   should   understand   something
•    Be   prepared   to   read   what   does   not   make   sense   now
•   It   might   make   sense   later
•      But   be   prepared   to   move   on   -   there   is   lots   of rubbish   out   there
Use   the   material
•      Many   of you   are   getting   stuck   with   broken   code
•    Read   the   error   messages
•      Here   statements   are   really   good
•    Change   your   code   carefully   and   thoughtfully
The   Coursework
•   What   the   coursework   is
•      How   you   have   to   submit
NESS   Submissions
•      Plenty   of time   left to   submit!
•    Can   submit   more   than   once
•      Rigid   timing –   please   submit   early
Modules
•    So   far,   you   have   written   code   in   one   place
•   That’s   okay   for   small   programs
•      But   becomes   unwieldly   later   on
•      Python   provides   a   module   system   to   split   things   up
•    Some   of   the   terminology   overlaps   with   other   usages
Modules   and   Packages
•   A   module   consists   of   a   set   of   functions   and   objects
•      Defined   in   a   single   file
•    Related   modules   can   be   grouped   into   packages
•   These   are   all   in   the   same   directory
•   This   usage   of package   is   different   the   package   we   have   seen   earlier
•      Mostly,   package   means   “a   package   on   PyPI”
•   This   kind   of terminology   collision   is   unfortunate,   but   not   really   anyone’s   fault.
Modules
•   There   is   an   important   motivation   beyond   a   neat   set   of files
•    Functions   should   be   sensibly   named
•    But   they   all   share   the   same   name   space
•   The   names   would   clash
•   We   need   a   way   to   disambiguate
Modules
•    Similar   to   human   names
•   I   currently working with   three   other   people   called   “Phil”
•   We   have   longer   names   to   disambiguate
•      Likewise,   Newcastle   (-upon-Tyne,   -under-Lyme)
Modules
•      Python   knows   about   all   the   functions   in   the   current   module
•    Others   must   be   import-ed   into   the   current   module
•    Consider   this   statement:
import      fred
•      Python   looks   for   fred.py   in the   current   directory
•      Loads   it
–   reads   the   file,   all   the   definitions   in   it
–   Also   known   as   evaluating   the   file,   or   eval’ing
•      Makes   all   the   definitions   available
Modules
•   There   is   more   to   say   about   modules
•   I   find   Python   modules   simple   in   theory   and   error-prone   in   practice
•   Try   to   keep   it   simple
•      Read   the   Manual
•   If all   else   fails,   use   brute   force   and   ignorance   to   figure   out   problems
Programming
•      Python   is   a   high-level   language
•    Comes   with   a   significant   degree   of abstraction
•    Sometimes   you   need   to   know   what   is   happening
Generators
•    range   is   a   very   useful   function
•   It   returns   a   list   of the   appropriate   size
for      i      in      [0   ,    1   ,    2   ,      3   ,      4   ,    5   ,      6   ,      7   ,      8   ,      9]:
print(i,      end=   '   ,   ' )   print()
for      i      in      range(10):               print(i,      end=   '   ,   ' )
0,1,2,3,4,5,6,7,8,9,
0,1,2,3,4,5,6,7,8,9,
Generators
•   Actually, though,   it   doesn’t
•   Try   this
print([0   ,1   ,2   ,3   ,4   ,5   ,6   ,7   ,8   ,9])
print(range(10))
[0,      1,      2,      3,      4,      5,      6,      7,      8,      9]   range(0,    10)
Generators
•    So,   what   range   returns   is   not   a   list
•   It   doesn’t   print   out   as   one
•   It   actually   behaves   very   differently
Generators
•   To   understand   this,   we   need   to   understand   memory
•    Python   uses   garbage   collection   for   memory   management
•   What   is   memory   management?
•    Consider   this   code:
for    i      in      range(1   ,100000):
x      =      [i]
Generators
•   We   create   lots   of   lists,   each   with   a   single   value
•    For   each   list,   we   must   allocate   some   memory
•   The   computer   has   a   fixed   amount   of memory
•      Eventually   we   are   going   to   run   out
•    So,   we   must   deallocate   or   recover   the   memory
Generators
•   What   is   memory   management,   and   why   do   we   care?
•   Two   main   mechanisms:
•    Some   languages   do   this   explicitly
•    Some   use   Garbage   Collection   or   GC
•    GC   is   automatic
•    So   automatic   you   might   not   realise   it’s   there
Demo
Moving   through   a   list
Generators
•      How   does   this   relate   to   the   range   function?
•   Imagine, we create a list
Generators
•      Now we   iterate   through   this   list   
•   The   list   references   all   of   its   elements
•   Including   those   we   have   used
•   And   those   we   have   not   go   to   yet
Generators
•   A   generator   works   differently
•   Imagine   it   as   a   function   with   some   data   attached   
•   It’s   now   cheap   to   create
•   And   costs   them   same   regardless   of the   size
Generators
•    Python   also   has   generator   expressions
•      Like   a   list   comprehension
•      Neat   and   succinct
•   With   a   slightly   odd   “naked”   syntax
##   Status:      Shell
any([x>42      for      x      in      range(0   ,    10**2)])
any(x>42      for      x      in      range(0   ,    10**2**2**2))
def      gen():
return      (x>42    for      x      in      range(0   ,    10**2**2**2))   any(gen())
NamedTuples   and   Typing
•   Will   finish   off programming   section   by   introducing   named   tuples
•   Also   lead   in   to   the   next   section
NamedTuples
•   If you   have   been   following   the   online   material,   we   have   dealt   with   trains   earlier
•      One   list
•      One   dictionary
##      0      -      Name
##    1      -      Colour
##   2      -    Engine      Type ##      3    -      Train      Type       ##   4      -      Role
wilson      =    [   "wilson"   ,    "red"   ,    "diesel"   ,      "EMD    F3"   ,    "Trainee"]
print(wilson)   wilson      =      {
"name"   :    "wilson"   ,
"colour"   :      "red"   ,
"engine"   :    "diesel"   ,   "type"   :      "EMD      F3"   ,
"role"   :      "Trainee"
}
print(wilson)
NamedTuples
•      Lists   are   shorter   to write
•      But   easy   to   forget,   or   make   mistakes
•    So,   dictionaries   solve   the   problems?
•   What   if   we   need   several?
wilson      =      {
"name"   :    "wilson"   ,
"colour"   :      "red"   ,
"engine"   :    "diesel"   ,   "type"   :      "EMD      F3"   ,
"role"   :      "Trainee"
}
brewster      =      {
"name"   :    "brewster"   ,   "colour"   :      "blue"   ,
"engine"   :    "diesel"   ,
"type"   :    "BR      Class      55"   ,   "role"   :      "Trainee"
}
koko      =    {
"name"   :      "koko"   ,
"color"   :    "green"   ,
"engine"   :      "electric"   ,
"type"   :    "0    Series    Shinkansen"   ,   "role"   :      "Trainee"
}
print(wilson[   "colour"])   red
NamedTuples
•   We   can   create   multiple   instances   of a   similar   dictionary
•   Which   is   nice
•      But,   still   error   prone
•      Possibly   you   saw   the   mistake
##   Status:    Crash
wilson      =      {
"name"   :    "wilson"   ,
"colour"   :      "red"   ,
"engine"   :    "diesel"   ,   "type"   :      "EMD      F3"   ,
"role"   :      "Trainee"
}
brewster      =      {
"name"   :    "brewster"   ,   "colour"   :      "blue"   ,
"engine"   :    "diesel"   ,
"type"   :    "BR      Class      55"   ,   "role"   :      "Trainee"
}
koko      =    {
"name"   :      "koko"   ,
"color"   :    "green"   ,
"engine"   :      "electric"   ,
"type"   :    "0    Series    Shinkansen"   ,   "role"   :      "Trainee"
}
print(wilson[   "colour"])   print(koko[   "colour"])
Traceback    (most      recent    call      last):
File    "/home/phillord/documents/teaching/2023-24/csc1034/dev-repo/lectures-1/python/train_   print(koko["colour"])
KeyError:      ' colour   '
NamedTuples
•      Even,   if we   build   our   instances   correctly
•   We   could   (accidentally)   change   the   keys   after
•      Named   tuples   address   both   of   these
import      collections
Train      =      collections.namedtuple(   "Train"   ,
[   "name"   ,    "colour"   ,    "engine"   ,   "kind"   ,      "role"])
wilson      =      Train(name=   "wilson"   ,      colour=   "red"   ,
engine=   "diesel"   ,      kind=   "EMD      F3"   ,   role=   "Trainee")
brewster      =      Train(name=   "brewster"   ,      colour=   "blue"   ,
engine=   "diesel"   ,      kind=   "BR      Classic      55"   ,   role=   "Trainee")
koko      =      Train(name=   "name"   ,    colour=   "green"   ,
engine=   "electric"   ,      kind=   "0      Series      Shinkansen"   ,   role=   "Trainee")
print(koko)Train(name=   '   name   '   ,    colour=   ' green   '   ,    engine=   ' electric   '   ,      kind=   ' 0    Series    Shinkansen   '   ,      role=   ' Tra代 写CSC1034: Lecture 3Python
代做程序编程语言
NamedTuples
•   We   cannot   misname   a   field
•   And,   it’s   a tuple,   so   it’s   immutable
##   Status:    Crash
import      collections
Train      =      collections.namedtuple(   "Train"   ,
[   "name"   ,    "colour"   ,    "engine"   ,   "kind"   ,      "role"])
wilson      =      Train(name=   "wilson"   ,      colour=   "red"   ,
engine=   "diesel"   ,      kind=   "EMD      F3"   ,   role=   "Trainee")
brewster      =      Train(name=   "brewster"   ,      colour=   "blue"   ,
engine=   "diesel"   ,      kind=   "BR      Classic      55"   ,   role=   "Trainee")
koko      =      Train(name=   "name"   ,    color=   "green"   ,
engine=   "electric"   ,      kind=   "0      Series      Shinkansen"   ,   role=   "Trainee")
Traceback    (most      recent    call      last):
File    "/home/phillord/documents/teaching/2023-24/csc1034/dev-repo/lectures-1/python/train_   koko      =      Train(name="name",    color="green",
TypeError:      Train   .__new__   ()      got    an      unexpected      keyword    argument      ' color   '
NamedTuples
•    Named   tuples   use   a   different   syntax   for   accessing   values   import      collections
Train      =      collections.namedtuple(   "Train"   ,
[   "name"   ,    "colour"   ,    "engine"   ,   "kind"   ,      "role"])
wilson      =      Train(name=   "wilson"   ,      colour=   "red"   ,
engine=   "diesel"   ,      kind=   "EMD      F3"   ,   role=   "Trainee")
print(wilson.name)               print(wilson.colour)   print(wilson.engine)
wilson   red
diesel
NamedTuples
•   This   is   actually   generic   syntax
•      Called   “field”   or   “attribute”   access
•   It’s   possible   to   introspect   on   attributes
•   The tuple   knows   all   of its   attributes
•      Use dir   and   hasattr
•   Also, getattr and   setattr
import      collections
Train      =      collections.namedtuple(   "Train"   ,
[   "name"   ,    "colour"   ,    "engine"   ,   "kind"   ,      "role"])
wilson      =      Train(name=   "wilson"   ,      colour=   "red"   ,
engine=   "diesel"   ,      kind=   "EMD      F3"   ,   role=   "Trainee")
print(dir(wilson))
print(hasattr(wilson,      "name"))
[   ' __add__   '   ,      ' __class__   '   ,      ' __class_getitem__   '   ,      ' __contains__   '   ,      ' __delattr__   '   ,      ' __dir__   '   ,      ' __   True
NamedTuples
•      Named   tuples   are   fantastic   for   data-centric   apps
•   Which   is   a   lot   of apps   in   Python
•   Will   see   an   example   in   a   minute
Testing
•      Remember   our minimum   function
•   There   is   a   difficulty
•   I’ve   gone   to   all   this   effort,   but   it   cannot   remain   in   the   final   code
•   If I   added   this   to   a   module,   we   would   run   our   tests
•    But   if   remove,   we   have   lost   the   test   cases
•   Which   we   probably   did   by   hand
•   Also,   test_minimum   might   be   more   generally   useful   def   minimum(lst):
if      len(lst)      ==      0   :
raise      ValueError   ("Cannot      find   minimum    of    an    empty    sequence")
lowest      =      lst[0]               for      i      in      lst[1   :]:
if      i      <      lowest:   lowest      =      i
return      lowest
def      test_minimum(expected,      lst):
print(   "Should      be"   ,      expected,    ":"   ,   minimum(lst))
test_minimum(-100,      [-100   ,      0   ,    100])
test_minimum(-100,      [100   ,      0   ,      -100])
test_minimum(-1000,      [-1000   ,      0   ,    1000])   test_minimum(-10,      [-10   ,      0   ,    10])
test_minimum(1000   ,      [1000   ,    10000])
Testing
•   We   can   check   whether   we   are   running   the   file
•    Or   python   is   loading   it   as   a   module   def   minimum(lst):
if      len(lst)      ==      0   :
raise      ValueError   ("Cannot      find   minimum    of    an    empty    sequence")
lowest      =      lst[0]               for      i      in      lst[1   :]:
if      i      <      lowest:   lowest      =      i
return      lowest
def      test_minimum(expected,      lst):
print(   "Should      be"   ,      expected,    ":"   ,   minimum(lst))
if    __name__    ==       ' __main__ '   :
test_minimum(-100,      [-100   ,      0   ,    100])
test_minimum(-100,      [100   ,      0   ,      -100])
test_minimum(-1000,      [-1000   ,      0   ,    1000])   test_minimum(-10,      [-10   ,      0   ,    10])
test_minimum(1000   ,      [1000   ,    10000])
Testing
•   What   we   need   it   Test   Driven   Development
•      Like   version   control,   Testing   is   an   essential   tool   for   the   programmer
•   In   the   last   15   years,   become   routine
•   This   has   rather   upended   development
Testing
•   The   process   of writing   code:
•      Have   a   problem
•    Define   a   set   of   requirements
•   Write   some   code   to   fulfil   the   requirements
•   Test   to   see   if you   have   solved   the   problem
•      Or,   alternatively
–    Have   a   problem
–    Define   a   set   of requirements
–   Turn   the   requirements   into   a   computational   runnable   test
–   Write   some   code,   till   the   tests   run
–    Stop
Testing
•   The   latter   is   called   Test-Driven   Development
•   Write   your   tests   before   your   code
•   If you   cannot   write   a   test,   you   do   not   understand   the   problem
•   There   are   limitations
•    For   large   datasets   -   where   you   do   not   know   the   answer
•      Or   highly   computational   tasks
•    Or   where   tests   are   not   automatable
–    Especially   GUIs
–   Where   there   is   human   interpretation
Testing
•   Assume   that   we   have   the   following   code
•   In a   file   called   stats   .py   def   minimum(lst):
if      len(lst)      ==      0   :
raise      ValueError   ("Cannot      find   minimum    of    an    empty    sequence")
lowest      =      lst[0]               for      i      in      lst[1   :]:
if      i      <      lowest:   lowest      =      i
return      lowest
Testing
•   To test this,   we   add   a   new   file   called   test_stats   .py
•   The test   part   of the   name   is   important
•   The   stats   can   be   anything
import      stats
def      test_minimum():
assert      stats.minimum([-100   ,      0   ,    100])    ==    -100
Testing
•   We   use   the   Python   assert   keyword
•   It   says   “I   claim that the   following   must   be   true”
•   We   also   need   to   ensure   pytest   is   installed
•      Now   run   pytest
•    If our   test   succeeds,   we   get   a   nice   short   message
=============================    test    session    starts    ==============================   platform      linux      --      Python      3.10.12,      pytest-7.4.2,      pluggy-1   .3   .0
rootdir:      /home/phillord/documents/teaching/2023-24/csc1034/dev-repo/lectures-1/python   collected    1      item
test_stats   .py      .                                                                                                                                                                                                                                                                                                                                                         [100%]
==============================    1    passed    in      0   .01s      ===============================
Testing
•   If you’re   tests   fail,   we   get   something   longer   telling   us   the   problem
import      pytest   import      stats
def      test_success_minimum():
assert      stats.minimum([-100   ,      0   ,    100])    ==    -200
=============================    test    session    starts    ==============================   platform      linux      --      Python      3.10.12,      pytest-7.4.2,      pluggy-1   .3   .0
rootdir:      /home/phillord/documents/teaching/2023-24/csc1034/dev-repo/lectures-1/python   collected    1      item
test_stats_fail.py      F                                                                                                                                                                                                                                                                                                                           [100%]
===================================    FAILURES    ===================================
test_success_minimum                                                                                                                                                                           
def      test_success_minimum():
>                                  assert      stats.minimum([-100,    0,    100])    ==    -200
E                                       assert      -100    ==    -200
E                                        +          where      -100    =    ([-100,    0,    100])   E                                           +                   where          =      stats   .minimum
test_stats_fail   .py:5:      AssertionError
===========================    short    test    summary      info    ============================   FAILED      test_stats_fail.py::test_success_minimum      -      assert      -100      ==      -200==============================    1    failed    in      0   .02s      ===============================
•   A   formal   test   harness   is   a   big   improvement   on   what   we   said   before
•   The   output   shows   us   what   we   need   and   nothing   else
•    Our   expectations   for   correct   results   are   clear
•   We   can   keep   tests   forever
•      But   not   have   them   in   deployed   code
Testing
•    Can   change   the   way   that   you   code
•   It’s   a   hard   practice to   adopt
•    But   one   that   will   make   life   easier   as   you   move   on
Conclusions
•   We   are   nearing   the   end   of the   taught   material   for   this   section
•      But   there   is   a   week   to   go:   take   the   time   to   read!
•   If   you   have   anything   you   want   me   to   cover   next   week,   please   email!

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
