# **Project: Text Summarization Model**

**Overview:**

This project leverages advanced deep learning techniques to develop a robust text summarization model capable of generating concise summaries from lengthy articles. The model is trained on the PubMed Summarization dataset, utilizing an LSTM-based encoder-decoder architecture. Additionally, a pre-trained GPT-2 model is employed for comparative analysis, enhancing the model's performance evaluation. The project includes comprehensive tools for data preparation, model training, and evaluation, as well as deployment of the summarization model. To ensure the quality of generated summaries, ROUGE metrics are used to assess and refine the model's output. This project offers a full pipeline from data processing to model deployment, providing an effective solution for automated text summarization tasks.

**Input:**

Example of the PubMed Dataset:

|                        Article                    |                   Abstract                           |
|---------------------------------------------------|------------------------------------------------------|
|A recent systematic analysis showed that in 2011, 314 (296 - 331) million children younger than....|background : the present study was carried out to assess the effects of community nutrition...|

URL: [https://huggingface.co/datasets/ccdv/pubmed-summarization]
Format: Parquet

**Functions:**
1. **clean_and_preprocess_text:** It performs several text-processing tasks such as converting numbers to words, removing unnecessary elements (like HTML tags and URLs), normalizing the text (lowercasing, removing punctuation), and optionally filtering out stopwords based on the input parameter num.
2. **decode_sequence:** transforms a predicted sequence of token probabilities into a readable text summary by selecting the most probable token for each position, converting these tokens into words using a provided dictionary (index_to_word), and excluding any padding tokens.
3. **calculate_accuracy:** It compares predicted and actual summaries by comparing tokens. It splits summaries into individual tokens, counts tokens in the actual summaries, and calculates accuracy. If empty, accuracy is set to 0.
4. **baseline_sum:** It extracts the first three sentences from an input text using sentence tokenization, resulting in a concise summary that serves as a baseline for comparison with more advanced summarization methods.

**Outputs:**

Example:
|                  Original Article              |                   Generated Summary               |        ROUGE-1            |         ROUGE-2         |        ROUGE-L        |   
|------------------------------------------------|---------------------------------------------------|---------------------------|-------------------------|-----------------------|
|eligible participants one thousand eight hundred|small urms characteristics small of the of of small....|        0.084507           |         0.0             |          0.070422     |
                      
As you can see:
- ROUGE-1 focuses on the recall of individual important words.
- ROUGE-2 goes a step further by evaluating how well the model captures essential phrases and maintains word order.
- ROUGE-L considers the overall structure, ensuring the generated summary maintains coherence with the reference summary.

By using all three metrics, you get a comprehensive evaluation of the model's performance across different aspects of text summarization: relevance, coherence, and structure. This helps in understanding where the model excels and where it might need improvement.

**Results for First 500 Records:**
|             Models          |        ROUGE-1            |       ROUGE-2           |      ROUGE-L          |   
|-----------------------------|---------------------------|-------------------------|-----------------------|
|              GPT-2          |          0.2017           |        0.0204           |         0.1096        |
|              BiLSTM         |          0.1465           |        0.0096           |         0.1237        |
