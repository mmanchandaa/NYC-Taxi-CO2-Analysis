**Azure Data Storage and Databricks Data Processing Project**

## **Project Overview**

This project demonstrates how to upload files into an Azure Storage Account container and process them in Databricks using Python. The project showcases my knowledge of cloud computing services, data storage, and big data processing.

## **Key Features**
- Uploading data to Azure Storage Account containers.
- Processing large datasets using Databricks on Azure.
- CO2 emissions calculation using New York Taxi Data.
- Clear step-by-step instructions for replicating the process.

## **Technologies Used**
- **Microsoft Azure**: For cloud storage and data pipeline setup.
- **Azure Databricks**: For big data processing and calculations.
- **Python**: For processing data and performing CO2 emission analysis.
- **GitHub**: For version control and showcasing the project.

---

## **Setup and Installation Instructions**

### **Step 1: Upload Files to Azure Storage Account**

1. Sign in to your Azure Portal.
2. Create a new **Storage Account** and **Blob Container** within it.
3. Upload your dataset files into the container (e.g., NYC Taxi trip data files).
4. Generate a **Shared Access Signature (SAS)** token for secure access to the storage files.

### **Step 2: Access the Storage Account from Databricks**

1. Open your Databricks workspace on Azure.
2. Use the following code to mount the Azure Storage Blob container to Databricks.

   ```python
   dbutils.fs.mount(
       source = "wasbs://<container>@<storage-account>.blob.core.windows.net/",
       mount_point = "/mnt/<mount-name>",
       extra_configs = {"<conf-key>": "<sas-token>"}
   )
   ```

### **Step 3: Load the Data in Databricks**

1. After mounting the storage, use the following Python code to read the data:

   ```python
   df = spark.read.parquet("/mnt/<mount-name>/your_data.parquet")
   df.show()
   ```

2. Perform CO2 emissions calculations using the formula:  
   `CO2 Emissions = (Trip Distance / 22) * 8.89`.

### **Step 4: Data Processing in Databricks**

1. Calculate fuel consumption and CO2 emissions for each trip:

   ```python
   df = df.withColumn('fuel_consumed_gallons', df['trip_distance'] / 22)
   df = df.withColumn('co2_emissions_kg', df['fuel_consumed_gallons'] * 8.89)
   ```

2. Analyze emissions based on trip distance and passenger count.

### **Step 5: Visualize the Results**

1. Use `matplotlib` or Databricks built-in visualization tools to create comparison charts of CO2 emissions based on the number of passengers.

---

## **How to Run the Project Locally**

1. Clone this GitHub repository:
   ```bash
   git clone https://github.com/mmanchandaa/
   ```
2. Follow the setup steps to upload data to Azure Storage.
3. Use Databricks on Azure to run the Python scripts included in the repository.

---

## **Project Files**

- `q333333.ipynb`: Databricks notebook with step-by-step data processing instructions.

---

## **Screenshots**

Screenshots of the Databricks notebooks and Azure pipeline setup.
![image](https://github.com/user-attachments/assets/01380e11-f0a5-40f6-8b0f-a39ad1965d1d)
![image](https://github.com/user-attachments/assets/940a3dbe-1a39-4606-afca-1f4db2960b60)
![image](https://github.com/user-attachments/assets/3fb6c361-ef3f-46eb-99cd-a91b529fd1dd)
![image](https://github.com/user-attachments/assets/7b1a2580-9a56-4725-b126-e5dfce55b8fb)
![image](https://github.com/user-attachments/assets/b5188626-f003-45af-8cbb-01805bac46b2)

---

## **Conclusion**

This project demonstrates how to efficiently manage and process large datasets in a cloud environment using Azure and Databricks. It highlights skills in cloud data storage, data processing, and environmental impact analysis.

---

## **Links**

- **GitHub Profile**: https://github.com/mmanchandaa
- **Project Repository**: https://github.com/mmanchandaa/NYC-Taxi-CO2-Analysis

---

