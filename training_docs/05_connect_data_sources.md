# Add your datasets to `data`

In this section, we discuss the data set-up phase. The steps are as follows:

* Add datasets to your `data/` folder, according to [data engineering convention](https://kedro.readthedocs.io/en/stable/12_faq/01_faq.html#what-is-data-engineering-convention)
* Register the datasets with the Data Catalog in `conf/base/catalog.yml`, which is the registry of all data sources available for use by the project. This ensures that your code is reproducible when it references datasets in different locations and/or environments.

You can find further information about [the Data Catalog](https://kedro.readthedocs.io/en/stable/05_data/01_data_catalog.html) in specific documentation covering advanced usage.


## Add your datasets to `data`

The spaceflights tutorial makes use of fictional datasets of companies shuttling customers to the Moon and back. You will use the data to train a model to predict the price of shuttle hire. However, before you get to train the model, you will need to prepare the data for model building by creating a master table.

The spaceflight tutorial has three files and uses two data formats: `.csv` and `.xlsx`. Download and save the files to the `data/01_raw/` folder of your project directory:

* [reviews.csv](https://kedro-org.github.io/kedro/reviews.csv)
* [companies.csv](https://kedro-org.github.io/kedro/companies.csv)
* [shuttles.xlsx](https://kedro-org.github.io/kedro/shuttles.xlsx)

Here are some examples of how you can [download the files from GitHub](https://www.quora.com/How-do-I-download-something-from-GitHub) to the `data/01_raw` directory inside your project:

Using [cURL in a Unix terminal](https://curl.se/download.html):

<details>
<summary><b>Click to expand</b></summary>

```bash
# reviews
curl -o data/01_raw/reviews.csv https://kedro-org.github.io/kedro/reviews.csv
# companies
curl -o data/01_raw/companies.csv https://kedro-org.github.io/kedro/companies.csv
# shuttles
curl -o data/01_raw/shuttles.xlsx https://kedro-org.github.io/kedro/shuttles.xlsx
```
</details>

Using [cURL for Windows](https://curl.se/windows/):

<details>
<summary><b>Click to expand</b></summary>

```bat
curl -o data\01_raw\reviews.csv https://kedro-org.github.io/kedro/reviews.csv
curl -o data\01_raw\companies.csv https://kedro-org.github.io/kedro/companies.csv
curl -o data\01_raw\shuttles.xlsx https://kedro-org.github.io/kedro/shuttles.xlsx
```
</details>

Using [Wget in a Unix terminal](https://www.gnu.org/software/wget/):

<details>
<summary><b>Click to expand</b></summary>

```bash
# reviews
wget -O data/01_raw/reviews.csv https://kedro-org.github.io/kedro/reviews.csv
# companies
wget -O data/01_raw/companies.csv https://kedro-org.github.io/kedro/companies.csv
# shuttles
wget -O data/01_raw/shuttles.xlsx https://kedro-org.github.io/kedro/shuttles.xlsx
```
</details>

Using [Wget for Windows](https://eternallybored.org/misc/wget/):

<details>
<summary><b>Click to expand</b></summary>

```bat
wget -O data\01_raw\reviews.csv https://kedro-org.github.io/kedro/reviews.csv
wget -O data\01_raw\companies.csv https://kedro-org.github.io/kedro/companies.csv
wget -O data\01_raw\shuttles.xlsx https://kedro-org.github.io/kedro/shuttles.xlsx
```
</details>

## Register the datasets

You now need to register the datasets so they can be loaded by Kedro. All Kedro projects have a `conf/base/catalog.yml` file, and you register each dataset by adding a named entry into the `.yml` file. The entry should include the following:

* File location (path)
* Parameters for the given dataset
* Type of data
* Versioning

Kedro supports a number of different data types, and those supported can be found in the API documentation. Kedro uses [`fssspec`](https://filesystem-spec.readthedocs.io/en/latest/) to read data from a variety of data stores including local file systems, network file systems, cloud object stores and HDFS.


### `csv`

For the spaceflights data, first register the `csv` datasets by adding this snippet to the end of the `conf/base/catalog.yml` file:

```yaml
companies:
  type: pandas.CSVDataSet
  filepath: data/01_raw/companies.csv

reviews:
  type: pandas.CSVDataSet
  filepath: data/01_raw/reviews.csv
```

To check whether Kedro can load the data correctly, open a `kedro ipython` session and run:

```python
companies = catalog.load("companies")
companies.head()
```

The command loads the dataset named `companies` (as per top-level key in `catalog.yml`) from the underlying filepath `data/01_raw/companies.csv` into the variable `companies`, which is of type `pandas.DataFrame`. The `head` method from `pandas` then displays the first five rows of the DataFrame.

When you have finished, close `ipython` session as follows:

```python
exit()
```

### `xlsx`

Now register the `xlsx` dataset by adding this snippet to the end of the `conf/base/catalog.yml` file:

```yaml
shuttles:
  type: pandas.ExcelDataSet
  filepath: data/01_raw/shuttles.xlsx
```

To test that everything works as expected, load the dataset within a _new_ `kedro ipython` session and display its first five rows:

```python
shuttles = catalog.load("shuttles")
shuttles.head()
```
When you have finished, close `ipython` session as follows:

```python
exit()
```

## Custom data

Kedro supports a number of datasets out of the box, but you can also add support for any proprietary data format or filesystem in your pipeline.

You can find further information about [how to add support for custom datasets](https://kedro.readthedocs.io/en/stable/07_extend_kedro/03_custom_datasets.html) in specific documentation covering advanced usage.


_[Go to the next page](./06_jupyter_notebook_workflow.md)_
