# deferscript
Defer inline JavaScript tags that are not modules with this tiny script (274 bytes raw and 109 bytes compressed/gzipped).

The ECMA standard and browsers do not support the deferring on inline JavaScript code without the use of
the `module` or 'src' tag. This means that the regular script below will run before the module script and cause an error.

```javascript
<script type="module">
        var store = new Proxy({},
            {
                set(target,property,value) {
                    console.log(target,property,"=",value," old value ",target[property]);
                    target[property] = value;
                    return true;
                }
            });
   </script>
<script>
    store.name = "joe";
</script>
  ```

You could externalize the inline:

```javascript
<script src="assignjoe.js" defer></script>
```

But, that can obscure things.

With `deferscript` you do this:

```javascript
<script src="./deferscript.js" defer>
    store.name = "joe";
</script>
```

Take a look at the `./examples/index.html` file in the repository to see the code in action.

There is an extended discussion on deferring inline scripts here:

https://stackoverflow.com/questions/41394983/how-to-defer-inline-javascript/

