# Satpreet's R Quickstart Tutorial  
*Audience*: Programmers familiar with a dynamic programming language with an interactive command-line interpreter eg. [Python](www.python.org) or [Ruby](www.ruby-lang.org/‎)    

## What is R?  
* "*An environment for statistical computing and graphics*"  
* Functional, OO & Procedural Programming language  
* Fantastic collection (out-of-the-box) and repositories of statistical and machine-learning packages to operate on and visualize data  
* Python/MATLAB-like interactive programming environment and powerful data-analysis oriented data-structures  

### Installation  
* Mac/Windows: Get the installer from http://www.r-project.org
* Linux: `sudo yum install R` or `sudo apt-get r-base`  

## The R interactive programming environment  

### Getting help  
```help(mean)  
?mean #get help on the function 'mean' 
args(mean) #get arguments used with function  
example(mean) #get example of usage of fn.  
??plot #search for help pages for the function (or other) plot  
RSiteSearch("correlation") #search cran.r-project.com for this term  
vignette() #find code-snippet examples for function/packages etc.```   

### Objects  
```   
ls() #list variables in the workspace  
ls.str() #list string-summaries of variables  
rm(var) #remove/delete variable var from workspace  
q() #quit R  
.hiddenVar = 3  
ls(all.names=TRUE)  
rm(list=ls()```  

### Generic Functions  
```  
example(mean) #get example of usage of fn.  
mode(x)  
class(x)  
str(x) # string summary  
summary(x) # show 5-number summary
head(x) # first 5 elements  
tail(x) # last 5 elements```  
http://en.wikipedia.org/wiki/Five-number_summary


##  Data Types, mode & class  
* Data types are inferred, don't need to be specified  
* Mode: Physical type as which data is stored  
* Class: Abstract type, term from OOP, usu. implies associated attributes & methods exist

```#Types  
i = c(1, 2) #integer  
n = c(1.0, 2.5) #numeric  
m = c(T, F, T, F, F) #logical  
c = c('T', 'F') #character```  


```  
#Mode vs. Class  
d = as.Date('2010-01-01')  
mode(d) #numeric  
length(d) #1  
class(d) #Date```    

##  Data Structures  
From cran.r-project.org:  

* *vector*, which is a single entity consisting of an ordered collection of numbers.    
* *scalar*, vector with 1 element  
* *factors* provide compact ways to handle categorical data. See [Factors](http://cran.r-project.org/doc/manuals/R-intro.html#Factors)  
* *lists* are a general form of vector in which the various elements need not be  of the same type, and are often themselves vectors or lists. Lists  provide a convenient way to return the results of a statistical  computation. See [Lists](http://cran.r-project.org/doc/manuals/R-intro.html#Lists).  
* *matrices* or more generally *arrays* are multi-dimensional generalizations of vectors. In fact, they _are_ vectors that can be indexed by two or more indices and will be printed in special ways. See [Arrays and matrices](http://cran.r-project.org/doc/manuals/R-intro.html#Arrays-and-matrices).  
* *data.frames* are matrix-like structures, in which the columns can be of different types. 
    * Think of data frames as `data matrices' with one row per observational  unit but with (possibly) both numerical and categorical variables. 
    * Many experiments are best described by data frames: the treatments are  categorical but the response is numeric. See [Data frames](http://cran.r-project.org/doc/manuals/R-intro.html#Data-frames).  

### Vectors  
Properties:  

* Homogeneous  
* Indexed by position, names  
* Can be subset into sub-vectors  

```
#Vector creation  
z <- c(1,2,3)  
z[1]  
z[-1] # = z[2:3]  
z[c(1,3)]  
names(z)  
names(z) = c('one','two','three')  
z[1]  
z['one']  
z$one #ERR```  

```
#Creation shortcuts  
z <- c(1,2,3, 4, 5, 6, 7, 8)  
z = 1:8  
z = 9:1  
z = seq(from=1, to=9, by=3)  
z <- rep(pi, times=10)  
z <- rep(1:3, times=3)  
z <- numeric(5)  
z <- logical(5)```  
  
### Scalars  
Scalars are simply vectors with length 1, e.g. pi  
`x <- pi`

### Factors  
Properties:

* Are like vectors, but for categorical variables (Vector of enumerated values)  
* Compact storage: keeps track of unique values, called levels  

```
sizes = c('XS', 'S', 'M', 'L', 'XL', 'XXL')  
f = as.factor(rep(sizes, times=10)) #Forces creation of factor (compact storage)  
class(sizes)  
mode(sizes)  
class(f)  
mode(f) # Note 'numeric' mode  
sort(f) # Sort by levels  
mean(f) #NA, not meaningful  
sum(f) #ERROR, not meaningful```  

### Lists  
Properties  

* Heterogeneous, collection of R objects.  
* Indexed by position, or by name, or by key  
* Can be subset into sub-lists  
  
### Matrices & Arrays  
Properties  

* Can be heterogeneous, but usually homogeneous & integer/numeric  
* Can convert lists & vectors into Arrays  
* Matrix \--> Array with 2-dimensions  
  
```
#Create by re-dimensioning vectors/lists  
v = 1:10  
dim(v) = c(2,5)  
print(v) #Note 'fill-by-columns'  
nrow(v) #2  
ncol(v) #5```   

```
#Create by binding vectors/lists  
a = 1:3  
b = 4:6  
c = cbind(a,b) # Bind-as-columns  
d = rbind(a,b) #Bind-as-rows  
dim(c) #3 rows x 2 columns  
dim(d) #2 rows x 3 columns```  

```
#Create using matrix() function  
z = matrix( c(......), nrow=3 )  
z = matrix( c(......), ncol=2, byrow=T )```

```
#Matrix operations  
t(c)     # transpose  
solve(z)    # inverse  
c * c    # componentwise multiplication  
c %*% d  # matrix multiplication```    

### Data Frame  
Notes:  

* Equivalent to Excel-Worksheets or SQL-tables  
* Can be regarded of list of vectors and/or factors (as columns)  
* All columns of same length  
  
```
# Creating & Indexing  
v1 = 1:5  
v2 = c(T,T,F,F,T)  
df = data.frame(v1,v2)  
df[1,] #Row 1  
df[,1] #Column 1  
names(df) = c('id', 'value')  
df$id #Index by col-name  
df2 <- edit(df) #data.frame editor interface```  

```
# Import data frame from file/URL  
goodf = read.table("http://satsingh.myserver.com/good.tsv", sep="\t", header=TRUE)  
badf = read.table("http://satsingh.myserver.com/bad.tsv", sep="\t", header=TRUE, fill=TRUE)  

# Export data frame to file  
write.table(badf, file="fixed.csv", sep=",",row.names=FALSE)```

```
# More data.frame operations  
df = goodf  
summary(df)  
head(df)  
tail(df)  
ncol(df)  
nrow(df)  
df = df[order(-df$nimp)] #Sort by column, descending order  
#Select rows, based on expression  
df[df$nimp > 0,] 
#Create new derived column  
raw = raw[,-match("X", names(raw))] #Remove column X```  

### Packages  
```  
library() # list installed packages  
install.packages("nortest") # install the package 'nortest' 
install.packages("nortest", repos="http://cran.r-project.org") #specify repo  
remove.packages("nortest")  
update.packages()  
library(nortest) #load the nortest package  
help(package=nortest) #get help on the package  
vignette(package='nortest') #code-snippets and usage info.```  

#### Local package installation (if you do not have sudo access) 
```  
mkdir -p ~/R/libs #make a local directory for simplifying package installs 
echo 'R_LIBS_USER="~/R/libs"' >  $HOME/.Renviron  
install.packages("nortest",lib="~/R/libs", repos="http://cran.r-project.org")```  
More info:

* http://cran.r-project.org/doc/manuals/R-admin.html#Installing-packages 
* http://csg.sph.umich.edu/docs/R/localpackages.html    

#### Install from package source  
```
#On machine with internet connection:  
wget http://cran.r-project.org/src/contrib/Hmisc_3.9-3.tar.gz #get package from web (on a machine with internet) 
scp Hmisc_3.9-3.tar.gz myserver.com:~ #copy to edge node/destination machine    

#On destination-machine in shell:  
mkdir -p ~/R/libs  
echo 'R_LIBS_USER="~/R/libs"' >  $HOME/.Renviron    

#On destination-machine, in R:  
install.packages("Hmisc_3.9-3.tar.gz",lib="~/R/libs", repos=NULL) #install  
library("Hmisc",lib.loc="~/R/libs") #load library for this session```  

## Graphics  
Basic Graphics  

* High level functions: Create a new plot & initialize axes, labels, titles etc.  
* Low-level functions: Adds features (color, lines, legends...) to existing plot  
* Package: graphics (standard), lattice (alternative), zoo (time-series), ggplot (high-q: Grammar-of-Graphics)  
  
### Scatterplots  
```
r = runif(1000) # return 1k uniformly distrib. rand. no. in range [0-1]  
n = rnorm(1000) # return 1k normally distrib. rand. no. with mean 0, sd 1  
mean(n)  
sd(n)  
plot( r )  
plot( n )  
plot( sort(r) )  
plot( sort(n) )  
grid() #add a grid to the graph```  

### Histograms  
```
hist( r )  
hist( n )  
hist(n, breaks=length(n)/10) #Specify no. of histogram bins  
hist(n, main="Histogram for Normal Distribution ", xlab="(Normal) Random Variable" )```  

### Line chart  
```
df = read.table("http://satsingh.myserver.com/good.tsv", sep="\t", header=TRUE)  
df = df[order(-df$nimp),] #Sort by column, descending order  
plot(df$nbook)  
plot(df$saleamt)  
plot( df$nimp, df$nbook )  
plot( df$nimp, df$nbook, type='l') #Line chart```  

### Regression Line  
```
plot( df$nimp, df$nbook )  
abline(lsfit(df$nimp,df$nbook)) #Add a least-squares regression line to the plot```  

### Bar chart  
```
df = df[order(-df$nbook),|order(-df$nbook),] \#Sort by column, descending order  
topbook = df[1:10,]  
barplot(height=topbook$nbook, names.arg=topbook$oneg) #Bar plot```  

### Pie chart  
```
pie(topbook$nbook, labels=topbook$oneg) #Pie chart  
```  

### Misc. graphics: divide plot area, export to file 
```
par(mfrow=c(2,1)) #2 graphs on one plot  
plot( sort(runif(1000)) )  
plot( sort(nunif(1000)) )```  

```
#Output plot to file  
png("demo.png", bg="white")  
plot( sort(rnorm(1000)) )  
dev.off()  
```  
  
## R batch scripts  
```
#On shell
R CMD BATCH --vanilla '--args ~/input.txt' ~/myScript.R myScript.Rout  
R CMD BATCH --help  

# Within R 
args <- commandArgs(trailingOnly = TRUE) #To get CLI arguments within scripts```  

More info:

* http://stat.ethz.ch/R-manual/R-devel/library/utils/html/BATCH.html  
* http://stat.ethz.ch/R-manual/R-patched/library/base/html/commandArgs.html

##  References and further reading  
* http://www.r-tutor.com/elementary-statistics  
* http://cran.r-project.org/doc/manuals/R-intro.html  
* http://www.r-cookbook.com/recipe  
* http://stackoverflow.com/questions/192369/books-for-learning-the-r-language  
* http://rpy.sourceforge.net/rpy_demo.html  
* http://en.wikibooks.org/wiki/R_Programming  
  
## Endnote 
Contact [Satpreet](http://www.meetup.com/ChicagoRUG/members/13813928/) for more information about this tutorial, or reach out to your local [R Users Group](http://www.meetup.com/ChicagoRUG/)  
  
