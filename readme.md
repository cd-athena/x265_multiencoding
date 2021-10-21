# ===========x265 HEVC Encoder===========


| **Read:** | Online `documentation <http://x265.readthedocs.org/en/default/>`_ | Developer `wiki <http://bitbucket.org/multicoreware/x265/wiki/>`_

x265 is an open source HEVC encoder. See the developer wiki for instructions for
downloading and building the source. x265 is free to use under the `GNU GPL
<http://www.gnu.org/licenses/gpl-2.0.html>`_ and is also available under a commercial `license <http://x265.org>`_ 

## Multi-encoding CLI: 

| CLI option    | input type     | description   |
| :---          |     :---:      |      :---     | 
|--mr-save      | `<integer>`    |  to signal that the analysis data is to be saved in a file.|
|--mr-savefile  | `<filename>`   |to input the filename to save analysis data.|
|--mr-load      | `<integer>`    |to signal that the analysis data is to be re-used from a file/files.|
|--mr-loadfile1 | `<filename>`   |to input the file to load analysis data.|
|--mr-loadfile2 | `<filename>`   |to input the second file (if any) to load analysis data.|
|--scale-factor1| `<integer>`    |to indicate the scaling factor of the first load data.|
|--scale-factor2| `<integer>`    |to indicate the scaling factor of the second load data.|

## mr-load options:
| input         | description     | 
| :---          |     :---        | 
|<1>            | Enable multi-rate/ resolution optimization for I frames|
|<2>            |Enable upper single bound for CU depth estimation|
|<4>            |Enable lower single bound for CU depth estimation|
|<8>            |Enable double bound for CU depth estimation|
|<16>           |Enable the proposed PU heuristics|
|<32>           |Enable the proposed ME optimization|

## EMES-1 template: 

#### 540p encodings 

``` 
./x265 --input in_540p.y4m --crf 24 --mr-save 1 --mr-savefile test1.dat -o test1.hevc
./x265 --input in_540p.y4m --crf 34 --mr-load 50 --mr-loadfile1 test1.dat --mr-save 1 --mr-savefile test2.dat -o test1.hevc
./x265 --input in_540p.y4m --crf 26 --mr-load 56 --mr-loadfile1 test1.dat --mr-loadfile2 test2.dat -o test1.hevc 
```

#### 1080p encodings 
```
./x265 --input in_1080p.y4m --crf 22 --mr-load 5 --mr-loadfile1 test1.dat --scale-factor1 2 --mr-save 1 --mr-savefile test2.dat -o test1.hevc
./x265 --input in_1080p.y4m --crf 29 --mr-load 51 --mr-loadfile1 test2.dat --mr-save 1 --mr-savefile test3.dat -o test1.hevc
./x265 --input in_1080p.y4m --crf 24 --mr-load 57 --mr-loadfile1 test2.dat --mr-loadfile2 test3.dat -o test1.hevc
```
#### 2160p encodings 
```
./x265 --input in_2160p.y4m --crf 21 --mr-load 5 --mr-loadfile1 test2.dat --scale-factor1 2 --mr-save 1 --mr-savefile test3.dat -o test1.hevc
./x265 --input in_2160p.y4m --crf 27 --mr-load 51 --mr-loadfile1 test3.dat --mr-save 1 --mr-savefile test4.dat -o test1.hevc
./x265 --input in_2160p.y4m --crf 23 --mr-load 57 --mr-loadfile1 test3.dat --mr-loadfile2 test4.dat -o test1.hevc
```

## EMES-2 template:

#### 540p encodings 
```
./x265 --input in_540p.y4m --crf 24 --mr-save 1 --mr-savefile test1.dat -o test1.hevc
./x265 --input in_540p.y4m --crf 34 --mr-load 50 --mr-loadfile1 test1.dat --mr-save 1 --mr-savefile test2.dat -o test1.hevc
./x265 --input in_540p.y4m --crf 26 --mr-load 56 --mr-loadfile1 test1.dat --mr-loadfile2 test2.dat -o test1.hevc
```

#### 1080p encodings 
```
./x265 --input in_1080p.y4m --preset veryslow --crf 22 --mr-load 5 --scale-factor1 2 --mr-loadfile1 test2.dat --mr-save 1 --mr-savefile test3.dat -o test1.hevc
./x265 --input in_1080p.y4m --preset veryslow --crf 29 --mr-load 57 --scale-factor2 2 --mr-loadfile1 test3.dat --mr-loadfile2 test2.dat --mr-save 1 --mr-savefile test4.dat -o test1.hevc
./x265 --input in_1080p.y4m --preset veryslow --crf 24 --mr-load 57 --mr-loadfile1 test3.dat --mr-loadfile2 test4.dat -o test1.hevc
```

#### 2160p encodings 
```
./x265 --input in_2160p.y4m --preset veryslow --crf 21 --mr-load 5 --scale-factor1 2 --mr-loadfile1 test4.dat --mr-save 1 --mr-savefile test1.dat -o test1.hevc
./x265 --input in_2160p.y4m --preset veryslow --crf 27 --mr-load 57 --scale-factor2 2 --mr-loadfile1 test1.dat --mr-loadfile2 test4.dat --mr-save 1 --mr-savefile test2.dat -o test1.hevc
./x265 --input in_2160p.y4m --preset veryslow --crf 23 --mr-load 57 --mr-loadfile1 test1.dat --mr-loadfile2 test2.dat -o test1.hevc
```
## EMES-3 template:

#### 540p encodings 
```
./x265 --input in_540p.y4m --crf 24 --mr-save 1 --mr-savefile test1.dat -o test1.hevc
./x265 --input in_540p.y4m --crf 34 --mr-load 50 --mr-loadfile1 test1.dat --mr-save 1 --mr-savefile test2.dat -o test1.hevc
./x265 --input in_540p.y4m --crf 26 --mr-load 56 --mr-loadfile1 test1.dat --mr-loadfile2 test2.dat -o test1.hevc
```
#### 1080p encodings 
```
./x265 --input in_1080p.y4m --crf 22 --analysis-load test1.dat --analysis-load-reuse-level 10 --scale-factor 2 --refine-intra 4 --refine-inter 2 --refine-mv 1 --mr-save 1 --mr-savefile test2.dat -o test1.hevc
./x265 --input in_1080p.y4m --crf 29 --mr-load 51 --mr-loadfile1 test2.dat --mr-save 1 --mr-savefile test3.dat -o test1.hevc
./x265 --input in_1080p.y4m --crf 24 --mr-load 57 --mr-loadfile1 test2.dat --mr-loadfile2 test3.dat -o test1.hevc
```
#### 2160p encodings 
```
./x265 --input in_2160p.y4m --crf 21 --analysis-load test2.dat --analysis-load-reuse-level 10 --scale-factor 2 --refine-intra 4 --refine-inter 2 --refine-mv 1 --mr-save 1 --mr-savefile test3.dat -o test1.hevc
./x265 --input in_2160p.y4m --crf 27 --mr-load 51 --mr-loadfile1 test3.dat --mr-save 1 --mr-savefile test4.dat -o test1.hevc
./x265 --input in_2160p.y4m --crf 23 --mr-load 57 --mr-loadfile1 test3.dat --mr-loadfile2 test4.dat -o test1.hevc
```
