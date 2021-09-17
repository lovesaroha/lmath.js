## lmath.js
This is a generalized math package with clean and transparent API for the javascript.
Also available for golang [github/lovesaroha/lmath](https://github.com/lovesaroha/lmath) 

## Installation

```html
    <script type="text/javascript" src="lmath.js"></script>
```

## Usage

### Random

```js
  // Random value between given range.
  let random = lmath.Random(-1, 1)
```

### Map Given Value Between Given Range
```js
  // Return value between given range of (200, 1000).
  let value = lmath.Map(20 , 0, 100, 200, 1000)
```

## Apply Math Functions
```js
  // Sigmoid.
  let result = lmath.Sigmoid(1.5)
  // Diff of sigmoid.
  let dresult = lmath.Dsigmoid(result)
  // Relu.
  let result = lmath.Relu(2)
  // Diff of relu.
  let dresult = lmath.Drelu(result)
```
### Create Matrix 

```js
  // Create a matrix (rows, cols).
  let matrix = lmath.Matrix(4, 3)

  // Print matrix shape.
  matrix.Shape()
  // Print matrix values.
  matrix.Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/38.png)

### Create Random Matrix 

```js
  // Create a matrix (rows, cols, minimum , maximum).
  let matrix = lmath.Matrix(3, 4, -1 , 1)

  // Print matrix shape.
  matrix.Shape()
  // Print matrix values.
  matrix.Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/39.png)

### Convert Array Into Matrix 

```js
    // Array to matrix and print values.
    lmath.ToMatrix([1, 2, 3]).Print()
    lmath.ToMatrix([[1, 2], [3, 4]]).Print()
    lmath.ToMatrix([4, 5, 6]).Print()
        lmath.ToMatrix([[7, 8], [9, 0]]).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/45.png)

### Matrix Element Wise Operations (Add, Subtract, Multiply, Divide) 

```js
  // Create a matrix (rows, cols, minimum , maximum).
  let matrix = lmath.Matrix(3, 4, 10, 20)
  let matrixB = lmath.Matrix(3, 4, 0, 10)

  // Add and print values.
  matrix.Add(matrixB).Print()
  // Subtract and print values.
  matrix.Sub(matrixB).Print()
  // Multiply and print values.
  matrix.Mul(matrixB).Print()
  // Divide and print values.
  matrix.Sub(matrixB).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/40.png)

### Matrix Element Wise Operations With Scalar Value (Add, Subtract, Multiply, Divide) 

```js
  // Create a matrix (rows, cols, minimum , maximum).
  let matrix = lmath.Matrix(3, 4, 10, 20)

  // Add and print values.
  matrix.Add(2).Print()
  // Subtract and print values.
  matrix.Sub(2).Print()
  // Multiply and print values.
  matrix.Mul(2).Print()
  // Divide and print values.
  matrix.Sub(2).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/47.png)

### Matrix Dot Product 

```js
  // Create a matrix (rows, cols, minimum , maximum).
  let matrix = lmath.Matrix(3, 4, 10, 20)
  let matrixB = lmath.Matrix(4, 3, 0, 10)

  // Dot product and print values.
  matrix.Dot(matrixB).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/41.png)

### Matrix Transpose
```js
  // Create a matrix (rows, cols, minimum , maximum).
  let matrix = lmath.Matrix(3, 4, 10, 20)

  // Print values.
  matrix.Print()
  // Transpose and print values.
  matrix.Transpose().Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/42.png)

### Add All Column Values
```js
  // Create a matrix (rows, cols, minimum , maximum).
  let matrix = lmath.Matrix(3, 4, 10, 20)

  // Print values.
  matrix.Print()
  // Add columns and print values.
  matrix.AddCols().Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/46.png)

### Change Matrix Values (Map)
```js
  // Create a matrix (rows, cols, minimum , maximum).
  let matrix = lmath.Matrix(3, 4, 10, 20)

  // Print values.
  matrix.Print()
  // Square and print values.
  matrix.Map(function(x) {
      return x * x;
  }).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/43.png)

### Apply Function In Matrix
```js
  // Create a matrix (rows, cols, minimum , maximum).
  let matrix = lmath.Matrix(3, 4, -1, 1)

  // Print values.
  matrix.Print()
  // Apply sigmoid and print values.
  matrix.Map(lmath.Sigmoid).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/44.png)

## Examples

### Logistic Regression (OR Gate)
```js 
    // Learning rate.
    let learningRate = 0.2

    // Inputs and outputs.
    let inputs = lmath.ToMatrix([[1, 1, 0, 0] , [0, 1, 0, 1]])
    let outputs = lmath.ToMatrix([[1, 1, 0, 1]])

    // Weights and bias.
    let weights = lmath.Matrix(2, 1, -1, 1)
    let bias = lmath.Random(-1, 1)

    // Train weights and bias (epochs 1000).
    for(let i = 0; i < 1000; i++) {
      // Sigmoid(wx + b).
      let prediction = weights.Transpose().Dot(inputs).Add(bias).Map(lmath.Sigmoid)
      let dZ = prediction.Sub(outputs)
      weights = weights.Sub(inputs.Dot(dZ.Transpose()).Divide(4).Mul(learningRate))
      bias -= dZ.Sum() / 4
    }

    // Show prediction.
    weights.Transpose().Dot(inputs).Add(bias).Map(lmath.Sigmoid).Print()

```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/48.png)