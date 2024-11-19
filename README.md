# Meesho-ML-Challenge

## Embedding Generation [CLIP-emp.ipynb, vit-emb.ipynb]:
Models used: VIT and CLIP

Vit embeddings: original image embeddings no transformation  
Vit embeddings: Black and white image embedding  
Clip embeddings: Cropped in by 10 percent from each side   
Clip embeddings: Original Image with increase in hue,brightness ,saturation, contrast
Clip embeddings: Original Image with reduced  hue,brightness ,saturation, contrast

### Note (Why 5 embeddings): 
To increase metric score of the model slightly  
For actual business consideration only 1 or 2 embeddings combination should suffice  
As Meesho will provide this service for free, VIT model should be prefered (15-20 MIN KAGGLE GPU - 1 Lakh images)

## Data Preprocessing [meesho-pre-process.ipynb, meesho-pre-process]:
For Sarees category specifically  
To fill null values of train data with most frequent values of same saree  
Used product Id code to group same sarees  
Used Easy ocr to get text from image Data  

## Potential Issue:
Altough this Image text was just use to handle Null values  
Data leakage will still be present in the image embeddings which will be used for final predictions  

### Note (Data leakage)
For acutal business use we need to remove this text product id from images  
The metric score is not relevant for Saree Category in actual business sense  

## Final training and Inference [lgbm-meesho.ipynb]
This code uses all the previous generated embeddings merged together along with pre processed data   
The attributes values are labeled as numbers  
### Note
A better method would be to use Label encoder, i wanted to experiment with regression models too,so used attribute dictionary  

Trained seperate lgbm models for each category and each attribute seperatly [ reduced training time by 1/4 due to less possible choices to choose from]  
Ran a lgbm model to get most important features and drop others  
then used 5 stratified k fold strategy to get model scores and combined predictions  
  
Converted the labels back to categorical values


### Conclusion
Very brief approach  
Embeddings -> Boosting model (LGBM)-> result  

### Note from programmer
Sorry for the bad documentation and the code  
Would try to edit both the code and documenation to make it more readable, but a bit busy right no  
Feel free to ask me if you require anything


