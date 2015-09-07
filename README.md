# MIREX 2015: Music/Speech Classification and Detection

### Dependencies

* Install Docker: https://docs.docker.com/installation/
* Verify that docker is working properly by running the hello-world docker container: ```docker run hello-world```

### Classification Task - No training

Use the following format:

```docker run --rm=true nicktgr15/mirex2015 -v /absolute/path/to/input/dir:/absolute/path/to/input/dir -v /absolute/path/to/input/filelist:/tmp/filelist -v /absolute/path/to/results/directory:/tmp/output nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py classification-no-training```

#### Example:

If the filelist is located under **/var/my/data/fielist.txt** and looks like the following:
```
/var/my/data/track1.wav
/var/my/data/track2.wav
...
```
Then if we want to receive the classification results under the **/tmp/results** directory, the docker command would be:

```docker run --rm=true nicktgr15/mirex2015 -v /var/my/data/:/var/my/data/ -v /var/my/data/fielist.txt:/tmp/filelist -v /tmp/results:/tmp/output nicktgr15/mirex2015 python /opt/mirex2015/mirex2015.py classification-no-training```
