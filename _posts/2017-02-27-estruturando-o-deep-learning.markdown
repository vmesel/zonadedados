---
layout: post
title:  "Aprenda Deep Learning: Escolhendo a arquitetura de seu modelo"
date:   2017-02-27 19:22:00 -0300
categories: zonadedados deep-learning
---

![Escolhendo a arquitetura de seu modelo]

Deep learning é uma técnica de aprendizagem de máquina(machine learning) que permite uma melhor resolução de problemas a partir da generalização de dados em matrizes de N dimensões. Não existe nenhum padrão para a construção de qualquer tipo de redes de deep learning, mas se seguirmos algumas regras, conseguimos definir uma arquitetura consistente para podermos otimiza-la e chegar em um resultado mais plausível. Neste artigo, eu pretendo mostrar algumas coisas básicas que devem ser levadas em conta na montagem de seu modelo de deep learning e que podem fazer seu modelo chegar mais longe.

## Saiba o tipo de problema que você tem!

Você quer classificar uma imagem? Você não irá usar uma camada de LSTM para isso(a menos que você seja um louco, ou nunca tenha lido este post). O que eu quis dizer com a afirmação passada é: defina qual o seu objetivo, o que você levará em conta para a resolução e como você quer seu output.

Por exemplo:

Objetivo: Classificar uma imagem
O que tenho que levar em conta:

- [X] Filtros que podem encaixar(Convoluções)
- [ ] Sequência de acontecimentos(LSTMs e RNNs)
- [X] Processamento de dados em uma dimensão (Camada densa)

Neste caso, nós devemos pensar em usar camadas densas e de convolução[[1]] assim poderemos ter um modelo de classificação de imagem.

OU AINDA:

Objetivo: Criar um processador de textos
O que tenho que levar em conta:

- [ ] Filtros que podem encaixar(Convoluções)
- [X] Sequência de acontecimentos(LSTMs e RNNs)
- [X] Processamento de dados em uma dimensão (Camada densa)

Neste caso a gente tem que pensar nas sequências das palavras(elas são ou não necessárias), seu processamento(hot encoding? word2vec?) e algumas outras variáveis que tornam o trabalho de escolher a arquitetura um pouco mais complexa.


Qual/quais deve/devem ser meu/meus output/outputs:

No primeiro caso, você deve ter um output, sendo que ele é a probabilidade de tal item estar no grupo definido como padrão(isto se a classificação for binomial(vamos levar em consideração isto para o exemplo ser o mais simples o possível)), já no segundo o output poderia ser a próxima palavra, dada uma palavra anterior, a classificação sentimental de uma palavra ou ainda qual a classe morfológica dela.

## Definindo a arquitetura:

Agora que sabemos as coisas que nossa rede neural deve saber fazer, temos de definir sua estrutura! Para defini-la, nós primeiro levamos em conta a quantidade de itens que devem ser respondidos e a quantidade de respostas que cada item deve produzir(ou seja, a quantidade de inputs e outputs). Ao recebermos uma imagem como input, ele terá apenas 1 neurônio na camada(o único responsável pelo recebimento dos dados). E se como saida quisermos uma probabilidade? Nós devemos usar apenas um neurônio nesta camada, assim ele terá apenas uma resposta plausível e assim por diante.

A definição da arquitetura tem como parte mais importante o tamanho e formato das hidden layers, pois elas que irão definir como os dados serão levados e processados, podendo garantir um resultado totalmente errado ou preciso(como eu não posso descrever tudo com mais exatidão, estou deixando o link [[2]] para vocês olharem o FAQ sobre estruturas de NN e terem uma idéia de como é mais complexo do que imaginamos).

Se seus dados forem linearmente separáveis, não perca tanto tempo com NNs, vá para outro algoritmo mais simples como SVM, Random Forest ou ainda análises Bayesianas para facilitar o processamento e melhorar a rapidez do algoritmo. Se você sabe que seus dados não são linearmente separáveis, identifique a fonte deles(imagem, texto, ondas sonoras e etc.) para assim você definir como sua tratativa deve ser.

Na maioria das vezes, quando se constrói uma rede neural, do input a primeira camada escondida existe um salto no número de neurônios que é normal, mas deve se pensar na tendência que eles devem reduzir chegando a apenas uma transformação do output. Por exemplo: Eu tenho uma imagem 128 x 128px, na primeira camada escondida, eu teria uma camada convolucional de 64 neurônios/filtros, na segunda 32, na terceira 16, logo depois dessas convoluções, eu faria uma transformação para uma dimensão única e processaria como densa. Obviamente que entre estas camadas todas, devemos ter camadas de ativação para a rede funcionar efetivamente.

## Otimizando o modelo

Para otimizar o modelo, você deve realizar testes, a menos que você já tenha uma ideia daonde o problema se concentra. Algumas resoluções para problemas que estão "underfitando" ou "overfitando" são:

- Adicione camadas de dropout, assim você evitará que conexões que se ativam pouco sejam levadas em consideração
- Mexa no tamanho das camadas para tentar melhorar alguma parte da predição
- Modifique e treine com algum algoritmo que já esteja disponível online, assim você pode ter uma base melhor trabalhada

Vou ficando por aqui neste post, mais virão com mais frequência!!

Um grande abraço, [@vmesel]


[1]: https://keras.io/getting-started/sequential-model-guide/
[@vmesel]: http://www.twitter.com/vmesel
[Escolhendo a arquitetura de seu modelo]: http://www.kdnuggets.com/wp-content/uploads/cnn-architecture.jpg
