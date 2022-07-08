# Configuring git

- name
- email
- default editor
- line ending

## Configuration levels

- system: all user
- global: all repositories
- local: the current repository

## Config user information

```bash
git config --global user.name "Sirui Zhang"
git config --global user.email siruizhangdev@gmail.com

# addressing line feed      
git config --global core.autocrlf input

```

## Config default editor

```bash
git config --global core.editor "code --wait"
```

## Edit configuration file

```bash
git config --global -e
```

## Config how to handle end of lines

windows: `\r, \n`
mac: `\n`

```bash
git config --global core.autocrlf input
```
