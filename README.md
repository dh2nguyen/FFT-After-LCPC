# Note: This script is meant to be used for the data produced by the "LCPC Transform". However, it can be used to do the Fast Fourier Transform on any appropriate data. Just change the column names according to the instructions in the below "ReadMe" section. 

# Script for Fast Fourier Transform (FFT) 
# By David H. Nguyen, PhD www.TSG-Lab.org

#######
# Start of Readme Info

                  ###### How to Format the Data #######

# 1. The input file should have a column called "summedDistance", which is
#    the column that contains the lcpc distances.
# 2. The input file should have a column called "angle", which is 
#    the column that contains the angle measures of the LCPC grid system.
# 3. There should be no missing items in the "angle" and "summedDistance" columns.
# 4. There should only be numbers in the "angle" and "summedDistance" columns.
# 5. The script produces a .csv file called "fft_data.csv".
#
# You will have to type in the name of your file in Step 1.
# 
# End of ReadMe Info

#######

# Required Packages
install.packages("TSA")
library(TSA)

###### 

# Step 1 - Type in the name of your input file.
df = read.csv("sampleOutput_lcpc_data.csv")

# Step 2
the.data = df[, c('angle', 'summedDistance')]

p = periodogram(the.data$summedDistance)

show.table = data.frame(freq=p$freq, spec=p$spec)

sort.spec = show.table[order(-show.table$spec),]

# Step 3
write.csv(sort.spec, "fft_data.csv", row.names = F)


