Make a upload button
====================

Step 1. Create a simple html markup

```html
<div class="fileUpload btn btn-primary">
    <span>Upload</span>
    <input type="file" class="upload" />
</div>
```

Step 2. CSS: Tricky Part

```html

.fileUpload {
    position: relative;
    overflow: hidden;
    margin: 10px;
}
.fileUpload input.upload {
    position: absolute;
    top: 0;
    right: 0;
    margin: 0;
    padding: 0;
    font-size: 20px;
    cursor: pointer;
    opacity: 0;
    filter: alpha(opacity=0);
}

```