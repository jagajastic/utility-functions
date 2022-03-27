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


# Slider

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Slider</title>

    <style>
        body {
            padding: 0px;
            margin: 0px;
        }

        .main-wrapper {
            display: flex;
            flex-direction: row;
            position: relative;
            min-height: 45rem;
        }

        .main-wrapper .container {
            position: relative;
            width: 100%;
            display: flex;
            flex: 1;
        }

        .main-wrapper .container .wrapper {
            position: relative;
            width: 100%;
            display: flex;
            flex: 3;
            overflow: hidden;
        }
        
        .main-wrapper .container .wrapper_right {
            position: relative;
            flex: 1;
            display: flex;
            overflow: hidden;
        }

        .main-wrapper .container .slide_item {
            position: absolute;
            display: flex;
            width: 100%;
            height: 100%;
            z-index: 1;
            left: 100%;
        }

        .main-wrapper .container .slide_item.active_item {
            z-index: 9;
            position: absolute;
            left: 0;
            transition: left 1s;
        }

        .main-wrapper .container .wrapper .slide_item:nth-child(1), .main-wrapper .container .wrapper_right .slide_item:nth-child(4) {
            background: #ff0;
        }

        .main-wrapper .container .wrapper .slide_item:nth-child(2), .main-wrapper .container .wrapper_right .slide_item:nth-child(1) {
            background: #ff0000;
        }

        .main-wrapper .container .wrapper .slide_item:nth-child(3), .main-wrapper .container .wrapper_right .slide_item:nth-child(2) {
            background: #0ff;
        }

        .main-wrapper .container .wrapper .slide_item:nth-child(4), .main-wrapper .container .wrapper_right .slide_item:nth-child(3) {
            background: #0ff00f;
        }

        .main-wrapper .controls {
            display: flex;
        }

        .zindex8 {
            z-index: 8 !important;
        }

        .zindex11 {
            z-index: 11 !important;
        }
    </style>
</head>

<body>
    <div class="main-wrapper">
        <div class="container">
            <div class="wrapper">
                <div class="slide_item">
                    <div class="main">item 1 </div>
                </div>
                <div class="slide_item">
                    <div class="main">item 2 </div>
                </div>
                <div class="slide_item">
                    <div class="main">item 3</div>
                </div>
                <div class="slide_item">
                    <div class="main">item 4</div>
                </div>
            </div>
            <div class="wrapper_right">
                <div class="slide_item">
                </div>
                <div class="slide_item">
                </div>
                <div class="slide_item">
                </div>
                <div class="slide_item">
                </div>
            </div>
        </div>
    </div>
    </div>
    <div class="controls">
        <div class="cleft" onclick="previousItem()">Previous</div>
        <div class="cright" onclick="nextItem()">Next</div>
    </div>
    </div>


    <script>

        let currentIndex = 0;
        const sliders = document.querySelectorAll('.wrapper .slide_item')
        const right_sliders = document.querySelectorAll('.wrapper_right .slide_item')
        sliders[currentIndex].classList.add('active_item');
        right_sliders[currentIndex].classList.add('active_item');
        // sliders[currentIndex].firstElementChild.classList.add('active_item');

        function nextItem() {
            // sliders[currentIndex].firstElementChild.classList.remove('active_item');
            if (currentIndex === sliders.length - 1) {
                setTimeout(() => {
                    sliders[sliders.length - 1].classList.remove('active_item')
                    sliders[sliders.length - 1].classList.remove("zindex8");
                    right_sliders[sliders.length - 1].classList.remove('active_item')
                    right_sliders[sliders.length - 1].classList.remove("zindex8");

                }, 1000);
                sliders[sliders.length - 1].classList.add("zindex8");
                right_sliders[sliders.length - 1].classList.add("zindex8");
                currentIndex = 0;
                sliders[currentIndex].classList.add('active_item');
                right_sliders[currentIndex].classList.add('active_item');
                // sliders[currentIndex].firstElementChild.classList.add('active_tem');
                return;
            }
            setTimeout(() => {
                sliders[currentIndex - 1].classList.remove('active_item')
                right_sliders[currentIndex - 1].classList.remove('active_item')
            }, 1000);
            currentIndex++;
            sliders[currentIndex].classList.add('active_item');
            right_sliders[currentIndex].classList.add('active_item');
        }

        function previousItem() {
            sliders[currentIndex].classList.remove('active_item');
            if (currentIndex === 0 || currentIndex < 0) {
                currentIndex = sliders.length - 1;
                sliders[currentIndex].classList.add('active_item');
                return;
            }

            currentIndex--;
            sliders[currentIndex].classList.add('active_item');
        }
    </script>

</body>

</html>
```

#### React Native toast animation 

```
import React, {
    useEffect,
    useRef,
    useState,
  } from 'react';
  
  import {
    Animated,
    Button,
    Text,
    View,
  } from 'react-native';
  
  const getRandomMessage = () => {
    const number = Math.trunc(Math.random() * 10000);
    return 'Random message ' + number;
  };
  
  const Message = (props) => {
    const opacity = useRef(new Animated.Value(0))
      .current;
  
    useEffect(() => {
      Animated.sequence([
        Animated.timing(opacity, {
          toValue: 1,
          duration: 500,
          useNativeDriver: true,
        }),
        Animated.delay(2000),
        Animated.timing(opacity, {
          toValue: 0,
          duration: 500,
          useNativeDriver: true,
        }),
      ]).start(() => {
        props.onHide();
      });
    }, []);
  
    return (
      <Animated.View
        style={{
          opacity,
          transform: [
            {
              translateY: opacity.interpolate({
                inputRange: [0, 1],
                outputRange: [-20, 0],
              }),
            },
          ],
          margin: 10,
          marginBottom: 5,
          backgroundColor: 'white',
          padding: 10,
          borderRadius: 4,
          shadowColor: 'black',
          shadowOffset: {
            width: 0,
            height: 3,
          },
          shadowOpacity: 0.15,
          shadowRadius: 5,
          elevation: 6,
        }}
      >
        <Text>{props.message}</Text>
      </Animated.View>
    );
  };
  
  export default () => {
    const [messages, setMessages] = useState([]);
  
    return (
      <>
        <View
          style={{
            position: 'absolute',
            top: 45,
            left: 0,
            right: 0,
          }}
        >
          {messages.map((message) => (
            <Message
              key={message}
              message={message}
              onHide={() => {
                setMessages((messages) =>
                  messages.filter(
                    (currentMessage) =>
                      currentMessage !== message
                  )
                );
              }}
            />
          ))}
        </View>
  
        <Button
          title="Add message"
          onPress={() => {
            const message = getRandomMessage();
            setMessages([...messages, message]);
          }}
        />
      </>
    );
  };

```

