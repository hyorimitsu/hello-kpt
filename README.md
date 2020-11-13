# Kpt sample

## provision

### installation
https://googlecontainertools.github.io/kpt/installation/

### init
By running this command, a Kptfile will be created and can be treated as a Kpt package.
```
$ kpt pkg init sample/
```

### create setter
Create a key-value pair setter as a data item to change the settings for each environment.
When the command is executed, the setter is added to the Kptfile.
```
$ kpt cfg create-setter sample/ name xxx
$ kpt cfg create-setter sample/ image xxx
```

(created setter example)
```
openAPI:
  definitions:
    io.k8s.cli.setters.name:
      x-k8s-cli:
        setter:
          name: name
          value: xxx
```

### add template
You can change the settings for each environment by specifying them as comments in the resource file as follows.

(example)
```
name: xxx # {"$ref":"#/definitions/io.k8s.cli.setters.name"}
```