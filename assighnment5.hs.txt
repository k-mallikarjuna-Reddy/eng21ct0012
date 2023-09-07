sumOfNaturalNumbers :: Int -> Int
sumOfNaturalNumbers 0 = 0  
sumOfNaturalNumbers n = n + sumOfNaturalNumbers (n - 1)  

main :: IO ()
main = do
    let n = 6
    let result = sumOfNaturalNumbers n
    putStrLn $ "Sum of the first " ++ show n ++ " natural numbers: " ++ show result