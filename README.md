java c
CSC1034:   Lecture   4
Pizza 
•   Will   finish   with   a   worked   exampleAs   part   of   a   larger   project,   building   an   online   ordering   system   for   a   Pizza   company,   we   need   to   design   and   implement   a   system   for   calculating   the   costs and   some   other   features   about   a   pizza.   This   system   will   allow   you   to   build   a   pizza   from   a   base   and   some   toppings.
Pizza 
•   We   need   somewhere   to   put   the   data
•   What   features   do   pizza   have?
•    One   Base
•      Multiple toppings
Pizza: Iteration 1 
•    Pizza,   pizza   bases,   and   pizza   toppings   all   have   names
•    Need   a   list   of toppings,   and   one   base import      collections
Base      =    collections.namedtuple(   "Base"   ,    "name")
Topping      =      collections.namedtuple(   "Topping"   ,    "name")
Pizza      =      collections.namedtuple(   "Pizza"   ,    "name      base      toppings")
p    =      Pizza      (
name=   "Base"
base=Base(name=   "Thin"),   toppings=[
Topping("Olive"),   Topping("Garlic")
]
)
print(p)
Pizza(name=   ' Base   '   ,      base=Base(name=   ' Thin   ' ),    toppings=[Topping(name=   ' Olive   ' ),    Topping(name=   ' G
Pizza: Iteration 1 
•   I   have   used   typed   NamedTuples
•      Other   possibilities
– list   of ingredients,   with   base   first,
– (non-named)   tuple
– dictionary   with   two   elements
– Class   (next   lectures!)   import      collections
Base      =    collections.namedtuple(   "Base"   ,    "name")
Topping      =      collections.namedtuple(   "Topping"   ,    "name")
Pizza      =      collections.namedtuple(   "Pizza"   ,    "name      base      toppings")
p    =      Pizza      (
name=   "Base"
base=Base(name=   "Thin"),   toppings=[
Topping("Olive"),   Topping("Garlic")
]
)
print(p)
Pizza(name=   ' Base   '   ,      base=Base(name=   ' Thin   ' ),    toppings=[Topping(name=   ' Olive   ' ),    Topping(name=   ' G
•      Points   to   note
•      Have   test   within   file   not   in   test,   because   it’s   easier   to   show
Pizza:    Customer Reflections 
•   We’d   like   to   be   able   to   add   a   price
•    Output   is   a   bit   ugly
Pizza: Iteration 2 
•   Add   pizza_price   function
•   Add   pizza_report   function
•   Add   price   attribute   to   Base   and   Topping   import      collections      import      collections
Base      =    collections.namedtuple("Base",    "name")                                     |      Base    =    collections   .namedtuple("Base",
Topping      =      collections.namedtuple("Topping",    "name")                                     |
Topping      =      collections.namedtuple("Topping",    "name      price")
Pizza      =      collections.namedtuple("Pizza",    "name      base      toppings")   Pizza      =      collections.namedtuple("Pizza",    "name      base      toppings")
>def      pizza_price(p):
>                return      p.base.price    +    sum(t.price      for      t    in      p.toppings)   >
>def      pizza_report(p):
>                        return    """Pizza:      {name}   >Base:
>\t{base}\t\t\t:{baseprice:   .2f}
>Toppings:         >{toppings}   >
>Total:\t{total:   .2f}   >"""   .format(
>                     name=p   .name,
>                   base=p.base   .name,
>                     baseprice=p.base   .price,
>                        toppings="\n"   .join(["\t{}\t\t\t:{:   .2f}"   .format(t.name,      t   .   >                                                                                                                                             for      t      in      p.toppings]),
>                        total=      pizza_price(p)   >)
p    =      Pizza      (      p    =      Pizza      (
name="Base",                                  |                            name="SimplePizza",
base=Base(name="Thin"),                               |                            base=Base(name="Thin",    price=1.20),
toppings=[                              toppings=[
Topping("Olive"),                            |                                                      Topping("Olive",      price=0.70),
Topping("Garlic")                                  |                                           Topping("Garlic",      price=0.70)
]                              ]   )      )
print(p)                               |      print(pizza_report(p))
Pizza: Iteration 2 
import      collections
Base      =      collections.namedtuple(   "Base"   ,    "name      price")
Topping      =      collections.namedtuple(   "Topping"   ,    "name      price")
Pizza      =      collections.namedtuple(   "Pizza"   ,    "name      base      toppings")
def pizza_price(p):
return p.base   .price      +      sum(t.price for t in p.toppings)
def pizza_report(p):
return """Pizza:    {name}   Base:
\t{base}\t\t\t:{baseprice:.2f}
Toppings:         {toppings}
Total:\t{total:.2f}
"""   .format(
name=p   .name,
base=p.base   .name,
baseprice=p.base   .price,
toppings="\n"   .join(["\t{}\t\t\t:{:   .2f}"   .format(t.name,      t.price) for t in p.toppings]),
total=      pizza_price(p)   )
p    =      Pizza      (
name=   "SimplePizza"
base=Base(name=   "Thin",      price=1.20),   toppings=[
Topping("Olive",      price=0.70),   Topping("Garlic",      price=0.70)
]   )
print(pizza_report(p))
Pizza:      SimplePizza   Base:
Thin      :1   .20
Toppings:
Olive      :0   .70         Garlic      :0   .70
Total:      2   .60
•    Use   generator   expression   because   why   not?
•    format within   a   format   is   baroque
– I   can’t   find   an   easier   way
Pizza:    Customer Reflections 
•      Do   I   have   to   put   the   prices   for   the   ingredients   in   every   time?
•   Is   the   pizza   veggie   or   not?
Pizza: Iteration 3 
•   Add   veggie   attribute to   Topping
•   Add   pizza_veggie   function
•      Update   pizza   report   function
•   Add   catalogue   of   toppings   and   bases
import      collections      import      collections
Base      =      collections   .namedtuple("Base",    "name      price")      Base    =    collections   .namedtuple("Base",      "
Topping      =      collections.namedtuple("Topping",    "name      price")                         |Topping      =      collections   .namedtuple("Topping",    "name      price      veggi   Pizza      =      collections.namedtuple("Pizza",    "name      base      toppings")   Pizza      =      collections.namedtuple("Pizza",    "name      base      toppings")
def      pizza_price(p):      def      pizza_price(p):
return      p.base.price      +      sum(t.price      for      t      in      p.toppings)                   代 写CSC1034: Lecture 4
代做程序编程语言   return      p.base.price      +    sum(t.
>def      pizza_veggie(p):
>                return      all(t.veggie      for      t    in      p.toppings)   >
def      pizza_report(p):      def      pizza_report(p):
return    """Pizza:      {name}                      return      """Pizza:    {name}   Base:      Base:
\t{base}\t\t\t:{baseprice:   .2f}      \t{base}\t\t\t:{baseprice:   .2f}
Toppings:      Toppings:
{toppings}      {toppings}
Total:\t{total:   .2f}      Total:\t{total:   .2f}   >
>{veggie}
"""   .format(      """   .format(
name=p.name,                      name=p   .name,
base=p.base.name,                   base=p.base   .name,
baseprice=p.base.price,                     baseprice=p.base   .price,
toppings="\n"   .join(["\t{}\t\t\t:{:   .2f}"   .format(t.name,      t   .   toppings="\n"   .join(["\t{}\t\t\t:{:   .2f}"   .format(t.name,      t   .
for      t      in      p.toppings]),                                                                                                                                             for      t      in      p.toppings])   total=      pizza_price(p)                                          |                              total=pizza_price(p),
>                        veggie="Is      Vegetarian"      if      pizza_veggie(p)      else    "Is      Not      Ve   >)
>
>base      =      {
>                   "thin":      Base(name="Thin",      price=1.20),
>                   "thick":      Base(name="Thick",      price=1.50),
>                   "stuffed":      Base(name="Stuffed    Crust      Monstrosity",      price=2   >}
>
>topping      =      {
>                   "olive":      Topping(name="Olive",      price=0.70),
>                        "garlic":      Topping(name="Garlic",      price=0.70),
>                   "asparagus":    Topping(name="Asparagus",    price=1.20),
>                   "mozzarella":    Topping(name="Mozzarella",      price=0.70),   >                   "scamorza":    Topping(name="Scamorza",    price=1.00),
>                   "tomato":    Topping(name="Tomato",    price=0.90),
>                   "speck":    Topping(name="Speck",    price=2.00,      veggie=False),   >}
>   >
>##      Nearly      a      Marghertisa   >margherita      =      Pizza      (
>                     name="Margherta",         >                     base=base["thin"],   >                   toppings=[
>                                     topping["tomato"],
>                                     topping["mozzarella"]
>                        ]   )      )
p      =      Pizza      (                                          |      with_speck      =      Pizza      (
name="SimplePizza",                                    |                            name="Margherta      with      Speck",
base=Base(name="Thin",      price=1.20),                               |                         base=base["thin"],   toppings=[                              toppings=[
Topping("Olive",      price=0.70),                            |                                           topping["tomato"],
Topping("Garlic",      price=0.70)                                  |                                           topping["mozzarella"],
>                                             topping["speck"]
]                              ]   )      )
print(pizza_report(p))                                          |
>print(pizza_report(margherita))   >print(pizza_report(with_speck))
Pizza: Iteration 3 
import      collections
Base      =      collections.namedtuple(   "Base"   ,    "name      price")
Topping      =      collections.namedtuple(   "Topping"   ,    "name      price      veggie",      defaults=[True])   Pizza      =      collections.namedtuple(   "Pizza"   ,    "name      base      toppings")
def pizza_price(p):
return p.base   .price      +      sum(t.price for t in p.toppings)
def pizza_veggie(p):
return all(t.veggie for t in p.toppings)
def pizza_report(p):
return """Pizza:    {name}   Base:
\t{base}\t\t\t:{baseprice:.2f}
Toppings:         {toppings}
Total:\t{total:.2f}
{veggie}
"""   .format(
name=p   .name,
base=p.base   .name,
baseprice=p.base   .price,
toppings="\n"   .join(["\t{}\t\t\t:{:   .2f}"   .format(t.name,      t.price) for t in p.toppings]),
total=pizza_price(p),
veggie=   "Is      Vegetarian" if pizza_veggie(p) else "Is      Not      Vegetarian"   )
base      =      {
"thin"   :      Base(name=   "Thin",      price=1.20),               "thick"   :      Base(name=   "Thick",      price=1.50),
"stuffed"   :      Base(name="Stuffed      Crust      Monstrosity",      price=2.50)   }
topping      =      {
"olive"   :      Topping(name="Olive",      price=0.70),               "garlic"   :      Topping(name="Garlic",      price=0.70),
"asparagus"   :      Topping(name="Asparagus",      price=1.20),               "mozzarella"   :      Topping(name="Mozzarella",      price=0.70),   "scamorza"   :      Topping(name="Scamorza",      price=1.00),
"tomato"   :      Topping(name="Tomato",      price=0.90),
"speck"   :      Topping(name="Speck",      price=2.00,      veggie=False),   }
## Nearly    a Marghertisa 
margherita    =      Pizza      (               name=   "Margherta"   ,         base=base["thin"],   toppings=[
topping[   "tomato"],
topping[   "mozzarella"]
]   )
with_speck      =      Pizza      (
name=   "Margherta      with    Speck"   ,   base=base["thin"],
toppings=[
topping[   "tomato"],
topping[   "mozzarella"],   topping["speck"]
]   )
print(pizza_report(margherita))   print(pizza_report(with_speck))
Pizza:      Margherta   Base:
Thin      :1   .20
Toppings:
Tomato      :0   .90
Mozzarella      :0   .70
Total:      2   .80
Is      Vegetarian
Pizza:      Margherta      with      Speck   Base:
Thin      :1   .20
Toppings:
Tomato      :0   .90
Mozzarella      :0   .70
Speck      :2   .00   Total:      4.80
Is      Not      Vegetarian
Pizza: Future Work 
•      Proper   test   suite
•   And   Price   report   structure
•   Add   VAT
•      Report output   a   bit   clunky
•      Move   pizza_price/veggie/report   to   be   methods
Thoughts 
•    Module   is   now   five   years   old
•   Taught   differently   every   year!
•   Welcome   feedback   on   how   well   it   worked
– Especially   combined   online/in   person   lecture   material
Thoughts 
•      Hope   that   I   have   introduced   you   to   software   engineering   culture
•   You   have   touched   on   a   lot   of topics
•   They   will   take   a   long   time   to   master
Thoughts 
•      Hope   that   you   have   enjoyed   the   material
•    Good   luck   and   enjoy   the   rest   of the   module







         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
