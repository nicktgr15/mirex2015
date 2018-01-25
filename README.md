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
With Training  (NT1) | With Self-Similarity Matrix and Silence Detection (TVDP1)
Without Training (NT2)  | With Self-Similarity Matrix (TVDP2)
| | Without Self-Similarity Matrix (TVDP3)

**Note**

The ```-v host-machine-directory-or-file:container-directory-or-file``` docker parameter used in the following commands allows to mount a directory from the host machine to the docker container in order to be able to process its contents in the container. In the same way a directory from the host machine is mounted in the container in order to be able to return the results generated in the container back to the host machine.  

### Classification Task
#### Without Training

Use the following format:

```docker run --rm -v /abs/path/to/input/dir:/abs/path/to/input/dir -v /abs/path/to/input/filelist:/abs/path/to/input/filelist -v /abs/path/to/results/dir:/abs/path/to/results/dir nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py classification-without-training --classification-file-list /abs/path/to/input/filelist --output-dir /abs/path/to/results/dir```

##### Example:

If the filelist is located under **/var/my/data/filelist.txt** and looks like the following:
```
/var/my/data/track1.wav
/var/my/data/track2.wav
...
```
Then if we want to receive the classification results under the **/var/my/results** directory, the docker command would be:

```docker run --rm -v /var/my/data/:/var/my/data/ -v /var/my/data/filelist.txt:/var/my/data/filelist.txt -v /var/my/results:/var/my/results nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py classification-without-training --classification-file-list /var/my/data/filelist.txt --output-dir /var/my/results```

#### With Training

Use the following format:

```docker run --rm -v /abs/path/to/input/dir:/abs/path/to/input/dir -v /abs/path/to/input/training_filelist:/abs/path/to/input/training_filelist -v /abs/path/to/input/classification_filelist:/abs/path/to/input/classification_filelist -v /abs/path/to/results/dir:/abs/path/to/results/dir nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py classification-with-training --training-file-list /abs/path/to/input/training_filelist --classification-file-list /abs/path/to/input/classification_filelist --output-dir /abs/path/to/results/dir```

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

```docker run --rm -v /var/my/data/:/var/my/data/ -v /var/my/data/training_filelist.txt:/var/my/data/training_filelist.txt -v /var/my/results:/var/my/results nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py -v /var/my/data/classification_filelist.txt:/var/my/data/classification_filelist.txt classification-with-training --training-file-list /var/my/data/training_filelist.txt --classification-file-list /var/my/data/classification_filelist.txt --output-dir /var/my/results```

### Detection Task

#### With Self-Similarity Matrix and Silence Detection

Use the following format:

```docker run --rm -v /abs/path/to/input/wav:/abs/path/to/input/wav -v /abs/path/to/results/dir:/abs/path/to/results/dir nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py detection-with-matrix-silence-detector --input-file /abs/path/to/input/wav --output-dir /abs/path/to/results/dir```

The results will be available under ```/abs/path/to/results/dir``` on the host machine.

#### With Self-Similarity Matrix

```docker run --rm -v /abs/path/to/input/wav:/abs/path/to/input/wav -v /abs/path/to/results/dir:/abs/path/to/results/dir nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py detection-with-matrix-no-silence-detector --input-file /abs/path/to/input/wav --output-dir /abs/path/to/results/dir```

The results will be available under ```/abs/path/to/results/dir``` on the host machine.

#### Without Self-Similarity Matrix

```docker run --rm -v /abs/path/to/input/wav:/abs/path/to/input/wav -v /abs/path/to/results/dir:/abs/path/to/results/dir nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py detection-without-matrix --input-file /abs/path/to/input/wav --output-dir /abs/path/to/results/dir```

The results will be available under ```/abs/path/to/results/dir``` on the host machine.

### Troubleshooting

#### Cannot attach directories from the host machine
In OS X there is an issue when trying to attach directories outside the /Users dir. For example attaching host's /tmp directory to the container is not possible.

#### Running out of memory or out of disk space (OS X only)
If the virtualbox VM in which the containers are executed under OS X is running out of resources then you need to remove the existing VM and create a new one with more resources. 

*e.g.*
```
docker-machine rm default
docker-machine create --virtualbox-disk-size 40000 -virtualbox-memory 2048 -d virtualbox default
docker-machine ls
docker-machine start default
```
You may have to set the environment variables for the new VM by running ```eval "$(docker-machine env default)"```
