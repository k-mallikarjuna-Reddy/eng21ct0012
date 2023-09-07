import Control.Monad.Writer
logOperation :: String -> Int -> Writer [String] Int
logOperation message value = writer (value, [message])
mainComputation :: Writer [String] Int
mainComputation = do
    x <- logOperation "Starting computation" 0
    y <- logOperation "Adding 5" (x + 5)
    z <- logOperation "Subtracting 3" (y - 3)
    return z

main :: IO ()
main = do
    let (result, logMessages) = runWriter mainComputation
    putStrLn $ "Final Result: " ++ show result
    putStrLn "Log Messages:"
    mapM_ putStrLn logMessages