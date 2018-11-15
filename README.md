# Dynamsoft JavaScript Barcode SDK

Version 6.3.0.2

The repository aims to help developers get familiar with [Dynamsoft JavaScript Barcode SDK](https://www.dynamsoft.com/Products/barcode-recognition-javascript.aspx).

## Online Demo

[Demo (version 6.3.0.2)](https://htmlpreview.github.io/?https://github.com/dynamsoft-dbr/javascript-barcode/blob/master/examples/decodeVideoWithSettings/barcode_reader_javascript.html)

[Demo (version 6.3.0)](https://demo.dynamsoft.com/dbr_wasm/barcode_reader_javascript.html)

## Browser compatibility

| browser | min version |
|-|-|
| Chrome | 57 |
| Firefox | 52 |
| Edge | 16 |
| Safari | 11 |

## Documentation

[Guide](https://github.com/dynamsoft-dbr/javascript-barcode/blob/master/documents/guide-original.md)(6.3.0.2)

[Api](https://github.com/dynamsoft-dbr/javascript-barcode/blob/master/documents/api-original.md)(6.3.0.2)

## Helloworld

Just copy into a html file and run it from file browser.

```html
<!DOCTYPE html>
<html>
<body>
    <div id="divLoadInfo">loading...</div>
    <input id="uploadImage" type="file" accept="image/bmp,image/jpeg,image/png,image/gif" style="display:none">
    <script src="https://demo.dynamsoft.com/dbr_wasm/js/dbr-6.3.0.2.min.js"></script>
    <script>
        dynamsoft.dbrEnv.resourcesPath = 'https://demo.dynamsoft.com/dbr_wasm/js';
        var reader = null;
        var iptEl = document.getElementById('uploadImage');
        dynamsoft.dbrEnv.onAutoLoadWasmSuccess = function(){
            reader = new dynamsoft.BarcodeReader();
            iptEl.style.display = '';
            document.getElementById('divLoadInfo').innerHTML="load dbr wasm success.";
        };
        dynamsoft.dbrEnv.onAutoLoadWasmError = function(ex){
            document.getElementById('divLoadInfo').innerHTML="load wasm failed: "+(ex.message || ex);
        };
        
        //https://www.dynamsoft.com/CustomerPortal/Portal/TrialLicense.aspx
        dynamsoft.dbrEnv.licenseKey = "t0068MgAAAITeFdSNvIYpkFMgjUw9+ssQhJwCsd78AhMIVO6NOdYfu1TQcDLwJvtO7y5bgYrZZXrq11jkf5UVL5Y5CVpb9nU=";
        
        iptEl.addEventListener('change', function(){
            reader.decodeFileInMemory(this.files[0]).then(function(results){
                var txts = [];
                for(var i=0;i<results.length;++i){
                    txts.push(results[i].BarcodeText);
                }
                alert(txts.join("\n"));
            }).catch(ex => {
                alert('error:' + (ex.message || ex));
            });
            this.value = '';
        });
    </script>
</body>
</html>
```

## Changelog

### 6.3.0.2

Add built-in worker support.

```js
// The default value is false. Set it true to decode in another thread. By this way, UI would not stuck.
dynamsoft.dbrEnv.bUseWorker = true;
```

### 6.3.0.1

Set `dbr-<version>.js`(stable) as the main branch.

Add `dbr-<version>.mobile.js`(smaller, compile quicker, need less memory, but not that stable) for the mobile safari.

### 6.3.0

Build Dynamsoft Barcode Reader 6.3.0 to JS(webassembly) version.

## Contact Us

If there is any questions, please feel free to contact <a href="mailto:support@dynamsoft.com?subject=DBR%20webassembly">support@dynamsoft.com</a>.
