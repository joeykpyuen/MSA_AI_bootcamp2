### Problem:
Nowadays writing and publishing texts online is very simple. Anyone can publish anything online from social media, product reviews, blogs, online novels to academic articles. However, many students or general people like me struggle to not write in abbreviations or write in an informal manner when needed as we are so used to typing on our smart devices or computer. Formal style is used often in writing and business situations and with those with whom we do not have close relationships.

### Solution:
Hence, to resolve this problem, a text suggestion AI solution can be done. 

This service can either be similar to text prediction in which text predictions help users write more efficiently by predicting text quickly and accurately. With this service, it will start from the basics where it eliminates all the user's frequent use of words that are been categorised in these certain fields: **abbreviations, swear words, contraction of words, slang, the figure of speech and broken syntax**. 

Or it can be done as a web app that is suggesting change of vocbulary for the text the user upload or typed in the editor interface. (like grammarly but check for formality).

This is part of an AI solution as it predicts and suggests text based on the user's choices in the past.

### How
Azure AI - Microsoft Editor is like a personal intelligent writing assistant available across other Microsoft services. The editor is built with Azure Machine Learning showing that by using Azure services and Azure ML, I will be able to build a model that predicts what I should use next but without informal words, with the help of Azure Text Analytic.

### Approach
Ideally, it will be using deep learning where it requires user testing and feedback (user accepting or declining the suggestion). But what this solution should start is with the approach of classifying text - whether it is formal or informal. Then use Natural Language Processing (NLP) to produce the word prediction which I can use the (Azure Suggestion API)[https://docs.microsoft.com/en-us/rest/api/searchservice/suggestions] for assistance. 

#### Data Phase
However, as a basic model, the approach would be to train the NLP model using data collected. Fortunately, text data can now be found in many areas hence, an example of the dataset would be [kaggle link](https://www.kaggle.com/aksharagadwe/abbreviations-and-slangs-for-text-preprocessing) which is a dataset of abbreviations and slangs for text preprocessing. Hence, I can train the model to know a type of informal writing. However, manually collecting datasets would make the result better such as collecting informal sentences from social media such as Twitter [kaggle (optional)](https://www.kaggle.com/mmmarchetti/tweets-dataset) and rewrite it to formal sentences so there can be a comparison of informal and formal writing. (Initially, finding scholarly articles is a good approach, however, there will be no comparison data)

### Model Phase
Once data is collected, I can start training the model. 
* Training model = giving it a lot of **source** sentences _i.e. informal setences_ along with **target** sentence _i.e. formal setences_ 
* As a first approach, it may be better to use the NLP model but to advance the model, it is possible to train using phrase-based models(PBMT) or even Neural machine translation (NMT) to learn to break sentences into smaller units and understand the underlying meaning of sentences. Which will not restrict to individual vocabs. 
* Along with training own model, opensource Text Classification API or [Azure Text Analytics](https://azure.microsoft.com/en-au/services/cognitive-services/text-analytics/) can be used to assist with the overall program.
* This is where the user feedback can come in: Show the user suggestion of vocabs that can be used, if the user finds the suggestion not formal enough, it will not accept the suggestion hence, the AI solution will learn from and know which vocab is more formal or informal. (Even when most informal been eliminated)

#### Method
* Decision tree - fast and tend to perform well with large datasets
    * E.G. 
    * Recall - informal = TP/ TP + FN
    * Recall - formal = TN / TN + FP
    * Precision - informal = TP / TP + FP
    * Precision - fprma; = TN / TN + FN
* Text classification - categories unstructured text 
    * keyword extraction - eliminate informal texts (use Azure Text Analytic as assistance)
    * classifies the informal word list and in first approach any non informal is formal text and formal text will be split further in the future.

### Deployment phase
As mentioned the final product of this should be suggesting the user formal text. Thus there are two ways this can be integrated, once the model has been trained and tested.
1. When a text has been put into the editor of the program (the AI solution user interface will have an editor), it will act like Grammarly but rather than checking grammar, it will check any informal vocabularies been used and suggest the formal word of that. It can be a contraction such as *can't* too *cannot* or an abbreviation such as *lemme* to *let me*. Swear words and other inappropriate words will be suggested to remove them. As for slang it will be either suggested to remove or change to another use of the word. 
2. It can be integrated into keyboards and act like auto-completion on a smart device's keyboard. It will however not show suggestions of words that you typed but rather the thesaurus of the word you typed. (however, this is a more advanced solution and will be hard to complete in short term)

The solution can be built by using the Azure Power App with Microsoft Text Analytic and open-source text classification to reduce the time for development. 

### Possible Approach (and Future scalability and extensibility): 
* Create own dataset by quantifying the formality of individual lexical terms and assigning each word a score of how formal the lexicon is in between the range of -1 to 1. 
    * There will be two lists: one formal and one informal. - test set for evaluation
    * Using the data collected (dataset of informal (i.e. social media post VS scholar articles) that represent both styles (formal and informal) and evaluate their lexicon using relative formality judgement between word pairs.
* Currently the first attempt is to identify informal text hence, the next phase would be a more detailed classification among the formal text.
* Next modelling phase to advance the model is as mentioned before, NMT and PBMT model as it will allow more detailed prediction.
* This does not need to limit to just informal and formal but to a more specific style such as academic, published text, medical, business etc. There is more than one situation for one needing to write in a formal style.
    * If wanted, it can change from suggesting text to formal to informal. In which the target user can be the older generation wanting to communicate with their younger family members.
