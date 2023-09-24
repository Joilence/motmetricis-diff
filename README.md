# MOT Metric Inconsistency

This repo trys to compute multi-object tracking metrics computed by [py-motmetric](https://github.com/cheind/py-motmetrics) and [TrackEval](https://github.com/JonathonLuiten/TrackEval).

Ground truth comes from [MOT17](https://motchallenge.net/data/MOT17/), tracking result comes from [ByteTrack](https://motchallenge.net/method/MOT=4809&chl=10). Three sequences from train set are selected to test.

## Run

Get output from [py-motmetric](https://github.com/cheind/py-motmetrics) following documentation [here](https://github.com/cheind/py-motmetrics#motchallenge-compatibility):

``` shell
python -m motmetrics.apps.eval_motchallenge data/gt/mot_challenge/MOT17/MOT17-train/ data/trackers/mot_challenge/MOT17/MOT17-train/BYTE_Pub/data
```

<details>
<summary>Expected Output</summary>

```shell
04:34:05 INFO - Found 3 groundtruths and 3 test files.
04:34:05 INFO - Available LAP solvers ['scipy']
04:34:05 INFO - Default LAP solver 'scipy'
04:34:05 INFO - Loading files.
04:34:05 INFO - Comparing MOT17-13-FRCNN...
04:34:06 INFO - Comparing MOT17-02-DPM...
04:34:07 INFO - Comparing MOT17-09-SDP...
04:34:07 INFO - Running metrics
04:34:07 INFO - partials: 0.168 seconds.
04:34:07 INFO - mergeOverall: 0.169 seconds.
                IDF1   IDP   IDR  Rcll  Prcn  GT MT PT ML  FP    FN IDs   FM  MOTA  MOTP IDt IDa IDm
MOT17-13-FRCNN 70.6% 82.7% 61.5% 73.1% 98.3% 110 58 28 24 147  3133  17   37 71.7% 0.162  37   6  27
MOT17-02-DPM   52.3% 73.1% 40.8% 54.4% 97.7%  62 21 21 20 238  8467  56  134 52.8% 0.142  62   8  17
MOT17-09-SDP   69.2% 75.0% 64.2% 84.0% 98.2%  26 18  7  1  83   850  24   49 82.0% 0.135  26   3   6
OVERALL        61.4% 77.0% 51.1% 65.0% 98.0% 198 97 56 45 468 12450  97  220 63.4% 0.148 125  17  50
04:34:07 INFO - Completed
```
  
</details>

Get output from [TrackEval](https://github.com/JonathonLuiten/TrackEval) following scripts [here](https://github.com/JonathonLuiten/TrackEval/blob/master/scripts/run_mot_challenge.py):

```shell
$ python run_mot_challenge.py \
  --GT_FOLDER data/gt/mot_challenge/MOT17 \
  --TRACKERS_FOLDER data/trackers/mot_challenge/MOT17 \
  --SPLIT_TO_EVAL train \
  --USE_PARALLEL False \
  --METRICS Hota \
  --TRACKERS_TO_EVAL BYTE_Pub \
  --BENCHMARK MOT17 \
  --METRICS HOTA CLEAR Identity
```

<details>
<summary>Expected Output</summary>

```shell
Eval Config:
USE_PARALLEL         : False
NUM_PARALLEL_CORES   : 8
BREAK_ON_ERROR       : True
RETURN_ON_ERROR      : False
LOG_ON_ERROR         : /opt/homebrew/Caskroom/miniforge/base/envs/mm-diff/lib/python3.8/site-packages/error_log.txt
PRINT_RESULTS        : True
PRINT_ONLY_COMBINED  : False
PRINT_CONFIG         : True
TIME_PROGRESS        : True
DISPLAY_LESS_PROGRESS : False
OUTPUT_SUMMARY       : True
OUTPUT_EMPTY_CLASSES : True
OUTPUT_DETAILED      : True
PLOT_CURVES          : True

MotChallenge2DBox Config:
PRINT_CONFIG         : True
GT_FOLDER            : data/gt/mot_challenge/MOT17
TRACKERS_FOLDER      : data/trackers/mot_challenge/MOT17
OUTPUT_FOLDER        : None
TRACKERS_TO_EVAL     : ['BYTE_Pub']
CLASSES_TO_EVAL      : ['pedestrian']
BENCHMARK            : MOT17
SPLIT_TO_EVAL        : train
INPUT_AS_ZIP         : False
DO_PREPROC           : True
TRACKER_SUB_FOLDER   : data
OUTPUT_SUB_FOLDER    :
TRACKER_DISPLAY_NAMES : None
SEQMAP_FOLDER        : None
SEQMAP_FILE          : None
SEQ_INFO             : None
GT_LOC_FORMAT        : {gt_folder}/{seq}/gt/gt.txt
SKIP_SPLIT_FOL       : False

CLEAR Config:
METRICS              : ['HOTA', 'CLEAR', 'Identity']
THRESHOLD            : 0.5
PRINT_CONFIG         : True

Identity Config:
METRICS              : ['HOTA', 'CLEAR', 'Identity']
THRESHOLD            : 0.5
PRINT_CONFIG         : True

Evaluating 1 tracker(s) on 3 sequence(s) for 1 class(es) on MotChallenge2DBox dataset using the following metrics: HOTA, CLEAR, Identity, Count


Evaluating BYTE_Pub

    MotChallenge2DBox.get_raw_seq_data(BYTE_Pub, MOT17-02-DPM)             0.1422 sec
    MotChallenge2DBox.get_preprocessed_seq_data(pedestrian)                0.0598 sec
    HOTA.eval_sequence()                                                   0.0907 sec
    CLEAR.eval_sequence()                                                  0.0145 sec
    Identity.eval_sequence()                                               0.0040 sec
    Count.eval_sequence()                                                  0.0000 sec
1 eval_sequence(MOT17-02-DPM, BYTE_Pub)                                  0.3124 sec
    MotChallenge2DBox.get_raw_seq_data(BYTE_Pub, MOT17-09-SDP)             0.0536 sec
    MotChallenge2DBox.get_preprocessed_seq_data(pedestrian)                0.0457 sec
    HOTA.eval_sequence()                                                   0.0694 sec
    CLEAR.eval_sequence()                                                  0.0101 sec
    Identity.eval_sequence()                                               0.0025 sec
    Count.eval_sequence()                                                  0.0000 sec
2 eval_sequence(MOT17-09-SDP, BYTE_Pub)                                  0.1821 sec
    MotChallenge2DBox.get_raw_seq_data(BYTE_Pub, MOT17-13-FRCNN)           0.0986 sec
    MotChallenge2DBox.get_preprocessed_seq_data(pedestrian)                0.0676 sec
    HOTA.eval_sequence()                                                   0.1027 sec
    CLEAR.eval_sequence()                                                  0.0158 sec
    Identity.eval_sequence()                                               0.0043 sec
    Count.eval_sequence()                                                  0.0000 sec
3 eval_sequence(MOT17-13-FRCNN, BYTE_Pub)                                0.2904 sec

All sequences for BYTE_Pub finished in 0.79 seconds

HOTA: BYTE_Pub-pedestrian          HOTA      DetA      AssA      DetRe     DetPr     AssRe     AssPr     LocA      OWTA      HOTA(0)   LocA(0)   HOTALocA(0)
MOT17-02-DPM                       45.64     45.475    45.959    47.51     85.359    54.791    65.744    87.5      46.709    53.551    84.211    45.096
MOT17-09-SDP                       57.674    71.003    46.911    74.766    87.348    60.033    64.682    88.413    59.214    67.925    85.985    58.405
MOT17-13-FRCNN                     59.349    59.762    59.075    62.517    84.083    73.721    69.45     85.644    60.769    70.861    83.279    59.012
COMBINED                           52.442    53.964    51.101    56.508    85.275    62.937    67.147    87.008    53.724    61.937    84.214    52.159

CLEAR: BYTE_Pub-pedestrian         MOTA      MOTP      MODA      CLR_Re    CLR_Pr    MTR       PTR       MLR       sMOTA     CLR_TP    CLR_FN    CLR_FP    IDSW      MT        PT        ML        Frag
MOT17-02-DPM                       52.677    86.104    53        54.33     97.612    32.258    37.097    30.645    45.128    10095     8486      247       60        20        23        19        120
MOT17-09-SDP                       82.723    87.466    83.155    84.376    98.574    73.077    23.077    3.8462    72.148    4493      832       65        23        19        6         1         43
MOT17-13-FRCNN                     71.68     83.835    71.826    73.089    98.302    52.727    25.455    21.818    59.865    8509      3133      147       17        58        28        24        35
COMBINED                           63.402    85.533    63.683    64.974    98.051    48.99     28.788    22.222    54.002    23097     12451     459       100       97        57        44        198

Identity: BYTE_Pub-pedestrian      IDF1      IDR       IDP       IDTP      IDFN      IDFP
MOT17-02-DPM                       52.346    40.741    73.197    7570      11011     2772
MOT17-09-SDP                       69.19     64.207    75.011    3419      1906      1139
MOT17-13-FRCNN                     70.559    61.51     82.729    7161      4481      1495
COMBINED                           61.417    51.058    77.05     18150     17398     5406

Count: BYTE_Pub-pedestrian         Dets      GT_Dets   IDs       GT_IDs
MOT17-02-DPM                       10342     18581     39        62
MOT17-09-SDP                       4558      5325      23        26
MOT17-13-FRCNN                     8656      11642     70        110
COMBINED                           23556     35548     132       198

Timing analysis:
MotChallenge2DBox.get_raw_seq_data                                     0.2944 sec
MotChallenge2DBox.get_preprocessed_seq_data                            0.1731 sec
HOTA.eval_sequence                                                     0.2629 sec
CLEAR.eval_sequence                                                    0.0404 sec
Identity.eval_sequence                                                 0.0108 sec
Count.eval_sequence                                                    0.0000 sec
eval_sequence                                                          0.7850 sec
Evaluator.evaluate                                                     1.6773 sec
```
</details>

## Results

| Sequence      | Package       | MOTA   | MOTP  | IDF1  | IDsw |
|---------------|---------------|--------|-------|-------|------|
| MOT17-02-DPM  | TrackEval     | 52.677 | 86.104| 52.346| 60   |
| MOT17-02-DPM  | py-motmetrics | 52.8%  | 0.142 | 52.3% | 56   |
| MOT17-09-SDP  | TrackEval     | 82.723 | 87.466| 69.19 | 23   |
| MOT17-09-SDP  | py-motmetrics | 82.0%  | 0.135 | 69.2% | 24   |
| MOT17-13-FRCNN| TrackEval     | 71.68  | 83.835| 70.559| 17   |
| MOT17-13-FRCNN| py-motmetrics | 71.7%  | 0.162 | 70.6% | 17   |
