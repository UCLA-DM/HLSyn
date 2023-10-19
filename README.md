# Towards a Comprehensive Benchmark for FPGA Targeted High-Level Synthesis

## Description

High-level synthesis (HLS) aims to raise the abstraction layer in hardware design, enabling the design of domain-specific accelerators (DSAs) like field-programmable gate arrays (FPGAs) using C/C++ instead of hardware description languages (HDLs). Compiler directives in the form of pragmas play a crucial role in modifying the microarchitecture within the HLS framework. However, the space of possible microarchitectures grows exponentially with the number of pragmas. Moreover, the evaluation of each candidate design using the HLS tool consumes significant time, ranging from minutes to hours, leading to a time-consuming optimization process. To accelerate this process, machine learning models have been used to predict design quality in milliseconds. However, existing open-source datasets for training such models are limited in terms of design complexity and available optimizations. In this paper, we present HLSyn, the first benchmark that addresses these limitations. It contains more complex programs with a wider range of optimization pragmas, making it a comprehensive dataset for training and evaluating design quality prediction models. The HLSyn benchmark consists of 42 unique programs/kernels, resulting in over 42,000 labeled designs. We conduct an extensive comparison of state-of-the-art baselines to assess their effectiveness in predicting design quality. As an ongoing project, we anticipate expanding the HLSyn benchmark in terms of both quantity and variety of programs to further support the development of this field.

## Citation

If you use the dataset in your work, please cite our paper.
```
@article{chang2023dr,
  title={Towards a Comprehensive Benchmark for FPGA Targeted High-Level Synthesis},
  author={Yunsheng Bai, Atefeh Sohrabizadeh, Zongyue Qin, Ziniu Hu, Yizhou Sun, and Jason Cong},
  journal={NeurIPS},
  year={2023}
}
```

## Data

`data/HLSyn\_data.tar.gz` is the data stored in .json, .gexf, and .c format.

In addition, the format used by our baseline code can be downloaded from [here](https://zenodo.org/records/8034115) 

The two format has same contents. And the former one is more readable.

## Data Content and Format

The source code and pragma-augmented programl graph representation of each kernel is stored in the `.c` and `.gexf` file under `sources` and `graphs` folders, respectively. 

Notice that in the source code and graph, the value of praga parameters is are variables. To get specific values for them and the corresponding prediction labels under those values, you need to load the json file under the `design/v18` (13,729 data points) and `design/v20` (27,867 data points) folders, which contain design data points under different version of HLS tools. 

In the `design/v18` and `design/v20` folders, each json file is a dictionary where the key is the specific parameters of a design and the value is the corresponding prediction labels. 

The value of each design data point contains the following fields:

- `points`: the dictionary stores the specific values for each pragma parameter.
- `valid`: if the design is a valid design. Notice that if for a design point `valid=False` but `perf != 0`, it can still be used for regression task.
- `perf`: value of the performance target
- `res\_util`: a dictionary of values for the resource utilization targets

An example of the design data point is shown below

```
      "__PARA__L0-8.__PARA__L1-8.__PARA__L2-2.__PARA__L3-4.__PARA__L4-32.__PARA__L5-1.__PIPE__L0-NA.__PIPE__L1-off.__PIPE__L2-NA.__PIPE__L3-flatten.__TILE__L0-1.__TILE__L1-1.__TILE__L2-1.__TILE__L3-1": {
            "perf": 1070661.0,
            "point": {
                  "__PARA__L0": 8,
                  "__PARA__L1": 8,
                  "__PARA__L2": 2,
                  "__PARA__L3": 4,
                  "__PARA__L4": 32,
                  "__PARA__L5": 1,
                  "__PIPE__L0": "",
                  "__PIPE__L1": "off",
                  "__PIPE__L2": "",
                  "__PIPE__L3": "flatten",
                  "__TILE__L0": 1,
                  "__TILE__L1": 1,
                  "__TILE__L2": 1,
                  "__TILE__L3": 1
            },
            "res_util": {
                  "util-BRAM": 0.29,
                  "util-DSP": 3.42,
                  "util-LUT": 1.72,
                  "util-FF": 1.37,
                  "total-BRAM": 1292.0,
                  "total-DSP": 23403.0,
                  "total-LUT": 2042745.0,
                  "total-FF": 3258281.0
            },
            "valid": false
      }
```


## Leaderboard

Coming soon


## Running Baselines

Check instructions [here](https://github.com/ZongyueQin/HLSyn/tree/main/baselines) 

## License

[CC BY-SA 4.0 license](https://creativecommons.org/licenses/by-sa/4.0/legalcode)

## Acknowledgement

This work was partially supported by NSF 2211557, NSF 1937599, NSF 2119643, NSF 2303037, NASA, SRC JUMP 2.0 Center, Okawa Foundation, Amazon Research, Cisco, Picsart, Snapchat, and CDSC industrial partners ( https://cdsc.ucla.edu/partners/). We would also like to thank Marci Baun for editing the paper.
