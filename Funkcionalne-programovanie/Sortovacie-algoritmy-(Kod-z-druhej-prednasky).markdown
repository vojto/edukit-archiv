# Sortovacie algoritmy

    -- Insertion Sort --
    --------------------

    isort xs = foldr insert [] xs
      where
        insert x []                 = [x]
        insert x (y:ys) | x < y     = x:y:ys
                        | otherwise = y:insert x ys

    -- Merge Sort--
    ---------------

    merge [] ys = ys
    merge (x:xs) [] = x:xs
    merge (x:xs) (y:ys) | x <= y    = x : (merge xs (y:ys))
                        | otherwise = y : (merge (x:xs) ys)

    msort xs  | n <= 1 = xs
              | otherwise = merge (msort us) (msort vs)
                where
                  n = length xs
                  us = take (n `div` 2) xs
                  vs = drop (n `div` 2) xs

    -- QuickSort --
    ---------------

    qsort []      = []
    qsort (x:xs)  = qsort [u | u <- xs, u <= x]
                    ++ [x] ++
                    qsort [v | v <- xs, v > x]