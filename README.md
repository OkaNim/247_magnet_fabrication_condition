# A third-level heading
This site includes the scripts using in our manuscript.<br>
If it is necessarty to run the scripts, please download the zip and run according to the below descriptions.
<br>
<br>
The Python libraries written in requirements.txt in /src are necessary to run.<br>
<br>

## How to run the extractor using LLM
It is necessary to do the following two in advance.


(1) Download the model of "gemma-2-9b-it" from the Huggin Face website.
https://huggingface.co/google/gemma-2-9b-it <br>
(Log-in and authentification are neccesarry.) 


(2) Write the model path in your computer in line 10 of 247_01_extract_data_llm_250513.py.

![alt text](image-4.png)
<br>

After these, the _text.txt files (the plain text extracted from PDF of US patents) in /data/text are copied to /run and then hit the following command at /src (GPUs are necessary to run fast):
```
python 247_01_extract_data_llm_250513.py
```

All _text.txt files in /run are sequentially processed and  the output files (_output_llm.json and _output_llm.txt) are saved in /run.<br>
(The files outputted by us are in /data/output_llm.)<br>
* _output_llm.json includes the raw output from the LLM.<br>
* _output_llm.txt is the file edited the contents of _output_llm.json to evaluate the extraction. In the edition, the inappropriate outputs, e.g. numbers are not included in the value, are eliminated. Since the file format is TSV,  a spreadsheet software such as Excel is convenient to check.<br>
<br>
## How to run our extractor
It is necessary to do the following two in advance.


(1) Download the model of "matscibert" from the Huggin Face website.
https://huggingface.co/m3rg-iitd/matscibert<br>


(2) Write the model path in your computer in line 14 of 247_02_extract_data_our-extarctor_250516.py.

![alt text](image-5.png)

The _text.txt files in /data/text are copied to /run and then  hit the following command at /src (only CPU is enough):
```
python 247_02_extract_data_our-extarctor_250516.py
```
All _text.txt files in /run are sequentially processed and the output files (_output_our-extractor.txt) are saved in /run.<br>
(The files outputted by us are in /data/output_our-extractor.)<br>
* Since the file format is TSV, a spreadsheet software such as Excel is convenient to check.<br>
<br>
## How to evaluate the extractions
In the evaluation, _output_llm.txt, _output_our-extractor.txt, and the correct answer files put in /data/output_ca are used.<br>
All of _output_llm.txt and _output_our-extractor.txt are put in /data/output_llm and /data/output_our-extractor, respectively, and then hit the command at /src:
```
python 247_03_evaluate_250516.py output_llm
```
and
```
python 247_03_evaluate_250516.py output_our-extractor
```
The result files (evaluation_output_llm.txt and evaluation_output_our-extractor.txt) are saved in /data/evaluation_results.<br>
* The minor differences in expression between the outputs and the correct answers are ignored using correct-expressions.txt in /src/supplement.
* Since the file format is TSV, a spreadsheet software such as Excel is convenient to check.<br>
