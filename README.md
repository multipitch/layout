# layout
# Example python package layout.

## Steps taken to set up this template project

## General setup (do once)
```
$ sudo pacman -S git python pyenv python-virtualenv python-virtualenvwrapper
$ mkdir ~/devel
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc
$ echo -e 'export WORKON_HOME=~/.virtualenvs\nexport PROJECT_HOME=~/devel\nsource /usr/bin/virtualenvwrapper.sh' >> ~/.bashrc
$ curl -sSL \https://raw.githubusercontent.com/sdispater/poetry/master/get-poetry.py | python
$ echo -e 'for bcfile in ~/.bash_completion.d/* ; do\n  [ -f "$bcfile" ] && . $bcfile\ndone' > ~/.bash_completion
$ mkdir ~/bash_completion.d
$ poetry completions bash > ~/bash_completion.d/poetry.bash-completion
$ echo 'source ~/.bash_completion' >> ~/.bashrc
$ pacman -S code
```
Ensure python add-on is installed in VS Code via its internal package manager
Add the following settings to VS Code (as a user setting, not a workspace setting)
```
"python.venvPath": "~/.virtualenvs",
"git.autofetch": true,
"git.enableCommitSigning": true,
```

## Install version of python required e.g.
`$ pyenv install 3.7.0`

## Create project folder and virtual environment
```
$ mkdir ~/devel/layout
$ mkvirtualenv -a ~/devel/layout/ -p ~/.pyenv/versions/3.7.0/bin/python layout
```

## Create some files
```
$ cd ~/devel/layout
$ touch README
$ touch LICENSE
```
Populate LICENSE with MIT License text
```
$ mkdir -p src/layout tests
$ touch src/layout/__init__.py
$ echo 'print("hello, world")' > src/layout/hello.py
```

## Initialize poetry
```
$ poetry init
```
- Description: "Example python package layout."
- mostly use defaults
- fill in Author
- don't define dependencies
- License: MIT
- confirm generation

## Install some dev packages
```
$ poetry add pylint
$ poetry add --dev --allow-prereleases black
```

## Add settings for black
```
$ echo -e '\n[tool.black]\nline-length = 79' >> pyproject.toml
```

## Add workspace-specific settings to VS code (~/layout/.code/settings.json)
```
$ cd ~/devel/layout
$ code .
```
Edit workspace settings and add the following:
```
"editor.rulers": [
    72,
    79,
    80
],
"editor.formatOnSave": true,
"python.pythonPath": "~/.virtualenvs/layout/bin/python",
"python.formatting.provider": "black",
```

## Git setup 
Assumes user is already using git and github and has already set up an ssh key on github.
```
$ cd ~/devel/layout
$ curl -LJo .gitignore https://raw.githubusercontent.com/github/gitignore/master/Python.gitignore
$ echo -e '\n # VS Code settings\n.vscode/' >> .gitignore
$ curl -u 'multipitch' https://api.github.com/user/repos -d '{"name":"layout"}'
$ git init
$ git add .
$ git commit -m "Initial commit."
$ git remote add origin "git@github.com:multipitch/layout.git"
```

## Make some changes and do another commit
```
$ git pull git@github.com:multipitch/layout.git master
$ git mv README README.md
```
 Now updating the text here...
```
$ git add README.md
$ git commit -m "Reformatted README in .md format"
$ git push --set-upstream origin master
