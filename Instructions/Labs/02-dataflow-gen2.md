# Exercise 2: Create a Dataflow (Gen2) in Microsoft Fabric

### Estimated Duration: 50 Minutes

## Lab Scenario 

With the high-volume historical sales data (2019–2021) successfully processed using Spark, you now need to ingest weekly promotion and store lookup data into the Contoso Retail analytics platform.

Unlike the massive e-commerce datasets, this operational data is smaller but requires frequent updates and quick, low-code formatting fixes before it can be used for reporting.

In this exercise, you will create a Dataflow (Gen2) using Power Query Online to ingest and clean this promotional data. You will configure your fabric_Lakehouse as the final data destination and then integrate the completed dataflow into a Fabric Data Pipeline to automate the ingestion workflow.

## Overview

In this exercise, you will create and manage Dataflows (Gen2) within Microsoft Fabric to ingest, transform, and prepare data for analysis. You will learn how to build a dataflow to connect to various data sources, apply transformations using Power Query Online, configure data destinations for storing processed data in a lakehouse, and integrate the dataflow into a pipeline to automate data processing workflows.

## Lab objectives

You will be able to complete the following tasks:

- Task 1: Create a Dataflow (Gen2) to ingest data
- Task 2: Add data destination for Dataflow
- Task 3: Add a dataflow to a pipeline

## Task 1: Create a Dataflow (Gen2) to ingest data

In this task, you will create a Dataflow (Gen2) to efficiently ingest and transform data from multiple sources for analysis. This process streamlines data preparation, enabling you to prepare the data for further processing and insights.

1. From the left pane, click on **fabric-<inject key="DeploymentID" enableCopy="false"/>** **(1)** workspace then select the **fabric-<inject key="DeploymentID" enableCopy="false"/> (2)** workspace.  

    ![](./Images2/2/e2-t2-7.png)

1. In the **fabric-<inject key="DeploymentID" enableCopy="false"/>** workspace, click on **+ New item (1)**, then in the right pane, search for **Dataflow Gen2 (2)** in the search bar, and select **Dataflow Gen2 (3)** under the **Get data** section.

     ![](./Images2/lab3-11-02.png)

1. In the New Dataflow Gen2 dialog, keep the **Name (1)** as default and click **Create (2)** to proceed.

    ![](./Images2/2/e2-t1-3.png)

1. After a few seconds, the Power Query editor for your new dataflow opens as shown here. Select **Import from a Text/CSV file**.

    ![](./Images2/2/t1-3.png)

1. Add the following details and then click **Next (7)**:

    - **Link to file**: *Selected* **(1)**
    - **File path or URL**: `https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/orders.csv` **(2)**
    - **Connection**: Create new connection **(3)**
    - **data gateway**: (none) **(4)**
    - **Authentication kind**: Anonymous **(5)**
    - **Privacy level**: None **(6)**

      ![](./Images2/2/t1-4p.png)

1. Click on **Create** from the bottom-right corner to initiate the data source creation. The Power Query editor shows the data source and an initial set of query steps to format the data, as shown below:

    ![](./Images2/lab3-11-1.png)

1. From the top menu bar, click the **Add column (1)** tab, then select **Custom column (2)** to create a new column.

    ![](./Images2/2/t1-6.png)

1. In the **Custom column** dialog, enter **MonthNo (1)** as the new column name, input the formula `Date.Month([OrderDate])` **(2)**, and then click **OK (3)** to apply.

    ![](./Images2/lab3-11-3.png)

1. The custom column **MonthNo** is now added to the query, and its values are displayed in the data preview pane.

    ![](./Images2/2/t1-8.png)

## Task 2: Add data destination for Dataflow

In this task, you will add a data destination for the Dataflow to determine where the ingested and transformed data will be stored for future use.

1. From the bottom right corner, click the **+ (1)** icon and select **Lakehouse (2)** from the New destination menu.

    ![](./Images2/2/t2-1.png)

   >**Note:** If this option is greyed out, it indicates that a data destination may already be configured. To verify, check the bottom of the Query settings pane on the right side of the Power Query editor. If a destination exists, you can modify it by clicking the gear icon.

1. In the **Connect to data destination** dialog box, keep everything as default and click on **Next**.

    ![](./Images2/2/t2-2.png)

1. From the left pane, expand the **fabric-<inject key="DeploymentID" enableCopy="false"/> (1)**, then select the **dbo (2)** under **fabric-lakehouse<inject key="DeploymentID" enableCopy="false"/>** table. The Table name field will automatically populate with **orders (3)**. Click **Next (4)** to continue.

    ![](./Images2/2/e2-t2-des-target.png)

1. On the **Choose Destination settings** page, toggle **off** the **use automatic settings (1)** option. Then, for the **MonthNo** column header, set the **Source type** to **Whole number (2)**. Finally, click **Save settings (3)** to apply the changes.

    ![](./Images2/lab3-11-4.png)

1. Click the **Save & run (3)** button under **save (2)** dropdown located in the top-left corner of the **Home (1)** ribbon to apply your destination and execute the dataflow.

    ![save the changes](./Images2/2/e2-t2-5.png)

1. Once published, click on the **ellipsis (...) (2)** next to the published **Dataflow (1)** in the workspace, select **Settings (3)**, 

    ![](./Images2/2/e2-t2-6-1.png)

1. Rename the dataflow as **Transform Orders Dataflow (1)** and click on **X** to close.

    ![](./Images2/2/e2-t2-6-2.png)

## Task 3: Add a dataflow to a pipeline

In this task, you will add a dataflow to a pipeline to streamline the data processing workflow and enable automated data transformations.

1. From the left pane, click on **fabric-<inject key="DeploymentID" enableCopy="false"/> workspace (1)**, then select the **fabric-<inject key="DeploymentID" enableCopy="false"/> (2)** workspace.  

     ![](./Images2/e2-t2-7.png)

1. In the **fabric-<inject key="DeploymentID" enableCopy="false"/>** workspace, click on **+ New item (1)**, then in the right pane, search for **Pipeline (2)** in the search bar, and select **Pipeline (3)** under the **Get data** section.

     ![](./Images2/lab3-11-5n.png)

1. In the New pipeline dialog box, enter the name **Load Orders pipeline (1)**, then click **Create (2)**.

    ![](./Images2/2/t3-2.png)
  
   > **Note:** If the Copy Data wizard opens automatically, close it!

1. Select **Pipeline activity (1)** and add a **Dataflow (2)** activity to the pipeline.

    ![](./Images2/2/E2T3S4.png)

1. Select the Dataflow1 activity, go to **Settings (1)** from the bottom pane, choose **fabric-<inject key="DeploymentID" enableCopy="false"/>**  **(2)** as the **Workspace**, and select **Transform Orders Dataflow (3)** as the **Dataflow**.

    ![](./Images2/2/t3-4.png)

     >**Note :** Drag the Settings tab upward to view all available options.
   
1. **Save (1)** the pipeline using the **disk icon** from the top-left, then click **Run (2)** to execute it.

    ![](./Images2/2/t3-5.png)

1. The pipeline run may take a few minutes. Verify its completion under the **Output** tab at the bottom, where the Pipeline status and Activity status should show as Succeeded.

    ![](./Images2/2/t3-6a.png)

1. From the left pane, click on **fabric-<inject key="DeploymentID" enableCopy="false"/> workspace (1)**, then then select the **fabric_lakehouse<inject key="DeploymentID" enableCopy="false"/> (2)**.  

    ![](./Images2/2/e2-lakehouse.png)

1. In the **fabric_lakehouse<inject key="DeploymentID" enableCopy="false"/>** view, expand the **Tables (1)** section, and then select the **orders (2)** table to view the loaded data.

    ![](./Images2/lab3-11-7.png)

   >**Note:** You might have to refresh the browser to get the expected output.

## Summary

In this exercise, you have completed the following:

- Created a Dataflow (Gen2) to ingest data.
- Added a data destination for the Dataflow.
- Added a Dataflow to a pipeline.

### You have successfully completed the exercise. Now, click on **Next >>** from the lower right corner to proceed to the next exercise.
       
![05](./Images2/nextpage.png)
