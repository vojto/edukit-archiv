Vaclavik 7:30 : Prva : spravit funkciu pp kt spoji dva zoznamy , nieco ako (++) 
Druha : funkcia pocet znaku v retazci count a xs 

1. pp [] xy = xy
pp (x:xs) xy = pp xs reverse(x : reverse(xy))

2. count a xs = length ([x | x <- xs , x==a])

Vaclavik povedal ze syntax az tak nerozhoduje ide hlavne o myslienku
 