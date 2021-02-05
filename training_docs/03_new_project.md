# Create a new project

This section mirrors the [spaceflights tutorial in the Kedro documentation](https://kedro.readthedocs.io/en/stable/03_tutorial/01_spaceflights_tutorial.html). 

As we work with the spaceflights tutorial, will follow these steps:

### 1. Set up the project template

* Create a new project with `kedro new`
* Configure the following in the `conf` folder:
	* Logging
	* Credentials
	* Any other sensitive / personal content
* Install project dependencies with `kedro install`

### 2. Set up the data

* Add data to the `data/` folder
* Reference all datasets for the project in `conf/base/catalog.yml`

### 3. Create the pipeline

* Create the data transformation steps as Python functions
* Construct the pipeline by adding your functions as nodes
* Choose how to run the pipeline: sequentially or in parallel

### 4. Package the project

 * Build the project documentation
 * Package the project for distribution


## Create and set up a new project

In this section, we discuss the project set-up phase, which is the first part of the [standard development workflow](./01_spaceflights_tutorial.md#kedro-project-development-workflow). The set-up steps are as follows:


* Create a new project
* Install dependencies
* Configure the project

----
In the text, we assume that you create an empty project and follow the flow of the tutorial by copying and pasting the example code into the project as we describe. This tutorial will take approximately 2 hours and you will learn each step of the Kedro project development workflow, by working on an example to construct nodes and pipelines for the price-prediction model.

However, you may prefer to get up and running more swiftly so we provide the full spaceflights example project as a [Kedro starter](../02_get_started/06_starters.md). 

If you decide to create the example project fully populated with code, navigate to your chosen working directory and run the following:

```bash
kedro new --starter=spaceflights
```

This will generate a project from the [Kedro starter for the spaceflights tutorial](https://github.com/quantumblacklabs/kedro-starters/tree/master/spaceflights) so you can follow the tutorial without any of the copy/pasting.

----

If you prefer to create an empty tutorial and cut and paste the code to follow along with the steps, you should instead run the following to [create a new empty Kedro project](../02_get_started/04_new_project.md#create-a-new-project-interactively) using the default interactive prompts:

```bash
kedro new
```

Feel free to name your project as you like, but this guide will assume the project is named **`Kedro Training`**.

Keep the default names for the `repo_name` and `python_package` when prompted.


### Project structure
Take a few minutes to familiarise yourself with the [Kedro project structure](https://kedro.readthedocs.io/en/stable/02_get_started/05_example_project.html#project-directory-structure) by exploring the contents of `kedro-training` folder.


## Configure the project

You may optionally add in any credentials to `conf/local/credentials.yml` that you would need to load specific data sources like usernames and passwords. Some examples are given within the file to illustrate how you store credentials. Additional information can be found in the [advanced documentation on configuration](../04_kedro_project_setup/02_configuration.md).

When it runs, Kedro automatically reads credentials from the `conf` folder and feeds them into the Data Catalog, which is responsible for loading and saving data as inputs and outputs of pipeline nodes. You can configure your credentials once and then reuse them in multiple datasets.

Example of `conf/local/credentials.yml`:

```yaml
dev_s3:
  client_kwargs:
    aws_access_key_id: key
    aws_secret_access_key: secret
```


For security reasons, we strongly recommend not committing any credentials or other secrets to the Version Control System. By default any file inside the `conf` folder (and subfolders) in your Kedro project containing `credentials` word in its name will be ignored and not committed to your repository.

Please bear it in mind when you start working with Kedro project that you have cloned from GitHub, for example, as you might need to configure required credentials first. 

>**Note**: If you maintain a project, you should document how to configure any required credentials in your project's documentation.

The Kedro documentation lists some [best practices to avoid leaking confidential data](https://kedro.readthedocs.io/en/stable/02_get_started/05_example_project.html#what-best-practice-should-i-follow-to-avoid-leaking-confidential-data).


Example of the dataset using those credentials defined in `conf/base/catalog.yml`:

```yaml
cars:
  type: pandas.CSVDataSet
  filepath: s3://my_bucket/data/02_intermediate/company/cars.csv
  credentials: dev_s3
```

_[Go to the next page](./04_dependencies.md)_
