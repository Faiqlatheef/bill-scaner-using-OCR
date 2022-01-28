Preprocessing
Since the receipt is not in greyscale but there’s not a lot of noise, I’m only going to do thresholding by applying a threshold of 210. We can tweak the value to get the right output. Too less and you will miss out on a lot. Too close to 255 will make everything black.
We’ll need to install OpenCV first.
 
Figure 2: install OpenCV
Here’s the code for implement the libraries.
 
Figure 3: code for implement the libraries
Here’s the code for thresholding.
 
Figure 4: code for thresholding
This is what the output of thresholding looks like.
 
Figure 5: Output of thresholding.
Text Detection
For text detection I will be using an open-source library called Tesseract. It’s the definitive OCR library and has been developed by Google since 2006. The latest release of Tesseract (v4) supports deep learning-based OCR that is significantly more accurate. The underlying OCR engine itself utilizes a Long Short-Term Memory (LSTM) network.
First let’s install the latest version of Tesseract.
 
Figure 6: install the latest version of Tesseract
Now that we’ve installed Tesseract let’s start detecting the text boxes. Tesseract has in built functionality to detect text boxes.
 
Figure 7: detecting the text boxes

Here’s the output of the text detection code.
 
Figure 8: output of the text detection code
Text Recognition
We will Tesseract to perform OCR. Tesseract 4 uses a deep learning approach that performs significantly better than most other open-source implementations.
Here’s the code of text recognition. Although it is a very simple one-liner, there’s a lot that goes under the hood.
 
Figure 9: Text Recognition



Here’s the formatted output of Text Recognition
 
Figure 10: formatted output of Text Recognition






Information Extraction
As I’ve mentioned before the most common way of extracting information is by a rule-based approach.
All receipts from this hotel will follow a fixed structure and the information appears on different lines. This is reflected in the OCR output where newlines are represented by ‘\n’. Using these let’s write a set of rules to extract information. This set of rules can be applied to any receipt from this hotel since they’ll follow the same format.
I will be extracting the Restaurant name, the items bought, their quantity, total costs per item and the total amount using simple python commands and regular expressions.

This is a dictionary where I’ll be storing the extracted information.
 
Figure 11: This is a dictionary
The first step is to extract the Restaurant name. The location of the restaurant name is going to be constant in all receipts and that is in the first 2 lines. Let’s use this to create a rule.
 
Figure 12: extract the Restaurant name






Next, we extract all information related to the items and cost.
The items contain the line of “X”. Let's detect all occurrences of price. Now we can detect lines by recognizing the characters between 2 \n and containing a “X”.
 
Figure 13:  get lines with price
 
Figure 14: get items, total
 
Figure 15: Get Name, quantity and cost
I stored the results is the dictionary like below
 
Figure 16: Store the results in the dict
The code for the final output of json file
 
Figure 17: Show the results in the json file
Final output
 
Figure 18: Final output

Challenges which I faced
1.	Install and implement the pytesseract – because I have to download the application and install by the application and again, I want pip install tesseract in cmd also.
2.	text detection with output and convert it into text – I need to show the path of tesseract folder for these two processes.
3.	Long image – because of the long image tesseract didn’t recognize all the text. That’s why I can’t able to add other items and prices and exact total.
4.	Detecting “X” line for food and cost price and total – tesseract didn’t detect the “X” properly because some lines it detect as “x” and also “*” that’s why I can’t able to add the all items and prices and exact total.
