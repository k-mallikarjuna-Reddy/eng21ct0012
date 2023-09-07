import Control.Monad.Reader

-- Define the environment (input) for the reader computation
data Env = Env { userName :: String }

-- Define the reader computation type
type GreetingReader a = Reader Env a

-- Function to generate a personalized greeting
greetUser :: GreetingReader String
greetUser = do
    name <- asks userName
    return $ "Hello, " ++ name ++ "! Welcome!"

-- Main function to demonstrate the reader monad for personalized greetings
main :: IO ()
main = do
    putStrLn "Enter your name:"
    name <- getLine
    let env = Env { userName = name }
    let greeting = runReader greetUser env
    putStrLn greeting