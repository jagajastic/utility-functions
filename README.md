# JavaScript Utility Functions

### Capitalize string

This function takes a string as argument and return the capitalized string passed 

```
function capitalize(stringVal){
    if(typeof(stringVal) !== 'string' ) return;
    const trimText = stringVal.trim();
    const textLen = trimText.length
    const capitalize = String(trimText[0]).toUpperCase();
    const truncatedText = String(trimText.slice(1)).toLowerCase();
    
    return `${capitalize + truncatedText}`;
}

usage
capitalize('hello'); // Hello
```

[View code sand box](https://opfde.csb.app/)
