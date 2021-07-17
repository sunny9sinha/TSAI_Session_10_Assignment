# TSAI_Session_10_Assignment
Task in this assignement was to replace the Embedding layer used in class code with GLOVE embedding and to perform the translation from English to French.
During this assignment we have used GLOVE Embedding as glove.6B.50d.txt which is from GLOVE 6B ( “Wikipedia 2014 + Gigaword 5” ), from this the file is the smallest one
represented by vectors of dim 50 (“glove.6B.50d.txt”). 
We are using bcolz library to store the array of vectors and this library is based on numpy.
We need to go through the text file to get the list of words, dictionary mapping word to index and vectors.
Then we need to create the weight matrix that will be uploaded to the Embedding layer.
For each word we check if it exists in Glove mapping, if yest then we load the corresponding embedding vector at the same index
if it does not exist in Glove mapping then we initialize a random vector.
After this we use this weight matrix to load into the embedding layer of the encoder, decoder and attention decoder.
For the encoder part, we created embedding layer with dimension input_lang.n_words (which is the number of words in input language) and hidden size (which is 50 here).
For the decoder part, we created embedding layer with dimension as output_lang.n_words ( which the number of words in output language) and hidden size(which is 50).
For the Attension decoder part, we created embedding layer with dimension as output_lang.n_words ( which the number of words in output language) and hidden size(which is 50).
Training log for this model:
```python
1m 7s (- 15m 51s) (5000 6%) 3.9046
2m 13s (- 14m 25s) (10000 13%) 3.4218
3m 19s (- 13m 18s) (15000 20%) 3.2237
4m 25s (- 12m 8s) (20000 26%) 3.0269
5m 30s (- 11m 1s) (25000 33%) 2.9602
6m 36s (- 9m 54s) (30000 40%) 2.8272
7m 41s (- 8m 47s) (35000 46%) 2.7511
8m 48s (- 7m 42s) (40000 53%) 2.7046
9m 55s (- 6m 36s) (45000 60%) 2.6657
11m 0s (- 5m 30s) (50000 66%) 2.6027
12m 5s (- 4m 23s) (55000 73%) 2.5590
13m 10s (- 3m 17s) (60000 80%) 2.5293
14m 15s (- 2m 11s) (65000 86%) 2.4444
15m 19s (- 1m 5s) (70000 93%) 2.4338
16m 24s (- 0m 0s) (75000 100%) 2.3639
````

Compairing with the code covered in class, we see that our average loss is more.
One of the reason could be that in class we used embedding layer of size input_lang.n_words (Here input lang was French, number of words 4345) and the hidden layer size which was 256.
While in our case the input language was English ( numbner of words being 2803) and hidden layer size of which is 50.
So, we observe considerable difference in average loss.
In class code we used our own Embedding layer with weights which was trained in model itself, while in asssignement we are using GLOVE Embeddings and considering glove file which has vector of dimension 50.

Random evaluation in our assignment code gives following result. Here First sentence is the input, second is the correct output and third is the predicted output.
```python
> they re all watching us .
= ils nous regardent tous .
< elles sont tous a tous . <EOS>

> i m ticklish .
= je suis chatouilleuse .
< je suis en . <EOS>

> i m very much aware of the danger .
= je suis tres conscient du danger .
< je suis tres occupe pour l <EOS>

> they are spraying the fruit trees .
= ils epandent les arbres fruitiers .
< elles sont des train de . . <EOS>

> i m pleased with his performance .
= je suis satisfait de sa prestation .
< je suis suis pour de . <EOS>

> i m not really angry .
= je ne suis pas vraiment en colere .
< je ne suis pas si fatigue . <EOS>

> we re not really brothers .
= nous ne sommes pas vraiment freres .
< nous ne sommes pas si tres . <EOS>

> you are a good boy .
= vous etes un bon garcon .
< tu es un personne menteur . <EOS>

> you are in my way .
= tu es sur mon chemin .
< tu es le qui . . <EOS>

> he s ready to go .
= il est pret a partir .
< il est a a . . . <EOS>
````
ALso as compared with the class code the assignement code was faster to execute as we have used pre trained Glove embeddings in our code.
However the performance of the code is not satisfactory, as we can see in the random evaluations mentioned above that predictions are not as accurate as the actual output/translation.
We can improve on this probably by using Glove embeddings of higher dimension vector.
