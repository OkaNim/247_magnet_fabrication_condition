# Scripts for our study
This website includes the scripts used in our study.<br>
If it is necessarty to run the scripts, please download the zip and run according to the below description.<br>
<br>
The scripts were created by Python 3 and can be run on Linux OS.<br>
The Python libraries including Anaconda and written in requirements.txt in /src are necessary to run them.<br>
<br>
## How to run the script for data extraction by LLM (Gemma 2)
The following two settings are necessary in advance.<br>
<br>
(1) Download the model of "gemma-2-9b-it" (all files in the folder) from the Huggin Face website.<br>
https://huggingface.co/google/gemma-2-9b-it<br>
(Log-in and authentification etc. are neccesarry.)<br>
<br>
(2) Write the model path (the path to the folder including the downloaded files) in your computer in line 10 of 247_01_extract_data_llm_250513.py.<br>
![image](https://github.com/user-attachments/assets/a606819a-277a-4232-9cd9-18c07300a0dd)<br>
<br>
<br>
After the settings, the _text.txt files (the plain text extracted from PDF of US patents) in /data/text are moved or copied to /run and then hit the following command at /src (GPUs are necessary to run fast):
```
python 247_01_extract_data_llm_250513.py
```
All _text.txt files in /run are sequentially processed and the output files (_output_llm.json and _output_llm.txt) are saved in /run.<br>
(The files outputted previously by us are in /data/output_llm.)<br>
* _output_llm.json includes the raw output from the LLM.<br>
* _output_llm.txt is the file edited the contents of _output_llm.json to evaluate the extraction.<br>
In the edition, the inappropriate outputs, e.g. numbers are not included in a value, are eliminated.
* Since the file format for _text.txt and _output_llm.txt is TSV, a spreadsheet software such as Excel is convenient to check.
## How to run our extractor
The following two settings are necessary in advance.<br>
<br>
(1) Download the model of "matscibert" (all files in the folder) from the Huggin Face website.<br>
https://huggingface.co/m3rg-iitd/matscibert<br>
<br>
(2) Write the model path (the path to the folder including the downloaded files) in your computer in line 14 of 247_02_extract_data_our-extarctor_250516.py.<br>
![image](https://github.com/user-attachments/assets/fad8d16b-e9e7-4506-b2a6-fc06a3f4d286)<br>
<br>
<br>
After the settings, the _text.txt files (the plain text extracted from PDF of US patents) in /data/text are moved or copied to /run and then hit the following command at /src (only CPU is used):
```
python 247_02_extract_data_our-extarctor_250516.py
```
All _text.txt files in /run are sequentially processed and the output files (_output_our-extractor.txt) are saved in /run.<br>
(The files outputted previously by us are in /data/output_our-extractor.)<br>
* Since the file format for _text.txt and _output_our-extractor.txt is TSV, a spreadsheet software such as Excel is convenient to check.
## How to run the script to evaluate the above extractions
In the evaluation, _output_llm.txt, _output_our-extractor.txt, and the correct answer files in /data/output_ca are used.<br>
<br>
Put all _output_llm.txt and _output_our-extractor.txt files in /data/output_llm and /data/output_our-extractor, respectively, and then hit the command at /src:
```
python 247_03_evaluate_250529.py output_llm
```
and
```
python 247_03_evaluate_250529.py output_our-extractor
```
The result files (evaluation_output_llm.txt and evaluation_output_our-extractor.txt) are saved in /data/evaluation_results.<br>
* The minor differences in expression between the outputs and the correct answers are ignored using correct-expressions.txt in /src/supplement.<br>
* Since the file format is TSV, a spreadsheet software such as Excel is convenient to check.<br>
