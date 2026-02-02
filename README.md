# Simple-Breakfast
#First R project
library(shiny)

ui <- fluidPage(
  titlePanel("محاسبه قیمت خرید"),
  
  # نمایش محصولات با قیمت کنار اسم
  checkboxGroupInput(
    "items",
    "محصولات:",
    c("شیر - 30,000" = "شیر",
      "نان - 15,000" = "نان",
      "روغن - 79,000" = "روغن",
      "تخم مرغ - 120,000" = "تخم مرغ",
      "رب - 67,000" = "رب",
      "پنیر - 77,500" = "پنیر")
  ),
  
  # تعداد جداگانه برای هر محصول
  numericInput("qty_shir", "تعداد شیر:", value = 1, min = 0),
  numericInput("qty_nan", "تعداد نان:", value = 1, min = 0),
  numericInput("qty_roghan", "تعداد روغن:", value = 1, min = 0),
  numericInput("qty_tokhme", "تعداد تخم مرغ:", value = 1, min = 0),
  numericInput("qty_rob", "تعداد رب:", value = 1, min = 0),
  numericInput("qty_panir", "تعداد پنیر:", value = 1, min = 0),
  
  textOutput("total")
)

server <- function(input, output) {
  
  prices <- c(shir = 30000, nan = 15000, roghan = 79000,
              tokhme = 120000, rob = 67000, panir = 77500)
  
  output$total <- renderText({
    total <- 0
    
    # جمع کردن قیمت بر اساس انتخاب و تعداد
    if ("شیر" %in% input$items) total <- total + prices["shir"] * input$qty_shir
    if ("نان" %in% input$items) total <- total + prices["nan"] * input$qty_nan
    if ("روغن" %in% input$items) total <- total + prices["roghan"] * input$qty_roghan
    if ("تخم مرغ" %in% input$items) total <- total + prices["tokhme"] * input$qty_tokhme
    if ("رب" %in% input$items) total <- total + prices["rob"] * input$qty_rob
    if ("پنیر" %in% input$items) total <- total + prices["panir"] * input$qty_panir
    
    paste("قیمت کل:", total, "تومان")
  })
}

shinyApp(ui, server)
