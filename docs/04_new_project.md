# Create a new project

This section mirrors the [spaceflights tutorial in the Kedro documentation](https://kedro.readthedocs.io/en/stable/03_tutorial/01_spaceflights_tutorial.html).

Navigate to your chosen working directory and run the following to [create a new empty Kedro project](https://kedro.readthedocs.io/en/stable/02_get_started/04_new_project.html#create-a-new-project-interactively) using the default interactive prompts:

```bash
kedro new
```

This will ask you to specify:

1. Project name - you can call it `Kedro Training`
2. Repository name - accept the default by pressing the `Enter` key
3. Python package name - accept the default by pressing the `Enter` key

Change your working directory so that you are in your newly created project folder with:

```bash
cd kedro-training
```

### Project structure
Take a few minutes to familiarise yourself with the [Kedro project structure](https://kedro.readthedocs.io/en/stable/02_get_started/05_example_project.html#project-directory-structure) by exploring the contents of `kedro-training` folder.

## Credentials management

For security reasons, we strongly recommend not committing any credentials or other secrets to the Version Control System. By default any file inside the `conf` folder (and subfolders) in your Kedro project containing `credentials` word in its name will be ignored and not committed to your repository.

Please bear it in mind when you start working with Kedro project that you have cloned from GitHub, for example, as you might need to configure required credentials first. 

>**Note**: If you maintain a project, you should document how to configure any required credentials in your project's documentation.

The Kedro documentation lists some [best practices to avoid leaking confidential data](https://kedro.readthedocs.io/en/stable/02_get_started/05_example_project.html#what-best-practice-should-i-follow-to-avoid-leaking-confidential-data).

### Storing credentials in `conf/local`

When it runs, Kedro automatically reads credentials from the `conf` folder and feeds them into the Data Catalog, which is responsible for loading and saving data as inputs and outputs of pipeline nodes. You can configure your credentials once and then reuse them in multiple datasets.

Example of `conf/local/credentials.yml`:

```yaml
dev_s3:
  client_kwargs:
    aws_access_key_id: key
    aws_secret_access_key: secret
```

Example of the dataset using those credentials defined in `conf/base/catalog.yml`:

```yaml
cars:
  type: pandas.CSVDataSet
  filepath: s3://my_bucket/data/02_intermediate/company/cars.csv
  credentials: dev_s3
```

_[Go to the next page](./05_connect_data_sources.md)_
