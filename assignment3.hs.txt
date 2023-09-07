import Control.Exception (catch, SomeException)
import System.IO (readFile)

main :: IO ()
main = do
    result <- readAndSumNumbers "numbers.txt"
    case result of
        Left err -> putStrLn err
        Right totalSum -> putStrLn $ "Sum of the numbers: " ++ show totalSum

readAndSumNumbers :: FilePath -> IO (Either String Double)
readAndSumNumbers filename = do
    content <- catch (readFile filename) handleReadError
    let numbers = map readNumber (lines content)
    case sequence numbers of
        Left err -> return $ Left err
        Right nums -> return $ Right (sum nums)

readNumber :: String -> Either String Double
readNumber str =
    case reads str of
        [(num, "")] -> Right num
        _ -> Left $ "Non-numeric input found: " ++ str

handleReadError :: SomeException -> IO String
handleReadError _ = return "The file 'numbers.txt' was not found."