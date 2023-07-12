# Flan-T5-inference-optimisation

# BenchMark Env:
    Ubuntu 20.04.5 LTS \n \l  
    GPU 0: NVIDIA GeForce GTX 1080 Ti   

    nvcc: NVIDIA (R) Cuda compiler driver  
    Copyright (c) 2005-2021 NVIDIA Corporation  
    Built on Mon_Sep_13_19:13:29_PDT_2021  
    Cuda compilation tools, release 11.5, V11.5.50  
    Build cuda_11.5.r11.5/compiler.30411180_0  
    Python 3.9.16  
    ii  cudnn-local-repo-ubuntu2004-8.3.2.44                        1.0-1                                      amd64        cudnn-local repository configuration files  
    ii  libcudnn8                                                   8.3.2.44-1+cuda11.5                        amd64        cuDNN runtime libraries  
    ii  libcudnn8-dev                                               8.3.2.44-1+cuda11.5                        amd64        cuDNN development libraries and headers  
    ii  libcudnn8-samples                                           8.3.2.44-1+cuda11.5                        amd64        cuDNN samples  

# Versions:
    1. Name: optimum  Version: 1.9.1.dev0   
    2. Name: torch  Version: 2.0.1+cu118  
    3. Name: transformers Version: 4.29.2
    4. Name: protobuf Version: 4.23.1

Comparesd results on 1080 ti and T4 Tesla :https://understood-casquette-cdf.notion.site/results-94e3e9f59e9d4fa8926ee13755bc2c88?pvs=4

# Results
# original
### output  MAX len → 1024
**1. For Flan-T5 large: orignal (CPU) :**

        seq_len:  8 time:  0.7163788008689881
        seq_len: 32 time: 0.7263164758682251
        seq_len: 128 time: 0.727803738117218
        seq_len: 512 time: 0.7193972730636596

**2. For Flan-T5 large: original (GPU)**

        seq_len:  8 time:  0.10314885377883912
        seq_len: 32 time: 0.10179906606674194
        seq_len: 128 time: 0.11348598957061767
        seq_len: 512 time: 0.17275093793869017
        seq_len: 1024 time: 0.29372969150543216

### output  MAX len → 5  
**1. For Flan-T5 large: orignal (CPU) :**

        seq_len: 8 time: 0.4637493824958801  
        seq_len: 32 time: 0.4152503275871277  
        seq_len: 128 time: 0.41513345956802367  
        seq_len: 512 time: 0.4186572504043579  
        seq_len: 1024 time: 0.4186951422691345  

**2. For Flan-T5 large: orignal: (GPU)** 

        seq_len:  8 time:  0.09575546979904175
        seq_len: 32 time: 0.09438462972640992
        seq_len: 128 time: 0.10955139875411987
        seq_len: 512 time: 0.16158395528793335
        seq_len: 1024 time: 0.27651875734329223

# Onnx
### output  MAX len → 1024  
**1. For Flan-T5 large: onnx (CPU):**  

        seq_len:  8 time:  0.5394865775108337  
        seq_len: 32 time: 0.5388318037986756  
        seq_len: 128 time: 0.5383210611343384  
        seq_len: 512 time: 0.538268404006958  
        seq_len: 1024 time: 0.5396303057670593  
        
### output  MAX len → 5  
**For Flan-T5 large: onnx (CPU):**  

      seq_len:  8 time:  0.30158501625061035  
      seq_len: 32 time: 0.30127585649490357  
      seq_len: 128 time: 0.30130538940429685  
      seq_len: 512 time: 0.3012810492515564  
      seq_len: 1024 time: 0.30131051540374754  

# ONNX + Tensorrt
### output  MAX len → 5  
**For FlanT5 large: onnx - tensorRt**

    seq_len:  8 time:  1st - iter: 237.54 ,  rest: 0.06368    
    seq_len: 32 time:  1st - iter: 147.87 ,  rest: 0.07280   
    seq_len: 128 time: 1st - iter:148.3674 ,  rest: 0.1131  
    seq_len: 512 time: 1st - iter: 155.785 ,  rest: 0.2668  
    seq_len: 1024 time: 1st -iter: 165.788,   rest: 0.4750   

# CTranslate2
    1. C2 translate(cpu)  

        seq_len: 8 time: 0.6379863619804382  
        seq_len: 32 time: 1.165667852342340   

    2. Ctranslate2(gpu)  

        seq_len: 8 time: 0.06818238019943237  
        seq_len: 32 time: 0.2116452622413635  
        seq_len: 128 time: 2.117751100063324  
        seq_len: 512 time: 2.260249288082123  
Comparesd results on 1080 ti and T4 Tesla :https://understood-casquette-cdf.notion.site/results-94e3e9f59e9d4fa8926ee13755bc2c88?pvs=4
