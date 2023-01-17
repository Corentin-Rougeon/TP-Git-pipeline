# TP - pipeline GITHUB
## ROUGEON Corentin

### 1. Lié votre compte via clé SSH à votre ordinateur


via gitbash on crée notre clé ssh :
`ssh-keygen -t ed25519 -C "corentin.rougeon@ynov.com"`

on Copie le contenue notre clé publique et on la colle dans 
`Setting > SSH and GPG KEYS > New SSH Key` via le site github 

pour tester notre clé :
`ssh -T git@github.com`

resultat :

`Hi Corentin-Rougeon! You've successfully authenticated, but GitHub does not provide shell access.`


### 2. Tester un premier workflow Github

creation d'un fichier workflow directement sur github 
dans `.github/workflows/github-actions-demo.yml`

```yaml
name: GitHub Actions Demo
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v3
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```

test du workflow :

![img.png](screenshots/workflow_test.png)

### 3. Créer deux classes python, une classe SimpleMath

`simplemath.py`
```python
class SimpleMath:
    def addition(a, b):
        return a + b
```

`test_simplemath.py`
````python
import unittest
from simplemath import SimpleMath

class TestSimpleMath(unittest.TestCase):
    def test_addition(self):
        result = SimpleMath.addition(1, 2)
        self.assertEqual(result, 3)
````

### 4. Créer un workflow permettant de lancer les tests unitaires de votre application.

`.github/test_add.yml`
```yaml
name: Test and Deploy

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.x

      - name: Run tests
        run: |
          python -m unittest test_simplemath.py
        env:
          CI: true
```

resultat du push:
![img.png](screenshots/workflow_py_add.png)


### 5. Créer la fonction soustraction et le test associé

`simplemath.py`
````python
class SimpleMath:
    def addition(a, b):
        return a + b

    def substraction(a,b):
        return a - b

````

`test_simplemath.py`
````python
import unittest
from simplemath import SimpleMath

class TestSimpleMath(unittest.TestCase):
    def test_addition(self):
        result = SimpleMath.addition(1, 2)
        self.assertEqual(result, 3)

    def test_substraction(self):
        result = SimpleMath.substraction(1, 2)
        self.assertEqual(result,-1)
````

resultat push :
![img.png](screenshots/workflow_py_add_sub.png)

