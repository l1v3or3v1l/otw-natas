# Level 24 -> Level 25

strcmp vulnerability  

If the strcmp function is used to compare a string with an array, the function returns 0.   
If this holds true in our case, modification of variable passwd to passwd[] should give us the password for the next level.  

```html
<input type="text" size="20" name="passwd">
```

to

```
<input type="text" size="20" name="passwd">
```
