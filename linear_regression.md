 
# Linear Regression

## Experimenting with Math.NET

### Creatng a vector

```fsharp
let velocities = vector[23.;4.;5.;2.]
```
### Creating a matrix
```fsharp
let y = matrix [[1.;3.]
                [1.;5.]
                [1.;4.]]
```                
#### Creating a matrix from a list of rows
```fsharp
//Loading values of the csv file and generating a dense matrix
//Please modify the file path to point it in your local disc
let rows = File.ReadAllLines("C:\\mpg.csv")
               |> Array.map (fun t -> t.Split(',')
               |> Array.map (fun t -> float t);
let mpgData = DenseMatrix.ofRowArrays rows
```
### Finding transpose of a matrix

### Finding the inverse of a matrix
### Trace of a matrix
### QR decomposition of a matrix
### SVD of a matrix

## Linear Regression Method of Least Square
```fsharp
let x =  [14;16;27;42;39;50;83]
let y =  [02;05;07;09;10;13;20]

let diff = List.zip x y
let xy = diff |> List.map ( fun it -> float (fst it) * float (snd it))  |> List.sum
let x_ = x |> List.map ( fun z -> float z) |> List.average
let y_ = y |> List.map ( fun z -> float z) |> List.average
let sx_2 = x |> List.sumBy ( fun  t -> float t * float t)
let sy_2 = y |> List.sumBy ( fun t -> float t * float t)
let n = float x.Length
let b1 =  (xy - n*x_*y_)/(sx_2 - n * x_ * x_) 
let b0 = y_ - b1*x_ 
b1.Dump("b1")
b0.Dump("b0")


type Entry = {
              DiskIO:int; 
              CPUTime:int; 
              Estimate:float; 
              Error : float; 
              ErrorSquared:float
              }

let result = List.zip x y |> List.map (fun elem -> { DiskIO = fst elem; 
                 CPUTime  = snd elem; 
                 Estimate = b0 + b1 * float( fst elem);
                 Error = float(snd elem) - b0 - b1 * float (fst elem);
                 ErrorSquared = Math.Pow(float(snd elem) - b0 - b1 * float (fst elem),2.)})
result.Dump("Result of the linear regression")
```
