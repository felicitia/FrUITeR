* ToC
{:toc}

## FrUITeR's Automated Workflow

<img src="figs/workflow.png" >  


## Artifact Dolownload

FrUITeR's artifacts consist of eight different repositories as follows. Their descriptions can be found in the rest of this website.

**Repo #1.** [EventExtractor.zip](repos/EventExtractor.zip)

**Repo #2.** [TestAnalyzer.zip](repos/TestAnalyzer.zip)

**Repo #3.** [AppFlowGUIMapper.zip](repos/AppFlowGUIMapper.zip)

**Repo #4.** [ATMGUIMapper.zip](repos/ATMGUIMapper.zip)

**Repo #5.** [GTMGUIMapper.zip](repos/GTMGUIMapper.zip)

**Repo #6.** [GUIMaps.zip](repos/GUIMaps.zip)

**Repo #7.** [TestBenchmark.zip](https://drive.google.com/file/d/1rCxkBW4-Hl1cBS3BenjbXqLIVSGkK4Dl/view?usp=sharing)

**Repo #8.** [DataAnalysis.zip](repos/DataAnalysis.zip)


## FrUITeR's Components and Baseline

FrUITeR has three components (shaded boxes in the workflow), and two baseline techniques Naïve and Perfect.

### Components

**Event Extractor** is
implemented in Java using [Soot framework](https://github.com/Sable/soot) (235 SLOC).

`Location:` Repo #1 `EventExtractor/src/`

**Fidelity Evaluator** and **Utility Evaluator** are implemented in Python (1,045 SLOC). 

`Location:` Repo #2 `TestAnalyzer/gui_mapper/result_generator.ipynb`; `TestAnalyzer/gui_mapper/process_final_results.ipynb`

### Baseline

FrUITeR’s baseline techniques **Naïve** and **Perfect** are implemented in Python (112 SLOC). 

`Location:` Repo #2 `TestAnalyzer/gui_mapper/baseline/`



## Modularization of Existing Techniques

To modularize existing techniques, we (1) extracted their [GUI Mappers](#extracted-gui-mappers), and (2) unified their [GUI Maps and Transferred Tests](#unified-gui-maps-and-transferred-tests).

### Extracted GUI Mappers

The GUI Mapper components extracted from existing techniques are implemented in their original programing languages. 

**AppFlow's GUI Mapper** is implemented in Python. (1,084 SLOC). 

`Location:` Repo #3 `AppFlowGUIMapper/elements.py`

**ATM's GUI Mapper** is in Java (1,314 SLOC). 

`Location:` Repo #4 `ATMGUIMapper/src/`

**GTM's GUI Mapper** is implemented in Java (1,409 SLOC).

`Location:` Repo #5 `GTMGUIMapper/src/`

As explained in the paper (Section 5.1), we did not implement **CraftDroid's GUI Mapper**, but can only interpret its published artifacts [[link]](https://sites.google.com/view/craftdroid/); that functionality is implemented in Python (86 SLOC). 

`Location:` Repo #2 `TestAnalyzer/gui_mapper/craftdroid/`


### Unified GUI Maps and Transferred Tests

The functionality that processes the GUI Mappers' outputs and generates the uniform representation of *GUI Maps* and *Transferred Tests* (recall FrUITeR's workflow) is implemented in Python (404 SLOC). 

`Location:` Repo #2 `TestAnalyzer/gui_mapper/{technique_name}`  
*Note: GTM reused `TestAnalyzer/gui_mapper/atm`*

The processed **GUI Maps** and **Transferred Tests** are stored as `.csv` files.

`Location:` Repo #6 `GUIMaps/{technique_name}`

## FrUITeR's Benchmark

1. Benchmark Apps are located in Repo #7 `TestBenchmark/subjects/`
2. Benchmark Tests are located in Repo #7 `TestBenchmark/src/`
3. Benchmark *Canonical Maps* are located in Repo #2 `TestAnalyzer/gui_mapper/ground_truth_mapping/`

## FrUITeR's Final Datasets

Final Datasets are located in Repo #8 `DataAnalysis/FSE2020-dataset.RData`

If you are unable to view `.RData` file, the same final datasets are exported as two `.csv` files.
1. Repo #8 `DataAnalysis/final_2381.csv` contains the data of the 2,381 cases
2. Repo #8 `DataAnalysis/final_12.csv` contains the data of the 12 cases

### Header Description

|     Header Name    | Description                                                                                 |
|:------------------:|---------------------------------------------------------------------------------------------|
|       `source`       | source app                                                                                  |
|       `target`       | target app                                                                                  |
|       `method`       | test case being transferred                                                                 |
|     `gui_mapper`     | the GUI Mapper used to transfer the test                                                    |
|     `src_events`     | source events in the source test                                                            |
|    `trans_events`    | transferred events in the transferred test                                                  |
|      `gt_events`     | ground-truth events in the ground-truth test                                                |
|       `num_src`      | the number of source events                                                                 |
|      `num_trans`     | the number of transferred events                                                            |
|       `num_gt`       | the number of ground-truth events                                                           |
|       `correct`      | the set of *correct* events                                                                 |
|      `incorrect`     | the set of *incorrect* events                                                               |
|       `missed`       | the set of *missed* events                                                                  |
|      `nonExist`      | the set of *nonExist* events                                                                |
|     `num_correct`    | the number of the *correct* events                                                          |
|    `num_incorrect`   | the number of the *incorrect* events                                                        |
|     `num_missed`     | the number of the *missed* events                                                           |
|    `num_nonExist`    | the number of the *nonExist* events                                                         |
|   `percent_correct`  | FrUITeR's fidelity metric: the percentage of the *correct* events                           |
|  `percent_incorrect` | FrUITeR's fidelity metric: the percentage of the *incorrect* events                         |
|   `percent_missed`   | FrUITeR's fidelity metric: the percentage of the *missed* events                            |
|  `percent_nonExist`  | FrUITeR's fidelity metric: the percentage of the *nonExist* events                          |
| `accuracy_precision` | FrUITeR's fidelity metric: the value of the *precision*                                     |
|   `accuracy_recall`  | FrUITeR's fidelity metric: the value of the *recall*                                        |
|      `accuracy`      | FrUITeR's fidelity metric: the value of the *accuracy*                                      |
|      `distance`      | FrUITeR's utility metric: *effort* needed to correct the transferred test                   |
|      `reduction`     | FrUITeR's utility metric: manual effort *reduction* compared to writing the test from scratch |


## FrUITeR's Data Analyses

The data analyses that interpret our final datasets are written in R (585 SLOC).

`Location:` Repo #8 `DataAnalysis/scripts/`
