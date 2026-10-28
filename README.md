# Group 4 NLP Project
Members: Nalweyiso Racheal and Orishaba Jenipher

## App 1: Sentiment analyser
- Model: https://huggingface.co/Jenicoder/group4-sentiment-model
- Screenshots: Screenshot1.png, Screenshot2.png
- Test accuracy: 0.90
- Test F1: 0.90
- How to run the API:
  pip install -r requirements.txt
  uvicorn main:app --reload
- Example: send {"text": "Data science is not for the weak"} to /predict
  -> {"label": "POSITIVE", "score": 0.64}

## App 2: Document chatbot
- Screenshots: Screenshot3.png, Screenshot4.png
- Document used: Campus Hostel & Student Living Guidelines (hostel_guide.pdf)
- Test results:

| Question | Right page found? | Answer correct? | Invented anything? |
|---|---|---|---|
| 1. What are the visiting hours for guests in the hostel? | Yes (page 1) | Yes | No |
| 2. What electrical appliances are prohibited in hostel rooms? | Yes (page 2) | Yes | No |
| 3. What happens if a student misses an exam? | Yes (page 4) | Yes | No |
| 4. Who won the 2010 World Cup? | N/A | Yes (refused) | No |
| 5. What is the capital city of Australia? | N/A | Yes (refused) | No |

- What broke and how we fixed it:
  When calling the LLM through Hugging Face, we got a 402 error saying our account had no remaining credits. We fixed this by running an open-source instruction model directly on our Colab T4 GPU, which let us test the RAG chatbot without needing API credits.

## Our model vs the LLM
We would use our fine-tuned DistilBERT model when we need very fast predictions, lower server costs, or when the system needs to work offline without an internet connection. The LLM is better when we want to handle general questions or extract data without having to label thousands of training examples first, but it is slower and uses much more memory.

## Limitations
- Our sentiment model was trained on English movie reviews, so it can make mistakes on sarcasm, local slang, or mixed Luganda and English sentences.
- The document chatbot only knows what is written inside our uploaded hostel rules PDF and will say it does not know if asked about anything else.

## Who did what
- Member A (Orishaba Jenipher): Trained the DistilBERT model in Colab, uploaded the model weights and tokenizer to Hugging Face, and filled in the model card.
- Member B (Nalweyiso Racheal): Built the Gradio and FastAPI apps, handled the PDF text chunking and embeddings, tested the chatbot, and managed the GitHub repository.
