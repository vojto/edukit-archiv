Tu by sa mohli pridavat jednotlive zadania, tak kto uz ma urobene, sem snimi:


    **********Okruh 1:**********
    -----------------------------
    1.
    numbersCount :: Num a => [Char]-> a
    numbersCount str = length'[c|c<-str,isDigit c]
    length' xs = sum [1 | _ <- xs] 
    -----------------------------
    2.
    transform :: [Char] -> Int  
    transform xs = sum [ (ord (xs !! i) - 48)*2^((length xs-1)- i) | i <- [0..(length xs-1)] ]
    -----------------------------
    3. (poznamka: pri vstupe inom, ako cislic vyhodi chybu, vstupom maju byt cisla v uvodzovkach, pred cislom moze byt + alebo -)
    atoi :: [Char] -> Int
    atoi (x:xs) | x == '+' = read xs :: Int
                | otherwise = read (x:xs) :: Int
    -----------------------------
    4.
    smallAndOther2 :: [Char] -> ([Char],[Char])
    smallAndOther2 str = ([x|x<-str,isLower x],[y|y<-str,not(isLower y)])
    smallAndOther1 str = (filter isLower str, filter oth str)
	where oth str = not(isLower str)
    -----------------------------
    5.
    isPrime :: Int -> Bool
    isPrime x = null [y | y<-[2..floor (sqrt (fromIntegral x))], x `mod` y == 0]

    primeFilter1 xs = filter (isPrime) xs
    primeFilter2 xs = [x | x <- xs, isPrime x == True ]
    -----------------------------
    6.
    primeGenerator :: Int -> [Int]
    primeGenerator n = take n primes 
          where primes = sieve [2..]
                sieve (x:xs) = x : sieve[p | p <- xs, p `mod` x /= 0]
    -----------------------------
    7.
    intToBin :: Int -> [Int]
    intToBin x | x <= 0 = []
                     | otherwise = intToBin (div x 2) ++ [(mod x 2)]

    binToString :: [Int] -> [Char]
    binToString [] = []
    binToString xs = map (chr) $  map (+48) xs
    -----------------------------
    8. (poznamka: pri vstupe inom, ako hexa vyhodi chybu, vstup ma byt HEXA v uvodzovkach, nic ine)
    htoi :: [Char] -> Int
    htoi (x:xs) = foldl make 0 (x:xs)
        where make x y | elem y ['A'..'F'] = x * 16 + (ord y) - 55
                       | elem y ['0'..'9'] = x * 16 + (ord y) - 48
    -----------------------------
    9. (obmedzenia: program funguje iba pre to, ako to je zadane, teda pre 2 zoznamy oddelene nulou, pre viac zoznamov ich oddeluje posledna nula)
    groups :: [Int] -> [Int]
    groups xs = zero (foldl make [] (foldl make [] xs))
        where make xs y | y == 0 = 0 : (foldl (+) 0 xs) : []
                        | otherwise = y:xs
              zero (x:y:xs) = x : xs
    -----------------------------
    **********Okruh 2:**********
    -----------------------------
    1. mergesort
    mergeSort f xs = f xs
   
    mergeDesc xs = reverse (mergeAsc xs)
    mergeAsc [] = []
    mergeAsc [x] = [x]
    mergeAsc xs = merge (mergeAsc top) (mergeAsc bottom)
         where (top, bottom) = splitAt (length xs `div` 2) xs
   
    merge [] ys = ys
    merge xs [] = xs
    merge (x:xs) (y:ys) | x <= y    = x : merge xs (y:ys)
                                | otherwise = y : merge (x:xs) ys
     -----------------------------
     3. (obmedzenia: ziadne, len naprat hodnoty :))
     selectSort :: Ord a => [a] -> [a]
     selectSort (x:xs) | xs == [] = x:[]
                       | x <= minimum xs = x : selectSort xs
                       | otherwise = selectSort (xs ++ x:[])
     -----------------------------
     5.
     bubbleSort xs = iterate sort xs!! (length xs - 1) 
     sort [x] = [x] 
     sort (x:y:zs) 	| x> y = y: sort (x:zs) 
		| otherwise = x: sort (y:zs) 
     -----------------------------

     7. (poznamka: su tam nejake povkladane zaciatocne udaje v databaze, pomente si ich dajak, diky...)
     type HashedPassword = Int
     type PassDB = [(String, HashedPassword)]
     db :: PassDB
     db = [("Matus",258724081),("Mattias",17496271),("Konkol",914711)]
     login :: PassDB -> String -> String -> Bool
     login [] x y = False
     login (d:db) x y | (fst d == x) && (snd d == foldl code 0 y) = True
                      | otherwise = login db x y
         where code x y = x * 20 + ord y
     addPassword :: (String,String) -> PassDB -> PassDB
     addPassword (x,y) db = (x,foldl code 0 y):db
         where code x y = x * 20 + ord y
     -----------------------------
     6.
     diamant x | odd x == True = putStr (kresli1 (((div x 2) + 1), 1) 1 x)
               | otherwise = putStr (kresli2 ((div x 2), 2) 1 x)
   
      where kresli1 (x,y) c d | c < ((div d 2) + 1) = ((take x (repeat ' ')) ++ (take y (repeat '*')) ++ ("\n") ++ kresli1 ((x-1), (y+2)) (c+1) d)
                              | c == d = ((take x (repeat ' ')) ++ (take y (repeat '*')) ++ ("\n"))
                              | c >= ((div d 2) + 1) = ((take x (repeat ' ')) ++ (take y (repeat '*')) ++ ("\n") ++ kresli1 ((x+1), (y-2)) (c+1) d)
   
            kresli2 (x,y) c d | c < (div d 2) = ((take x (repeat ' ')) ++ (take y (repeat '*')) ++ ("\n") ++ kresli2 ((x-1), (y+2)) (c+1) d)
                              | c == (div d 2) = ((take x (repeat ' ')) ++ (take y (repeat '*')) ++ ("\n\
                                \") ++ (take x (repeat ' ')) ++ (take y (repeat '*')) ++ ("\n") ++ kresli2 ((x+1), (y-2)) (c+1) d)
                              | c == d = ((take x (repeat ' ')) ++ (take y (repeat '*')) ++ ("\n"))
                              | c > (div d 2) = ((take x (repeat ' ')) ++ (take y (repeat '*')) ++ ("\n") ++ kresli2 ((x+1), (y-2)) (c+1) d)
   
     -----------------------------
     **********Okruh 3:**********
     -----------------------------
     1.
     format vstup pocet | length vstup < pocet = 
	                             unwords ( fill ( number vstup pocet ) ( words vstup ) ) ++
	                             ( replicate ( number2 vstup pocet )  '.' )
	                  | otherwise = vstup

     number xs ys = ( ys - length xs ) `div` ( length ( words xs ) )
     number2 xs ys = ( ys - length xs ) `mod` ( length ( words xs ) )

     fill y [] = []
     fill y ( x : xs ) = ( x ++ ( replicate y '.' ) ) : ( fill y xs )
     -----------------------------
       2.
       putStick [] y = []
       putStick (x:xs) y | x >= y = "|" ++ putStick xs y
                                | otherwise = " " ++ putStick xs y
       hist xs max | max > 0 = putStick xs max ++ "\n" ++ hist xs (max - 1)
                       | otherwise = ""
       histogram xs = putStr(hist xs (maximum xs))
    -----------------------------
     4. (jedina chybicka krasy: nefunguje to spravne pre rok 2000, ale sa mi s tym uz hrat nechcelo a cviciacehmu to ani nenapadlo :)) )
     data Date = Date Int Int Int -- Year, Month, Day
     data Sex = Male | Female deriving Eq


     rc r m d s = (r `mod` 100)*10000 + m*100 + d + (pohlavie s)

     pohlavie s | (s == Male) = 0
                      | otherwise = 5000

     rodc r m d s = [(rc (r `mod` 100) m d s)*10000 + o | o <- [0..9999], ((rc (r `mod` 100) m d s)*10000 + o) `mod` 11 == 0]

     lomitko n = first ++ '/':second
       where
         s = show n
         (first,second) = splitAt 6 s

     lomitko2 n = '0':first ++ '/':second
       where
         s = show n
         (first,second) = splitAt 5 s


     rodnecislo r m d s | ((r `mod` 100)>9) = map lomitko (rodc (r `mod` 100) m d s)
          	                  | otherwise = map lomitko2 (rodc (r `mod` 100) m d s)   
    -----------------------------
     5.
     import Random
  
     randNumber :: StdGen -> Integer -> Integer -> Integer 
     randNumber gen a b = fst (randomR (a, b) gen)
  
     main a b = getStdGen >>= (\gen -> guessTheNumber gen a b)
  
     guessTheNumber gen a b = putStr ("\nV tejto hre si A vymysli cele cislo od " ++ show a ++ " do " ++ show b ++ " a B bude hadat.\n\n\
                                       \A: Myslim si cislo " ++ show (randNumber gen a b) ++ ". B o tom nevie :)\n\n\
                                       \" ++ pokracuj (randNumber gen a b) ((div (div (a + b) 2) 10) * 10) ((div (a+b) 2) + (mod (a+b) 2)))
         where pokracuj x c z | x /= c = ("B: Je tvoje cislo vacsie ako " ++ show c ++ "?\n" ++ check x c z)
                              | otherwise = ("B: Je to cislo " ++ show c ++ "?\n" ++ check x c z)
               check x c z | x == c = "Bingo!!!"
                           | (x > c) = ("A: Ano.\n" ++ pokracuj x (c + ((div z 2) + (mod z 2))) ((div z 2) + (mod z 2)))
                           | (x < c) = ("A: Nie.\n" ++ pokracuj x (c - ((div z 2) + (mod z 2))) ((div z 2) + (mod z 2)))
     -----------------------------
       8.
     data Unit = UG | MG deriving (Show,Eq) {- Microgram & Miligram -}
     type Drug = (DrugID,Unit,UnitAmount,Rule,Prescription)
     type DrugID = [Char]
     type UnitAmount = Float
     type Rule = (Price,Compensation)
     type Prescription = Bool
     type Price = Float
     type Compensation = Float
     type DrugRequest = (DrugID,Unit,UnitAmount,Prescription,PackAmount)
     type PackAmount = Int
     type Patient = [Char]
     type ToPay = Float
     
     lineLength :: Int
     lineLength = 45
  
     drugDB :: [Drug]
     drugDB = [("Celaskon",MG,10*500,(1.56,0.00),False),("Celaskon",MG,20*500,(2.85,0.00),False),("Celaskon",MG,30*500,(3.41,0.00),False),("Euthyrox",UG,100*25,(2.34,2.34),True),("Euthyrox",UG,100*50,(2.34,2.34),True),("Euthyrox",UG,100*75,(3.02,3.02),True),("Euthyrox",UG,100*100,(3.44,3.44),True),("Euthyrox",UG,100*125,(3.85,3.85),True),("Euthyrox",UG,100*150,(4.24,4.24),True),("Euthyrox",UG,100*200,(8.28,5.76),True),("Alerid",MG,10*10,(1.67,0.86),True),("Alerid",MG,20*10,(2.88,1.73),True),("Alerid",MG,50*10,(6.99,4.32),True),("Alerid",MG,100*10,(13.24,8.43),True),("VentolinInhaler",UG,200*100,(3.02,3.02),True),("Zodac",MG,10*10,(1.70,0.86),True),("Zodac",MG,30*10,(4.65,2.59),True),("Zodac",MG,60*10,(9.08,5.18),True),("Zodac",MG,100*10,(15.18,0.00),True),("Ibalgin",MG,30*200,(1.79,0.00),False),("Ibalgin",MG,30*400,(2.51,0.00),False),("Ibalgin",MG,100*400,(5.80,2.21),True),("Ibalgin",MG,100*600,(7.58,0.00),True),("Tritazide",MG,70,(5.42,3.30),True),("Tritazide",MG,28*5,(6.64,5.40),True)]

    patientDB :: [(Patient,[DrugRequest])]
    patientDB = [("Jan Hrach",[("Celaskon",MG,30*500,False,3)]),("Jozef Mrkva",[("Euthyrox",UG,100*125,True,1)]),("Anna Mala",[("Ventolin Inhaler",UG,200*100,True,1),("Ibalgin",MG,30*200,False,1)]),("Jan Poleno",[("Zodac",MG,10*10,False,1),("Ibalgin",MG,30*400,False,2),("Alerid",MG,10*10,True,2)]),("Chuck Norris",[("Chuck Norris",UG,0*0,False,8)])]

    processPatList :: [(Patient,[DrugRequest])] -> [(Patient,[(DrugID,Unit,UnitAmount)],ToPay)]
    processPatList patient = map check patient
           where check (x,list@((_,_,_,_,y):ys)) = (x,(checkDrug list),(countPay (checkDrug list) (fromIntegral y)))
                 checkDrug [] = []
                 checkDrug (drug@(drugID,unit,unitAmount,prescription,packAmount):xs) | searchDrug drug = (drugID,unit,unitAmount):(checkDrug xs)
                                                                                      | otherwise = checkDrug xs
                 searchDrug (drugID,unit,unitAmount,prescription,packAmount) | vlastnyElem (drugID,unit,unitAmount,prescription) drugDB = True
                                                                             | otherwise = False
                 countPay [] _ = 0
                 countPay (x:xs) y = price x drugDB y + countPay xs y
                 price _ [] _ = 0
                 price (drugID,unit,unitAmount) ((drugID',unit',unitAmount',(price',compensation'),prescription'):xs) y | (drugID == drugID') && (unit == unit') && (unitAmount == unitAmount') && prescription' = ((price' - compensation') * y) + 0.17
                                                                                                                        | (drugID == drugID') && (unit == unit') && (unitAmount == unitAmount') = ((price' - compensation') * y)
                                                                                                                        | otherwise = price (drugID,unit,unitAmount) xs y
                 vlastnyElem _ [] = False
                 vlastnyElem (drugID,unit,unitAmount,prescription) ((drugID',unit',unitAmount',rule',prescription'):xs) | (drugID == drugID') && (unit == unit') && (unitAmount == unitAmount') && ((prescription == prescription') || prescription) = True
                                                                                                                        | otherwise = vlastnyElem (drugID,unit,unitAmount,prescription) xs

    unitConversion :: (Unit,UnitAmount) -> (Unit,UnitAmount)
    unitConversion (x,y) | show x == "UG" = (MG,(y / 1000))
                         | otherwise = (x,y)

    vypisNespracovane :: IO()
    vypisNespracovane = putStr(concat (map vypisuj patientDB))
            where vypisuj (x,y) = (mojShow x ++ ":\n" ++ concat (map vypisZvysok y))
                  vypisZvysok x = (vypisZaciatok x ++ vypisMedzery (vypisZaciatok x) (vypisKoniec x) ++ vypisKoniec x)
                  vypisZaciatok (drugID,unit,unitAmount,_,_) = ("   " ++ mojShow drugID ++ " (" ++ show unitAmount ++ " " ++ show unit ++ "):")
                  vypisKoniec (_,_,_,prescription,packAmount) | prescription = (show packAmount ++ " pkgs (P)\n")
                                                              | otherwise = (show packAmount ++ " pkgs    \n")
                  vypisMedzery x y | (lineLength - (length x) - (length y)) < 0 = " "
                                   | otherwise = take (lineLength - (length x) - (length y) + 1) (repeat ' ')
                  mojShow [] = []
                  mojShow (x:xs) = x:(mojShow xs)
 
    vypisVyhodnotene :: IO()
    vypisVyhodnotene = putStr(concat (map vypisuj (processPatList patientDB)))
            where vypisuj (patient,lieky,toPay) = (mojShow patient ++ ":\n" ++ concat (map vypisLieky lieky) ++ vypisZvysok toPay)
                  vypisLieky (drugID,unit,unitAmount) = (mojShow drugID ++ " (" ++ show (fst (unitConversion (unit,unitAmount))) ++ " " ++ show (snd (unitConversion (unit,unitAmount))) ++ ")\n")
                  vypisZvysok x = ("Total:" ++ take (lineLength - 6 - (length (show x))) (repeat ' ') ++ show x ++ "\n")
                  mojShow [] = []
                  mojShow (x:xs) = x:(mojShow xs)
    -----------------------------
    **********Okruh 4:**********

    -----------------------------
    2.
    separator = ["","/","-","->"]

    type IDNumber = String

    persons :: [IDNumber]
    persons = ["850228/7772","846224/7772","846224777","12345->123","850228->6666","123456->>123","880230-8889"]

    rodneCislo :: [IDNumber] -> [Bool] 
    rodneCislo xs | xs == [] = []
                         | otherwise = map check xs
       where check xs | ((length xs) == 11) && (cisla (take 6 xs) == True) && (elem ((xs !! 6):[]) separator) && (cisla (drop 7 xs) == True) = True
                      | ((length xs) == 12) && (cisla (take 6 xs) == True) && (elem ((xs !! 6):(xs !! 7):[]) separator) && (cisla (drop 8 xs) == True) = True
                      | ((length xs) == 10) && ((cisla xs) == True) = True
                      | otherwise = False
             cisla [] = True
             cisla (x:xs) | isDigit x = cisla xs
                              | otherwise = False


     4.
    data Currency = EUR deriving Show {- Currency -}
    data Customer = Student Name | Teacher Name deriving Show {- Customer -}
    type Name = String {- Name of customer -}
    type Meal = (MealID,Price,Bool) {- Meal -}
    type MealID = String {-Meal ID -}
    type Price = (Fee,Currency) {- Price -}
    type Fee = Float {- Fee -}
    type Purchase = (Customer,[MealID],Price,Dotation) {- Purchase -}
    type Order = (Customer,[MealID]) {- Order -}
    type Dotation = Price {- Dotation -}
    -- Database of meals
    meals :: [Meal]
    meals = [("Chicken soup",(0.50,EUR),True),("Potatoe soup",(0.45,EUR),True),("Tomatoe soup",(0.45,EUR),False),("Vegetable soup",(0.45,EUR),False),("Chicken nuggets",(1.70,EUR),True),("Chicken cutlet",(1.70,EUR),False),("Beef steak",(1.80,EUR),True),("Pork steak",(1.80,EUR),False),("Fried fish",(1.65,EUR),True),("Fried cheese",(1.65,EUR),True),("Lasagna",(1.60,EUR),False),("Spaghetti Bolognese",(1.55,EUR),True),("Steamed buns",(2.00,EUR),True),("Serbian tofu",(1.50,EUR),False),("Rice",(0.45,EUR),True),("French fries",(0.80,EUR),True)]
    -- Input with customers’ orders
    orders :: [Order]
    orders =[(Student "Jan Hrach",["Chicken soup","Beef steak","Mashed potatoes","Pudding"]),(Teacher "Anna Mrkvova",["Potatoe soup","Fried fish","Steamed vegetables","Ice Fruit"]),(Student "Janko Polienko",["Tomatoe soup","Fried cheese","French fries","Coca-Cola"])]
    -- Line length
    lineLength :: Int
    lineLength = 70

    vypisTabulku = putStr(concat (map vypisZoznam meals))
           where vypisZoznam (x,(m,n),y) | y = x ++ " " ++ (take (lineLength - (length x) - (length (show n)) - (length (show m))  - 5) (repeat '.')) ++ " " ++ (show m) ++ " " ++   (show n) ++ " *\n"
		                               | otherwise = x ++ " " ++ (take (lineLength - (length x) - (length (show n)) - (length (show m))  - 5) (repeat '.')) ++ " " ++ (show m) ++ " " ++ (show n) ++ "\n"

    vypisObjednavky = putStr(concat (map vypisuj orders))
            where vypisuj x = (vypisZaciatok x) ++ " " ++ (take (lineLength - (length (vypisZaciatok x)) - (length (vypisKoniec x meals)) - 2) (repeat '.')) ++ " " ++ (vypisKoniec x   meals) ++ "\n" ++ vypisSpodok x meals ++ "\n"
               vypisZaciatok (Student x,_) = x ++ " (S)"
               vypisZaciatok (Teacher x,_) = x ++ " (T)"
               vypisKoniec (Student x,xs) ys = "Totals: " ++ (show (total xs ys)) ++ " EUR " ++ "(Dotation: " ++ (show (dotation (total xs ys) (Student x))) ++ " EUR)"
               vypisKoniec (Teacher x,xs) ys = "Totals: " ++ (show (total xs ys)) ++ " EUR " ++ "(Dotation: " ++ (show (dotation (total xs ys) (Teacher x))) ++ " EUR)"
               total [] _ = 0
               total (x:xs) [] = total xs meals
               total (x:xs) ((m,(k,l),n):ms) | x == m && n = k + (total xs meals)
			                                 | otherwise = total (x:xs) ms
               dotation x (Student y) | (x < 1.66) = 0
			                          | (x < 3.32) = 0.80
						        	  | (x > 3.32) = 1.6
               dotation x (Teacher y) | (x < 1) = 0
							          | (x < 2.7) = (x - 0.93)
							          | (x > 2.7) = (x - 0.93) + dotation (x - 2.7) (Teacher y)
               vypisSpodok (_,x) meals = (take (lineLength - length (concat (map vypisJedla (filtrujJedla x meals)))) (repeat '.')) ++ " " ++ (concat (map vypisJedla (filtrujJedla x meals)))
               vypisJedla x = x ++ ", "
               filtrujJedla [] _ = []
               filtrujJedla (x:xs) [] = filtrujJedla xs meals
               filtrujJedla (x:xs) ((m,(k,l),n):ms) | (x == m) && n = x : filtrujJedla xs meals
			                                        | otherwise = filtrujJedla (x:xs) ms
