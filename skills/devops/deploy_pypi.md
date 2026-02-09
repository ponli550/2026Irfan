---
tags: [pypi, packaging, distribution]
grade: A
---

# 🚀 Deploy to PyPI

> Automated workflow to package and distribute Python projects globally via PyPI.

## ⚖️ Evaluation
- **Pros**: Enables global `pip install` capability; establishes versioned distribution.
- **Cons**: Requires strict metadata management; TestPyPI is ephemeral (packages may be deleted).

## 🛠 Implementation

```bash
echo "💎 Initializing Glass Box Environment..."
PROJECT_NAME=$(basename "$PWD" | tr '[:upper:]' '[:lower:]' | tr ' ' '_')

# 1. Environment Setup
echo "📦 Setting up isolated build environment..."
python3 -m venv venv
source venv/bin/activate
python3 -m pip install --upgrade pip build twine

# 2. Structure Creation
echo "🏗 Building directory scaffolding..."
mkdir -p "src/${PROJECT_NAME}"
touch "src/${PROJECT_NAME}/__init__.py"
touch "src/${PROJECT_NAME}/main.py"

# 3. Metadata Generation
echo "📝 Writing pyproject.toml..."
cat << EOF > pyproject.toml
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "${PROJECT_NAME}"
version = "0.0.1"
authors = [
  { name="Developer", email="dev@example.com" },
]
description = "A Jaavis-generated automated package"
readme = "README.md"
requires-python = ">=3.9"
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]

[project.urls]
Homepage = "[https://github.com/user/$](https://github.com/user/$){PROJECT_NAME}"
EOF

echo "📖 Creating documentation..."
cat << EOF > README.md
# ${PROJECT_NAME}

Generated via Jaavis Workflow.
Install using:
\`\`\`bash
pip install ${PROJECT_NAME}
\`\`\`
EOF

# 4. Build Phase
echo "🔨 Generating distribution archives (Wheel & SDist)..."
python3 -m build



# 5. Deployment Phase (TestPyPI)
echo "🚀 Uploading to TestPyPI..."
# Note: Requires __token__ as username and your PyPI API token as password
python3 -m twine upload --repository testpypi dist/*

echo "✅ Deployment Complete."
echo "To verify, run: pip install --index-url [https://test.pypi.org/simple/](https://test.pypi.org/simple/) --no-deps ${PROJECT_NAME}"

# Cleanup
deactivate
