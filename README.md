# Synthetic Data Generator Project for Lake Databases

This repository contains a notebook which creates synthetic data for a Lake Database. It does fill data on all the tables of a lake database often created with a database template. The templates are pure metadata and are created empty.
It is designed to populate an empty database. If the lake database data exists, it will be deleted. 
The created tables size order of magnitude will be 1x, 10x and 100x from the base size. Base size of tables is 1000 rows. We can pass the size parameter to the creation method. Table size is generated with a 10% random variation to avoid having the exact same length. 

## Purpose

Often, we will create an empty lake database from the database industry templates. This notebook creates artificial data to allow for basic testing and demos of the lake databases.

## Prerequisites

- A Synapse Workspace with an existing Lake Database. Creating that database from the lake database templates is a simple manner to generate a good starting point for a dummy environment. 
- A Spark cluster with the Python Faker library installed.

## Configuration

If you have not created a lake database yet, open the synapse workspace Gallery and select one of the templates. During that creatin step you should:

1.	Select the tables to be created 
2.	give your new database a name,
3.	select the lake folder used by the db (verify it’s empty).
4.	and select the type of database format supported, text delimited or Parquet (better select the second one / Parquet):

Once created, the lake database has no data. At this point we should create a Synapse Spark cluster with a midsize node (8 cores) and an elastic number of workers from 3-6, and add a requirements.txt file to include the python package faker in the cluster.
Open the synthetic data generator notebook. You must introduce the name of the lake database in the notebook first cell. Then we can execute the cells of the notebook. The first cell contains configuration and libraries. The second cell contains the python class definition, the creation of one instance of the generator and its execution.  

## Foreign keys and value distributions

This process generates tables and populates them with arbitrary data that fits into the type definition. Primary keys expect to be composed of the tablename with the suffix Id. The secondary keys are generated as with the name of the secondarytable and the suffix Id. The generator determines the number of rows to be created. Foreign key are valid as:
- Primary key is an integer sequence generated from 1 to n elements, 
- Secondary keys are random integers from 1 to n being n the length of secondary table. The distribution of these keys is uniform.

## Customization

This process generates some unrealistic values. There is no business logic related to the dates. For example, a contract start date and contract end date in real data are linked, so that end date must be bigger than contract start, moreover sometimes we might need to introduce a minimum (typical) contract length or a certain specific length distribution.
To simulate certain distributions creation a specific distribution of foreign keys could help us to simulate specific synthetic data distributions avoiding the all-uniform we have generated. That might be done after the first generation has already been performed or modifying the original methods of the class in the notebook. 

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft 
trademarks or logos is subject to and must follow 
[Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.
Any use of third-party trademarks or logos are subject to those third-party's policies.
