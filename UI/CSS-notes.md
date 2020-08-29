# CSS Notes

## For creating box

```html
<html>
<body>
  <nav class="container">
    <div class="b1">Home</div>
    <div class="b2">Search</div>
    <div class="b3">Logout</div>
  </nav>
</body>

</html>
```

```css
.container > div {
  padding: 10px;
  text-align: center;
  font-size: 2em;
  color: #ffeead;
}

html,body {
  background-color: #ffeead;
  margin: 10px;
}

.container > div:nth-child(1) {
  background-color: red;
}

.container > div:nth-child(2) {
  background-color: green;
}

.container > div:nth-child(3) {
  background-color: orange;
}
```
