---
tags: [tag1, tag2]
grade: A
---

# Deploy pypi

> to package python

## Pros
  - "world wide use"

## Cons
  - "good"

## Implementation
<!-- jcapy:EXEC -->
```bash
echo "set up variables"
PROJECT_NAME=$(basename "$PWD" | tr '[:upper:]' '[:lower:]')

echo "set up venv"
python3 -m venv venv
echo "activating venv"
source venv/bin/activate
echo "making sure you have the latest version installed"
python3 -m pip install --upgrade pip
echo "creating a new directory for your project and cd into it"
<!-- jcapy:EXEC -->
mkdir packaging_tutorial
cd packaging_tutorial
<!-- jcapy:EXEC -->
mkdir src/example_package_YOUR_USERNAME_HERE
cd src/example_package_YOUR_USERNAME_HERE
<!-- jcapy:EXEC -->
touch __init__.py example.py

```
packaging_tutorial/
└── src/
    └── example_package_YOUR_USERNAME_HERE/
        ├── __init__.py
        └── example.py

<!-- jcapy:EXEC -->
```bash
echo "creating pyproject.toml"
cd ..
mkdir pyproject.toml
echo "writing pyproject.toml"
<!-- jcapy:EXEC -->
cat << EOF > pyproject.toml
[project]
name = "$PROJECT_NAME"
version = "0.0.1"
authors = [
  { name="Example Author", email="author@example.com" },
]
description = "A small example package"
readme = "README.md"
requires-python = ">=3.9"
classifiers = [
    "Programming Language :: Python :: 3",
    "Operating System :: OS Independent",
]
license = "MIT"
license-files = ["LICEN[CS]E*"]

[project.urls]
Homepage = "https://github.com/pypa/sampleproject"
Issues = "https://github.com/pypa/sampleproject/issues"
EOF

<!-- jcapy:EXEC -->
```bash
echo "creating README.md"
cat << EOF > README.md
# Example Package

This is a simple example package. You can use
[GitHub-flavored Markdown](https://guides.github.com/features/mastering-markdown/)
to write your content.
EOF
<!-- jcapy:EXEC -->
echo "Generating distribution archives"
python3 -m pip install --upgrade build
python3 -m build
echo "This command should output a lot of text and once completed should generate two files in the dist directory:

dist/
├── example_package_YOUR_USERNAME_HERE-0.0.1-py3-none-any.whl
└── example_package_YOUR_USERNAME_HERE-0.0.1.tar.gz"

<!-- jcapy:EXEC -->
```bash
echo "Uploading the package to PyPI"
python3 -m pip install --upgrade twine
twine upload dist/*
echo "You will be prompted for an API token. Use the token value, including the pypi- prefix. Note that the input will be hidden, so be sure to paste correctly."
```
<!-- jcapy:EXEC -->
```bash
echo "Installing your newly uploaded package"
echo "Make sure to specify your username in the package name!"
python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps $PROJECT_NAME
echo "test it"
$PROJECT_NAME
echo "Keep in mind that this tutorial showed you how to upload your package to Test PyPI, which isn’t a permanent storage. The Test system occasionally deletes packages and accounts. It is best to use TestPyPI for testing and experiments like this tutorial."

echo "deactivate venv"
python3 deactivate
```

