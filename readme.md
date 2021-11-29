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

## EMES-1 encoding CLI example: 

``` 
./x265 --input in_540p.y4m --preset veryslow --crf 24 --vbv-maxrate 2000 --vbv-bufsize 3000 --no-cutree --aq-mode 0 --mr-save 1 --mr-savefile test_1.dat -o test_540p_1.hevc --tune psnr
./x265 --input in_540p.y4m --preset veryslow --crf 34 --vbv-maxrate 500 --vbv-bufsize 750 --no-cutree --aq-mode 0 --mr-load 51 --mr-loadfile1 test_1.dat --mr-save 1 --mr-savefile test_2.dat -o test_540p_2.hevc --tune psnr
./x265 --input in_540p.y4m --preset veryslow --crf 26 --vbv-maxrate 1500 --vbv-bufsize 2250 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_540p_3.hevc --tune psnr
./x265 --input in_540p.y4m --preset veryslow --crf 29 --vbv-maxrate 1000 --vbv-bufsize 1500 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_540p_4.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 22 --vbv-maxrate 7000 --vbv-bufsize 10500 --no-cutree --aq-mode 0 --mr-load 5 --scale-factor1 2 --mr-loadfile1 test_1.dat --mr-save 1 --mr-savefile test_3.dat -o test_1080p_1.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 29 --vbv-maxrate 3000 --vbv-bufsize 4500 --no-cutree --aq-mode 0 --mr-load 51 --mr-loadfile1 test_3.dat --mr-save 1 --mr-savefile test_4.dat -o test_1080p_2.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 24 --vbv-maxrate 5800 --vbv-bufsize 8700 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_3.dat --mr-loadfile2 test_4.dat -o test_1080p_3.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 26 --vbv-maxrate 4500 --vbv-bufsize 6750 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_3.dat --mr-loadfile2 test_4.dat -o test_1080p_4.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 21 --vbv-maxrate 25000 --vbv-bufsize 37500 --no-cutree --aq-mode 0 --mr-load 5 --scale-factor1 2 --mr-loadfile1 test_3.dat --mr-save 1 --mr-savefile test_1.dat -o test_2160p_1.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 27 --vbv-maxrate 11600 --vbv-bufsize 17400 --no-cutree --aq-mode 0 --mr-load 51 --mr-loadfile1 test_1.dat --mr-save 1 --mr-savefile test_2.dat -o test_2160p_2.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 23 --vbv-maxrate 20000 --vbv-bufsize 30000 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_2160p_3.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 24 --vbv-maxrate 16800 --vbv-bufsize 25200 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_2160p_4.hevc --tune psnr
```

## EMES-2 encoding CLI example:

```
./x265 --input in_540p.y4m --preset veryslow --crf 24 --vbv-maxrate 2000 --vbv-bufsize 3000 --no-cutree --aq-mode 0 --mr-save 1 --mr-savefile test_1.dat -o test_540p_1.hevc --tune psnr
./x265 --input in_540p.y4m --preset veryslow --crf 34 --vbv-maxrate 500 --vbv-bufsize 750 --no-cutree --aq-mode 0 --mr-load 51 --mr-loadfile1 test_1.dat --mr-save 1 --mr-savefile test_2.dat -o test_540p_2.hevc --tune psnr
./x265 --input in_540p.y4m --preset veryslow --crf 26 --vbv-maxrate 1500 --vbv-bufsize 2250 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_540p_3.hevc --tune psnr
./x265 --input in_540p.y4m --preset veryslow --crf 29 --vbv-maxrate 1000 --vbv-bufsize 1500 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_540p_4.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 22 --vbv-maxrate 7000 --vbv-bufsize 10500 --no-cutree --aq-mode 0 --mr-load 5 --scale-factor1 2 --mr-loadfile1 test_2.dat --mr-save 1 --mr-savefile test_3.dat -o test_1080p_1.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 29 --vbv-maxrate 3000 --vbv-bufsize 4500 --no-cutree --aq-mode 0 --mr-load 57 --scale-factor2 2 --mr-loadfile1 test_3.dat --mr-loadfile2 test_2.dat --mr-save 1 --mr-savefile test_4.dat -o test_1080p_2.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 24 --vbv-maxrate 5800 --vbv-bufsize 8700 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_3.dat --mr-loadfile2 test_4.dat -o test_1080p_3.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 26 --vbv-maxrate 4500 --vbv-bufsize 6750 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_3.dat --mr-loadfile2 test_4.dat -o test_1080p_4.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 21 --vbv-maxrate 25000 --vbv-bufsize 37500 --no-cutree --aq-mode 0 --mr-load 5 --scale-factor1 2 --mr-loadfile1 test_4.dat --mr-save 1 --mr-savefile test_1.dat -o test_2160p_1.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 27 --vbv-maxrate 11600 --vbv-bufsize 17400 --no-cutree --aq-mode 0 --mr-load 57 --scale-factor2 2 --mr-loadfile1 test_1.dat --mr-loadfile2 test_4.dat --mr-save 1 --mr-savefile test_2.dat -o test_2160p_2.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 23 --vbv-maxrate 20000 --vbv-bufsize 30000 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_2160p_3.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 24 --vbv-maxrate 16800 --vbv-bufsize 25200 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_2160p_4.hevc --tune psnr
```

## EMES-3 encoding CLI example:

```
./x265 --input in_540p.y4m --preset veryslow --crf 24 --vbv-maxrate 2000 --vbv-bufsize 3000 --no-cutree --aq-mode 0 --mr-save 1 --mr-savefile test_1.dat --analysis-save test_sa_1.dat --analysis-save-reuse-level 10 -o test_540p_1.hevc --tune psnr
./x265 --input in_540p.y4m --preset veryslow --crf 34 --vbv-maxrate 500 --vbv-bufsize 750 --no-cutree --aq-mode 0 --mr-load 51 --mr-loadfile1 test_1.dat --mr-save 1 --mr-savefile test_2.dat -o test_540p_2.hevc --tune psnr
./x265 --input in_540p.y4m --preset veryslow --crf 26 --vbv-maxrate 1500 --vbv-bufsize 2250 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_540p_3.hevc --tune psnr
./x265 --input in_540p.y4m --preset veryslow --crf 29 --vbv-maxrate 1000 --vbv-bufsize 1500 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_540p_4.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 22 --vbv-maxrate 7000 --vbv-bufsize 10500 --no-cutree --aq-mode 0 --scale-factor 2 --analysis-load test_sa_1.dat --analysis-load-reuse-level 10 --refine-intra 4 --refine-inter 2 --refine-mv 1 --mr-save 1 --mr-savefile test_3.dat --analysis-save test_sa_2.dat --analysis-save-reuse-level 10 -o test_1080p_1.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 29 --vbv-maxrate 3000 --vbv-bufsize 4500 --no-cutree --aq-mode 0 --mr-load 51 --mr-loadfile1 test_3.dat --mr-save 1 --mr-savefile test_4.dat -o test_1080p_2.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 24 --vbv-maxrate 5800 --vbv-bufsize 8700 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_3.dat --mr-loadfile2 test_4.dat -o test_1080p_3.hevc --tune psnr
./x265 --input in_1080p.y4m --preset veryslow --crf 26 --vbv-maxrate 4500 --vbv-bufsize 6750 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_3.dat --mr-loadfile2 test_4.dat -o test_1080p_4.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 21 --vbv-maxrate 25000 --vbv-bufsize 37500 --no-cutree --aq-mode 0 --scale-factor 2 --analysis-load test_sa_2.dat --analysis-load-reuse-level 10 --refine-intra 4 --refine-inter 2 --refine-mv 1 --mr-save 1 --mr-savefile test_1.dat -o test_2160p_1.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 27 --vbv-maxrate 11600 --vbv-bufsize 17400 --no-cutree --aq-mode 0 --mr-load 51 --mr-loadfile1 test_1.dat --mr-save 1 --mr-savefile test_2.dat -o test_2160p_2.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 23 --vbv-maxrate 20000 --vbv-bufsize 30000 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_2160p_3.hevc --tune psnr
./x265 --input in_2160p.y4m --preset veryslow --crf 24 --vbv-maxrate 16800 --vbv-bufsize 25200 --no-cutree --aq-mode 0 --mr-load 57 --mr-loadfile1 test_1.dat --mr-loadfile2 test_2.dat -o test_2160p_4.hevc --tune psnr
```
