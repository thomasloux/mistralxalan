# GoldoRag Team: Hackathon Mistral x Alan
Team: Maxime Moutet, Gaëtan Narozniak, Thomas Loux.

The challenge is a medical Multiple Choice Question! The dataset is composed of 103 questions with 5 possible choices, without correct answers provided.

We made a clever knowledge retrieval to find information in a fast and explanable way, leveraging RAG for few-shot prompting and using a plain foundation model (Mistral Large). Please find our presentation for details about the implementation.

## Our approaches

### Theme identification is easy
We use Mistral to identify main themes, that in our context, are often complex medical terms. Actually, they are often quite rare, have a precise and single definition (compare to complex polysemic words) for instance "hematopoiesis". We then use several sources online (wikipedia, medicine dictionary...) to retrieve pages and texts providing valuable information about the medical terms. We extracted main themes in each question and choices.

### Information retrieval
We search the question's theme's pages for themes from the choices. The idea is that simple regex search is enough to determine chunks of valuable information.

### Few-shot prompting
Using RAG on MedQA, we extracted similar examples from the famous MedQA dataset. The encoder is Mistral-embed and we use FAISS for vector search. 

### LLM processing
We then provided the LLM the question, choices, information retrieved and few examples and ask Mistral Large to provide an explanation and list of correct answers.

## Results
We obtain a 41% accuracy, starting from a naive LLM answering of 25%. As a comparison, the best score reached is 48%.

## If we had more time!
We would have finetuned Mistral Large on MedQA, increase our knowledge database for few-shot examples and knowledge retrieval, and prompt engineer to optimize the results.



