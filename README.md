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

## Usage

### get package
Get the kpt package from the git repository by specifying the output folder.
```
$ kpt pkg get https://github.com/hyorimitsu/kpt-sample.git/sample@master kpt-nginx
```

### set values to the template
Set the value to the template by specifying a key-value pair.
```
$ kpt cfg set kpt-nginx/ name kpt-nginx-test
$ kpt cfg set kpt-nginx/ image nginx:1.14
```

If you look at the resource file here, you will see that you can set the values as follows.
```
name: kpt-nginx-test # {"$ref":"#/definitions/io.k8s.cli.setters.name"}
```

### apply
```
kubectl apply -R -f kpt-nginx/
```

### delete
```
kubectl delete -R -f kpt-nginx/
```