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


### Convert array of object to excel 

````
export function transformArrOfObj(arr) {
  let newArrToExcel = [['Name', 'email', 'Submission Date', 'Submission Time', 'Sector']];
  const result = arr.reduce((acc, record) => {
    const vals = [record.fullName, record.email, record.createdAt, record.createdAt, record.sector];
    acc.push(vals);
    return acc;
  }, newArrToExcel);

  return result;
}

export const exportToCsv = function (Results) {
  var CsvString = '';
  Results.forEach(function (RowItem, RowIndex) {
    RowItem.forEach(function (ColItem, ColIndex) {
      CsvString += ColItem + ',';
    });
    CsvString += '\r\n';
  });
  CsvString = 'data:application/csv,' + encodeURIComponent(CsvString);
  var x = document.createElement('A');
  x.setAttribute('href', CsvString);
  x.setAttribute('download', 'somedata.csv');
  document.body.appendChild(x);
  x.click();
};

````
### Sort Alphabet

````
const arr = [
  {firstName: "Coder", lastName: "Byte"},
  {firstName: "Mike", lastName: "Adenuga"},
  {firstName: "Ibra", lastName: "Joe"},
]

arr.sort((a,b) => {
  if(a.lastName < b.lastName) {
    return -1
  } else if(a.lastName > b.lastName) {
    return 1;
  } else {
    return 0;
  }
});

````
