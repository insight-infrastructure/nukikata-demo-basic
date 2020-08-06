# nukikata-demo-monty

Simple demo to introduce the format and features for [`nukikata`](https://github.com/insight-infrastructure/nukikata)

```
python3 -m venv env 
source env/bin/activate 

pip3 install nukikata 
nukikata https://github.com/insight-infrastructure/nukikata-demos
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
    - blue
    - green
    - grey

wingspeed:
  type: select
  message: What is the airspeed velocity of an unladen swallow??
  choices:
    - I donno
    - What do you mean? African or European swallow?

bad_outcome:
  type: print
  statement: Wrong answer {{ nuki.name }}... (Flung off bridge)
  when: "{{ 'I donno' in nuki.wingspeed }}"

color_essays:
  type: input
  message: Please tell me how much you like the color {{nuki.item}}?
  default: Oh color {{nuki.item}}, you are so frickin cool...
  loop: "{{ nuki.colors }}"
  when: "{{ nuki.colors|length > 0 }}"
```

This demo is only for showing off the new syntax.  Nukikata still supports all cookiecutter features including templating of file structures but of course with operators, there are many more possibilities.
