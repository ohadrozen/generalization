# Challenge Datasets for Testing Models' Generalization Capacity
These are the datasets we used for our experiments as described in our [paper](https://arxiv.org/pdf/1910.09302.pdf).

## Dative Alternation Datasets

### Syntactic Complexity Dimension  
3 datasets: Simple_dataset, Medium_dataset, Complex_dataset

For variance along the syntactic complexity dimension (see Section 3.5), we generate 3 different datasets – one for each syntactic complexity level: *simple*, *medium* and *complex*. To test generalization across this dimension, we fine-tune the model on one of those datasets and test on the other two. For example, to test how a model generalize from *simple* to *medium* and *complex* syntactic complexity, we train the model on the *simple* dataset and test it on the *medium* and *complex*. 
To test performance without changing the complexity level (e.g. from *simple* to *simple*), we simply split the dataset in focus into training and test sets, making sure not to include the same templates in both sets.

#### Datasets structure
Each dataset contains a collection of files, each consists of examples generated using our templating method (see Section 3.3) from premises of the relevant complexity level. So, for instance, the *simple* dataset is simply the collection of examples listed in the files in the Simple_dataset directory, all generated from templates derived from simple premises. The filenames are of the form Dt_S[i]_[verb], while S represents the simple complexity level and [verb] is the dative verb in the template. For example, the *simple* dataset for Dative Alternation is the set of examples appear in the directory Simple_dataset with the files {Dt_S0_bring.txt, … Dt_S9_write.txt}.

#### File structure
Each subset file consists of examples derived from a template generated from one extracted premise (see Section 3.2). Note that each premise template has a few hypotheses templates, and each such hypothesis generates a few dozens of examples. For example, the subset file Dt_S3_offer.txt has the following premise template:  
**Premise**: *\*you\* \*would\* offer \*him\* \*a fight\*?*  
And three hypotheses templates with matching labels:  
**Hypothesis 0**: *\*you\* \*would\* offer \*a fight\* to \*him\*?*  
Label: Entailment  
**Hypothesis 1**: *\*you\* \*would\* offer \*a fight\**?  
Label: Entailment  
**Hypothesis 2**: *\*you\* \*would\* offer \*him\*?*  
Label: Contradiction  

For the ease of reading the template, instead of ARG<sub>i</sub>, the arguments are marked with their original instantiations bounded by *, so in the example above, instead of writing the premise template ARG0 ARG1 *offer* ARG2 ARG3, we use \*you\* as ARG0, \*would\* as ARG1 and so on.
Commented lines are marked with # at the beginning of the line.
The different instantiations of the arguments are detailed in the commented lines below the template lines. 
Each hypothesis template is followed by examples automatically generated from it. In the commented line above each example you can find the instantiations used to create the example

### Lexical Dimension
6 datasets: Simple_lex1, Simple_lex2, Simple_lex2b, Complex_lex1, Complex_lex2, Complex_lex2b

For variance along the lexical dimension (see Section 3.5) we only used half of the templates of Dative Alternation (Dt_S5_… - Dt_S9_…, Dt_M6_… - Dt_M8_…, and Dt_C3_… - Dt_C8_…). As explained in that section, to create from a subset S two additional subsets S<sub>Lex1</sub> and S<sub>Lex2</sub> with similar syntax (yet with different words), we instantiated different arguments into the same original template. We repeat this process for the *complex* dataset.

Let’s take as an example the template we used to generate the examples in Dt_S6_give.txt:  
**Extracted Premise** (from MultiNLI): *[You] [can] give [me] [milk and spinach].*  
**Premise Template**: *ARG1 ARG2 give ARG3 ARG4.*  
**Hypothesis Template** (Ent. #1): *ARG1 ARG2 give ARG4 to ARG3.*  
**Hypothesis Template** (Ent. #2): *ARG1 ARG2 give ARG4.*  
**Hypothesis Template** (Cont.): *ARG1 ARG2 give ARG3.*  

ARG1 has the following instantiations:  
Inst1 = *You*  
Inst2 = *The waiter*  
Inst3 = *He*  
Inst4 = *The chef*  
Inst5 = *Our mom*  
Inst6 = *The doctor*  
Inst7 = *The grocer*  

To generate the subset Dt_S6_give_1.txt we used the same templates for both the premise and hypotheses, but instantiated only Inst1 to Inst4. To generate Dt_S6_give_2.txt, we only used Inst5 to Inst7. We split in the same way the instantiations for arguments ARG2, ARG3 and ARG4. To generate Dt_S6_give_2**b**.txt, we used Inst5 to Inst7 again, but this time we replaced the main dative verb give with the dative verb pass. The examples in Dt_S6_give_1.txt and Dt_S6_give_2b.txt has now examples with similar syntax, different dative verb, and they never share the same instantiation for a specific argument.
To test generalization across the lexical dimension, we fine-tune the model on a Lex1 dataset from a certain complexity level, and test it on a Lex2’ (different verb) dataset from the same complexity level. For example, to test how a model generalize over different dative verbs while maintaining similar syntactic structure for the *complex* complexity level, we train the model on the Complex_lex1 dataset and test it on Complex_lex2b dataset that contains examples derived from the same templates, but with different instantiations, and using unseen (in fine-tuning) dative verbs.

 
## Numerical Reasoning

Datasets for the Numerical Reasoning phenomenon were generated similarly to the Dative Alternation case, with a few differences detailed below.

### Syntactic Complexity Dimension
3 datasets: Simple_dataset, Medium_dataset, Complex_dataset

For variance along the syntactic complexity dimension, we again generate 3 different datasets – one for each syntactic complexity level: *simple*, *medium* and *complex*

#### Datasets structure
Filenames are of the form Nr_S[i], while in this case S represents the *simple* complexity level. For example, the *simple* dataset for Numerical Reasoning is the set of examples appear in the directory Simple_dataset with the files {Nr_S0.txt, … Nr_S8.txt}.

#### File structure
Same as in Dative Alternation, but with multiple templates in each file, where all templates of the same file derived from the same extracted premise and differ only in the relation expressions Relp    {more than, less than, ∅} (see Section 3.4 and Table 1 row 9).

### Lexical Dimension
12 datasets, *simple* and *complex* datasets for 6 different number ranges.  
Number ranges: 30-50, 60-80, 100-199, 200-299, 400-499, 1k-10k

As explained in Section 4.3, for variation across the lexical dimension, we instantiate different number ranges into NUM<sub>p</sub> (see Table 1 row 9), also appears in the dataset files as <_num_>.
Like in the Dative Alternation case, to create additional datasets (S<sub>Lex1</sub> and S<sub>Lex2</sub>) with similar syntax (yet with different words) from the *simple* dataset (Numerical Reasoning), we again instantiated different arguments into the same original template.  We repeat this process for the *complex* dataset.
For number ranges 30-50 and 100-199 we created both Lex1 and Lex2 datasets, and only lex2 for the rest of the ranges. 
To test generalization across the number range (lexical) dimension, we fine-tune the model on a Lex1 dataset from a certain complexity level and a certain number range, and test it on a Lex2 dataset of the same complexity level but with a different number range. For example, to test how a model generalize from range 30-50 to range 1k-10k for syntactically *simple* examples, we train the model on the Simple_lex1_R30-50 dataset and test it on Simple_lex2_R1k-10k dataset that contains examples derived from the same templates, but with different instantiations, using different number instantiations. To test, for example, how a model performs with similar settings but on the same number range, we simply fine-tune the model on Simple_lex1_R30-50 (or R100-199) and test it on Simple_lex2_R30-50 (or R100-199, respectively).

We hope to add to this collection of datasets a broader range of inference types and data dimensions soon.



Please feel free to contact ohadrozen@gmail.com for any questions.

## License
Copyright 2019, Bar Ilan University

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
