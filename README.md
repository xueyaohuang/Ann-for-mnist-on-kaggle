\documentclass{article}
\usepackage{amsmath}
\usepackage{mathrsfs}
\usepackage{amssymb}
\usepackage{amsfonts}
\usepackage{gauss}
\usepackage[top=1in,bottom=1in,left=1.25in,right=1.25in]{geometry}
\usepackage{dsfont}
\usepackage{amsthm}
\usepackage{graphicx}
\usepackage{multirow}
\usepackage{color}
\usepackage{graphicx}
\usepackage{amsmath}
\usepackage{mathrsfs}
\usepackage{amssymb}
\usepackage{amsfonts}
\usepackage{gauss}
\usepackage{dsfont}
\usepackage{amsthm}
\usepackage{multirow}
\usepackage{float}
\usepackage{algorithm}             
\usepackage{algorithmic}            
\usepackage{multirow}           
\usepackage{amsmath} 
\usepackage{hyperref}
\usepackage{xcolor} 
\usepackage{enumitem}

\DeclareMathOperator*{\argmin}{argmin}         

\renewcommand{\algorithmicrequire}{\textbf{Input:}}  

\renewcommand{\algorithmicensure}{\textbf{Output:}} 
\begin{document}
\title {Homework 4}
\author{Xueyao Huang}
\maketitle

\section{Problem 3}
\begin{enumerate}[label=(\alph*)]
\item
 $MSE_i$ and $MSE_j$ are two random variables. The covariance of these tow R.V. is a measure of the joint variability of the R.V. Intuitively, $Cov(MSE_i , MSE_j)$ is how close $MSE_i$ and $MSE_j$ are related to each other.\\
 The magnitude of the covariance is not easy to interpret because it is not normalized. However, if we assume $std(MSE_i)$ and $std(MSE_j)$ are of the same order, we can regard it approximately as the correlation of $MSE_i$ and $MSE_j$. The larger the $Cov(MSE_i , MSE_j)$, the stronger $MSE_i$ and $MSE_j$ are linearly related. As k increase, the difference between two training samples gets smaller. Namely, the two training sets has more and more examples in common. So $MSE_i$ and $MSE_j$ are more related. Thus, as k increases, $Cov(MSE_i , MSE_j)$ becomes larger.
\item
\begin{align*}
Var(CV_k)&=Var(\cfrac{1}{k}\displaystyle \sum_{i=1}^{k}MSE_i)\\
&=\cfrac{1}{k^2}Var(\displaystyle \sum_{i=1}^{k}MSE_i)\\
&=\cfrac{1}{k^2}\displaystyle \sum_{i=1}^{k}\displaystyle \sum_{j=1}^{k}Cov(MSE_i , MSE_j)
\end{align*}
As k increases, since we have two nested sum, $\displaystyle \sum_{i=1}^{k}\displaystyle \sum_{j=1}^{k}$ will compensate the decrease of $\cfrac{1}{k^2}$. As shown in (a), $Cov(MSE_i , MSE_j)$ will increase because the training become more and more dependent. Thus, $Var(CV_k)$ is higher for larger values of k.



\item

$Var(CV_k|S)$ when k = n, means that we know all the examples in S, and there is no randomness of the n training set, i.e. we know all the examples in each training set. So each $MSE_i$ is determined, and $CV_n$ will be a constant. So $Var(CV_n|S)$ = 0. If $k\neq n$, there is randomness in the combination of the training sets. However, as k increases, the randomness or possibilities in the combination of the training sets decreases. Thus, $Var(CV_k|S)$ is lower for larger values of k.



\item
$Err_k$ is chosen randomly from $\{MSE_1, MSE_2, ..., MSE_k\}$, with possibility $\cfrac{1}{k}$. So the distribution is $P(Err_k=MSE_i)=\cfrac{1}{k}$, for $i=1,2,...k$.
\item
We know the distribution of $Err_k$ in (d), so 
\[
E(Err_k|D)=\displaystyle\sum_i^k MSE_i\cdot P(Err_k=MSE_i)=\displaystyle\sum_i^k MSE_i\cdot \cfrac{1}{k} = CV_k
\]
Hence, $Var(E(Err_k|D) = Var(CV_k)$.
\item
$Bias_{Err_k} = E_D(E_i(Err_k|D))-True\ error$\\
$Bias_{CV_k} = E_D(CV_k|D)-True\ error$\\
Since we know from (e) that $E(Err_k|D)=CV_k$, then $Bias_{Err_k} =Bias_{CV_k}$.
\item
\begin{align*}
Var(Err_k) &= Var(E(Err_k|D)) + E(Var(Err_k|D))\\
&=Var(CV_k) + E(Var(Err_k|D))
\end{align*}
Obviously, $E(Var(Err_k|D))\geq0$, so $Var(Err_k)\geq Var(CV_k)$.


\end{enumerate}

\section{Problem 4}
If there is a probability $\delta$ that the class label on a training data point has been incorrectly set, then
\[
P(y = 1|x;w) = P(label\ correct)\cdot P(y = 1|x;w) + P(label\ wrong)\cdot P(y = 0|x;w)=(1-\delta)h_w(x)+\delta (1-h_w(x))
\]
\[
P(y = 0|x;w) = P(label\ correct)\cdot P(y = 0|x;w) + P(label\ wrong)\cdot P(y = 1|x;w)=(1-\delta)(1-h_w(x))+\delta h_w(x)
\]
We can write this more compactly as 
\[
P(y |x;w) = (P(y = 1|x;w))^y+(1-P(y = 1|x;w))^{1-y}
\]
Assuming that the m training examples were generated independently, we can then write down the likelihood of the parameters as
\[
L(w) = \displaystyle \prod_{i=1}^{m} p(y^{(i)}|x^{(i)};w)=\displaystyle \prod_{i=1}^{m}((1-\delta)h_w(x^{(i)})+\delta (1-h_w(x^{(i)})))^{y^{(i)}}((1-\delta)(1-h_w(x^{(i)}))+\delta h_w(x^{(i)}))^{1-y^{(i)}}
\]
Thus, the log likelihood is 
\[
l(w) = \displaystyle \sum_{i=1}^{m}y^{(i)}log((1-\delta)h_w(x^{(i)})+\delta (1-h_w(x^{(i)}))) + (1-y^{(i)})log((1-\delta)(1-h_w(x^{(i)}))+\delta h_w(x^{(i)}))
\]
If $\delta$ is 0, then it is the same as the formula given in the problem.

\section{Problem 5}
\begin{align*}
Err &= \displaystyle\sum_i (h-y)^2 \\
&=80\cdot (1-h)^2 + 20\cdot (0-h)^2\\
&=100h^2-180h+80
\end{align*}
Differentiate the error function and set it to zero we get
\[
\cfrac{\partial Err}{\partial h}=0
\]
\[
h=0.8
\]
So the probability that the output value is 1 is 0.8.\\
Since the network has been trained and reaches a global optimum, i.e., the result should minimize the cost, it is resonable to diï¬erentiate with respect to the output.
\section{Problem 6}
Please see ann.py.\\


\section{Problem 7}
My approach to solve this problem is as follows.\\
1. Read data from csv and construct the features X and labels y.\\
2. Normalize the training features by dividing 255 of each pixel value, to keep the result in the high derivative area of activation function(sigmoid).\\
3. Use one hot encoding to transform lables y to vectors.\\
4. Use sklearn train\_test\_split to split data into 2 parts, i.e. training and testing.\\
5. Use the predefined ann to fit the training data. I use L2 loss and mini-batch SGD to train the ann. I also implemented cross entropy loss, however, not used in this mnist task.\\
6. The strcuture of my ann is 5 layers ann, including input layer, 3 hidden layers and output layer. The size of the hidden layers is [256, 128, 64].\\
7. I did some hyperparameter tuning during the training. The final hyperparameter I used is learning rate is 0.1, number of epoches is 20, batch size is 32.\\
8. After 20 epoches of training, the accuracy on validation data is 97.24\%.\\
9. Plot the training cost and validation cost as a function of number of epoches, as shown below.\\
\[
\includegraphics[scale=0.75]{1.png}
\]
10. Plot the training accuracy and validation accuracy as a function of number of epoches, as shown below.\\
\[
\includegraphics[scale=0.75]{2.png}
\]
11. Plot the confusion matrix, as shown below.\\
\[
\includegraphics[scale=0.75]{3.png}
\]



\end{document}










