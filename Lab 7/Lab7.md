# Lab 07- Implementing a Data Science scenario in Microsoft Fabric

**Introduction**

The lifecycle of a Data science project typically includes (often,
iteratively) the following steps:

- Business understanding

- Data acquisition

- Data exploration, cleansing, preparation, and visualization

- Model training and experiment tracking

- Model scoring and generating insights.

The goals and success criteria of each stage depend on collaboration,
data sharing and documentation. The Fabric data science experience
consists of multiple native-built features that enable collaboration,
data acquisition, sharing, and consumption in a seamless way.

In these tutorials, you take the role of a data scientist who has been
given the task to explore, clean, and transform a dataset containing the
churn status of 10000 customers at a bank. You then build a machine
learning model to predict which bank customers are likely to leave.

**Objective**

1.  Use the Fabric notebooks for data science scenarios.

2.  Ingest data into a Fabric lakehouse using Apache Spark.

3.  Load existing data from the lakehouse delta tables.

4.  Clean and transform data using Apache Spark and Python based tools.

5.  Create experiments and runs to train different machine learning
    models.

6.  Register and track trained models using MLflow and the Fabric UI.

7.  Run scoring at scale and save predictions and inference results to
    the lakehouse.

8.  Visualize predictions in Power BI using DirectLake.

## Task 1: Create a workspace 

Before working with data in Fabric, create a workspace with the Fabric
trial enabled.

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL: <https://app.fabric.microsoft.com/> then press
    the **Enter** button.

> **Note**: If you are directed to Microsoft Fabric Home page, then skip
> steps from \#2 to \#4.
>
> <img src="./media/image1.png" style="width:4.4875in;height:2.70202in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In the **Microsoft Fabric** window, enter your credentials, and
    click on the **Submit** button.

> <img src="./media/image2.png" style="width:6.04905in;height:2.90417in"
> alt="A close up of a white and green object Description automatically generated" />

3.  Then, In the **Microsoft** window enter the password and click on
    the **Sign in** button**.**

> <img src="./media/image3.png" style="width:3.9375in;height:3.34797in"
> alt="A login screen with a red box and blue text Description automatically generated" />

4.  In **Stay signed in?** window, click on the **Yes** button.

> <img src="./media/image4.png" style="width:3.3875in;height:2.71in"
> alt="A screenshot of a computer error Description automatically generated" />

5.  In the **Microsoft Fabric** home page, select the **Power BI**
    template.

> <img src="./media/image5.png" style="width:6.49167in;height:4.20833in"
> alt="A screenshot of a computer Description automatically generated" />

6.  In the **Power BI Home** page menu bar on the left,
    select **Workspaces** (the icon looks similar to 🗇).

> <img src="./media/image6.png" style="width:6.5in;height:6.23333in"
> alt="A screenshot of a computer Description automatically generated" />

7.  In the Workspaces pane, select **+** **New workspace**.

> <img src="./media/image7.png" style="width:3.32126in;height:6.1625in"
> alt="A screenshot of a computer Description automatically generated" />

8.  In the **Create a workspace tab**, enter the following details and
    click on the **Apply** button.

| **Name** | **Data-ScienceXX**(XX can be a unique number) |
|----|----|
| **Advanced** | Under **License mode**, select **Trial** |
| **Default storage format** | **Small dataset storage format** |

> <img src="./media/image8.png"
> style="width:5.16667in;height:7.06667in" />

<img src="./media/image9.png" style="width:5.25417in;height:6.23887in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image10.png"
style="width:4.99885in;height:4.0891in" />

<img src="./media/image11.png" style="width:3.8718in;height:4.72917in"
alt="A screenshot of a computer Description automatically generated" />

9.  Wait for the deployment to complete. It takes 2-3 minutes to
    complete. When your new workspace opens, it should be empty.

## Task 2: Create a lakehouse and upload files

Now that you have a workspace, it’s time to switch to the *Data
engineering* experience in the portal and create a data lakehouse for
the data files you’re going to analyze.

1.  At the bottom left of the Power BI portal, select the **Power
    BI** icon and switch to the **Data Engineering** experience.

2.  In the **Synapse Data Engineering** home page, Select
    **Lakehouse(Preview)** under **New** pane.

<img src="./media/image12.png" style="width:5.75in;height:7.58333in"
alt="A screenshot of a computer Description automatically generated" />

3.  In the **New lakehouse** dialog box, enter
    **FabricData_Sciencelakehouse** in the **Name** field, click on the
    **Create** button and open the new lakehouse.

> <img src="./media/image13.png" style="width:5.44795in;height:4.59583in"
> alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image14.png" style="width:3.83333in;height:1.875in" />

4.  After a minute or so, a new empty lakehouse will be created. You
    need to ingest some data into the data lakehouse for analysis.

<img src="./media/image15.png" style="width:6.5in;height:5.01944in" />

5.  You will see a notification stating **Successfully created SQL
    endpoint**.

> <img src="./media/image16.png" style="width:3.39196in;height:2.88358in"
> alt="A screenshot of a computer Description automatically generated" />

10. At the bottom left of the Power BI portal, select the **Data
    Engineering** icon and switch to the **Data Science** experience.

<img src="./media/image17.png"
style="width:4.4625in;height:6.52444in" />

## **Task 3: Import tutorial notebooks**

1.  On the Data science experience homepage, select **Import
    notebook** and upload the notebook files.

<img src="./media/image18.png" style="width:6.49167in;height:4.825in" />

2.  On the **Import status** pane that appears on the right side, click
    on **Upload** button and then browse to
    **C:\Labfiles\data-science\data-science-tutorial** and then select
    all ***files*** and click on the **Open** button.

<img src="./media/image19.png"
style="width:3.81667in;height:3.09167in" />

<img src="./media/image20.png" style="width:6.5in;height:4.04167in" />

3.  Once the notebooks are imported, select **Go to workspace** in the
    import dialog box

<img src="./media/image21.png" style="width:4.75in;height:3.075in" />

4.  The imported notebooks are now available in your workspace for use.

<img src="./media/image22.png" style="width:6.5in;height:2.85903in"
alt="A screenshot of a computer Description automatically generated" />

5.  On the Data-ScienceXX workspace homepage, select the
    **1-ingest-data** notebook.

<img src="./media/image23.png"
style="width:6.49167in;height:3.03333in" />

6.  If the imported notebook includes output, select the **Edit** menu,
    then select **Clear all outputs**.

<img src="./media/image24.png"
style="width:6.92955in;height:3.5625in" />

## **Task 4: Attach a lakehouse to the notebooks**

To demonstrate Fabric lakehouse features, many of the tutorials require
attaching a default lakehouse to the notebooks. The following steps show
how to add an existing lakehouse to a notebook in a Fabric-enabled
workspace.

1.  Select **Add lakehouse** in the left pane and select **Existing
    lakehouse** to open the **Data hub** dialog box.

> <img src="./media/image25.png" style="width:6.32917in;height:5.575in" />

2.  In the **Add lakehouse** box, select the **Existing
    lakehouse** radio button and click on the **Add** button.

> <img src="./media/image26.png"
> style="width:3.11667in;height:2.05833in" />

3.  In **OneLake data hub** tab, Select the
    **FabricData_Sciencelakehouse** and select **Add**.

> <img src="./media/image27.png"
> style="width:6.49167in;height:3.93333in" />

4.  Once a lakehouse is added, it's visible in the lakehouse pane in the
    notebook UI where tables and files stored in the lakehouse can be
    viewed.

> <img src="./media/image28.png" style="width:6.5in;height:4.53333in" />

## **Task 5: Ingest data into a Microsoft Fabric lakehouse using Apache Spark**

**Bank churn data**

The dataset contains churn status of 10,000 customers. It also includes
attributes that could impact churn such as:

- Credit score

- Geographical location (Germany, France, Spain)

- Gender (male, female)

- Age

- Tenure (years of being bank's customer)

- Account balance

- Estimated salary

- Number of products that a customer has purchased through the bank

- Credit card status (whether a customer has a credit card or not)

- Active member status (whether an active bank's customer or not)

The dataset also includes columns such as row number, customer ID, and
customer surname that should have no impact on customer's decision to
leave the bank.

The event that defines the customer's churn is the closing of the
customer's bank account. The column exited in the dataset refers to
customer's abandonment. There isn't much context available about these
attributes so you have to proceed without having background information
about the dataset. The aim is to understand how these attributes
contribute to the exited status.

1.  If the imported notebook includes output, select the **Edit** menu,
    then select **Clear all outputs**.

<img src="./media/image24.png" style="width:6.92917in;height:1.37917in"
alt="A screenshot of a computer Description automatically generated" />

2.  Download dataset and upload to lakehouse, select the code cell and
    click on the **play** button to execute cell.

<img src="./media/image29.png" style="width:6.5in;height:2.80833in" />

3.  This code downloads a publicly available version of the dataset and
    then stores it in a Fabric lakehouse. Select the code cell and click
    on the **play** button to execute cell.

<img src="./media/image30.png"
style="width:6.49167in;height:3.44167in" />

## **Task 6: Explore and visualize data using Microsoft Fabric notebooks**

1.  Now, click on **Data_ScienceXX** on the left-sided navigation pane.

<img src="./media/image31.png" style="width:6.49167in;height:5.225in" />

2.  On the Data-ScienceXX workspace homepage, select the
    **FabricData_Sciencelakehouse** lakehouse.

<img src="./media/image32.png" style="width:6.5in;height:3.51667in" />

3.  In the Fabric**Data_Sciencelakehouse** page, select **Open
    notebook** \> **Existing notebook** from the top navigation menu.

<img src="./media/image33.png" style="width:6.5in;height:3.13333in" />

4.  From the list of **Open existing notebook**, select
    the **2-explore-cleanse-data** notebook and select **Open**.

<img src="./media/image34.png" style="width:6.49167in;height:6.275in" />

<img src="./media/image35.png" style="width:6.5in;height:3.99306in"
alt="A screenshot of a computer Description automatically generated" />

4.  If the imported notebook includes output, select the **Edit** menu,
    then select **Clear all outputs**.

<img src="./media/image24.png" style="width:6.7625in;height:1.49583in"
alt="A screenshot of a computer Description automatically generated" />

5.  Read raw data from the **Files** section of the lakehouse. You
    uploaded this data in the previous notebook. Make sure you have
    attached the same lakehouse you used in Task 5 to this notebook
    before you run this code.

6.  Select the code cell and click on the **play** button to execute
    cell.

<img src="./media/image36.png"
style="width:7.06983in;height:2.90417in" />

7.  Convert the spark DataFrame to pandas DataFrame for easier
    processing and visualization. Select the code cell and click on the
    **play** button to execute cell.

<img src="./media/image37.png" style="width:6.5in;height:3.55in" />

8.  Explore the raw data with display, do some basic statistics and show
    chart views. You first need to import required libraries for data
    visualization such as seaborn, which is a Python data visualization
    library to provide a high-level interface for building visuals on
    DataFrames and arrays. Select the code cell and click on the
    **play** button to execute cell.

<img src="./media/image38.png"
style="width:7.17574in;height:2.7875in" />

<img src="./media/image39.png"
style="width:7.00862in;height:3.3875in" />

9.  Use Data Wrangler to perform initial data cleansing, under the
    notebook ribbon select **Data** tab , dropdown the **Launch Data
    Wrangler** and select the **df** data wrangler.

<img src="./media/image40.png" style="width:6.42083in;height:3.52917in"
alt="A screenshot of a computer Description automatically generated" />

10. Once the Data Wrangler is launched, a descriptive overview of the
    displayed data panel is generated.

11. In df(Data Wrangler) pane, under **Operations** select the **Find
    and replace\>Drop duplicate rows.**

<img src="./media/image41.png" style="width:6.0125in;height:3.43461in"
alt="A screenshot of a computer Description automatically generated" />

12. Under the Target columns, select the **RowNumber and CustomerId**
    check boxs**,** and then click on the **Apply** button.

<img src="./media/image42.png" style="width:6.48333in;height:3.91667in"
alt="A screenshot of a computer Description automatically generated" />

13. In df(Data Wrangler) pane, under **Operations** select the **Find
    and replace\>Drop missing values.**

<img src="./media/image43.png"
style="width:6.37917in;height:4.35417in" />

14. Under the Target columns, select the **RowNumber, CustomerId,
    Surname** check boxs**,** and then click on the **Apply** button.

<img src="./media/image44.png" style="width:6.5in;height:3.93333in"
alt="A screenshot of a computer Description automatically generated" />

15. In df(Data Wrangler) pane, under **Operations** select the **Find
    and replace\>Drop missing values.**

<img src="./media/image45.png" style="width:7.22613in;height:3.8125in"
alt="A screenshot of a computer Description automatically generated" />

16. Under the Target columns, select the **Select all** check box**,**
    and then click on the **Apply**
    button.<img src="./media/image46.png" style="width:6.49167in;height:3.975in"
    alt="A screenshot of a computer Description automatically generated" />

17. In df(Data Wrangler) pane, select the **+Add code to notebook.**

<img src="./media/image47.png" style="width:6.49167in;height:4.28333in"
alt="A screenshot of a computer Description automatically generated" />

18. This code is similar to the code produced by Data Wrangler, but adds
    in the argument **inplace=True** to each of the generated steps. By
    setting **inplace=True**, pandas will overwrite the original
    DataFrame instead of producing a new DataFrame as an output.

<img src="./media/image48.png" style="width:6.5in;height:2.49167in" />

19. Select new added code cell and click on the **play** button to
    execute cells.

<img src="./media/image49.png"
style="width:6.49167in;height:3.69167in" />

20. To determine categorical, numerical, and target attributes. Select
    the code cell and click on the **play** button to execute cell.

<img src="./media/image50.png" style="width:6.5in;height:3.39167in" />

21. To show the five-number summary (the minimum score, first quartile,
    median, third quartile, the maximum score) for the numerical
    attributes, using box plots. Select the code cell and click on the
    **play** button to execute cell.

<img src="./media/image51.png" style="width:7.23155in;height:2.5125in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image52.png" style="width:6.5in;height:3.26111in"
alt="A screenshot of a computer screen Description automatically generated" />

22. To show the distribution of exited versus non-exited customers
    across the categorical attributes. Select the code cell and click on
    the **play** button to execute cell.

<img src="./media/image53.png" style="width:6.49167in;height:3.375in"
alt="A screenshot of a computer Description automatically generated" />

23. Show the frequency distribution of numerical attributes using
    histogram. Select the code cell and click on the **play** button to
    execute cell.

<img src="./media/image54.png" style="width:6.5in;height:3.225in"
alt="A screenshot of a computer Description automatically generated" />

24. Perform the feature engineering generates new attributes based on
    current attributes. Select the code cell and click on the **play**
    button to execute cell.

<img src="./media/image55.png" style="width:6.49167in;height:2.275in"
alt="A screenshot of a computer Description automatically generated" />

25. Perform the feature engineering generates new attributes based on
    current attributes. Select the code cell and click on the **play**
    button to execute cell.

<img src="./media/image55.png" style="width:6.49167in;height:2.275in"
alt="A screenshot of a computer Description automatically generated" />

26. Use the **Data Wrangler** to perform one-hot encoding, under the
    notebook ribbon select **Data** tab , dropdown the **Launch Data
    Wrangler** and select the **df** data wrangler.

<img src="./media/image56.png" style="width:6.49167in;height:2.35417in"
alt="A screenshot of a computer Description automatically generated" />

27. In df(Data Wrangler) pane, under **Operations** select the
    **Formulas\>One-hot encode.**

<img src="./media/image57.png" style="width:6.12917in;height:3.5125in"
alt="A screenshot of a computer Description automatically generated" />

28. Under the Target columns, select the **Geography** and **Gender**
    check boxs**,** and then click on the **Apply** button.

<img src="./media/image58.png" style="width:6.5in;height:3.86667in"
alt="A screenshot of a computer Description automatically generated" />

29. In df(Data Wrangler) pane, select the **+Add code to notebook.**

<img src="./media/image59.png" style="width:6.2875in;height:4.50417in"
alt="A screenshot of a computer Description automatically generated" />

30. Code generated by Data Wrangler, Select the **df_copy()** data and
    replace with **df_clean.copy** ().

31. Select the code cell and click on the **play** button to execute
    cell.

> <img src="./media/image60.png" style="width:6.5in;height:2.53333in" />

<img src="./media/image61.png"
style="width:7.04064in;height:2.3875in" />

32. Create a delta table for the cleaned data, select the code cell and
    click on the **play** button to execute cell.

<img src="./media/image62.png" style="width:6.5in;height:2.98333in" />

## **Task 7: Train and register a machine learning model**

1.  Now, click on **FabricData_Sciencelakehouse** on the left-sided
    navigation pane

<img src="./media/image63.png"
style="width:6.49167in;height:4.70833in" />

2.  In the Fabric**Data_Sciencelakehouse** page, select **Open
    notebook** \> **Existing notebook** from the top navigation menu.

> <img src="./media/image33.png" style="width:6.5in;height:3.13333in"
> alt="A screenshot of a computer Description automatically generated" />

3.  From the list of **Open existing notebook**, select
    the **3-train-evaluate** notebook and select **Open**.

<img src="./media/image64.png" style="width:6.49167in;height:6.2in" />

4.  If the imported notebook includes output, select the **Edit** menu,
    then select **Clear all outputs**.

<img src="./media/image24.png" style="width:6.92917in;height:1.37917in"
alt="A screenshot of a computer Description automatically generated" />

5.  For this task, you'll install imbalanced-learn (imported
    as imblearn) using %pip install. Imbalanced-learn is a library for
    Synthetic Minority Oversampling Technique (SMOTE) which is used when
    dealing with imbalanced datasets. The PySpark kernel will be
    restarted after %pip install, so you'll need to install the library
    before you run any other cells.

6.  Select the code cell and click on the play button to execute cell.

<img src="./media/image65.png"
style="width:7.10334in;height:3.67917in" />

7.  Prior to training any machine learning model, you need to load the
    delta table from the lakehouse in order to read the cleaned data you
    created in the previous notebook. Select the code cell and click on
    the play button to execute cell.

<img src="./media/image66.png"
style="width:7.0453in;height:2.70417in" />

8.  Demonstrates how to generate an experiment, specify the machine
    learning model and training parameters as well as scoring metrics,
    train the machine learning models, log them, and save the trained
    models for later use.

9.  Select the code cell and click on the play button to execute cell.

<img src="./media/image67.png"
style="width:7.02837in;height:2.9375in" />

10. All the experiments with their respective names are logged and
    you'll be able to track their parameters and performance metrics. 

11. Select the code cell and click on the play button to execute cell.

<img src="./media/image68.png" style="width:7.0788in;height:2.6625in" />

12. With your data in place, you can now define the machine learning
    models. You'll apply Random Forrest and LightGBM models in this
    notebook. Use scikit-learn and lightgbm to implement the models
    within a few lines of code.

13. Select the code cell and click on the play button to execute cell.

<img src="./media/image69.png"
style="width:6.99077in;height:2.67083in" />

14. Use the train_test_split function from scikit-learn to split the
    data into training, validation, and test sets. Select the code cell
    and click on the play button to execute cell.

<img src="./media/image70.png"
style="width:7.06968in;height:3.15417in" />

15. Save the test data to the delta table for use in the next notebook.
    Select the code cell and click on the play button to execute cell.

<img src="./media/image71.png"
style="width:7.13206in;height:3.3875in" />

16. The data exploration in part 2 showed that out of the 10,000 data
    points corresponding to 10,000 customers, only 2,037 customers
    (around 20%) have left the bank. This indicates that the dataset is
    highly imbalanced. The problem with imbalanced classification is
    that there are too few examples of the minority class for a model to
    effectively learn the decision boundary. SMOTE is the most widely
    used approach to synthesize new samples for the minority class.

17. Select the code cell and click on the play button to execute cell.

<img src="./media/image72.png"
style="width:7.10295in;height:3.4375in" />

18. Train the model using Random Forest with maximum depth of 4 and 4
    features. Select the code cell and click on the play button to
    execute cell.

> <img src="./media/image73.png"
> style="width:7.01271in;height:3.42083in" />

19. Train the model using Random Forest with maximum depth of 8 and 6
    features. Select the code cell and click on the play button to
    execute cell.

<img src="./media/image74.png"
style="width:7.12181in;height:3.57917in" />

20. Train the model using LightGBM. Select the code cell and click on
    the play button to execute cell.

> <img src="./media/image75.png"
> style="width:7.12877in;height:3.6375in" />

21. The experiment runs are automatically saved in the experiment
    artifact that can be found from the workspace. They're named based
    on the name used for setting the experiment. All of the trained
    machine learning models, their runs, performance metrics, and model
    parameters are logged.

22. Now, click on **Data_ScienceXX** workspace on the left-sided
    navigation pane.

> <img src="./media/image76.png"
> style="width:3.37083in;height:4.05417in" />

23. Find and select the experiment name, in this
    case ***bank-churn-experiment***. If you don't see the experiment in
    your workspace, refresh your browser.

> <img src="./media/image77.png"
> style="width:7.00826in;height:4.07917in" />
>
> <img src="./media/image78.png" style="width:6.5in;height:3.17083in" />

24. Now, click on **Data_ScienceXX** workspace on the left-sided
    navigation pane.

> <img src="./media/image76.png" style="width:3.37083in;height:4.05417in"
> alt="A screenshot of a computer Description automatically generated" />

25. On the Data-ScienceXX workspace homepage, select the
    **3-train-evaluate** notebook.

> <img src="./media/image79.png"
> style="width:6.49167in;height:5.24167in" />

26. Open the saved experiment from the workspace, load the machine
    learning models, and then assess the performance of the loaded
    models on the validation dataset. Select the code cell and click on
    the play button to execute cell.

<img src="./media/image80.png"
style="width:6.72552in;height:2.99583in" />

27. Directly assess the performance of the trained machine learning
    models on the validation dataset. Select the code cell and click on
    the play button to execute cell.

<img src="./media/image81.png"
style="width:7.08526in;height:2.3375in" />

28. Next, develop a script to plot the confusion matrix in order to
    evaluate the accuracy of the classification using the validation
    dataset. The confusion matrix can be plotted using SynapseML tools
    as well, Select the code cell and click on the play button to
    execute cell.

<img src="./media/image82.png"
style="width:6.89593in;height:4.90417in" />

<img src="./media/image83.png" style="width:6.5in;height:3.28333in" />

29. Confusion Matrix for Random Forest Classifier with maximum depth of
    4 and 4 features. Select the code cell and click on the play button
    to execute cell.

<img src="./media/image84.png" style="width:6.5in;height:4.60833in" />

30. Confusion Matrix for Random Forest Classifier with maximum depth of
    8 and 6 features. Select the code cell and click on the play button
    to execute cell.

<img src="./media/image85.png"
style="width:7.03398in;height:4.44583in" />

31. Confusion Matrix for LightGBM. Select the code cell and click on the
    play button to execute cell.

<img src="./media/image86.png"
style="width:6.49167in;height:4.95833in" />

## **Task 8: Perform batch scoring and save predictions to a lakehouse**

In this task, you'll learn to import the registered LightGBMClassifier
model that was trained in part 3 using the Microsoft Fabric MLflow model
registry, and perform batch predictions on a test dataset loaded from a
lakehouse.

** **Microsoft Fabric allows you to operationalize machine learning
models with a scalable function called PREDICT, which supports batch
scoring in any compute engine. You can generate batch predictions
directly from a Microsoft Fabric notebook or from a given model's item
page. Learn about [PREDICT](https://aka.ms/fabric-predict).

To generate batch predictions on the test dataset, you'll use version 1
of the trained LightGBM model that demonstrated the best performance
among all trained machine learning models. You'll load the test dataset
into a spark DataFrame and create an MLFlowTransformer object to
generate batch predictions. You can then invoke the PREDICT function
using one of following three ways:

- Transformer API from SynapseML

- Spark SQL API

- PySpark user-defined function (UDF)

1.  Now, click on **FabricData_Sciencelakehouse** on the left-sided
    navigation pane

<img src="./media/image63.png"
style="width:6.49167in;height:4.70833in" />

2.  In the Fabric**Data_Sciencelakehouse** page, select **Open
    notebook** \> **Existing notebook** from the top navigation menu.

> <img src="./media/image33.png" style="width:6.5in;height:3.13333in"
> alt="A screenshot of a computer Description automatically generated" />

3.  From the list of **Open existing notebook**, select
    the **4-predict** notebook and select **Open**.

<img src="./media/image87.png"
style="width:5.5125in;height:5.18034in" />

4.  If the imported notebook includes output, select the **Edit** menu,
    then select **Clear all outputs**.

<img src="./media/image88.png" style="width:6.5in;height:2.49167in" />

<img src="./media/image89.png" style="width:6.5in;height:4.08889in"
alt="A screenshot of a computer Description automatically generated" />

5.  Load the test data that you saved in **Task 7**. Select the code
    cell and click on the play button to execute cell.

<img src="./media/image90.png"
style="width:7.05203in;height:3.77917in" />

6.  The MLFlowTransformer object is a wrapper around the MLFlow model
    that you registered in Part 3. It allows you to generate batch
    predictions on a given DataFrame. To instantiate the
    MLFlowTransformer object, you'll need to provide the following
    parameters:

- The columns from the test DataFrame that you need as input to the
  model (in this case, you would need all of them).

- A name for the new output column (in this case, predictions).

- The correct model name and model version to generate the predictions
  (in this case, lgbm_sm and version 1).

7.  Select the code cell and click on the play button to execute cell.

<img src="./media/image91.png"
style="width:7.11806in;height:2.60417in" />

8.  Now that you have the MLFlowTransformer object, you can use it to
    generate batch predictions. Select the code cell and click on the
    play button to execute cell.

<img src="./media/image92.png"
style="width:6.98983in;height:3.74583in" />

9.  The code invokes the PREDICT function with the Spark SQL API. Select
    the code cell and click on the play button to execute cell.

<img src="./media/image93.png"
style="width:7.07242in;height:3.70417in" />

10. The code invokes the PREDICT function with a PySpark UDF. Select the
    code cell and click on the play button to execute cell.

<img src="./media/image94.png"
style="width:7.03945in;height:3.5875in" />

11. Once you have generated batch predictions, write the model
    prediction results back to the lakehouse. Select the code cell and
    click on the play button to execute cell.

<img src="./media/image95.png" style="width:6.49167in;height:3.275in" />

## **Task 9: Visualize predictions with a Power BI report**

1.  Now, click on **FabricData_Sciencelakehouse** on the left-sided
    navigation pane

<img src="./media/image63.png" style="width:3.02083in;height:4.70833in"
alt="A screenshot of a computer Description automatically generated" />

2.  Select **New semantic model** on the top ribbon.

<img src="./media/image96.png" style="width:6.25in;height:4.26667in" />

3.  In the **New dataset** box, enter the dataset a name, such as **bank
    churn predictions** .Then select
    the **customer_churn_test_predictions** dataset and
    select **Confirm**.

<img src="./media/image97.png"
style="width:4.44167in;height:5.65833in" />

4.  Add a new measure for the churn rate.

<!-- -->

4)  Select **New measure** in the top ribbon. This action adds a new
    item named **Measure** to
    the **customer_churn_test_predictions** dataset, and opens a formula
    bar above the table.

> <img src="./media/image98.png" style="width:6.5in;height:4.525in" />

5)  To determine the average predicted churn rate, replace Measure = in
    the formula bar with:

> ```PythonCopy
>
> Churn Rate = AVERAGE(customer_churn_test_predictions\[predictions\])
>
<img src="./media/image99.png" style="width:6.5in;height:5.55833in" />

6)  To apply the formula, select the **check mark** in the formula bar.
    The new measure appears in the data table. The calculator icon shows
    it was created as a measure.

<img src="./media/image100.png"
style="width:7.27614in;height:4.2125in" />

7)  Change the format from **General** to **Percentage** in
    the **Properties** panel.

8)  Scroll down in the **Properties** panel to change the **Decimal
    places** to 1.

 <img src="./media/image101.png" style="width:6.49167in;height:3.9in" />

9.  Add a new measure that counts the total number of bank customers.
    You'll need it for the rest of the new measures.

<!-- -->

10)  Select **New measure** in the top ribbon to add a new item
    named **Measure** to the customer_churn_test_predictions dataset.
    This action also opens a formula bar above the table.

<img src="./media/image102.png"
style="width:6.49167in;height:4.38333in" />

11)  Each prediction represents one customer. To determine the total
    number of customers, replace Measure = in the formula bar with:

> ```PythonCopy
>
> Customers = COUNT(customer_churn_test_predictions[predictions])
>
 <img src="./media/image103.png" style="width:6.49167in;height:4.3in" />

12)  Select the **check mark** in the formula bar to apply the formula.

> <img src="./media/image104.png"
> style="width:6.30238in;height:3.4625in" />

13.  Add the churn rate for Germany.

14.  Select **New measure** in the top ribbon to add a new item
        named **Measure** to the customer_churn_test_predictions
        dataset. This action also opens a formula bar above the table.

<img src="./media/image105.png"
style="width:6.49167in;height:4.59167in" />

15.  To determine the churn rate for Germany, replace Measure = in the
    formula bar with:

> ```Copy
> Germany Churn = CALCULATE(customer_churn_test_predictions[Churn Rate],customer_churn_test_predictions[Geography_Germany] = 1)

<img src="./media/image106.png"
 style="width:6.49167in;height:4.20833in" />

This filters the rows down to the ones with Germany as their geography
(Geography_Germany equals one).

16.  To apply the formula, select the **check mark** in the formula bar.

<img src="./media/image107.png"
style="width:6.1875in;height:3.42917in" />

17.  Repeat the above step to add the churn rates for France and Spain.

<!-- -->

18)  **Spain's churn rate**: Select **New measure** in the top ribbon to
    add a new item named **Measure** to the
    customer_churn_test_predictions dataset. This action also opens a
    formula bar above the table.

19)  Select the **check mark** in the formula bar to apply the formula

> ```Copy
>Spain Churn = CALCULATE(customer_churn_test_predictions[Churn Rate],customer_churn_test_predictions[Geography_Spain] = 1)

<img src="./media/image108.png"
style="width:7.1103in;height:3.6875in" />

20)  France's churn rate: Select **New measure** in the top ribbon to add
    a new item named **Measure** to the customer_churn_test_predictions
    dataset. This action also opens a formula bar above the table.

21)  Select the **check mark** in the formula bar to apply the formula

>```PythonCopy
> France Churn =CALCULATE(customer_churn_test_predictions\[Churn Rate\],customer_churn_test_predictions\[Geography_France\] = 1)
>
 <img src="./media/image109.png"
 style="width:7.04711in;height:3.59583in" />

## **Task 10: Create new report**

1.  On the tools at the top of the dataset page, select **New report**
    to open the Power BI report authoring page.

<img src="./media/image110.png"
style="width:6.49167in;height:3.59167in" />

2.  In the Ribbon, select **Text box**. Type in **Bank Customer Churn**.
    **Highlight** the **text** Change the font size and background color
    in the Format panel. Adjust the font size and color by selecting the
    text and using the format bar.

<img src="./media/image111.png"
style="width:7.30829in;height:2.94583in" />

<img src="./media/image112.png"
style="width:7.10287in;height:3.29798in" />

3.  In the Visualizations panel, select the **Card** icon. From
    the **Data** pane, select **Churn Rate**. Change the font size and
    background color in the Format panel. Drag this visualization to the
    top right of the report.

<img src="./media/image113.png"
style="width:5.275in;height:6.20833in" />

<img src="./media/image114.png" style="width:6.5in;height:3.63958in"
alt="A screenshot of a computer Description automatically generated" />

4.  In the Visualizations panel, select the **Line and stacked column
    chart** icon. Select **age** for the x-axis, **Churn Rate** for
    column y-axis, and **Customers** for the line y-axis.

<img src="./media/image115.png"
style="width:7.3672in;height:3.98978in" />

5.  In the Visualizations panel, select the **Line and stacked column
    chart** icon. Select **NumOfProducts** for x-axis, **Churn
    Rate** for column y-axis, and **Customers** for the line y-axis.

> <img src="./media/image116.png"
> style="width:4.44167in;height:7.01667in" />

<img src="./media/image117.png" style="width:7.34635in;height:4.22415in"
alt="A screenshot of a computer Description automatically generated" />

6.  In the Visualizations panel, select the **Stacked column
    chart** icon. Select **NewCreditsScore** for x-axis and **Churn
    Rate** for y-axis.

> <img src="./media/image118.png"
> style="width:4.38333in;height:6.54167in" />

7.  Change the title **NewCreditsScore** to **Credit Score** in the
    Format panel. Select **Format your visuals** and dropdown the
    **X-axis**, enter the Title text as **Credit Score.**

> <img src="./media/image119.png"
> style="width:4.025in;height:6.70833in" />
>
> <img src="./media/image120.png"
> style="width:7.11321in;height:3.8625in" />

8.  In the Visualizations panel, select the **Clustered column
    chart** card. Select **Germany Churn**, **Spain Churn**, **France
    Churn** in that order for the y-axis.

> <img src="./media/image121.png"
> style="width:4.425in;height:7.01667in" />
>
> <img src="./media/image122.png" style="width:6.9627in;height:3.85552in"
> alt="A screenshot of a computer Description automatically generated" />

The Power BI report shows:

- Customers who use more than two of the bank products have a higher
  churn rate although few customers had more than two products. The bank
  should collect more data, but also investigate other features
  correlated with more products (see the plot in the bottom left panel).

- Bank customers in Germany have a higher churn rate than in France and
  Spain (see the plot in the bottom right panel), which suggests that an
  investigation into what has encouraged customers to leave could be
  beneficial.

- There are more middle aged customers (between 25-45) and customers
  between 45-60 tend to exit more.

- Finally, customers with lower credit scores would most likely leave
  the bank for other financial institutes. The bank should look into
  ways that encourage customers with lower credit scores and account
  balances to stay with the bank.
