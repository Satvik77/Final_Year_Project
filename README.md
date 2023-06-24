# Automatic-Essay-Scoring (AES)
An Automated Essay Grading System (AEGS) is a tool designed to evaluate and score essays written in response to specific prompts. It involves the use of computer programs to automate the assessment process of essays. AEGS provides a systematic and efficient way to analyze and assign scores to essays, offering several benefits for educators and learners alike.

For educators, an AEGS can save time and effort in grading large numbers of essays. Instead of manually reading and evaluating each essay, the system automates the scoring process, providing quicker results. This allows educators to allocate their time and resources more effectively, focusing on other aspects of teaching and providing feedback on areas where human judgment is critical.

For learners, an AEGS offers the opportunity for iterative improvement in their writing skills. With automated scoring, students can receive immediate feedback on their essays, including strengths and areas for improvement. This feedback can guide students in revising their work, making necessary adjustments, and enhancing their writing abilities over time.

Additionally, an AEGS can contribute to standardization and fairness in grading. By utilizing predefined scoring criteria, the system can provide consistent evaluations, reducing potential bias and variability that may occur in manual grading. This promotes fairness in the assessment process, ensuring that students are evaluated based on objective criteria.

However, it's important to note that AEGS is not a perfect replacement for human grading. While it offers efficiency and consistency, there are certain aspects of essay evaluation that require human judgment, such as creativity, critical thinking, and nuanced interpretations. AEGS should be seen as a complementary tool that assists educators in the assessment process, providing valuable insights and support.

In summary, an Automated Essay Grading System (AEGS) is a useful tool that automates the assessment and scoring of essays. It benefits educators by saving time and providing consistency, and it benefits learners by offering immediate feedback and opportunities for improvement. AEGS promotes standardization and fairness in grading while acknowledging the importance of human judgment in certain aspects of essay evaluation.

## Why AES?
Automated grading if proven effective will not only reduce the time for assessment but comparing it with human scores will also make the score realistic. The project aims to develop an automated essay assessment system by use of machine learning techniques and Neural networks by classifying a corpus of textual entities into a small number of discrete categories, corresponding to possible grades.

## Dataset

The dataset used for our project is the 'The Hewlett Foundation: Automated Essay Scoring Dataset' by ASAP. This dataset can be accessed and downloaded from the Kaggle competition page using the following link:

https://www.kaggle.com/c/asap-aes/data

The dataset consists of a collection of essays written by students, along with their corresponding scores. The essays cover a variety of prompts or topics, and each essay is scored based on a predefined scoring rubric. The dataset provides a valuable resource for developing and evaluating automated essay scoring models.

To obtain the dataset, you can visit the provided Kaggle link and follow the instructions on the page to download the necessary files. Alternatively, you can also access the dataset from the 'Dataset' folder, if it has been provided separately in this project.

Once you have downloaded the dataset, you will have access to the essays and their associated scores, which can be used for training and evaluating the essay scoring model.



## Architecture Diagram
 
![image](https://github.com/Satvik77/AEGS/assets/83899207/1071fc97-3123-4ff7-9ed9-1a6d531ec342)



## Proposed Model

The proposed model for essay scoring consists of the following components:

1. Word2Vec Model:
   - We create a list of words from each sentence and essay in the dataset.
   - This list of words is fed into the Word2Vec model, which assigns numerical vector values to each word.
   - The Word2Vec model acts as an embedding layer in the neural network, providing meaningful representations of words.

2. LSTM Layers:
   - The model includes two LSTM layers for sequential learning.
   - The first LSTM layer takes the features generated by the Word2Vec model as input and produces 300 features as output.
   - The output of the first LSTM layer is then passed to the second LSTM layer, which reduces the dimensionality to 64 features.

3. Dropout Layer:
   - A dropout layer is added after the LSTM layers to prevent overfitting.
   - The dropout layer randomly drops out a fraction of the input units during training, helping to improve generalization and reduce overfitting.

4. Dense Layer:
   - The final layer is a fully connected dense layer with a single output unit.
   - This dense layer predicts the score of the essay based on the features extracted from the LSTM layers.

5. Model Compilation and Training:
   - The model is compiled with the mean squared error loss function and the root mean square optimizer.
   - It is trained for 150 epochs with a batch size of 64, optimizing the model's parameters to minimize the mean squared error between the predicted scores and the actual scores.

By incorporating Word2Vec for word embeddings, LSTM layers for sequential learning, and a dense layer for score prediction, this proposed model aims to capture the semantic relationships in the essays and make accurate predictions of their scores. The dropout layer helps prevent overfitting, and the model is trained using the mean squared error loss function to improve performance.


But first the model achieved is divided into 4 modules as follows:

**1. Data Preprocessing**

In the data preprocessing stage of our project, we followed several standard steps to prepare our dataset for further analysis and modeling. Here is an overview of the preprocessing steps we performed:

Handling Null Values: We addressed any missing or null values in the dataset by filling them in with appropriate values based on the nature of the data. This step ensures that our dataset is complete and ready for analysis.

Feature Selection: After a thorough examination of the dataset, we selected relevant features that are likely to have an impact on the essay scoring task. This step helps us focus on the most informative attributes and discard irrelevant ones, reducing noise and improving model performance.

Skewness Reduction: We analyzed the distribution of our data and identified any significant skewness. To mitigate this skewness, we applied normalization techniques such as logarithmic transformations or scaling to bring the data closer to a normal distribution. This step aids in improving the performance of certain machine learning algorithms that assume data normality.

Essay Cleaning: To facilitate the training process and enhance accuracy, we performed text cleaning on the essays. This involved removing unnecessary symbols, stopwords (common words that do not contribute much to the overall meaning), and punctuation marks. By eliminating noise and irrelevant text components, we improve the quality of the data and the subsequent analysis.

Additional Feature Engineering: In order to further improve the accuracy of our models, we incorporated additional features into our dataset. These features include the number of sentences, number of words, number of characters, and average word length in each essay. Additionally, we leveraged techniques such as parts-of-speech tagging to extract counts of nouns, verbs, adjectives, and adverbs. Furthermore, we calculated the total number of misspellings in an essay by comparing it with a corpus or dictionary. These additional features provide valuable insights and enhance the predictive power of our models.

After completing the data preprocessing steps, the processed dataset can be found in the file named "Processed_data.csv". This file contains the cleaned and transformed data, ready for further analysis and modeling in subsequent stages of the project.


**2. Machine Learning**

To prepare our data for applying machine learning algorithms, an additional preprocessing step is required. Machine learning algorithms cannot directly operate on sentences or words, but instead require numerical data. In our dataset, the essays need to be transformed into a numeric representation before they can be used for training.

To achieve this, we utilize a technique called CountVectorizer. The CountVectorizer works by tokenizing a collection of text documents, splitting them into individual words or tokens, and then encoding each document as a vector. The resulting vector has a length equal to the entire vocabulary, with each element representing the count of a specific word in the document.

By applying the CountVectorizer, we convert our essays into a numeric form that can be processed by machine learning algorithms. Each essay is represented as a vector with a length equal to the vocabulary size, and the value of each element indicates the frequency of the corresponding word in the essay.

Initially, we applied machine learning algorithms such as linear regression, SVR (Support Vector Regression), and Random Forest to our dataset without incorporating the additional features mentioned in the preprocessing section. However, the results were not satisfactory, as the mean squared error (MSE) was relatively high for all three algorithms.

To address this, we included the extra features, applied the CountVectorizer once again on the modified dataset, and re-applied the same three algorithms. This time, there was a significant improvement in the performance of all three algorithms, particularly Random Forest, where the mean squared error decreased drastically.

For a more detailed implementation of this module, including the preprocessing steps and the application of machine learning algorithms, you can refer to the Python notebook titled "Essay_Scoring_1.ipynb". This notebook contains the necessary code and explanations to understand and replicate the implementation of our essay scoring model using machine learning algorithms.

 
 
 **3. Applying Neural Networks**
 
The preprocessing steps for neural networks in our essay scoring project differ from those used for traditional machine learning algorithms. In our approach, we utilize the Word2Vec algorithm, which is a shallow, two-layer neural network specifically designed to reconstruct linguistic contexts of words. This technique allows us to represent words as vectors in a high-dimensional space.

To begin the preprocessing, we start with a large corpus of words, typically from the training data. The Word2Vec algorithm takes this input and learns to assign each unique word in the corpus a corresponding vector in the vector space. The dimensions of this vector space are typically several hundred. The key characteristic of Word2Vec is that it positions word vectors in a way that words with similar contexts in the corpus are located close to each other in the vector space.

The Word2Vec model is computationally efficient and capable of learning word embeddings from raw text. In our project, we utilize the features extracted from Word2Vec as inputs to the LSTM (Long Short-Term Memory) layer. The LSTM is a type of recurrent neural network that can effectively capture and learn the importance of sequential data. In the context of essay scoring, the LSTM can learn which parts of the essay sequence are crucial for determining the score.

Finally, we employ a Dense layer with a single output unit to predict the score for each essay. This layer takes the learned representations from the LSTM and performs the final mapping to a predicted score value.

For a detailed implementation of this module, including the preprocessing steps and the architecture of the neural network, you can refer to the Python notebook titled "Automatic Essay Scoring with NN.ipynb". This notebook contains the necessary code and explanations to understand and replicate the implementation of our essay scoring model using neural networks.
![image](https://github.com/Satvik77/AEGS/assets/83899207/7fd05d80-42f4-41f3-8736-b704c56a8338)

 
 **4. Creation of web App**
 
After completing the training of our model, the next crucial step was to make our project accessible to users. To achieve this, we decided to develop a web application that would allow users to interact with our model effectively. To implement the web application, we utilized the Flask framework.

Flask is a widely used Python web framework that provides the necessary tools and functionality for developing web applications. By leveraging Flask, we were able to create an API (Application Programming Interface) that could receive essay details from users through a graphical user interface (GUI) and compute the predicted score based on our trained model.

Using the Flask framework, we established an API endpoint where users could send a POST request containing JSON inputs representing the essay details. The API then utilized our trained model to make predictions based on the provided information. The predicted score was returned to the user in JSON format, which could be easily accessed through the API endpoint.

This web application allowed users to conveniently input their essays, and with a simple request, receive the predicted score from our model. The Flask framework facilitated the communication between the user interface and the underlying model, making the process seamless and user-friendly.

By developing this web application, we aimed to make our model accessible to a wider audience and provide a user-friendly interface for scoring essays. The integration of Flask allowed us to leverage the power of our trained model and deliver accurate predictions to users in a convenient and efficient manner.


The essential of the webpage can be found in the folder, webapp. Screenshots of the webpage can be found in the following links:



 # STEP 1
![image](https://github.com/Satvik77/AEGS/assets/83899207/2bb52586-405f-4b80-b853-f54a23459a5d)

 
 # STEP 2
![image](https://github.com/Satvik77/AEGS/assets/83899207/36e8dbcb-e00c-4d59-b232-7a2a319b2d1f)


 # STEP 3
![image](https://github.com/Satvik77/AEGS/assets/83899207/521821bf-9118-40ab-b06b-a92f61209928)


 
 
 ## Conclusion

In conclusion, we have successfully developed a deep neural network model that demonstrates superior performance in essay scoring by effectively capturing both local and contextual information. By leveraging score-specific word embeddings and employing a recurrent neural network, our model surpasses existing state-of-the-art systems in this domain. Additionally, we have introduced a novel approach to explore and understand the internal scoring criteria of the network, making our models interpretable and capable of providing valuable feedback to the author.

Our most successful model utilized a 300-dimensional LSTM as initialization to the embedding layer, yielding impressive results. However, we believe that further improvement can be achieved by conducting a more extensive hyperparameter search with our LSTM-based models. Moreover, exploring ensemble methods to combine the strengths of multiple models is an avenue we plan to explore in the near future.

The outcomes of this project are encouraging and open up exciting possibilities for future research. By continuing to refine and optimize our models, we can enhance the accuracy and effectiveness of essay scoring systems. Furthermore, investigating alternative approaches and incorporating additional linguistic features could lead to even more robust and reliable performance.

Overall, this project contributes to the advancement of essay scoring methodologies and showcases the potential of deep neural networks in this field. With further exploration and refinement, we aim to make significant strides in automated essay evaluation, providing valuable insights and feedback to writers while maintaining a high level of interpretability and accuracy.

