NYC Taxi Carbon Emissions Analysis

Project Overview: This project analyzes the carbon emissions generated by NYC taxis in 2015, using the NYC Taxi Limousine Commission dataset. The analysis was conducted on Azure Databricks using Python, with the results visualized using matplotlib.
The project demonstrates the ability to process large datasets, compute environmental impacts (CO2 emissions), and generate actionable insights for sustainability.

Steps to Reproduce the Project:
  1. Setup Azure Storage and Upload Data
    a. Create an Azure Storage Account:
    b. Navigate to the Azure portal and create a storage account.
    c. Set up a Blob Storage Container in the storage account.
    d. Upload the NYC Taxi 2015 dataset:
    e. Download the NYC Taxi dataset for 2015 from NYC Taxi Data.
    f. Upload the .parquet files for the full year into your Blob Storage Container.
2. Mount Data in Databricks:
    a. Access Azure Databricks:
    b. Set up a Databricks Workspace in Azure.
    c. Mount the Blob storage to Databricks:
    Use the following Python code to mount the storage container to Databricks:
    
        #python
        # Replace with your Azure Storage credentials
        storage_account_name = "your_storage_account"
        container_name = "your_container"
        sas_token = "your_sas_token"

        dbutils.fs.mount(
          source = f"wasbs://{container_name}@{storage_account_name}.blob.core.windows.net",
          mount_point = "/mnt/nyctaxi",
          extra_configs = {f"fs.azure.sas.{container_name}.{storage_account_name}.blob.core.windows.net": sas_token}
        )


3. Process Data in Databricks

  a. Load the Parquet data:
  Load the 12 .parquet files for each month into Databricks using the spark.read.parquet() method.
  
  b. Calculate fuel consumption and CO2 emissions:
  Use the following formula to calculate the fuel consumed and CO2 emissions for each trip:

    #  Python code to calculate emissions
    df = df.withColumn('fuel_consumed_gallons', df['trip_distance'] / 22)
    df = df.withColumn('co2_emissions_kg', df['fuel_consumed_gallons'] * 8.89)

  c. Create passenger group categories:
  Split passengers into two groups: 1-2 passengers and 3 or more passengers.

    python
    
    from pyspark.sql.functions import when
    
    df = df.withColumn('passenger_group', 
                       when(df['passenger_count'] <= 2, '1-2 Passengers')
                       .otherwise('3+ Passengers'))

4. Generate Visualizations
  Compare emissions based on passenger groups:
  Use matplotlib in Databricks to visualize the emissions by date and passenger group:

        import matplotlib.pyplot as plt
        # Group data by passenger group and date
        emissions_data = df.groupBy('pickup_date', 'passenger_group') \
                           .sum('co2_emissions_kg') \
                           .toPandas()
        
        # Create plot
        plt.plot(emissions_data['pickup_date'], emissions_data['sum(co2_emissions_kg)'], label='1-2 Passengers')
        plt.xlabel('Date')
        plt.ylabel('Total Emissions (kg)')
        plt.title('Daily CO2 Emissions by Passenger Groups')
        plt.legend()
        plt.show()

  Store the resulting visualizations:
  Save the generated plots in the /results directory.
5. View Results
Results: The results, including the processed data and visualizations, can be found in the /results directory. For example, the chart comparing daily emissions for different passenger groups.

Project Files
/scripts/processing_script.py: Python script for loading data, calculating emissions, and processing.
/notebooks/emissions_analysis.ipynb: Databricks notebook used for data analysis and visualization.
/results/emissions_chart.png: Visualization comparing emissions of 1-2 passenger trips with 3+ passenger trips.

Conclusion: This project showcases how Azure Databricks can be used to process large datasets, compute carbon emissions, and visualize results. The insights generated can help inform strategies to reduce environmental impacts from taxi operations in NYC.

Additional Instructions:

Upload Files to GitHub:

Upload your Python script, Databricks notebook, and result files (charts/visualizations) to your GitHub repository.
Ensure the repository is public and organized with clear folder structures as per the structure provided earlier.
Customize the GitHub Repository:

Add a clear description to your repository and include relevant tags such as "Azure", "Databricks", "Carbon Emissions", "NYC Taxi", etc.
Make sure the README.md file is well-formatted and easy to read.




