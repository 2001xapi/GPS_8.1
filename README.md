# Explicació CI

Per tal d'implementar el Continuous Integration he afegit un fitxer anomenat python-app.yml que a cada push que es realitzi al projecte executarra una serie de tests que en cas de superar-los farà el push. Ara desgranaré el codi.

    runs-on: ubuntu-latest


    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.9
      uses: actions/setup-python@v2
      with:
        python-version: 3.9
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install flake8 pytest
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
    - name: Lint with flake8
      run: |
        # stop the build if there are Python syntax errors or undefined names
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
        # exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide
        flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
    - name: Test with pytest
      run: |
        python test.py
    - name: Coverage
      run: |
        pip install coverage
        coverage run test.py
        coverage report  
        
# Set up Python 3.9

    - name: Set up Python 3.9
          uses: actions/setup-python@v2
          with:
            python-version: 3.9
        
En aquesta part el programa indica que s'executarà en la versió 3.9 de python.

# Install dependencies

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install flake8 pytest
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
        
 Aqui s'indica que tots els requisits, llibreries externes que es puguin fer servir durant la prova és guardaran en un fitxer de text anomenat requirements.txt.
 
 #Lint with flake8
 
    - name: Lint with flake8
      run: |
        # stop the build if there are Python syntax errors or undefined names
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
        # exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide
        flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
        
  Flake8 és una llibreria de python que serveix per depurar el codi, es a dir, avisar-nos d'errors a l'hora de programar com llibreries o variables no utilitzades que pugui haver-hi en el nostre codi que volem evaluar.
  
  # Test with pytest
  
      - name: Test with pytest
          run: |
            python test.py
           
  Part molt simple que l'únic que far és executar el test amb nom test.py.
  
  # Coverage
  
      - name: Coverage
          run: |
            pip install coverage
            coverage run test.py
            coverage report 
            
  Finalment la secció del coverage on és realitzarà un informe de l'execució del test test.py.

        
        
        
        
        
        
