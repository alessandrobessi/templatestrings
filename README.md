Template strings
================

Simple string substitution library that supports \"$\"-based
substitution.  Meant to be used when `Text.Printf` or string
concatenation would lead to code that is hard to read but when a full
blown templating system is overkill.

Usage example:
```
    {-# LANGUAGE OverloadedStrings #-}
    module Main where

    import qualified Data.ByteString.Lazy as S
    import qualified Data.Text as T
    import qualified Data.Text.Lazy.Encoding as E

    import Data.Text.Template

    -- | Create 'Context' from association list.
    context :: [(T.Text, T.Text)] -> Context
    context assocs x = maybe err id . lookup x $ assocs
      where err = error $ "Could not find key: " ++ T.unpack x

    main :: IO ()
    main = S.putStr $ E.encodeUtf8 $ substitute helloTemplate helloContext
      where
        helloTemplate = "Hello, $name!\n"
        helloContext  = context [("name", "Joe")]
```
