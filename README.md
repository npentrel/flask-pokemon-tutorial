# flask-pokemon-tutorial

1. Sign up for an account at [https://codeanywhere.com/](https://codeanywhere.com/)!
This will give you a good development environment without you having to set anything up.

2. Confirm you email address.

3. Log in. 

4. Click on `File` and then `New project`. Type in `Pokemon API test` and click `ok`.

5. Select python 3...


7. Add this code:
```
from flask import Flask, request, redirect, render_template
app = Flask(__name__)

@app.route('/')
def index():
    return "Hello World!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port="5000")
```

8. Run.

9. Change `return "Hello World"` to `return render_template('./index.html')`. 

You should now have:
```
from flask import Flask, request, redirect, render_template
app = Flask(__name__)

@app.route('/')
def index():
    return render_template('./index.html')

if __name__ == "__main__":
    app.run(host="0.0.0.0", port="5000")
```
10. Add a basic html file. To do this click on File > New File... and create the new file called `index.html` inside a folder called `templates`. This is important as Python Flask expects the html file to be in such a folder.
```
<!doctype html>
<title>Pokemons</title>
<h1>Hello World!</h1>
```

11. Run.

```
from flask import Flask, request, redirect, render_template
import requests
import json

app = Flask(__name__)

def get_pokemons():
  response = requests.get("http://pokeapi.co/api/v2/pokemon-color/blue", verify=False)
  json_obect = json.loads(response.text)
  pokemon_data = json_obect['pokemon_species']
  pokemons = []
  for p in pokemon_data:
    pokemons.append({"name": p['name']})
  print(pokemons)
  return pokemons

@app.route('/')
def index():
    pokemons = get_pokemons()
    return render_template('./index.html', pokemons=pokemons)
  
if __name__ == "__main__":
    app.run(host="0.0.0.0", port="3000")
```


```
<!doctype html>
<title>Pokemons</title>
<h1>Hello World!</h1>
{% for pokemon in pokemons %}
    <div>
      <p>{{ pokemon.name }}</p>
    </div>
{% endfor %}
```

