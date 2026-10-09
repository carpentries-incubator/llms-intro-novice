---
title: 'Large Language Models'
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What does a large language model do?
- How is a large language model developed?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

After this episode, learners will be able to:

- Summarise how a language model produces output based on its training data and conditioning.

::::::::::::::::::::::::::::::::::::::::::::::::

## Advanced Pattern Matching 
FFFFFFS

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::


# Reprex: daemon server with re-entrant save loop
# documentSaveAll() saves files → watcher detects change → calls handler again                                                    
library(httpuv)                                                                                                                   
                                                                                                                                 
tmpdir <- tempfile("reprex")                                                                                                      
dir.create(tmpdir)
writeLines("hello", file.path(tmpdir, "test.txt"))                                                                                
               
# Open the file in Positron so documentSaveAll has something to save                                                              
rstudioapi::navigateToFile(file.path(tmpdir, "test.txt"))
                                                                                                                                 
call_count <- 0L
s <- startDaemonizedServer("127.0.0.1", 9996, list(                                                                               
   onWSOpen = function(ws) {                                                                                                       
   ws$onMessage(function(binary, message) {
      call_count <<- call_count + 1L                                                                                              
      message("Handler call #", call_count)
      if (call_count > 5) {                                                                                                       
         message("Stopping after 5 calls")
         ws$send("stop")                                                                                                           
         return()
      }                                                                                                                           
      tryCatch( 
         rstudioapi::documentSaveAll(),
         error = function(e) message("ERROR: ", conditionMessage(e))
      )
      ws$send("ok")                                                                                                               
   })
   }                                                                                                                               
))              

message("Server on 9996. Trigger with:")                                                                                          
message("  websocket::WebSocket$new('ws://127.0.0.1:9996')$onOpen(function(e) e$target$send('go'))")                                                           


