# Using knime with Python

To use Knime and Keras/Tensorflow deep learning libraries, you need to setup Python environments with particular versions of each library.

You should do so using `anaconda` or `miniconda`.

# Knime default environnment

This is the requirements.txt for the basic knime env (recent one, here with Python 3.11.5):

```
Package                 Version
----------------------- ------------
absl-py                 1.4.0
aiohttp                 3.8.5
aiosignal               1.2.0
astunparse              1.6.3
async-timeout           4.0.2
attrs                   23.1.0
blinker                 1.6.2
Bottleneck              1.3.5
Brotli                  1.0.9
cachetools              4.2.2
certifi                 2023.11.17
cffi                    1.16.0
charset-normalizer      2.0.4
click                   8.1.7
cryptography            41.0.3
flatbuffers             1.12
frozenlist              1.4.0
gast                    0.4.0
google-auth             2.22.0
google-auth-oauthlib    0.5.2
google-pasta            0.2.0
grpcio                  1.48.2
h5py                    3.9.0
idna                    3.4
install                 1.3.5
joblib                  1.2.0
keras                   2.12.0
Keras-Preprocessing     1.1.2
Markdown                3.4.1
MarkupSafe              2.1.1
multidict               6.0.2
numexpr                 2.8.7
numpy                   1.23.5
oauthlib                3.2.2
opt-einsum              3.3.0
packaging               23.1
pandas                  2.1.1
pip                     23.3
protobuf                3.20.3
py4j                    0.10.9.7
pyarrow                 14.0.1
pyasn1                  0.4.8
pyasn1-modules          0.2.8
pycparser               2.21
PyJWT                   2.4.0
pyOpenSSL               23.2.0
PySocks                 1.7.1
python-dateutil         2.8.2
pytz                    2023.3.post1
requests                2.31.0
requests-oauthlib       1.3.0
rsa                     4.7.2
scikit-learn            1.3.0
scipy                   1.11.3
setuptools              68.0.0
six                     1.16.0
tensorboard             2.12.1
tensorboard-data-server 0.7.0
tensorboard-plugin-wit  1.8.1
tensorflow              2.12.0
tensorflow-estimator    2.12.0
termcolor               2.1.0
threadpoolctl           2.2.0
typing_extensions       4.7.1
tzdata                  2023.3
urllib3                 1.26.18
Werkzeug                2.2.3
wheel                   0.35.1
wrapt                   1.14.1
yarl                    1.8.1
```

## Knime environnement for Keras

For Keras a much older environnment is required. 

!!! warning annotate "Apple silicon (M1/M2) mac users"

    For Apple Silicon macs, you will need to create an environment using Intel reposititory, to do that you need to prefix conda commands with: `CONDA_SUBDIR=osx-64`
    
    You will also need to install [Rosetta2](https://support.apple.com/en-us/HT211861)

Here is the list of packages:

```
Package             Version
------------------- ---------
absl-py             0.15.0
astor               0.8.1
certifi             2021.5.30
coverage            5.5
Cython              0.29.24
dataclasses         0.8
gast                0.5.3
grpcio              1.36.1
h5py                2.8.0
importlib-metadata  4.8.1
Keras               2.2.4
Keras-Applications  1.0.8
Keras-Preprocessing 1.1.2
Markdown            3.3.4
numpy               1.19.2
pandas              0.23.0
pip                 21.2.2
protobuf            3.17.2
python-dateutil     2.8.2
pytz                2021.3
PyYAML              5.4.1
scipy               1.5.2
setuptools          58.0.4
six                 1.16.0
tensorboard         1.12.2
tensorflow          1.12.0
termcolor           1.1.0
typing_extensions   4.1.1
Werkzeug            2.0.3
wheel               0.37.1
zipp                3.6.0
```