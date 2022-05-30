
#### Creating Project
```bash
mkdir project-folder
cd project-folder
zola init my_zola_project

#Zola Generated:
#├── config.toml
#├── content
#├── static
#├── templates
#└── themes
```

#### Serving Zola Project Directly
```bash
zola serve -u localhost --port 1111`
```
*Note that when using zola serve, Japanese Characters do not get converted properly*

#### Testing websites with non english symbols
[[Miniserve website server]]
```bash
zola build
# miniserve must be installed
# cargo install miniserve
miniserve . -p 1111 --spa --index index.html
```