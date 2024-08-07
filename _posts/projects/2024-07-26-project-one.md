---
title: "Custom size File Generator"
link: https://github.com/Het-Joshi/FileGenerator
description: "A tool to generate a random dummy file that is of a specified size"
categories: projects
layout: post
date: 2024-07-26
comments: true
en: "/robots_txt/projects/fileGen/"
authors:
  - Het Joshi
---

# What is this project exactly?
This is a tool that generates a random dummy file that is of a specified size.
You input the output file name, format and size. After that, BOOM out comes the expected file of that size and name which contains random characters.

# Why bother making this?
I was working on a project where I had to test download speeds of different hosting tools. So to measure the metrics, I had to download a 10 MB and 100 MB files using these toolsso I can get comparable results.
When I satrted working, I asked my self:
> How do I generate a 10 MB file?
> How do I generate a 100 MB file?

Now my mentor reminded me of the below fact:
> Each character in a .py file is 1 B

Now, I didn't want to type so many letters also so I came up with another method as I will describe in the next section.

# The Implementation

I have linked the repository so you can view the whole code in its enterity but the fumnction that writes random bits below:

```python3
def generate_file(file_name, size, unit):
    """
    Generates a file of the specified size filled with random data.

    Parameters:
    file_name (str): The name of the file to be created.
    size (float): The size of the file.
    unit (str): The unit of the file size (b, kb, mb, gb).
    """
    size_bytes = convert_size_to_bytes(size, unit)
    with open(file_name, 'wb') as f:
        f.write(os.urandom(size_bytes))
    print(f'File "{file_name}" of size {size} {unit.upper()} ({size_bytes} bytes) has been created.')
    print(f'Output file path: {os.path.abspath(file_name)}')
```
The above function takes in the file name, size and unit as parameters.

The important line here is `f.write(os.urandom(size_bytes))`.

- os.urandom(size_bytes):

    This function generates size_bytes bytes of random data.
    os.urandom is a function from the os module in Python that provides a way to generate secure random numbers suitable for cryptographic use.
    The size_bytes parameter specifies how many random bytes you want to generate.

- f.write(...):

    This method writes the data (in this case, the random bytes generated by os.urandom) to the file represented by the file object f.
    f is a file object created by the open function in write-binary mode ('wb'), meaning the file is opened for writing, and any existing file with the same name will be overwritten.
    The write method writes the specified bytes to the file.

Other functions:

- `convert_size_to_bytes(size, unit)`

Converts the size from the specified unit to bytes.

Parameters:

    size (float): The size of the file.
    unit (str): The unit of the file size (b, kb, mb, gb).

Returns:

    int: The size of the file in bytes.

- `generate_file(file_name, size, unit)`

Generates a file of the specified size filled with random data.

Parameters:

    file_name (str): The name of the file to be created.
    size (float): The size of the file.
    unit (str): The unit of the file size (b, kb, mb, gb).

`print_instructions()`
Prints the instructions for using the script.

# Conclusion:
If you face a problem, make your own solution so you learn a new concept and put it in the public domain so other can learn and use it too!
