# LETS-GO

<h1>2 Title: Implement data structures in R on datasets.</h1>

Theory: A data structure is a particular way of organizing data in a computer so that
it can be used effectively. The idea is to reduce the space and time complexities of
different tasks. Data structures in R programming are tools for holding multiple
values.
R’s base data structures are often organized by their dimensionality (1D, 2D, or nD)
and whether they’re homogeneous (all elements must be of the identical type) or
heterogeneous (the elements are often of various types). This gives rise to the six
data types which are most frequently utilized in data analysis.
ration with other programming languages like Python, C, and Java.
The most essential data structures used in R include:
• Vectors
• Lists
• Dataframes
• Matrices
• Arrays
• Factors
• Tibbles

1) From the mtcars dataset, create a vector from the mpg column. Replace values
greater than the 75th percentile with &quot;High&quot; and less than the 25th
percentile with &quot;Low&quot;leaving the rest as &quot;Medium&quot;.
Code:
data(mtcars)
mpg_vector <- mtcars$mpg
lower_percentile <- quantile(mpg_vector, 0.25)
upper_percentile <- quantile(mpg_vector, 0.75)
mpg_category <- ifelse(mpg_vector > upper_percentile, "High",
ifelse(mpg_vector < lower_percentile, "Low", "Medium"))
print(mpg_category)

2) Create two vectors from the iris dataset (Sepal.Length and Sepal.Width). Calculate
the element-wise difference and product. Find the sum of only the positive
differences.
Code:
data(iris)
sepal_length <- iris$Sepal.Length
sepal_width <- iris$Sepal.Width
difference <- sepal_length - sepal_width
product <- sepal_length * sepal_width
positive_difference_sum <- sum(difference[difference > 0])
print(paste("Sum of positive differences: ", positive_difference_sum))
print("Product of Sepal.Length and Sepal.Width: ")
print(product) 


3) From the mtcars dataset, extract rows where mpg is greater than the median and hp
is below the median. Find the correlation between mpg and hp for this subset.
Code:
data(mtcars)
median_mpg <- median(mtcars$mpg)
median_hp <- median(mtcars$hp)
subset_data <- mtcars[mtcars$mpg > median_mpg & mtcars$hp < median_hp, ]
correlation <- cor(subset_data$mpg, subset_data$hp)
print(correlation)

4) Create a list from the mtcars dataset containing mpg, hp, and cyl. Update the list to
include the row names as a new element. Then filter out the cars where mpg is less
than 20.
Code:
data(mtcars)
car_list <- list(
mpg = mtcars$mpg,
hp = mtcars$hp,
cyl = mtcars$cyl
)
car_list$row_names <- rownames(mtcars)
car_df <- data.frame(car_list)
filtered_cars <- car_df[car_df$mpg >= 20, ]
print(filtered_cars)

5) From the iris dataset, create a list containing Sepal.Length, Sepal.Width, and
Species.Merge this list with a new list containing a summary of Sepal.Length
using the summary() function.
Code:
data(iris)
iris_list <- list(
Sepal.Length = iris$Sepal.Length,
Sepal.Width = iris$Sepal.Width,
Species = iris$Species
)
sepal_length_summary <- summary(iris$Sepal.Length)
merged_list <- c(iris_list, Sepal.Length.Summary = sepal_length_summary)
print(merged_list)


6) Create a matrix from the mtcars dataset containing the first 10 rows of mpg, hp,
and cyl. Add a new row representing a car with mpg = 18, hp = 150, and cyl = 6,
and a new column showing the sum of all rows.
Code:
data(mtcars)
car_matrix <- as.matrix(mtcars[1:10, c("mpg", "hp", "cyl")])
new_car <- c(18, 150, 6)
car_matrix <- rbind(car_matrix, new_car)
rownames(car_matrix)[nrow(car_matrix)] <- "New_Car"
car_matrix <- cbind(car_matrix, Sum = rowSums(car_matrix))
print(car_matrix)

7) From a matrix created from mtcars (mpg and hp), write a function that accepts row
and column indices and returns the value at that position. If the indices are out of
bounds, return &quot;Invalid&quot;.
Code:
data(mtcars)
car_matrix <- as.matrix(mtcars[, c("mpg", "hp")])
get_value <- function(matrix, row_index, col_index) {
if (row_index < 1 || row_index > nrow(matrix) || col_index < 1 || col_index >
ncol(matrix)) {
return("Invalid")
} else {
return(matrix[row_index, col_index])
}
}
value1 <- get_value(car_matrix, 5, 1)
print(value1)
value2 <- get_value(car_matrix, 10, 2)
print(value2)
invalid_value <- get_value(car_matrix, 15, 1) # Out of bounds
print(invalid_value)

8) Create a 3D array from the iris dataset using Sepal.Length, Sepal.Width, and
Petal.Length. Find the row-wise mean for each matrix level and store the result in
a new matrix.
Code:
data(iris)
iris_array <- array(c(iris$Sepal.Length[1:10],
iris$Sepal.Width[1:10],
iris$Petal.Length[1:10]),
dim = c(10, 3, 1))
dimnames(iris_array) <- list(paste("Row", 1:10),
c("Sepal.Length", "Sepal.Width", "Petal.Length"),
"Level 1")
print("3D Array:")
print(iris_array)
row_means <- apply(iris_array, c(1, 3), mean)
print("Row-wise Means:")
print(row_means)

<h1>3 Implement Linear Regression Algorithms</h1>

THEORY:
Linear regression is a statistical method used to model the relationship between a dependent
variable (target) and one or more independent variables (predictors). The goal is to find the
linear equation that best predicts the dependent variable based on the independent variables.

 CODE :-
install.packages(“caret”)
library(tidyverse)
library(caret)
url <- "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/mpg.csv"
data <- read.csv(url)
write.csv(data, "mpg_data.csv", row.names = FALSE)
head(data)
str(data)
summary(data)
data <- na.omit(data)
data <- data %>% select(mpg, horsepower, weight)
model <- lm(mpg ~ horsepower + weight, data = data)
summary(model)
cat("R-squared:", summary(model)$r.squared, "\n")
par(mfrow = c(2, 2))
plot(model)
new_data <- data.frame(horsepower = c(100, 150), weight = c(3000, 3500))
predictions <- predict(model, new_data)
print(predictions)
saveRDS(model, "linear_model.rds")
loaded_model <- readRDS("linear_model.rds")
new_predictions <- predict(loaded_model, new_data)
print(new_predictions)

