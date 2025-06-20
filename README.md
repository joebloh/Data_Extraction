1. **Training data extraction from pre-trained language models: a survey**  
   1. PLM (Pre-Trained Models)  
   2. Survey of data extraction from PLM  
   3. Unintentional memorization of training data  
      1. Memorization Type:  
         1. Verbatim  
            1. Eidetic  
            2. Differential Privacy  
            3. Counterfactual   
         2. Approximate   
      2. Model Inversion  
   4. Paper studies using autoregress language model architecture  
   5. Training Data Extraction  
      1. Candidate Generation  
      2. Membership Inference  
         1. Training Model  
         2. Adversarial Knowledge  
         3. Approach  
         4. Algo  
         5. Domain  
   6. Training Data Extraction Defenses  
      1. Preprocessing  
         1. Data Sanitization  
            1. Identify and Remove any text that conveys personal information  
         2. Data Deduplication  
            1. Data Dedup mitigates the memorization  
      2. Training  
         1. Differential Privacy  
            1. Data protection measure that is designed to ensure that providing data does not reveal much information about the user  
         2. Regularization  
            1. Well known approach for suppressing overfitting  
         3. Knowledge Distillation  
            1. The output of a larger model is used to train a smaller student model  
      3. Post Processing  
         1. Confidence Masking  
         2. Filtering  
   7. Larger Models Memorize More  
   8. Duplicate Strings are Memorized  
   9. Longer Prompts Extract More

2. **DP\_Froward: Fine tuning and inference on land models with diff privacy in forward pass**  
   1. Differential Private Stochastic gradient descent (DP-SGD) fail to cover threats like embedding inversion and sensitive attribute inference  
   2. Keywords and Concepts: Data Anonymization and sanitization. Privacy preserving protocols. Local Differential Privacy, NLP, Privacy-preserving Fine-tuning, Embedding matrix  
   3. Attacks:  
      1. Membership Inference Attacks  
         1. MIA predicts whether a data point is in the training set. They often exploit the disparity in model behavior between training set and unseen data, i.e, poor model generalization due to model overfitting  
      2. Embedding Inversion attack  
         1. Aims at recovering raw text as unordered tokens from embeddings  
      3. Sensitive Attribute Inference Attacks  
         1. Instead of recovering exact tokens, we try to infer sensitive attributes about target sequences  
   4. Pre-trained LM’s became pivotal in NLP. Alarmingly , fine-tuning corpora or inference-time inputs face various privacy attacks

3. **Effective Prompt Extraction from Language Models**   
   1. Text generation by LLM is commonly controlled by prompting, and these prompts are usually viewed as secret and/or proprietary. Sometimes even commodities to be traded or sold  
   2. 3 prompt sources, 11 underlying models and evaluate the feasibility to of prompt extraction attempts attacking a service API  
   3. Threat Model goal is to produce and accurate guess of the secret prompt by querying the service  
   4. LLM’s are prone to prompt extraction. For all 11 models over 50% of approximate prompts can be extracted, i.e, 90% of token in the majority of prompts are leaked  
   5. Prompt extraction attack is high-precision  
   6. More capability correlates with extractability  
   7. LLM services can be identified, it is possible to determine the exact model among several candidates with reasonable accuracy  
   8. Translation-based Prompt extraction 

4. **Demystifying RCE vulnerabilities in LLM integrated APPs**  
   1. RCE: Remote Code Execution  
   2. 20 Vulnerabilities in 11 LLM-integrated frameworks. 13 of with were given CVE ID’s  
   3. Frameworks(LangChain/LLamaIndex) for LLM apps exist as backend of functionality via API’s which could contain vulnerabilities (SQL inject by prompt injection) but more seriously RCE  
   4. LLMSmith employs static analysis technique to extract call chains from high level users API’s to hazardous functions  
   5. Contributions  
      1. An efficient and lightweight method for detecting RCE vulnerabilities in LLM-integrated frameworks  
      2. A prompt based exploitation method for LLM-integrated apps  
      3. The first systematic analysis of these new RCE exploit-vectors, vulnerabilities and practical attacks  
   6. Threat Model   
      1. For LLM-integrated apps built with vulnerable API, an attacker can remotely induce the LLM to generate malicious code through prompt attacks. When this untrusted code is executed by the vulnerable API, the attacker can RCE on the server of the app, executing arbitrary code , and even elevating privileges.  
   7. LLMSmith  
      1. Identify vulnerabilities in frameworks  
      2. Finding potential affected applications build on vulnerable frameworks  
      3. Validating and exploiting the vulnerabilities  
   8. White-box App collection   
   9. Black-box App collection  
   10. Strategies and Workflow   
       1. Base Usage Test  
          1. Is application live and functional  
       2. Hallucination Test  
          1. LLMSmith contains a small dataset with three questions about random hashes, base85 decoding, and complex math questions.  
          2. Once an app can answer at least two of the questions correctly, the test is passed  
       3. RCE Test Without Escape  
          1. Test aimed to induce the execution of certain system commands(env,id,echo)  
          2. If successful LLMSmith moves to network testing phase  
          3. If unsuccessful, the prompt seem to be too vanilla or encountering security checks and moves on to testing with escape  
       4. RCE Test With Escape  
          1. It will try two escape techniques  
             1. LLM escape  
                1. Tries to break prompt constraints or safety and moderation features using several prompt injection tactics and some light weight jailbreaking  
             2. Code escape   
                1. Tries to bypass potential predefined sandbox limitation inherent to the framework  
       5. Network Access Test  
          1. Is conducted to evaluate the exploitability level and caused hazards  
          2. LLMSmith introduces the curl command into the prompt that will send a request to the attacker and detection of incoming connection from a remote machine indicates the app's capacity to access external networks. If successful, advancing to the backdoor test.  
       6. Backdoor Test  
          1. Serves as the conclusive step focusing primarily on addressing the download and execution of backdoor scripts   
       7. Exploitability levels  
          1. SQL Injection  
          2. Limited RCE  
          3. Reverse Shell  
          4. Root

5. **ProPILE: Probing Privacy Leakage in Large Language Models**  
   1. Introduces ProPILE as a tool for Data Subjects to examine the possible leakage of Personal Identifiable Information (PII)  
   2. Experiments performed on OPT model and Pile dataset confirm the following  
      1. A significant amount of PII included in training can be disclosed through strategically crafted prompts  
      2. By prompt refining, model parameter access,and utilizing a few hundred data points, the degree of PII leakage can be significantly magnified  
   3. Sometimes referred to as data reconstruction or model inversion  
   4. Formulation of PII  
      1. Linkability  
         1.  A collection of seemingly unrelated information that when tied together can become identifiable   
      2. Structurality  
         1. PII that often occurs in a structured pattern (phone number, snn, zip code)   
      3. Unstructured   
         1. Doesn’t follow classical patterns  
   5. Threat Model  
      1. Goal to enable data subjects to probe LLM’s  
      2. Actors  
         1. Data subject \- have data in training sets  
         2. LLM providers \- who collect data for training models  
         3. LLM users \- Users who eventually have access to use LLM  
   6. Probing methods  
      1. Black-box  
      2. White-box  
   7. Quantifying PII leakage  
      1. String match  
      2. Likelihood matching

6. **Extracting Training Data from Large Language Models**  
   1. Demonstrate that an attack on GPT can extract hundreds of example (including PII, IRC conversation, code, and UUID’s)  
   2. Eidetic Memorization  
   3. Threat Model  
      1. Capabilities  
         1. Only has Input-output access to black-box  
      2. Objectives  
         1. To extract memorized training data  
      3. Target  
         1. GPT-2  
   4. Risks  
      1. Data Secrecy  
         1. Contextual Integrity  
   5. Attack  
      1. Generate Text  
         1. Generate Large quantity of of data by unconditionally sampling  
      2. Predict which output is memorized  
         1. By removing unlikely samples using membership inference  
   6. Initial Results  
      1. Generate 3 x 200k examples  
         1. Clear Memorization of things like MIT public Licence, Twitter Handles, Emails.  
         2. Contains a fair number of false positives  
   7. Improve Sample Strategy  
      1. Sampling with Decaying Temperature  
      2. Conditioning with Internet Text  
   8. Improve Membership Inference  
      1. Trivial Memorization and Repeated Substrings  
      2. Other Models  
      3. zlib Compression  
      4. Lowercase Text  
      5. Sliding Window  
   9. Final Methodology   
      1. Data Deduplication  
      2. Manual Inspection  
      3. Validate Against Training Data  
   10. Final Result   
       1. Identified 604 unique memorized training examples from among 1800 possible candidates. With aggregate true positive rate of 33%-67%  
   11. Categories  
       1. News, log files, terms of use, named items, Wiki, URL’s, named individuals, promotions, high entropy (UUID, base64), contact info, code, configuration files, numbers
