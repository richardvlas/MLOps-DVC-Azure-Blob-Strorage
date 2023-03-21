# MLOps with DVC & Azure Blob Storage
Demonstrating MLOps workflow with DVC and Azure Blob Storage for versioning and storage of machine learning data.

In this tutorial, we introduce DVC (data version control) and explain how to transfer and manage large datasets that are too big to store in Git repositories. DVC is a tool that works with Git to assist in managing code and data while helping to store the data somewhere else, but still accessible to someone who might clone the project later.

## Why DVC is useful in CI/CD approach

In the continuous integration and continuous delivery (CI/CD) approach, it's important to ensure that any changes to the code or data do not break the pipeline. Git is often used to version control the code, but storing large datasets in Git can slow down the process and create issues in the pipeline. 

This is where DVC comes in. By using DVC to version control large datasets, you can avoid slowing down the pipeline while still maintaining the ability to track changes to the data. Additionally, DVC can be used to manage the data pipeline, enabling you to automate the pipeline and ensure that it runs smoothly.

## Requirements

- Git
- Python
- DVC
- Azure Account for Remote Storage (alternatives are Google Drive account, S3, Azure Blob Storage, etc.)

## Getting started

### Create a GitHub repository

Create a new GitHub repository with a README file that provides an overview of the repository's purpose and contents. 

### Clone the repository into a local directory
- Copy the repository's URL by clicking on the green "Code" button and selecting "HTTPS".
- Open a terminal on your local machine and navigate to the directory where you want to clone the repository.
- Run the command `git clone <repository_url>` to clone the repository to your local machine.

### Create Python scripts for analyzing and generating data
  
Use the files from this repository:
    
```
analyze.py
get_data.py
```
  
### Set up DVC for versioning and managing data
The `dvc init` command initializes a new DVC repository in your current working directory. It creates the necessary files and directories needed to manage your data and pipelines with DVC, including the `.dvc` directory which contains the configuration and metadata files used by DVC.

The output will look something like the following snippet:

```
Initialized DVC repository.

You can now commit the changes to git.

+---------------------------------------------------------------------+
|                                                                     |
|        DVC has enabled anonymous aggregate usage analytics.         |
|     Read the analytics documentation (and how to opt-out) here:     |
|             <https://dvc.org/doc/user-guide/analytics>              |
|                                                                     |
+---------------------------------------------------------------------+
```

### Create Azure Storage account
To create an Azure Storage account, follow these steps:

1. Go to the Azure portal and log in with your account credentials
2. Click on **Create a resource** and search for **Storage account** in the search bar.
3. Select **Storage account** from the search results and click on **Create**.
4. Follow the steps to create the account
5. Click on **Review + create** and then **Create** to create the storage account.
6. Create a new Blob container in your storage account
7. Once the storage account is created, navigate to the **Access keys** tab and copy one of the connection strings.
8. Paste the connection string into a text file and save it for later use in the DVC configuration.

### Set up a DVC remote storage for data
We will use the Azure storage set up in the previous step. 

### Add the remote storage to DVC
Runn `dvc remote add -d myremote TODO`

### Add data to DVC by running `dvc add <data-file>`.

### Commit the changes
Run `git add . && git commit -m "Add DVC tracked data"`

### Push the changes to Github 
Run `git push`

### Push the data to the DVC remote
Run `DVC push`

## Accessing data on another machine

1. Clone the GitHub repository on another machine.
2. Pull the data from the DVC remote by running `DVC pull`.

## Conclusion
In this tutorial, you learned how to transfer and manage large datasets with DVC, a tool that works with Git to assist in managing code and data while helping to store the data somewhere else. By using DVC, you can avoid slowing down the pipeline in a CI/CD approach while still maintaining the ability to track changes to the data.
