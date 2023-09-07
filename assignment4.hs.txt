import Control.Exception (try, SomeException)
import System.IO

main :: IO ()
main = do
    result <- try readAndSumNumbers :: IO (Either SomeException Double)
    case result of
        Left ex -> putStrLn $ "An error occurred: " ++ show ex
        Right totalSum -> do
            writeFile "sum.txt" (show totalSum ++ "\n")
            putStrLn "Sum written to 'sum.txt'."

readAndSumNumbers :: IO Double
readAndSumNumbers = do
    content <- readFile "numbers.txt"
    let numbers = map readNumber (lines content)
    case sequence numbers of
        Left _ -> error "Non-numeric input found."
        Right nums -> return $ sum nums

readNumber :: String -> Either String Double
readNumber str =
    case reads str of
        [(num, "")] -> Right num
        _ -> Left $ "Non-numeric input found: " ++ str