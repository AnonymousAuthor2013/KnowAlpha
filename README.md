<!DOCTYPE html>
<html>
<body>
  <div id="readme" class="readme blob instapaper_body">
    <article class="markdown-body entry-content" itemprop="text"><h1><a id="user-content-improving-ir-based-bug-localization-with-context-aware-query-reformulation" class="anchor" aria-hidden="true" href="#improving-ir-based-bug-localization-with-context-aware-query-reformulation"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>The KnowAlpha: Automatically Finding Useful Information to Programmers through Semantic Understanding</h1>


<pre><code>
We shall give an insturction that will guide you to use the source code in this project to 
build KnowAlpha, and then deploy it in practice.
</code></pre>

    
<h3>
<a id="user-content-subject-systems-6" class="anchor" aria-hidden="true" href="#subject-systems-6"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
Instruction for building the KnowAlpha recommender system from source code and executing experiments
</h3>
<ul>
<li>Prepare system environment</li>
<li>Models</li>
<li>Data Pipeline</li>
<li>Build Models</li>
<li>Deploy System</li>
<li>Evaluation Results</li>
</ul>

<h3><a id="user-content-materials-included" class="anchor" aria-hidden="true" href="#materials-included"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
Prepare system environment
</h3>
<p><strong>Minimum configuration of machines</strong></p>

<ul>
<li><code>RAM:</code> 512G</li>
<li><code>CPU:</code> 56 logic cores</li>
<li><code>Disk:</code> 1TB+</li>
<li>GPU: 4X Tesla V100(32G X 4)</li>

</ul>
<p><strong>Install python environment</strong></p>
<p>We develop the whole system using python, so we recommend you to install an anaconda virtual python3.6 environment at: https://www.anaconda.com/
</p>

<p><strong>Install MongoDB Database</strong></p>
<p>
Install MongoDB database into your computer with a linux system, and configure db ip and port according to the instruction of https://www.mongodb.com/.
To enable, fast retrieval of those data, install an Elastic Search Engine according to the instruction of 
https://www.elastic.co/.
</p>

<p><strong>Required python packages</strong></p>
<ul>
<li><code>machine learning:</code>scikit-learn, tensorflow, openNMT,texar,pytorch,networkx,sumeval,summy,TextBlob,bert-as-service</li>
<li><code>data preprocessing:</code> pymongo, numpy, pandas</li>
</ul>

<p><strong>Project Check</strong></p>
<ul>
<li>Prepare Data</li>
<li>The mentioned neural network models are in ProgrammingAlpha/programmingalpha/models. </li>
<li>Run the scripts in ProgrammingAlpha/test/db_test/ folder to prepare training data. </li>
<li>Run the scripts in ProgrammingAlpha/test/retriver_test/ folder to build the model mentioned in KnowAlpha.</li>
</ul>


<h3><a id="user-content-available-operations" class="anchor" aria-hidden="true" href="#available-operations"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
Prepare Data
</h3>
<p>Download the data dump from archieve.org. 
Our training data from 4 online Q&A forums currently consists of Stack Overflow, Artificail Intelligence, Cross Validated and Data Science. 
</p>
<ul>
<li>
Build a MongoDB cluster and put all the data needed to the Database. Then deploy the elastic search engine on top of your database cluster.
</li>
<li>
Make the dirs listed in ProgrammingAlpha/programmingalpha/__init__.py.
</li>
</ul>

<h3><a id="user-content-required-parameters-for-the-operations" class="anchor" aria-hidden="true" href="#required-parameters-for-the-operations"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
Download the BERT Model
</h3>
<p><strong>
As the project is heavily based on several open released pretraining models, we at least need to prepare the BERT models according to
the instructions of https://github.com/google-research/bert (tensorflow version) and https://github.com/huggingface/pytorch-pretrained-BERT (pytorch version).
Store the pretrained model weight and auxiliary data of BERT model to the dirs BertBasePath or BertLargePath mentioned in ProgrammingAlpha/programmingalpha/__init__.py.
</strong></p>

<h3><a id="user-content-required-parameters-for-the-operations" class="anchor" aria-hidden="true" href="#required-parameters-for-the-operations"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
Prepare the training Data
</h3>

<p><strong>Data Analysis and Link Analysis</strong></p>
  <ul>
  <li>
  Run ProgrammingAlpha/test/associationAlg_test/seedSearchForTags.py to analyze the AI related tags and using association mining to find all required posts data.
  </li>
  <li>
  Run ProgrammingAlpha/test/graphLinke_test/build_link_path.py to build the posts link graph. If you have a spark cluster, you can boost the computaion space via running ProgrammingAlpha/test/graphLinke_test/spark-graph.py; or you can run ProgrammingAlpha/test/graphLinke_test/extract_link_semi_path.py to build an incomplete graph for quick test.
  </li>
  <li>
  Exract link distance posts pairs: run ProgrammingAlpha/test/graphLinke_test/build_label_pair.py to generate "link distance + posts ids(1+2)" data record, which is later used to generate inference task data.
  </li>
  </ul>


<p><strong>Training Data for KnowAlpha</strong></p>
  <ul>
  <li>
  Run ProgrammingAlpha/test/db_test/gen_corpus+_inference.py and push the generated corpus to mongodb cluster.
  </li>
  <li>
  Run ProgrammingAlpha/test/db_test/gen_samples.py with task parameter as 'inference' to sample training and validating data.
  </li>
  <li>
  Preprocess the generated samples by running ProgrammingAlpha/test/tokenizer_test/tokenize_corpus.py.
  </li>
  </ul>

<p><strong>Build Local Knowledge Base</strong></p>
  <ul>
  <li>
  Run ProgrammingAlpha/test/db_test/buildQAIndexer.py firstly to gather all answers to each question.
  </li>
  <li>
  Run ProgrammingAlpha/test/db_test/gen_kwnowledge_unit.py to generate knowledge unit data used by KnowAlpha.
  </li>
  <li>
  Push the knowledge units data to mongoDB cluster.
  </li>
  </ul>
  
<p><strong>After finished running all the above scripts, the system is ready for model training.</strong></p>

<h3><a id="user-content-q1-how-to-install-the-blizzard-tool" class="anchor" aria-hidden="true" href="#q1-how-to-install-the-blizzard-tool"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
Build Models
</h3>
<p><strong>Document Search Engine
</strong></p>
<ul>
<li>
The document search engine is in KnowAlpha/programmingalpha/retrievers/SearchEngine folder.
</li>
<li>
Follow the requirement.txt and see the run.py about how to use doc search engine.
</li>
</ul>

<p><strong>Build Knowledge Inference Model
</strong></p>
<ul>
<li>
Run ProgrammingAlpha/test/retriever_test/build_linkprediction_model.py to train the Knowledge Inference Net.
</li>
<li>
Other Inference Networks are available in https://github.com/asyml/texar/tree/master/examples/sentence_classifier and https://github.com/zhangzhenyu13/ATEC_NLP.
</li>
</ul>


<h3><a id="user-content-query-file-format" class="anchor" aria-hidden="true" href="#query-file-format"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
Evaluate the Model Performance
</h3>

<p><strong>Evaluate the KnowlAlpha</strong></p>
<ul>
<li>
Sample 2000 solved questions via runining "ProgrammingAlpha/test/db_test/gen_samples.py --maxSize 2000 --task inference" to generate the test samples. 
</li>
<li>
Run the ProgrammingAlpha/test/retriever_test/run_model.sh --do_eval to predict the link distance results directly, which is used to measure model performance on the test samples.
</li>
<li>
Run the ProgrammingAlpha/test/retriever_test/interactive.py with input stream re-directed to a file containing post ids of test samples, which is the evaluation of KnowAlpha.
</li>
<li>
1)Use the sklearn metrics toolkit to evaluate the model performance of Inference Net; 2) Refer to https://github.com/microsoft/recommenders for evaluation of the retrieved results of KnowAlpha. 
</li>
<li>
Other Inference Networks can be found and used in https://github.com/asyml/texar/tree/master/examples/sentence_classifier and https://github.com/zhangzhenyu13/ATEC_NLP.
</li>
</ul>
<p>..........................................................</p>
      
      


<h3><a id="user-content-please-cite-our-work-as" class="anchor" aria-hidden="true" href="#please-cite-our-work-as"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
Deploying The KnowAlpha System
</h3>

<p><strong>User Interface</strong></p>
<ul>
<li>
We currently implemented a  simple web page, which is available in https://github.com/zhangzhenyu13/ProgrammingAlpha/tree/master/alphaservices/AlphaWeb. 
And we also host a public service which consists of KnowAlpha and other services of our team.
Readers are recommended to visit http://www.i-cooper.net:10808/webServices/QApage. But keep in mind only the lines(in white background) under the blue block after you invoke the system(press the "ask XXX" button) is the return results of KnowAlpha.
The results are just a list of titles of the returned posts, and you can search them via Google or StackOverflow to access detailed description.
</li>
<li>
  To start the web page service:
  cd /path/to/repo/programmingalpha/alphaservices/AlphaWeb, then
just use the bash to run the start_server_web.sh.
</li>
<li>
To start the backend service:
  just use bash to run  /path/to/repo/test/servers_test.sh.
</li>
  <li>
    Make sure the service config files are set properly so that each service can be routed properly by the portal backend service. Those config files are contained in
    /path/to/repo/ConfigData
  </li>
  <li>
    After finishing above steps, you can access the service online: ip:port/webServices/alpha-QA, where ip and port are set via the config files.
    </li>
</ul>

<h3><a id="user-content-please-cite-our-work-as" class="anchor" aria-hidden="true" href="#please-cite-our-work-as"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
Please give a cite to our work if you want use the project somewhere else. 
</h3>


  </body>
</html>

