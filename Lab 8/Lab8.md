# Lab 08-Develop, evaluate, and score a forecasting model for superstore sales
**Introduction**

In this lab, you'll see Microsoft Fabric's end-to-end data science
workflow for a forecasting model. This scenario uses the historic sales
data to predict the sales for different categories of products at a
superstore.

Forecasting is a crucial asset in sales, harnessing historical data and
predictive methods to provide insights into future trends. By analyzing
past sales, identifying patterns, and learning from consumer behavior,
businesses can optimize inventory, production, and marketing strategies.
This proactive approach enhances adaptability, responsiveness, and
overall performance of businesses in a dynamic marketplace.

**Objective**

1.  Load the data

2.  Understand and process the data using exploratory data analysis

3.  Train a machine learning model using an open source software package
    called SARIMAX and track experiments using MLflow and Fabric
    Autologging feature

4.  Save the final machine learning model and make predictions

5.  Demonstrate the model performance via visualizations in Power BI

## **Task 1: Load the Data**

**Dataset**

The dataset contains the churn status of 9995 instances of sales of
different products, along with 21 attributes that include: Row ID, Order
ID, Order Date, Ship Date, Ship Mode, Customer ID, Customer
Name, Segment, Country, City, State, Postal Code, Region, Product
ID, Category, Sub-Category, Product
Name, Sales, Quantity, Discount, Profit.

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL: <https://app.fabric.microsoft.com/home> then
    press the **Enter** button

2.  In the **Microsoft Azure** window, enter your **Sign-in**
    credentials, and click on the **Next** button.

> <img src="./media/image1.png" style="width:3.98672in;height:3.65509in"
> alt="A screenshot of a computer Description automatically generated" />

3.  Then, In the **Microsoft** window enter the password and click on
    the **Sign in** button**.**

> <img src="./media/image2.png" style="width:4.50833in;height:3.83333in"
> alt="A login screen with a red box and blue text Description automatically generated" />

4.  In **Stay signed in?** window, click on the **Yes** button.

> <img src="./media/image3.png" style="width:4.58333in;height:3.66667in"
> alt="A screenshot of a computer error Description automatically generated" />

5.  In the **Power BI** **Home** page, on the left-side pane navigate
    and click on **Workspaces**.

<img src="./media/image4.png" style="width:4.44167in;height:6.78333in"
alt="A screenshot of a computer Description automatically generated" />

6.  In the Workspaces pane Select **Data-ScienceXX** workspace.

<img src="./media/image5.png" style="width:3.975in;height:7.575in" />

7.  In the **Data-ScienceXX** workspace page, click on the drop-down
    arrow in the **+New** button, then select **Import notebook.**

<img src="./media/image6.png"
style="width:6.49167in;height:6.81667in" />

8.  On the **Import status pane that appears on the right side, click on
    Upload button** and then browse to **C:\Labfiles\data-science** and
    then select **AIsample - Superstore Forecast** notebook and click on
    the **Open** button.

<img src="./media/image7.png" style="width:3.81667in;height:2.9125in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image8.png" style="width:6.49167in;height:4.075in" />

9.  Once the notebooks are imported, select **Go to workspace** in the
    import dialog box

<img src="./media/image9.png"
style="width:3.54167in;height:1.99167in" />

<img src="./media/image10.png" style="width:6.5in;height:4.44931in"
alt="A screenshot of a computer Description automatically generated" />

10. On the Data-ScienceXX workspace homepage, select the
    **FabricData_Sciencelakehouse** lakehouse.

<img src="./media/image11.png"
style="width:6.49167in;height:3.93333in" />

11. In the Fabric**Data_Sciencelakehouse** page, select **Open
    notebook** \> **Existing notebook** from the top navigation menu.

<img src="./media/image12.png" style="width:6.5in;height:3.13333in" />

12. From the list of **Open existing notebook**, select the **AIsample -
    Superstore Forecast** notebook and select **Open**.

<img src="./media/image13.png" style="width:6.49167in;height:6.1in" />

13. If the imported notebook includes output, select the **Edit** menu,
    then select **Clear all outputs**.

<img src="./media/image14.png" style="width:7.15in;height:2.52083in" />

14. To load the data, select the code cell and click on the **play**
    button to execute cell.

<img src="./media/image15.png"
style="width:7.05691in;height:3.5375in" />

15. Download a publicly available version of the dataset and then store
    it in a Fabric lakehouse. Select the code cell and click on the
    **play** button to execute cell.

<img src="./media/image16.png"
style="width:7.03037in;height:4.29583in" />

16. Start recording the time it takes to run this notebook. Select the
    code cell and click on the **play** button to execute cell.

<img src="./media/image17.png"
style="width:6.49167in;height:2.53333in" />

17. Autologging in Microsoft Fabric extends the MLflow autologging
    capabilities by automatically capturing the values of input
    parameters and output metrics of a machine learning model as it is
    being trained. This information is then logged to the workspace,
    where it can be accessed and visualized using the MLflow APIs or the
    corresponding experiment in the workspace.

18. Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image18.png"
style="width:7.06845in;height:2.60417in" />

19. Read raw data from the **Files** section of the lakehouse. Add
    additional columns for different date parts and the same information
    will be used to create partitioned delta table. Since the raw date
    is stored as an Excel file, you need to use Pandas to read the raw
    data.

20. Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image19.png"
style="width:6.96985in;height:2.00417in" />

## **Task 2: Exploratory Data Analysis**

1.  To import the required libraries. Select the code cell and click on
    the **play** button to execute cell.

<img src="./media/image20.png" style="width:6.5in;height:4.475in" />

2.  To review the dataset, it is recommended to manually go through a
    subset of the data to gain a better understanding. In this regard,
    you could use the display function to print the DataFrame. You can
    also show the "Chart" views to easily visualize subsets of the
    dataset.

3.  Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image21.png"
style="width:6.85934in;height:3.57917in" />

4.  The primary focus will be on forecasting the sales for
    the Furniture category. This choice is made to speed up the
    computation and facilitate the demonstration of the model's
    performance. However, it is important to realize that this
    techniques used in this notebook are adaptable and can be extended
    to predict the sales of various other product categories.

5.  Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image22.png"
style="width:7.08036in;height:2.79583in" />

6.  To Pre-processing the data, select the code cell and click on the
    **play** button to execute cell.

<img src="./media/image23.png"
style="width:7.11965in;height:3.92083in" />

7.  The dataset is structured on a daily basis, and since the goal is to
    develop a model to forecast the sales on a monthly basis, you need
    to resample on the column Order Date.

8.  First, group the Furniture category by Order Date and then calculate
    the sum of the Sales column for each group in order to determine the
    total sales for each unique Order Date. Then, resample
    the Sales column using the MS frequency to aggregate the data by
    month and then you calculate the mean sales value for each month.

9.  Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image24.png"
style="width:7.11861in;height:3.2125in" />

10. Demonstrate the impact of Order Date on the Sales for the Furniture
    category. Select the code cell and click on the **play** button to
    execute cell.

<img src="./media/image25.png" style="width:6.95627in;height:3.2375in"
alt="A graph with a line Description automatically generated" />

11. Prior to any statistical analysis, you need to
    import statsmodels. Statsmodels is a Python module that provides
    classes and functions for the estimation of many different
    statistical models, as well as for conducting statistical tests and
    statistical data exploration.

12. Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image26.png" style="width:6.83075in;height:1.97917in"
alt="A screenshot of a computer Description automatically generated" />

13. A time series tracks four data elements at set intervals in order to
    determine the variation of those four elements in the time series
    pattern. These elements include:

- **Level:** Refers to the fundamental component that represents the
  average value for a specific time period.

- **Trend:** Describes whether the time series is decreasing, constant,
  or increasing over time.

- **Seasonality:** Describes the periodic signal in the time series and
  looks for cyclic occurrences that affect the time series' increasing
  or decreasing patterns.

- **Noise/Residual:** Refers to the random fluctuations and variability
  in the time series data that cannot be explained by the model.

14. Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image27.png"
style="width:6.49167in;height:3.74167in" />

<img src="./media/image28.png"
style="width:7.29294in;height:3.83892in" />

## Task 3: Model Training and Tracking

With your data in place, you can define the forecasting model. Apply the
Seasonal AutoRegressive Integrated Moving Average with eXogenous
regressors (SARIMAX) in this notebook. SARIMAX is a time series
forecasting model that extends SARIMA to include exogenous variables. It
combines autoregressive (AR) and moving average (MA) components,
seasonal differencing, and external predictors to make accurate and
flexible forecasts for time series data, making it a powerful tool for
various forecasting tasks.

1.  Use MLfLow and Fabric Autologging to track the experiments. Here
    you'll load the delta table from the lakehouse. You may use other
    delta tables considering the lakehouse as the source. Select the
    code cell and click on the **play** button to execute cell.

<img src="./media/image29.png" style="width:6.6375in;height:2.54438in"
alt="A screenshot of a computer Description automatically generated" />

2.  SARIMAX takes into account the parameters involved in regular ARIMA
    mode (p,d,q) and also adds the seasonality parameters (P,D,Q,s).
    These arguments to SARIMAX model are called order (p,d,q) and
    seasonal order (P,D,Q,s) respectively and hence 7 parameters to
    tune. Prior to model training, you need to set up these parameters
    which are defined in the following.

3.  Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image30.png" style="width:6.49167in;height:3.79167in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image31.png" style="width:6.5in;height:4.24125in"
alt="A screenshot of a computer Description automatically generated" />

4.  To model training, select the code cell and click on the **play**
    button to execute cell.

<img src="./media/image32.png" style="width:6.5in;height:2.99574in"
alt="A screenshot of a computer Description automatically generated" />

5.  Visualize a time series forecast for furniture sales data, showing
    both the observed data and the one-step-ahead forecast with a
    confidence interval shaded region. Select the code cell and click on
    the **play** button to execute cell.

<img src="./media/image33.png"
style="width:7.11736in;height:2.26586in" />

<img src="./media/image34.png" style="width:7.01271in;height:3.56404in"
alt="A graph showing a line of blue and red lines Description automatically generated with medium confidence" />

<img src="./media/image35.png" style="width:6.89404in;height:1.07083in"
alt="A screenshot of a computer Description automatically generated" />

6.  Note that predictions is utilized to assess the model's performance
    by contrasting it with the actual values,
    whereas **predictions_future** is indicative of future forecasting.

7.  Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image36.png" style="width:7.33239in;height:2.87083in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image37.png" style="width:7.39302in;height:2.10417in"
alt="A screenshot of a computer Description automatically generated" />

## Task 4: Score the model and save predictions

1.  The actual values are integrated with the forecasted values, which
    will be employed to create the Power BI report. Note that these
    results will be stored into a table within the lakehouse.

2.  Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image38.png" style="width:6.5in;height:3.69649in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image39.png"
style="width:7.03126in;height:3.52917in" />

## **Step 5: Business Intelligence via Visualizations in Power BI**

The Power BI report shows the mean absolute percentage error (MAPE) of
16.58. MAPE is a metric that defines the accuracy of a forecasting
method and represents how accurate the forecasted quantities are in
comparison with the actual quantities. MAPE is a straightforward metric,
with a 10% MAPE representing that the average deviation between the
forecasted values and actual values was 10%, regardless of whether the
deviation was positive or negative. Note that what one considers to be a
desirable MAPE value varies across different industries.

The light blue line in the graph represents the actual sales values,
while the dark blue line represents the forecasted sales values. An
analysis of the comparison between the actual and forecasted sales
reveals that the model effectively predicts sales for the Furniture
category during the first six months of 2023.

Based on this observation, it is justifiable to have confidence in the
model's forecasting capabilities for the overall sales in the last six
months of 2023 and extending into 2024. This confidence can inform
strategic decisions regarding inventory management, raw material
procurement, and other business-related considerations.

1.  Now, click on **FabricData_Sciencelakehouse** on the left-sided
    navigation pane

<img src="./media/image40.png" style="width:3.02083in;height:4.70833in"
alt="A screenshot of a computer Description automatically generated" />

2.  Select **New semantic model** on the top ribbon.

<img src="./media/image41.png" style="width:6.25in;height:4.26667in"
alt="A screenshot of a computer Description automatically generated" />

3.  In the **New dataset** box, enter the dataset a name, such as **bank
    churn predictions**.Then select
    the **customer_churn_test_predictions** dataset and
    select **Confirm**.

> <img src="./media/image42.png"
> style="width:4.48333in;height:5.49167in" />
>
> <img src="./media/image43.png" style="width:6.5in;height:5.03333in" />

4.  Add a new measure for the MAPE.

<!-- -->

1)  Select **New measure** in the top ribbon. This action adds a new
    item named **Measure** to the **Demand_Forecast_New_1** dataset, and
    opens a formula bar above the table.

> <img src="./media/image44.png" style="width:6.5in;height:4.93333in" />

2)  To determine the average the MAPE , replace Measure = in the formula
    bar with:

> ```PythonCopy
>
> MAPE_Value = AVERAGE(Demand_Forecast_New_1[MAPE])

3)  To apply the formula, select the **check mark** in the formula bar.
    The new measure appears in the data table. The calculator icon shows
    it was created as a measure.

<img src="./media/image45.png" style="width:6.5in;height:4.75833in" />

5.  Add a new measure that average the total number of forecasted sales
    . You'll need it for the rest of the new measures.

<!-- -->

1)  Select **New measure** in the top ribbon to add a new item
    named **Measure** to the **Demand_Forecast_New_1**  dataset. This
    action also opens a formula bar above the table.

> ```PythonCopy
>
> Forecasted_Value = AVERAGE(Demand_Forecast_New_1[Forecasted_Sales])

2)  Select the **check mark** in the formula bar to apply the formula.

> <img src="./media/image46.png" style="width:6.49167in;height:4.325in" />

6.  Add a new measure that counts the total number of actual sales .
    You'll need it for the rest of the new measures.

<!-- -->

3)  Select **New measure** in the top ribbon to add a new item
    named **Measure** to the **Demand_Forecast_New_1**  dataset. This
    action also opens a formula bar above the table.

> ```PythonCopy
>
> Actual_Value = AVERAGE(Demand_Forecast_New_1[Actual_Sales])

4)  Select the **check mark** in the formula bar to apply the formula.

<img src="./media/image47.png"
style="width:6.49167in;height:4.99167in" />

7.  On the tools at the top of the dataset page, select **New report**
    to open the Power BI report authoring page.

<img src="./media/image48.png"
style="width:6.49167in;height:4.41667in" />

8.  In the Ribbon, select **Text box**. Type in **ML-Forecast** .
    **Highlight** the **text** Change the font size and background color
    in the Format panel. Adjust the font size and color by selecting the
    text and using the format bar.

<img src="./media/image49.png"
style="width:7.41488in;height:3.17917in" />

9.  In the Visualizations panel, select the **Card** icon. From
    the **Data** pane, select **MAPE_Value**. Change the font size and
    background color in the Format panel. Drag this visualization to the
    top right of the report.

<img src="./media/image50.png"
style="width:3.33333in;height:5.0375in" />

<img src="./media/image51.png"
style="width:7.36029in;height:2.8875in" />

10. In the Visualizations panel, select the **Slicer** icon. From
    the **Data** pane, select **Category**.

11. Change the slicer settings, click on **Format your visual**, under
    the **Visual** drop down the **Slicer settings** and select the
    **style** as **Dropdown** font size. Change the background color in
    the Format panel. Drag this visualization to the top right of the
    report.

<img src="./media/image52.png"
style="width:7.20185in;height:4.74583in" />

<img src="./media/image53.png"
style="width:5.45417in;height:3.65816in" />

<img src="./media/image54.png"
style="width:5.35417in;height:4.51516in" />

12. In the Visualizations panel, select the **Line chart** icon.
    Select **Date** for the x-axis, **Actual_Value** for column y-axis,
    and **Forecasted_value** for the line y-axis.

<img src="./media/image55.png" style="width:3.55in;height:6.34167in" />

<img src="./media/image56.png" style="width:7.27512in;height:3.48055in"
alt="A screenshot of a computer Description automatically generated" />

13. From the ribbon, select **File** \> **Save**

<img src="./media/image57.png" style="width:5.575in;height:4.7in" />

14. Enter the name of your report as **ML-Forecast**. Select **Save**.

<img src="./media/image58.png" style="width:3.025in;height:2.26667in" />

## **Task 6: Clean up resources**

1.  Select your workspace, the **Data-ScienceXX** from the left-hand
    navigation menu. It opens the workspace item view.

<img src="./media/image59.png" style="width:5in;height:4.35in" />

2.  Select the ***...*** option under the workspace name and
    select **Workspace settings**.

<img src="./media/image60.png" style="width:6.5in;height:2.99167in" />

3.  Select **Other** and **Remove this workspace.**

<img src="./media/image61.png" style="width:6.5in;height:4.29167in" />

4.  Click on **Delete** in the warning that pops up.

<img src="./media/image62.png" style="width:5.85051in;height:1.62514in"
alt="A white background with black text Description automatically generated" />

5.  Wait for a notification that the Workspace has been deleted, before
    proceeding to the next lab.

<img src="./media/image63.png" style="width:6.5in;height:2.15208in"
alt="A screenshot of a computer Description automatically generated" />
