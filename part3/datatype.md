# 資料類型(值) Data Type

JavaScript有6種原始的原始資料類型(Primitive)，分別是字串、數字與布林值，以及兩種特殊情況的null(空)與undefined(未定義)，ES6標準中加入了符號(symbol)。

JavaScript中還有另一個非常重要的第7種資料類型 - Object(物件)。

我們常常會把屬於物件的Array(陣列)、Data(日期時間)、Function(函式)、RegExp(正規表述式)獨立出來說明，因為這些物件都有特殊的功能和作用，算是特別的物件類型。

總之，我們大致上的分類是像下面這樣，本章節也是以這個分類開始來介紹，陣列與物件將會再獨立為另一章節說明。至於新的資料類型symbol(符號)，它的使用情況會需要先了很多基礎知識，本書中並不會介紹。

主要的原始資料類型:

- 數字(Number)
- 字串(String)
- 布林值(Boolean)

特殊的原始資料類型:

- null(空)
- undefined(未定義)
- symbol(符號)

複合型(composite)或參考型(reference)的資料類型:

- array(陣列)
- object(物件)

> 註: 所謂的"原始資料類型"，指的是在程式語言中，最低階的一種資料類型，不屬於物件也沒有方法。它也具有不可改變的(immutable)特性。不過，JavaScript語言中也存在名稱為String、Number、Boolean對應原始資料類型的物件，它們是包裝物件(wrapper object)，提供了原始資料類型的一些延申的應用屬性與方法，真正會用到這些物件只有在特殊情況下。

> 註: 是的，JavaScript的確是一個物件導向的程式語言。不過，JavaScript的物件導向特性與其他語言例如Java、C++等有很大的不同。

## 鬆散資料類型

JavaScript語言是一個鬆散資料類型(loosely typed)或稱為動態的程式語言(dynamic language)。這代表你不需要為變數or常數在宣告時，就規定它的資料類型，而只是指定值。JavaScript會依照指定值決定變數or常數的資料類型。

```
let foo = 42    // foo現在是Number資料類型
let foo = 'bar' // foo現在是String資料類型
let foo = true // foo現在是Boolean資料類型
```

## 判斷資料類型 - typeof

對於要如何判斷目前變數or常數的資料類型，最簡便的方式就是使用這個運算符`typeof`，它是個運算符，類似正號(+)或負號(-)的行為，它是個一元的運算符，所以是加在運算元的前面。最後會回傳一個類型的字串，範例如下:

```js
console.log(typeof 37) //'number'
console.log(typeof NaN) //'number'
console.log(typeof '') //'string'
console.log(typeof (typeof 1)) //'string'
console.log(typeof true) //'boolean'
console.log(typeof null) //'object'
```

> 註: 為何null資料類型的的typeof結果是'object'(物件)，而不是'null'呢？依據[ECMAScript的標準章節11.4.3條](http://www.ecma-international.org/ecma-262/5.1/#sec-11.4.3)對typeof結果的規定，就是回傳'object'。不過有一些反對的聲音，認為null是原始資料類型，應當回傳自己本身的資料類型。目前至ES6仍然沒有更動。

## 數字(Number)

JavaScript的數字(Number/難波/)類型必定是64位元的浮點數，類似於Java語言的`double`/打波/資料類型，並沒有如其他程式語言中，有獨立的整數(int)或浮點數(float)類型。在JavaScript中，`1`與`1.0`指的是相同的類型與值。此外，數字可以使用算術運算符(+-*/%)等來進行運算。以下是幾個宣告的範例:

```js
const intValue = 123
const floatValue = 10.01
const negValue= -5.5
```

電腦中的程式語言在數學上的運算，總會有處理上的極限與無法處理的情況。JavaScript使用三個特殊的記號，來代表在數字上處理的極限值或非數字的情況:

- +Infinity: 正無限值(相當於Infinity)
- -Infinity: 負無限值
- NaN: 不是數字

```js
console.log(1/0)
console.log(1/-0) //0有分+0與-0，這有點算陷阱
console.log(Infinity - Infinity) //NaN
```

數字的最大與最小值，可以使用`Number.MAX_VALUE`與`Number.MIN_VALUE`得到。

```js
console.log(Number.MAX_VALUE)
console.log(Number.MIN_VALUE)
```

### 整數進位

以整數來說，整數的進位是一個問題，一般的整數進位有2、8、16，以及最常使用的10進位。JavaScript中直接可以用`0x`開頭來定義16進位(Hexadecimal):

```js
const x = 0xFF
const y = 0xAA33BC   
```

2或8進位並沒有內建的直接可定義方式，需要透過一個字串的方法`parseInt(string, radix)`，將一個2進位或8進位的數字字串轉換，這方式也可以轉換16進位的數字字串:

```js
//8進位
const octalNumber = parseInt('071',8);

//2進位
const binaryNumber = parseInt('0111',2);

//16進位
const hexNumber = parseInt('0xFF',16);
```

> 註: 不論是2、8、16進位的數字，直接輸出到HTML碼中必定會自動轉成10進位輸出。

另一個情況是要將10進位數字以不同的進位基數(radix)轉為字串，通常是用在輸出時，這時要使用數字的方法 - `toString([radix])`

```js
const decimalNumber = 125
console.log(decimalNumber.toString())
console.log(decimalNumber.toString(2))
console.log(decimalNumber.toString(8))
console.log(decimalNumber.toString(16))
```

### 浮點數的轉換

#### 字串轉浮點數

對照上面的`parseInt`方法，字串也有另一個`parseFloat(string)`可以轉換數字字串為浮點數，不過就像最上面所說明的，數字1.0相當於1，對於JavaScript來說，數字就是數字。以下是範例:

```js
const aNumber = parseFloat("10")  //10
const bNumber = parseFloat("10.00") //10
const cNumber = parseFloat("10.33") //10.33
const dNumber = parseFloat("34 45 66") //34
const eNumber = parseFloat("40 years") //40
const fNumber = parseFloat("He was 40")  //NaN
```

####  浮點數轉整數

至於浮點數要轉換為整數，需要使用Math物件中的幾個方法來轉換，因為浮點數是要轉換為直接進位，還是四捨五入，還是直接去掉小數點，就看你需要的情況:

```js
const floatValue = 10.55
const intValueOne = Math.floor( floatValue ) //地板值 10
const intValueTwo = Math.ceil( floatValue ) //天花板值 11
const intValueThree = Math.round( floatValue ) //四捨五入值 11
```

> 註: Math是專門用於數學運算使用的JavaScript語言內建物件，裡面有很多好用的數學方法，請參考[Math(MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)與[JavaScript Math Object](http://www.w3schools.com/js/js_math.asp)

#### 整數轉浮點數

再強調一下，對於JavaScript來說，數字就是數字，沒有什麼浮點數或整數的類型。如果你強烈想要3.00而不是3的數字，這在JavaScript中來說都是一樣的，直接轉出數字3.00依然會用3來顯示。

唯一可能的情況，是希望調整輸出的格式。這時可以用數字物件中的`toFixed([digits])`方法來達成，不過它會回傳成字串，這已經不是數字了:

```js
const myString = (3).toFixed(2) //string, 3.00

const numObj = 12345.6789 
const numObjString = numObj.toFixed() //string, 123456
```

### 數字的精確問題

數字並非是永無極限的，有最大的數值上限也有最小的下限。上面已有說明它的最大與最小值怎麼獲得，但在運算時，有時候會出現不如你想像的情況，這些都與浮點數的精確度(precision)，有關以下是幾個典型的範例，這些都算是陷阱題目:

#### 範例一：

注意: 第二行的值失去精確，它會變成另一個值

```js
console.log(999999999999999)
console.log(9999999999999999)
```

#### 範例二

注意: x並不是0.3

```js
const x = 0.2 + 0.1
```

#### 範例三

注意: i永遠不會等於10，這個程式是無窮迴圈，可能會讓網頁當掉。

```js
let i = 0
while(i != 10) { 
  i += 0.2
}
```

> 註: 範例來自[Number, Math](http://JavaScript.info/tutorial/number-math#permissive-conversion-parseint-and-parsefloat)

因此，在處理浮點數時，要格外小心。如果你遇到了不可預期的結果，有可能是精確出了問題。程式語言永遠有其限制，這不是在JavaScript語言才會出現的，其他的程式語言也有可能有類似的問題。

## 字串(String)

字串類型用於描述一般的字串值，是使用相當廣泛的值。例如：

```js
const aString = '你好'
const bString = 'Hello'
```

對於JavaScript語言來說，使用雙引號標記("")與單引號標記('')來定義字串值，結果都是一樣的。但推薦只使用**單引號標記('')**，原因是HTML碼中也會使用引號來作為標記屬性值的定義，而JavaScript經常需要與HTML碼搭配使用，所以這個也變成一個約定俗成的撰寫習慣。

### 字串與字元

存取一個字串中的字元，可以用類似陣列的存取方式，或是用`charAt()`方法。不過，JavaScript中並沒有所謂的字元(Character)類型，所以它依然是個字串(String)資料類型，只是只有一個字元而已。

```js
const a = 'cat'.charAt(1)   //  'a'
const b = 'cat'[1]   // 'a'

console.log(typeof a)
```

### 跳脫字元(escape characters)

當需要在雙引號符號(")中使用雙引號(")，或在單引號(')中使用單引號(')時，或在字串中使用一些特殊用途的字元。使用反斜線符號`\`來進行跳脫，這稱為跳脫字元或跳脫記號。常見用於在英文縮寫，例如：

```js
'It\'s alright';
'This is a blackslash \\'
```

### 樣版字串(Template strings)

ES6中新式的字串寫法，稱為樣版字串(Template strings)，使用的是重音符號backtick(``)來敘述字串。樣版字串可以多行、加入字串變數，以及其他延申的用法。範例如下：

```js
`hello world`
`hello!
 world!`
`hello ${who}`
escape `<a>${who}</a>`
```

### 字串運算

字串中有很多運算用的函式與記號，以下是常用的幾個：

#### 字串連接

使用加號(+)是最直覺的方式，效能也比`concat()`好，這兩種方式都是同樣的結果，範例如下：

```

```

看到加號(+)時，你如果看到數字中也有運算用的加號(+)，可能會有個疑問，像下面這個程式碼，結果應該是什麼，到底會是101還是11？

```js
const a = '10' + 1
console.log(a)

const b = 10 + '1'
console.log(b)
```

依據[ECMAScript的標準章節11.6.1條](http://www.ecma-international.org/ecma-262/5.1/#sec-11.6.1)對加號(+)運算的規定，簡單說明如下:

> 當運算式的左邊運算元**或**右邊運算元，是字串類型時，則使用字串連接(concatenating)的運算，非字串類型的運算元則使用ToString轉換

所以上面的兩個輸出的結果會是101，沒問題吧

那更複雜的運算像下面的程式碼又會是什麼結果呢？

```js
console.log( 3 + 4 + '5' )
console.log( 4 + 3 + '5' + 3 )
```

### 風格指引

- (Airbnb 6.2) 雖然使用雙引號(")與單引號(')都是一樣的宣告方式，但建議使用單引號(')
- (Airbnb 6.3) 字串中的長度超過100字元時，需分成多個字串，然後使用字串的連接符號(+)
- (Airbnb 6.6) 避免在字串中使用不必要的跳脫字元

## 布林值(boolean)

## 空(null)與未定義(undefined)

空(null)就是空值，不是空白(space)。空代表的是沒有值(empty)，不存在值的意思。

未定義(undefined)即是尚未定義，沒有任何的定義。

這兩個資料類型常會被拿來比較，何為"空"又何為"未定義"?目前看到最好的解說如下:

```
當name從來未被定義過時
```

你問JavaScript: name是什麼?

JavaScript回答: name? 從來沒聽過? 我不知道你在說什麼?

```js
name = null 
```

你問JavaScript: name是什麼?

JavaScript回答: 我不知道

以上的回答來自: [Why is null an object and what's the difference between null and undefined?](http://stackoverflow.com/questions/801032/why-is-null-an-object-and-whats-the-difference-between-null-and-undefined)

### 比較運算

null與undefined作比較運算時，在值的比較(==)是相等的，而在值與類型比較(===)時，是不相等的，這是能夠比較出兩個差異的地方。

```js
null  == undefined // true
null === undefined // false
```

類型的部份，目前null的類型仍然是object，而不是null。這也呼應了上面的值與類型比較。

```js
typeof null        // object (bug in ECMAScript, should be null)
typeof undefined   // undefined
```

## 小結

## 作業

