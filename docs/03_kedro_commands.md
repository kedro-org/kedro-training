## Kedro commands

The list and the behaviour of Kedro CLI commands may vary depending of the working directory where Kedro command is executed. Kedro has 2 command types:

* Global commands (e.g., `kedro new`, `kedro info`) which work regardless of the current working directory
* Local or project-specific commands (e.g., `kedro run`, `kedro install`) that require the current working directory to be the root of your Kedro project

To see the full list of available commands, you can run `kedro --help` or consult [Kedro's command line documentation](https://kedro.readthedocs.io/en/stable/09_development/03_commands_reference.html).

### `kedro install`

This command allows you to easily install or update all your project third-party Python package dependencies. This is roughly equivalent to `pip install -r src/requirements.txt`, however `kedro install` is a bit smarter on Windows when it needs to upgrade its version. It also makes sure that the dependencies are always installed in the same virtual environment as Kedro.

One more very useful command is `kedro build-reqs`, which takes `requirements.in` file (or `requirements.txt` if the first one does not exist), resolves all package versions and 'freezes' them by putting pinned versions back into `requirements.txt`. It significantly reduces the chances of dependencies issues due to downstream changes as you would always install the same package versions.

#### Example

Let's install and try [Kedro Viz](https://github.com/quantumblacklabs/kedro-viz) so you can visualise your Kedro pipelines. You can do this by running the following commands from the terminal:

```bash
echo "kedro-viz>=3.0" >> src/requirements.txt  # src\requirements.txt on Windows
kedro build-reqs  # creates src/requirements.in and pins package versions in src/requirements.txt
kedro install  # installs packages from src/requirements.txt
kedro viz  # start Kedro Viz server
```