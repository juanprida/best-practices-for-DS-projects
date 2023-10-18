# Coding Style for Data Science projects

## ****Introduction****
This document aims to provide a set of guidelines for writing code in our data science projects. More and more companies are choosing to execute their data science projects using notebooks as the main tool. However, notebooks are not the best tool for developing large scale projects. Therefore, we propose a hybrid approach where notebooks are used as orchestrators and scripts as the main building blocks of our projects.


## Notebooks

### ****Philosophy****

Notebooks are versatile tools for various tasks in data science, from prototyping models to quick data analysis. However, as our projects scale, notebooks can become tangled with spaghetti code, making them challenging to maintain. Our preferred solution is to use notebooks as orchestrators. Ideally, a notebook should contain minimal code and instead call classes and functions defined in .py scripts. This approach keeps the codebase clean and organized.

In a well-designed project, the notebook's backend could easily change, but the notebook itself should remain relatively unchanged.

### ****Styling****

When it comes to notebook styling, a well-designed notebook should be self-explanatory, minimizing the need for excessive documentation. We also don't need to strictly adhere to PEP8 guidelines; line lengths can exceed 79 characters when necessary for clarity.

### ****Example****

Here's an example of a well-structured notebook. Note that function and class names should clearly convey their purpose to anyone reading the notebook for the first time.

```python
# Import required scripts
from your_amazing_library.data import DataConnector
from your_amazing_library.models import BestModelEver
```

```python
# We get our data
dc = DataConnector()
data = dc.get_data()
clean_data = dc.clean_data(data)
```

```python
# Run our model
bme = BestModelEver()
model = bme.fit(clean_data)
```

Note that we could change the model, but from a notebook’s perspective this doesn’t represent any change.

## ****Scripts****

Scripts are the building blocks of our projects, containing functions and classes used in our notebooks.

If you're curious about what makes a great script, take a look at the implementation of Logistic Regression from scikit-learn: **[Logistic Regression Implementation](https://github.com/scikit-learn/scikit-learn/blob/main/sklearn/linear_model/_logistic.py)**.

This leads us to a few important points to highlight:

### ****Script Docstring****

At the top of the file, typically as a one-liner, it's a good practice to briefly explain what the script is about.

### ****Script Imports****

As per the **[PEP 8](https://peps.python.org/pep-0008/#imports)** guidelines:

Imports should be organized in the following order:

1. Standard library imports.
2. Related third-party imports.
3. Local application/library-specific imports.

A blank line should separate each group of imports.

### ****Function and Classes Docstrings****

Docstrings within functions and classes serve as the primary point for documentation. There are two common styles:

**Numpy Docstrings:**
This is the docstring style followed in scikit-learn. Here's a quick example:

```python
"""Load and process chatlogs.

   Parameters
   ----------
   verbose : bool, default=False
       If True, print information about the current dataset.

   Returns
   -------
   Union[DataFrame, DataFrame]
       Final DataFrame with curated logs.
"""
```

For more details on this style, refer to this **[documentation guide](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_numpy.html)**.

**Google Docstrings:**
Some libraries, like PyTorch, adopt Google-style docstrings. Here's an example:

```python
"""Load and process chatlogs.

Args:
verbose (bool): If True, print information about the current dataset. Default to False

Returns:
  Union[DataFrame, DataFrame]: Final DataFrame with curated logs.
"""
```

You can find an example of this style in the **[PyTorch Linear module](https://github.com/pytorch/pytorch/blob/main/torch/nn/modules/linear.py)** and a guide **[here](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html)**.

### ****Hints****

PEP 484 introduced annotations, which can help clarify the types of arguments and return values in your functions and methods. Here's a quick example:

```python
def greeting(name: str) -> str:
return 'Hello ' + name
```

You can specify types for various data types, and for more complex data structures, consider using the **`typing`** module. For example:

```python
x: int = 1
x: float = 1.0
x: bool = True
x: str = "test"
x: bytes = b"test"
x: pd.DataFrame = pd.Dataframe([1,2,3])
x: np.array = np.array([1,2,3])
```

```python
from typing import List

x: List[int] = [1,2,3]
y: List[Dict[str, int]] = [{"a": 1}, {"a": 2}]
```

There are also useful constructs like **`Union`** and **`Optional`** that can be handy in type hints. You can find a helpful guide in the **[Mypy documentation](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html)**.

### **Line Length**

Following PEP8 guidelines, lines in your scripts should aim to be no longer than 79 characters. However, it's important to note that our team values code clarity, and if a longer line length, such as 120 characters, enhances readability and understanding, that is also acceptable. The key is to prioritize code comprehensibility while maintaining a balance with line length.

### Recommendations

- Always work on scripts in an integrated development environment (IDE) like **[Visual Studio Code](https://code.visualstudio.com/)** or **[PyCharm](https://www.jetbrains.com/pycharm/)**, applying both a linter (Pylint) and a formatter (Black).
- Consistency in the use of docstrings throughout the repository is essential. If code contains type hints, annotations in docstrings can be omitted.

## ****Pull Requests****

### ****For Developers****

A [recommended article](https://mtlynch.io/code-review-love/) could be found here, this are just some highlights from it.

**Review Your Own Code First**: Before sending your code for review, review it yourself, and imagine reading it for the first time. Take a break between writing and reviewing to catch errors.

**Write a Clear Changelist Description**: Provide a summary of the change in your code that includes necessary background knowledge for the reviewer.

**Automate the Easy Stuff**: Use automated tests and tools to catch common issues like formatting and syntax errors.

**Answer Questions with the Code Itself**: Ensure that your code is self-explanatory and doesn't require additional explanations. Refactor the code if needed for clarity.

**Narrowly Scope Changes**: Focus on making small, specific changes rather than trying to fix everything at once. Avoid scope creep.

### ****For Reviewers****

Familiarize yourself with Google's code review best practices for effective and efficient reviews. **[Google Code Review Guidelines](https://google.github.io/eng-practices/review/reviewer/)**