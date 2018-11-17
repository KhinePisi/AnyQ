AnyQ
AnyQ (ANswer Your Questions) The open source project mainly includes a question and answer system framework for the FAQ collection and a text semantic matching tool SimNet.

The Q&A system framework adopts a configuration and plug-in design. Each function is added through a plug-in form. Currently, 20+ plug-ins are open. Developers can use the AnyQ system to quickly build and customize FAQ Q&A systems for specific business scenarios and accelerate iterations and upgrades.

SimNet is a semantic matching framework independently developed by Baidu Natural Language Processing Department in 2013. The framework is widely used in Baidu's products, including core network structures such as BOW, CNN, RNN, and MM-DNN, and is also integrated based on the framework. The mainstream semantic matching models in the academic world, such as MatchPyramid, MV-LSTM, K-NRM and other models. SimNet is implemented using PaddleFluid and Tensorflow for easy model extension. The model built using SimNet can be easily added to the AnyQ system to enhance the semantic matching ability of the AnyQ system.
(English)

Detailed introduction
FAQ question and answer system framework
The AnyQ system framework is mainly composed of Question Analysis, Retrieval, Matching, Re-Rank, etc. The functions contained in the framework are added by plug-in form, such as Chinese word in Analysis, inverted index in Retrieval, semantic index, Matching The Jaccard feature and SimNet semantic matching feature currently open 20+ plugins. The configuration and plug-in design of the AnyQ system helps developers quickly build and quickly customize the FAQ question and answer system for specific business scenarios, speeding up iterations and upgrades. The framework of AnyQ is as follows:
Configuration
The AnyQ system integrates a number of plug-ins for retrieval and matching, which are effective through configuration; for example, plug-ins in the search and text matching similarity calculations:

Search method (Retrieval)
Inverted index: based on open source inverted index Solr, join Baidu open source participle
Semantic retrieval: based on SimNet semantic representation, using ANNOY for ANN retrieval
Manual intervention: Control output by providing precise answers
Matching calculation (Matching)
Literal matching similarity: Calculate literal matching features after processing Chinese words
Cosine similarity
Jaccard similarity
BM25
Semantic matching similarity
SimNet Semantic Matching: Modeling the semantics of the problem using semantically matching models trained by the SimNet architecture
Pluginization
In addition to the framework, all the functions of AnyQ are added through the plug-in form. User-defined plug-ins can be easily added to the AnyQ system, and only need to implement the corresponding interface, such as custom dictionary loading, Question analysis method, retrieval method, Match similarity, sorting, etc., and truly implement customizable and plug-in.

Text semantic matching framework SimNet
SimNet is a semantic matching framework independently developed by Baidu Natural Language Processing Department in 2013. The framework is widely used in Baidu's products, including core network structures such as BOW, CNN, RNN, and MM-DNN, and is also integrated based on the framework. The mainstream semantic matching models in the academic world, such as MatchPyramid, MV-LSTM, K-NRM and other models. SimNet is implemented using PaddleFluid and Tensorflow for easy model extension. Models built using SimNet can be easily added to the AnyQ system to enhance the semantic matching capabilities of the AnyQ system.

According to the text semantic matching network structure, the network model implemented in SimNet can be mainly divided into the following two categories:

Representation-based Models
Such as: BOW, CNN, RNN (LSTM, GRNN)
Features: The text is matched at both ends of the task input, respectively, and then expressed, and then the fusion calculation is performed;

Interaction-based Models
Such as: MatchPyramid, MV-LSTM, K-NRM, MM-DNN
Features: After obtaining the sequence representation of the text word level, the similarity matching matrix is calculated according to the two sequence representations, and the matching information at each position is merged to give the final similarity score;

SimNet is implemented using PaddleFluid and Tensorflow. For more documentation, please refer to: SimNet PaddleFluid SimNet TensorFlow Semantic model based on massive search data Based on Baidu's massive search data, we trained a SimNet-BOW semantic matching model. In some real FAQ question and answer scenarios, the model's effect is more than 5% higher than the literal-based similarity method AUC. The model usage and acquisition methods refer to the Demo.

Code compilation
Linux
Cmake 3.0 or above (recommended version 3.2.2), g++ >=4.8.2, bison >=3.0

Mkdir build && cd build && cmake .. && make
Others
For MacOS, Windows and other environments, it is recommended to use docker mode.

# paddle official image
Docker pull paddlepaddle/paddle:latest-dev
# paddle domestic mirror
Docker pull docker.paddlepaddlehub.com/paddle:latest-dev
Demo
Build index, configuration

# Get anyq custom solr, anyq example configuration
Cp ../tools/anyq_deps.sh .
Sh anyq_deps.sh

#Start solr, rely on python-json, jdk>=1.8
Cp ../tools/solr -rp solr_script
Sh solr_script/anyq_solr.sh solr_script/sample_docs

HTTP-Server
./run_server

#Request example:
Http:${host}:${port}/anyq?question=XXX

Lib
./demo_anyq sample_input_json
More documentation
Detailed explanation of AnyQ configuration
How to add plugins to AnyQ
AnyQ uses semantic indexing
How to contribute
You can customize the plugin for specific functions under the AnyQ framework. Tutorial refers to how AnyX adds plugins.
If you feel that your customized plugin function is versatile & beautiful, please feel free to submit us PR.

