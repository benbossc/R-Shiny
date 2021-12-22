# R-Shiny

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

# Acknowledgements
This lab is based off of the Coding Club tutorial titled <a href="https://ourcodingclub.github.io/tutorials/shiny/#challenge"> "Getting Started with Shiny." </a>

# Lab Goals
1. Downloading Shiny
2. Getting familiar with the Shiny app file structure
3. Getting familiar with the Shiny app.R layout
4. Creating a Shiny app
5. Exporting a finished app
6. Challenge yourself to write an app

# Introduction
At it’s core, Shiny is merely an R package like dplyr or ggplot2. The package is used to create web-applications, but uses the R language rather than javascript or HTML5, which are traditionally used for web applications. By using R, Shiny provides an efficient method of creating web applications designed around data presentation and analysis.'

Below is an example of the basic Shiny app that we will be recreating in today’s tutorial:

<img src = "figures/R-Shiny-fig1.png">

Have a look at <a href="https://shiny.rstudio.com/gallery/">these examples</a> if you want to see what a Shiny app looks like, or if you want inspiration for your own app.

# What are Shiyn Apps useful for?
1. Interactive data visualisation for presentations and websites
2. Sharing results with collaborators
3. Communicating science in an accessible way
4. Bridging the gap between R users and non-R users

# Downloading Shiny and tutorial resources
To get Shiny in RStudio, the first thing you need is the shiny package, by running the code below in RStudio:

```R
install.packages("shiny")
install.packages("rsconnect")  # For publishing apps online
install.packages("agridat")  # For the dataset in today's tutorial
```

# The Shiny app file structure
Next, select "File/ New File/ Shiny Web App…," give the application a descriptive name (no spaces) and change the application type to “Single File (app.R)”, save the app in an appropriate directory and click "Create."

RStudio generates a template R script called app.R. Delete all the code in the template so you have a blank script.

Notice that the name you gave to your app was assigned to the directory, not the app script file. For your app to work, the file must remain named ```app.R```!

It is possible to create a Shiny app with two files called ```ui.R``` and ```server.R```, but the same can be accomplished by using one file. In the past, Shiny apps had to be created using two files, but the Shiny package has since been updated to allow the single file app structure, making things much tidier. You will see some tutorials on the internet using the old two file structure, but these can be easily translated to the one file structure. This tutorial will assume you have the one file app structure.

Now we can set up the rest of the folders for your app. Add a folder called ```Data``` and a folder called ```www``` in your app directory.```Data``` will hold any data used by the app and ```www``` will hold any images and other web elements.

To review, a Shiny application should have this specific folder structure to work properly:
```{r}
Test_App
├── app.R
├── Data
│   └── data.csv
└── www
    └── A.jpg
```
# app.R layout

Now that the folder structure is set up, head back to RStudio to start building app.R. A basic app.R consists of these five parts:

1. A section at the top of the script loading any packages needed for the app to run. shiny is required at the very least, but others like dplyr or ggplot2 could be added as they are needed:

```R
# Packages ----
library(shiny)  # Required to run any Shiny app
library(ggplot2)  # For creating pretty plots
library(dplyr)  # For filtering and manipulating data
library(agridat)  # The package where the data comes from
```
2. A section loading any data needed by the app:
```R
# Loading data ----
Barley <- as.data.frame(beaven.barley)
```
3. An object called ```ui```, which contains information about the layout of the app as it appears in your web browser. ```fluidPage()``` defines a layout that will resize according to the size of the browser window. All the app code will be placed within the brackets.
```R
# ui.R ----
ui <- fluidPage()
```
4. An object called ```server```, which contains information about the computation of the app, creating plots, tables, maps etc. using information provided by the user. All the app code will be placed within the curly brackets.
```R
# server.R ----
server <- function(input, output) {}
```
5. A command to run the app. This should be included at the very end of ```app.R```. It tells shiny that the user interface comes from the object called ```ui``` and that the server information (data, plots, tables, etc.) comes from the object called ```server```.
```R
# Run the app ----
shinyApp(ui = ui, server = server)
```
Delete any example code generated automatically when you created ```app.R``` and create a basic Shiny app by copying the snippets of code above into your ```
app.R```. Your script should now look like this:
```R
 # Packages ----
 library(shiny)  # Required to run any Shiny app
 library(ggplot2)  # For creating pretty plots
 library(dplyr)  # For filtering and manipulating data
 library(agridat)  # The package where the data comes from

 # Loading data ----
 Barley <- as.data.frame(beaven.barley)

 # ui.R ----
 ui <- fluidPage()

 # server.R ----
 server <- function(input, output) {}

 # Run the app ----
 shinyApp(ui = ui, server = server)
```
# Creating a Shiny App - Basic Syntax
To illustrate how to code a Shiny app, we will recreate a simple app written by <a href="https://github.com/gndaskalova">Gergana Daskalova</a> to explore some data on the productivity of Barley genotypes.

Look at the new code below and compare what you have in your current RStudio environment (don't copy and past just yet!!!):
```R
# Packages ----
library(shiny)  # Required to run any Shiny app
library(ggplot2)  # For creating pretty plots
library(dplyr)  # For filtering and manipulating data
library(agridat)  # The package where the data comes from

# Loading data ----
Barley <- as.data.frame(beaven.barley)

# ui.R ----
ui <- fluidPage(
  titlePanel(""),  # Add a title panel
  sidebarLayout(  # Make the layout a sidebarLayout
    sidebarPanel(),  # Inside the sidebarLayout, add a sidebarPanel
    mainPanel()  # Inside the sidebarLayout, add a mainPanel
  )
)

# server.R ----
server <- function(input, output) {}

# Run the app ----
shinyApp(ui = ui, server = server)
```
What did you notice? We can see that the app has a ```sidebarLayout``` with a ```sidebarPanel```, ```mainPanel``` and ```titlePanel```. It uses a ```selectInput``` to choose the genotype of barley shown in the histogram and the table, another ```selectInput``` for the colour of the histogram, a ```sliderInput``` to choose the number of bins in the histogram and a ```textInput``` to display some text in the app. The histogram is located in the ```mainPanel``` along with a summary table of the data being shown, while the inputs are in the ```sidebarPanel```.

Now, go back to your ```app.R``` and fill in the code you already have with the new bits of code below, which will serve as the basic skeleton for our app. Remember that you should only have one ```ui``` and one ```server``` object. 

```titlePanel()``` indicates that we would like a separate panel at the top of the page in which we can put the title.

```sidebarLayout()``` indicates that we want our Shiny app to have the sidebar layout, one of many layouts we saw above. Within sidebarLayout we have:

```sidebarPanel()``` indicates that we want a sidebar panel included in our app. Sidebar panels often contain input widgets like sliders, text input boxes, radio buttons etc.

```mainPanel()``` indicates that we want a larger main panel. Main panels often contain the output of the app, whether it is a table, map, plot or something else.










