# Projeto - Neural Network Parallel with OPENMP

Este projeto é uma adaptação de código do projeto original presente em: [Neural-Network-MNIST-CPP](https://github.com/HyTruongSon/Neural-Network-MNIST-CPP)

Software: Artificial Neural Network for MNIST database (C++)
Author: Hy Truong Son
Major: BSc. Computer Science
Class: 2013 - 2016
Institution: Eotvos Lorand University
Email: sonpascal93@gmail.com
Website: http://people.inf.elte.hu/hytruongson/
Copyright 2015 (c). All rights reserved.

## Overall
O projeto original tem como objetivo realizar o treinamento de uma máquina capaz de reconhecer números escritos em "imagens" simuladas via terminal, como o seguinte exemplo:

```
No. input neurons: 784
No. hidden neurons: 128
No. output neurons: 10

No. iterations: 512
Learning rate: 0.001
Momentum: 0.9
Epsilon: 0.001

Training image data: mnist/train-images.idx3-ubyte
Training label data: mnist/train-labels.idx1-ubyte
No. training sample: 60000

Sample 1
Image:
0000000000000000000000000000
0000000000000000000000000000
0000000000000000000000000000
0000000000000000000000000000
0000000000000000000000000000
0000000000001111111111110000
0000000011111111111111110000
0000000111111111111111100000
0000000111111111110000000000
0000000011111110110000000000
0000000001111100000000000000
0000000000011110000000000000
0000000000011110000000000000
0000000000001111110000000000
0000000000000111111000000000
0000000000000011111100000000
0000000000000001111100000000
0000000000000000011110000000
0000000000000011111110000000
0000000000001111111100000000
0000000000111111111000000000
0000000011111111110000000000
0000001111111111000000000000
0000111111111100000000000000
0000111111110000000000000000
0000000000000000000000000000
0000000000000000000000000000
0000000000000000000000000000
Label: 5
No. iterations: 512
Error: 0.009284

Sample 2
Image:
0000000000000000000000000000
0000000000000000000000000000
0000000000000000000000000000
0000000000000000000000000000
0000000000000001111100000000
0000000000000011111100000000
0000000000000111111111000000
0000000000011111111111000000
0000000000011111111111000000
0000000000111111111111000000
0000000001111111110011100000
0000000011111100000011100000
0000000111111100000011100000
0000000111100000000011100000
0000000111000000000011100000
0000001111000000000011100000
0000001111000000001111100000
0000001110000000011111000000
0000001110000000111100000000
0000001110000001111000000000
0000001111111111111000000000
0000001111111111100000000000
0000001111111110000000000000
0000000111111100000000000000
0000000000000000000000000000
0000000000000000000000000000
0000000000000000000000000000
0000000000000000000000000000
Label: 0
No. iterations: 512
Error: 0.007427

```

Após o treinamento, a máquina é sujeita a uma avaliação em que é possível se verificar a taxa de acerto da máquina, da seguinte forma:

```
No. input neurons: 784
No. hidden neurons: 128
No. output neurons: 10

Testing image data: mnist/t10k-images.idx3-ubyte
Testing label data: mnist/t10k-labels.idx1-ubyte
No. testing sample: 10000

Sample 1
Error: 0.000000
Classification: YES. Label = 7. Predict = 7

...

Sample 9999
Error: 0.000001
Classification: YES. Label = 5. Predict = 5

Sample 10000
Error: 0.000002
Classification: YES. Label = 6. Predict = 6

Number of correct samples: 9440 / 10000
Accuracy: 94.40

```

## Structure

File training_nn.cpp: the code for training a neural network
File testing_nn.cpp: the code for testing a trained neural network
File model-neural-network.dat: contains the weights of the neural network
File training-report.dat, testing-report.dat: report files, saving results of training and testing
Folder ~/mnist/: MNIST database

Note: model-neural-network.dat is the input for teting process (testing_nn.cpp)

## Usage

* Compile:
  
```
$ g++ training_nn.cpp -o training_nn
$ g++ testing_nn.cpp -o testing_nn

```

* Training:
  
```
$ ./training_nn
```

* Testing:
  
```
$ ./testing_nn
```

## Results

Para realizar a paralelização do código, optamos por tentar fazer com que a máquina aprendesse mais rápido, paralelizando o treinamento. Dessa forma, a fins de demonstração de resultado,
utilizamos uma mesma quantidade de _samples_ (300) para os testes sequenciais e paralelos.

Seguem os resultados dos testes e os tempos de execução utilizando o servidor Parcode:

### Sequencial

Tempo de execução do treinamento

```
real    0m50,811s
user    0m50,714s
sys     0m0,076s
```

Taxa de acerto no teste da máquina
```
Number of correct samples: 8023 / 10000
Accuracy: 80.23%

real    0m1,475s
user    0m0,855s
sys     0m0,190s
```

### Paralelo

Tempo de execução do treinamento


