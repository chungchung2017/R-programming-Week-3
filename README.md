# R-programming-Week-3


#2 Finding the best hospital in a state


      
      best <- function(state, dataName) {
  
            ## Read outcome data
              data <- read.csv("outcome-of-care-measures.csv", colClasses = "character")
              states <- data$State
              cause <- c("heart attack","heart failure","pneumonia")
              ## Check that state and outcome are valid
                      ## if the state doesnt match the states
                         if (! state %in% states ){
                                           stop("invalid state")
                         } 
                      ## if the dataName cannot be found  
                         if (! dataName %in% cause){
                                                  stop("invalid outcome")
                         } 
              ## Return hospital name in that state with lowest 30-day death rate
              ## set up another index as col_id
              col_id <- 0
                        if (dataName == cause[1]){
                                                      col_id <- 11
                        } else if (dataName == cause[2]) {
                                                      col_id <- 17
                        } else if (dataName == cause[3]) {
                                                       col_id <- 23
                        }
                data.sub <- data[data[,7] == state, ]
                data.sub2 <- data.sub[,c(2,7,col_id)]
                data.sub3 <- data.sub2[data.sub2[,3]!="Not Available",]
                data.sub3[,3] <- as.numeric(data.sub3[,3])

                data2 <- data.sub3
                bestrow <- data2[data2[,3] == min(data2[,3]),]
                as.character(bestrow[1])

        }

