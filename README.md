# nukikata-demo-monty

Simple demo to introduce the format and features for [`nukikata`](https://github.com/insight-infrastructure/nukikata)

```
pip install nukikata 
nukikata https://github.com/insight-infrastructure/nukikata-demo-monty
cat ./output.json 
```

Simply write your nukikata per this format.

```json
{
  "name": {
    "type": "input",
    "message": "What is your name?"
  },
  "colors": {
    "type": "checkbox",
    "message": "What are your favorite colors?",
    "choices": [
      {"name": "blue"},
      {"name": "green"},
      {"name": "grey"}
    ]
  },
  "wingspeed": {
    "type": "list",
    "message": "What is the airspeed velocity of an unladen swallow??",
    "choices": [
      {"name": "I donno"},
      {"name": "What do you mean? African or European swallow?"}
    ]
  },
  "bad_outcome": {
    "type": "print",
    "statement": "Wrong answer {{ cookiecutter.name }}...",
    "when": "{{ 'I donno' in cookiecutter.wingspeed }}"
  },
  "color_essays": {
    "type": "input",
    "message": "Please tell me how much you like the color {{cookiecutter.item}}?",
    "default": "Oh color {{cookiecutter.item}}, you are so frickin cool...",
    "loop": "{{ cookiecutter.colors }}",
    "when": "{{ cookiecutter.colors|length > 1 }}"
  },
  "democmd": {
    "type": "command",
    "command": "pwd"
  },
  "verify": {
    "type": "confirm",
    "message": "Do you want to build a quick web application?"
  },
  "one_click_web_app": {
    "type": "nukikata",
    "template": "https://github.com/tiangolo/full-stack-fastapi-postgresql"
  },
  "dump_json": {
    "type": "json",
    "contents": "{{ cookiecutter }}",
    "path": "output.json"
  }
}
```