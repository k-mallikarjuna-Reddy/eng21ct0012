data Shape = Circle Double   -- Circle constructor with radius
           | Rectangle Double Double  -- Rectangle constructor with width and height

instance Show Shape where
    show (Circle radius) = "Circle with radius " ++ show radius
    show (Rectangle width height) = "Rectangle with width " ++ show width ++ " and height " ++ show height
main :: IO ()
main = do
    let circle = Circle 5.0
        rectangle = Rectangle 4.0 6.0
    putStrLn $ show circle
    putStrLn $ show rectangle