evenNumbers :: [Int]
evenNumbers = [0,2..]

main :: IO ()
main = do
    print $ take 10 evenNumbers