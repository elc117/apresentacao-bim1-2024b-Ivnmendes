# Para começar, um contexto...
A visão computacional é um campo da inteligência artificial que utiliza algoritmos de aprendizagem de máquina para interpretar e entender o conteúdo de imagens e vídeos. Uma das tarefas fundamentais na visão computacional é a detecção de objetos, que envolve localizar e identificar objetos de interesse dentro de uma imagem ou um vídeo.

Durante o processo de detecção de objetos, três informações principais são geradas:

Bounding Boxes (BBoxes): São retângulos ou caixas delimitadoras que representam a localização de objetos detectados em uma imagem. Cada bounding box é definida por quatro coordenadas (x1,y1,x2,y2), que correspondem aos cantos superior esquerdo e inferior direito da caixa. As bounding boxes ajudam a indicar onde os objetos estão localizados na imagem.
Scores: Para cada bounding box, um score é atribuído, representando a confiança do modelo na detecção do objeto. Esse score é um valor entre 0 e 1, onde valores mais altos indicam maior confiança de que um objeto foi detectado corretamente. O score é fundamental para filtrar detecções irrelevantes ou errôneas.
Classes: Cada objeto detectado é classificado em uma de várias categorias (ou classes) pré-definidas. Por exemplo, em um modelo treinado para detectar animais pode incluir "gato" e "cachorro".

A imagem abaixo ilustra as bounding boxes, classes e scores.

![image](src\image.svg)
fonte:  http://d2l.ai/chapter_computer-vision/anchor.html

# Dados para teste
Em Haskell, podemos usar listas para representar bounding boxes, scores e classes de objetos. Essas listas têm o mesmo número de elementos, sendo que o primeiro elemento em cada uma delas refere-se ao primeiro objeto, e assim por diante. Por exemplo, no código abaixo, o primeiro objeto é da classe 0, com score 0.95 e com bounding box (34.0, 60.0, 200.0, 320.0).

~~~
-- Bounding boxes: (xmin, ymin, xmax, ymax)
boundingBoxes :: [(Float, Float, Float, Float)]
boundingBoxes = [ (34.0, 60.0, 200.0, 320.0),
              	(100.0, 150.0, 250.0, 380.0),
              	(300.0, 220.0, 450.0, 450.0) ]

-- Scores: Confidence scores for each detection
scores :: [Float]
scores = [0.95, 0.80, 0.60]

-- Classes: Class 0 or 1 representing two object types
classes :: [Int]
classes = [0, 1, 0]
~~~

# Exercício

11. Crie uma função para obter a quantidade de objetos de uma determinada classe. Essa função deve receber um número representando uma classe e uma lista de classes.
Resolva esta função sem usar lambda.

Exemplo de uso:
~~~
ghci> countObjectsForClass 0 classes
2
~~~

Nome e tipo da função:
~~~
countObjectsForClass :: Int -> [Int] -> Int
~~~

12. Resolva o exercício 11 usando lambda:

Inicialmente tentei resolver usando a função fold que percorre uma lista e aplica uma função acumulativamente em um sentido (esquerda-direita ou direita-esquerda), retornando um valor. Porém, me atrapalhei um pouco para usar a condição de contar somente quando igual a classe desejada. Por fim, resolvi fazer utilizando um length em uma lista filtrada.

~~~
-- Versão com lambda
countObjectsForClass :: Int -> [Int] -> Int
countObjectsForClass classe lista = length (filter (\elemento -> elemento == classe) lista)

-- Versão sem lambda
countObjectsForClass :: Int -> [Int] -> Int
countObjectsForClass classe lista = length (filter (== classe) lista)
~~~

Provavelmente não é a forma mais simples ou mais otimizada, mas retorna corretamente quantos objetos de uma determinada classe tem na lista inserida.
