Image Processing Container for the HASTE Project.


[![Build Status](https://travis-ci.org/HASTE-project/haste-image-analysis-container2.svg?branch=master)](https://travis-ci.org/HASTE-project/haste-image-analysis-container2)



Interestingness Model:

Interestingness is the max of the magnitude of the Kendall's Tau over the sum of intensities and correlation image features, over a window for each well. 

```
docker build --no-cache=true -t "benblamey/image_analysis_container2:latest" .
docker push benblamey/image_analysis_container2:latest
```

Build + Run:
```
docker build --no-cache=true -t "benblamey/image_analysis_container2:latest" . ; docker run benblamey/image_analysis_container2
```


----
# Testing

To run a test:
```
# BEWARE DELETING REAL DATA!
rm -rf /mnt/mikro-testdata/source/**
mkdir /mnt/mikro-testdata/source/

# Copy single file from Polina
cp -v /mnt/mikro-testdata/PolinaG-KO/181214-KOday7-40X-H2O2-Glu/2018-12-14/9/181214-KOday7-40X-H2O2-Glu_B02_s1_w12DE5D0E6-1639-40D4-8654-9A6247B4B8CD.tif /mnt/mikro-testdata/source/ 

# Copy all files from Polina
cp -v /mnt/mikro-testdata/PolinaG-KO/181214-KOday7-40X-H2O2-Glu/2018-12-14/9/* /mnt/mikro-testdata/source/ 


# Simulate AZN dataset:
for i in {1..9}; do cp -v /mnt/mikro-testdata/azn/azn/*T000$i* /mnt/mikro-testdata/source ; sleep 1 ; done
for i in {10..81}; do cp -v /mnt/mikro-testdata/azn/azn/*T00$i* /mnt/mikro-testdata/source ; sleep 1 ; done
```

Login to the mongodb machine...
```
kubectl exec --namespace haste -it mongodb-d77749bb9-m7wvj bash
mongo
> show dbs
admin    0.000GB
config   0.000GB
local    0.000GB
streams  0.000GB
> use streams
switched to db streams
> show collections
strm_2019_03_01__13_54_20__ola-lab
strm_2019_03_01__14_02_34__ola-lab
strm_2019_03_01__14_04_18__ola-lab
strm_2019_03_01__14_09_47__ola-lab
strm_2019_03_01__14_21_44__ola-lab
> db['strm_2019_03_01__14_21_44__ola-lab'].find()

```

-or-
Port forward and use a local GUI...

```
kubectl --namespace haste port-forward mongodb-d77749bb9-m7wvj 27017:27017 
```



Contributors: Ben Blamey
