<h1>End to End Memory Networks</h1>
<h3>The project will be an implementation of the following paper:</h3> <a href="https://arxiv.org/pdf/1503.08895.pdf">End to End Memory Networks</a><br>
Implementation of an AI bot that can answer questions based on a story that is given to the bot.
<pre>
<b>Example:</b>
    Story: Betty went to the store. Don ran to the bedroom.
    Question: Is Don in the store?
    Answer: No
<b>Explanation:</b>
    Here the model understood that Don did not go to the store and answers accordingly. 
    If the model is asked another question such as "Is Don in the bedroom?" and now the 
    answer will be <b>yes</b>.
<b>Dataset Used:</b> <a href="https://research.fb.com/downloads/babi/">babi - Facebook Research</a>
</pre>
<h3>How the bot works:</h3>
<ul>
<li>
   Model takes a discreet set of inputs <b>x1, ..., xn</b>(Sentences) that are to be stored in the memory, a query <b>q</b>(Question), and outputs an answer <b>a</b>(Yes/No). 
</li>

<li>
   Each of the <b>x, q and a</b> contains symbols that come from a dictionary with <b>V</b> words.
</li>

<li>
   The model writes all <b>x</b> to the memory up to a fixed buffer size, and then finds a continous representation for the <b>x and q</b>.
</li>
</ul>

<h3>Model Architecture</h3>
<center>
<img src="https://github.com/mahajanhrishikesh/End-To-End-Memory-Network/blob/master/images/arch.png?raw=true" style="border: 2px black;">
</center>

<h3>Single memory hop:</h3>
Concentrating on the left part of the image. A set of sentences <b>x1, x2,..., xn</b> is fed to the network, these sentences are from the story provided to the network. The sentences are converted into two identical memory vector representations namely <b>mi and ci</b>.<br>
(For a quick refresher in word embeddings <a href="https://machinelearningmastery.com/what-are-word-embeddings/">click here</a>)

The question is also converted into a word embedding giving a result u, the word vectors mi and transpose of u are multiplied and passed through the softmax function to form the vector pi.

<center>
<img src="https://github.com/mahajanhrishikesh/End-To-End-Memory-Network/blob/master/images/utpi.png?raw=true">
<img src="https://github.com/mahajanhrishikesh/End-To-End-Memory-Network/blob/master/images/softmax.png?raw=true">
</center>

Now this resulting pi vector is multiplied with ci vector to give o.

<center>
<img src="https://github.com/mahajanhrishikesh/End-To-End-Memory-Network/blob/master/images/o.png?raw=true">
</center>

Finally we will pass this vector through the softmax function and get a probability vector that will assign probabilities to all the words in the vocabulary but only the probabilites of the words yes or no will be high.

<center>
<img src="https://github.com/mahajanhrishikesh/End-To-End-Memory-Network/blob/master/images/final_mh.png?raw=true">
</center>
<br>
<br>

<h3>Mulitple Layers</h3>
The above architecture explanation was for one memory hop, this process is repeated multiple times with the output of one memory hop becoming the input of the second memory hop. The sentences (x1,x2,...,xn) remain the same. For illustration refer right half of the diagram.
