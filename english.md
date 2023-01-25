<page id="566da7" name="Introduction">

This is a section! You can write any type of content you want here.

### This is a subtitle

According to our style guide, subtitles are `h3`, which means using 3 pads `###`.

### More formatting elements

This is just Markdown. That means you can freely use **bold text**, or *italic text*. Specific keywords should be styled with backticks. For example, we use `seaborn` for visualizations. Or I might ask you to write a `calculator.py` module.

Code blocks are written using backticks and including the language:

```python
import pandas as pd
def add(x, y):
    return x + y
```

Another example:

```sql
SELECT * FROM customers c
WHERE c.created_date > "2021-05-01"
ORDER BY c.last_name
LIMIT 100
```

Finally, introduce notes using the symbol `>` :

> This is an note! It can **also contain** formatting of different types.
Another example

> Hint: Use `python -V` to print the installed version of Python.

### Using images

All your images must be stored LOCALLY in your project. We usually recommend the path `images/`. You can embed them with the standard markdown syntax and make sure you include an `alt` text for accessibility purposes.

A few examples:

![A panda eating bamboo](images/jay-wennington-s-fD5Tpew2k-unsplash.jpg)

A image pasted directly from the clipboard using the [Paste Image VSCode extension](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image):

![a sample pandas code displaying two series](images/2023-01-16-11-41-12.png)

</page>

<page id="f445a7" name="The lab">

The lab of this project is configured using the `docker-compose.yml` file. All the data for your lab goes into the `jupyterlab/` directory. If your lab needs any special modules you can list them in the `requirement.txt` file.

To start the lab just run:

```bash
$ docker compose up
```

Now point your browser to: `http://localhost:5050`

</page>

<page id="68f238" name="Activities">

Remember all these activities are easy to create in VSCode using our snippets: [TODO](https://github.com/datawars-io-content/content-creator-handbook#-visual-studio-code)

### Single answer activities

This will render an input of text for the student to provide the correct answer.

<activity id="506c6b" title="What's the result of `3 + 9`?" type="input">

Just type your answer and click "Check"...

<correct-answer>12</correct-answer>
<hint>Use your phone calculator!</hint>
<solution>The result is `12`.</solution>
</activity>

### Multiple choice

These activities are of type `type="multiple-choice"` and the only thing it chances is the `widget`. If of type `radio`, it has only one correct answer. If the type is `checkbox` it accepts multiple valid answers.

<activity id="883ad7" title="Single Answer Multiple Choice Activity" type="multiple-choice" widget="radio">

This accepts only one correct answer. For example:

What is the result of `2 + 2`?

<answer id="1e9366" is-correct>4</answer>
<answer id="2465bd">10</answer>
<answer id="37b056">3</answer>
<answer id="4ed1cd">-4</answer>
<hint>Try your phone calculator!</hint>
<solution>The correct answer is `4`.</solution>
</activity>

<activity id="7fb8cb" title="Multiple Answer Multiple Choice activity" type="multiple-choice" widget="checkbox">

This activity has 2 correct answers. For example, it could be:

What of the following are valid fruits?

<answer id="0a368d" is-correct>Banana</answer>
<answer id="7c1e0d" is-correct>Apple</answer>
<answer id="b6d6b6">Hammer</answer>
<answer id="1dec24">Jiraffe</answer>
<hint>Mmmm, I don't think a hammer qualifies as a fruit. And a Jiraffe?</hint>
<solution>
The correct answer is `Banana` and `Apple`. A `Hammer` is a tool and a `Jiraffe` is an animal.
</solution>
</activity>


### Jupyter activity

This activity is exclusive to check exercises in Jupyter notebooks. Remember that these activities are checked using assertions. Make sure you write your assertions in the notebook, check the solution works correctly, and then delete the assertions from the notebook and leave them only in the activity.

Your project can potentially contain multiple Notebooks, so pay special attention to the tag `metadata` that contains WHAT notebook you're checking.

Here are a few examples:

> Before you check these activities, make sure the associated lab is started.
<activity id="fba1ea" title="Read the `pokemon.csv` data into a DataFrame `df`" type="code" template="jupyter-kernel" device="jupyter">

Make sure you use the column `#` as the index of the dataframe.

<validation-code>
assert "df" in globals(), "The variable `df` is not defined"
assert type(df) == pd.DataFrame, "The variable `df` doesn't seem to contain a DataFrame"

assert (df.index.name) == "#", "Are you sure you've used the column `#` as the index?"

expected_columns = [
    'Name', 'Type 1', 'Type 2', 'Total', 'HP',
    'Attack', 'Defense', 'Sp. Atk', 'Sp. Def',
    'Speed', 'Generation', 'Legendary']

assert list(df.columns) == expected_columns, "Your DataFrame doesn't seem to contain the right data"
</validation-code>
<hint>Use the `index_col` parameter of `read_csv` to specify what column to read as the index of the DataFrame</hint>
<solution>

```python
df = pd.read_csv('pokemon.csv', index_col='#')
```

</solution>
<metadata name="notebook_path">Project.ipynb</metadata>
</activity>

<activity id="e8888f" title="Select a sub-dataframe containing only the pokemons of type Fire" type="code" template="jupyter-kernel" device="jupyter">

Perform the selection and store the results in the variable `fire_pokemons_df`.

<validation-code>
assert "fire_pokemons_df" in globals(), "The variable `fire_pokemons_df` doesn't seem to be defined"
assert type(fire_pokemons_df) == pd.DataFrame, "The variable `fire_pokemons_df` doesn't seem to contain a DataFrame"

assert list(fire_pokemons_df['Type 1'].unique()) == ['Fire'], "Seems like you have pokemons of different types"
assert fire_pokemons_df.shape[0] == 47, "Your selection doesn't seem to contain the right amount of elements"
</validation-code>
<hint>You can use the `.loc` selector or the `query()` method</hint>
<solution>

Using the traditional `.loc` selector:
```python
fire_pokemons_df = df.loc[df['Type 1'] == 'Fire']
```

Or we could also use the `query()` method:

```python
fire_pokemons_df = df.query("`Type 1` == 'Fire'")
```

</solution>
<metadata name="notebook_path">Project.ipynb</metadata>
</activity>

The following activity is checked in the other notebook: `Another Notebook.ipynb`.

<activity id="9105ab" title="Define the function `add`" type="code" template="jupyter-kernel" device="jupyter">

The function `add` should receive two parameters `x` and `y` and return the sum of the elements.

<validation-code>
assert "add" in globals(), "The function `add` doesn't seem to be defined"
assert callable(add), "`add` doesn't seem to be a function"

assert add(2, 3) == 5, "Your function add is not working as expected"
</validation-code>
<hint></hint>
<solution>

```python
def add(x, y):
    return x + y
```
</solution>
<metadata name="notebook_path">Another Notebook.ipynb</metadata>
</activity>

</page>
