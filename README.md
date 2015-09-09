## MIREX 2015: Music/Speech Classification and Detection

### Supported OS

* OS X
* Linux

### Dependencies

* Install Docker: https://docs.docker.com/installation/
* Verify that docker is working properly by running the hello-world docker container: ```docker run hello-world```

### Available Implementations

Classification Task  | Detection Task
-------------  | -------------
With Training  (CWT) | With Self-Similarity Matrix and Silence Detection (DWSSMSD)
Without Training (CWOT)  | With Self-Similarity Matrix (DWSSM)
 | Without Self-Similarity Matrix (DWOSSM)

**Note 1**

The ```-v host-machine-directory-or-file:container-directory-or-file``` docker parameter used in the following commands allows to mount a directory from the host machine to the docker container in order to be able to process its contents in the container. In the same way a directory from the host machine is mounted in the container in order to be able to return the results generated in the container back to the host machine.  

### Classification Task
#### Without Training

Use the following format:

```docker run --rm=true -v /absolute/path/to/input/dir:/absolute/path/to/input/dir -v /absolute/path/to/input/filelist:/absolute/path/to/input/filelist -v /absolute/path/to/results/directory:/absolute/path/to/results/directory nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py classification-without-training --classification-file-list /absolute/path/to/input/filelist --output-dir /absolute/path/to/results/directory```

##### Example:

If the filelist is located under **/var/my/data/filelist.txt** and looks like the following:
```
/var/my/data/track1.wav
/var/my/data/track2.wav
...
```
Then if we want to receive the classification results under the **/var/my/results** directory, the docker command would be:

```docker run --rm=true -v /var/my/data/:/var/my/data/ -v /var/my/data/filelist.txt:/var/my/data/filelist.txt -v /var/my/results:/var/my/results nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py classification-without-training --classification-file-list /var/my/data/filelist.txt --output-dir /var/my/results```

#### With Training

Use the following format:

```docker run --rm=true -v /absolute/path/to/input/dir:/absolute/path/to/input/dir -v /absolute/path/to/input/training_filelist:/absolute/path/to/input/training_filelist -v /absolute/path/to/input/classification_filelist:/absolute/path/to/input/classification_filelist -v /absolute/path/to/results/directory:/absolute/path/to/results/directory nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py classification-with-training --training-file-list /absolute/path/to/input/training_filelist --classification-file-list /absolute/path/to/input/classification_filelist --output-dir /absolute/path/to/results/directory```

##### Example:

if the training filelist is located under **/var/my/data/training_filelist.txt** and has the following contents (tab separated):
```
/var/my/data/track1.wav m
/var/my/data/track2.wav s
...
```
and the classification filelist is located under **/var/my/data/classification_filelist.txt** and has the following contents:
```
/var/my/data/track1.wav
/var/my/data/track2.wav
...
```
Then if we want to receive the classification results under the **/var/my/results** directory, the docker command would be:

```docker run --rm=true -v /var/my/data/:/var/my/data/ -v /var/my/data/training_filelist.txt:/var/my/data/training_filelist.txt -v /var/my/results:/var/my/results nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py -v /var/my/data/classification_filelist.txt:/var/my/data/classification_filelist.txt classification-with-training --training-file-list /var/my/data/training_filelist.txt --classification-file-list /var/my/data/classification_filelist.txt --output-dir /var/my/results```

### Detection Task

#### With Self-Similarity Matrix and Silence Detection
#### With Self-Similarity Matrix
#### Without Self-Similarity Matrix

### Troubleshooting

