import Control.Monad.State

-- Define a stateful computation that represents the counter
type CounterState a = State Int a

-- Function to increment the counter
incrementCounter :: CounterState ()
incrementCounter = modify (+1)

-- Function to retrieve the counter value
getCounter :: CounterState Int
getCounter = get

-- Main function to demonstrate the counter using the State Monad
main :: IO ()
main = do
    let (result, finalState) = runState (incrementCounter >> incrementCounter >> getCounter) 0
    putStrLn $ "Final Counter Value: " ++ show result
    putStrLn $ "Final State: " ++ show finalState