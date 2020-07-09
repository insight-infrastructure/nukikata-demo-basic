# nukikata-demo-monty

Simple demo to introduce the format and features for [`nukikata`](https://github.com/insight-infrastructure/nukikata)

```
pip install nukikata 
nukikata https://github.com/insight-infrastructure/nukikata-demos
cat ./output.json 
```

Simply write your nukikata per this format. The key in the jinja syntax defaults to the context filename for the template, in this case `nuki.yaml`.

```yaml
---
name:
  type: input
  message: What is your name?

colors:
  type: checkbox
  message: What are your favorite colors?
  choices:
    - name: blue
    - name: green
    - name: grey

wingspeed:
  type: list
  message: What is the airspeed velocity of an unladen swallow??
  choices:
    - name: I donno
    - name: What do you mean? African or European swallow?

bad_outcome:
  type: print
  statement: Wrong answer {{ nuki.name }}...
  when: "{{ 'I donno' in nuki.wingspeed }}"

color_essays:
  type: input
  message: Please tell me how much you like the color {{nuki.item}}?
  default: Oh color {{nuki.item}}, you are so frickin cool...
  loop: "{{ nuki.colors }}"
  when: "{{ nuki.colors|length > 1 }}"

democmd:
  type: command
  command: pwd
  
dump_json:
  type: json
  contents: "{{ nuki }}"
  path: output.json

```

This is what it would look like if the file was called `cookiecutter.json`.

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

This demo is only for showing off the new syntax.  Nukikata still supports all cookiecutter features including templating of file structures but of course with operators, there are many more possibilities.
