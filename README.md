# singularity_conda

Ways of building Singularity containers


- Use an existing container

- Use the remote builder

- Build a Docker container on your own system and
  - transfer the image to Wynton
  - upload the Dockerfile to _

- Install Singularity on a system you have root access on. Build the Singularity container there and transfer the image to Wynton.




---

Reference:
link to official docs.  Version that is in use on _



---

Howto:

# singularity_conda


- Create a new conda environment

```sh
[murashka@dev3 test1]$ conda create --name env1
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /wynton/home/admins/murashka/miniconda3/envs/env1

Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate env1
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

- Activate the new environment:

```sh
[murashka@dev3 test1]$ conda activate env1
```

- Verify `conda list` doesn't show any packages installed:

```sh
(env1) [murashka@dev3 test1]$ conda list
# packages in environment at /wynton/home/admins/murashka/miniconda3/envs/env1:
#
# Name                    Version                   Build  Channel
```

- In the new environment, install a few conda packages:

```sh
(env1) [murashka@dev3 test1]$ conda install pandas matplotlib flask
...
```

- Now verify what packages are in the environment:

```sh
(env1) [murashka@dev3 test1]$ conda list
# packages in environment at /wynton/home/admins/murashka/miniconda3/envs/env1:
#
# Name                    Version                   Build  Channel
_libgcc_mutex             0.1                        main
_openmp_mutex             4.5                       1_gnu
blas                      1.0                         mkl
bottleneck                1.3.2            py39hdd57654_1
brotli                    1.0.9                he6710b0_2
ca-certificates           2021.7.5             h06a4308_1
certifi                   2021.5.30        py39h06a4308_0
click                     8.0.1              pyhd3eb1b0_0
cycler                    0.10.0           py39h06a4308_0
dataclasses               0.8                pyh6d0b6a4_7
dbus                      1.13.18              hb2f20db_0
expat                     2.4.1                h2531618_2
flask                     1.1.2              pyhd3eb1b0_0
fontconfig                2.13.1               h6c09931_0
fonttools                 4.25.0             pyhd3eb1b0_0
freetype                  2.10.4               h5ab3b9f_0
glib                      2.69.1               h5202010_0
gst-plugins-base          1.14.0               h8213a91_2
gstreamer                 1.14.0               h28cd5cc_2
icu                       58.2                 he6710b0_3
importlib-metadata        4.8.1            py39h06a4308_0
intel-openmp              2021.3.0          h06a4308_3350
itsdangerous              2.0.1              pyhd3eb1b0_0
jinja2                    3.0.1              pyhd3eb1b0_0
jpeg                      9d                   h7f8727e_0
kiwisolver                1.3.1            py39h2531618_0
lcms2                     2.12                 h3be6417_0
ld_impl_linux-64          2.35.1               h7274673_9
libffi                    3.3                  he6710b0_2
libgcc-ng                 9.3.0               h5101ec6_17
libgomp                   9.3.0               h5101ec6_17
libpng                    1.6.37               hbc83047_0
libstdcxx-ng              9.3.0               hd4cf53a_17
libtiff                   4.2.0                h85742a9_0
libuuid                   1.0.3                h1bed415_2
libwebp-base              1.2.0                h27cfd23_0
libxcb                    1.14                 h7b6447c_0
libxml2                   2.9.12               h03d6c58_0
lz4-c                     1.9.3                h295c915_1
markupsafe                2.0.1            py39h27cfd23_0
matplotlib                3.4.2            py39h06a4308_0
matplotlib-base           3.4.2            py39hab158f2_0
mkl                       2021.3.0           h06a4308_520
mkl-service               2.4.0            py39h7f8727e_0
mkl_fft                   1.3.0            py39h42c9631_2
mkl_random                1.2.2            py39h51133e4_0
munkres                   1.0.7                      py_1    bioconda
ncurses                   6.2                  he6710b0_1
numexpr                   2.7.3            py39h22e1b3c_1
numpy                     1.20.3           py39hf144106_0
numpy-base                1.20.3           py39h74d4b33_0
olefile                   0.46               pyhd3eb1b0_0
openjpeg                  2.4.0                h3ad879b_0
openssl                   1.1.1l               h7f8727e_0
pandas                    1.3.2            py39h8c16a72_0
pcre                      8.45                 h295c915_0
pillow                    8.3.1            py39h2c7a002_0
pip                       21.2.4           py37h06a4308_0
pyparsing                 2.4.7              pyhd3eb1b0_0
pyqt                      5.9.2            py39h2531618_6
python                    3.9.7                h12debd9_1
python-dateutil           2.8.2              pyhd3eb1b0_0
pytz                      2021.1             pyhd3eb1b0_0
qt                        5.9.7                h5867ecd_1
readline                  8.1                  h27cfd23_0
setuptools                58.0.4           py39h06a4308_0
sip                       4.19.13          py39h2531618_0
six                       1.16.0             pyhd3eb1b0_0
sqlite                    3.36.0               hc218d9a_0
tk                        8.6.10               hbc83047_0
tornado                   6.1              py39h27cfd23_0
tzdata                    2021a                h5d7bf9c_0
werkzeug                  2.0.1              pyhd3eb1b0_0
wheel                     0.37.0             pyhd3eb1b0_1
xz                        5.2.5                h7b6447c_0
zipp                      3.5.0              pyhd3eb1b0_0
zlib                      1.2.11               h7b6447c_3
zstd                      1.4.9                haebb681_0
```

- If you have a Python script that uses those packages, in this example the script just prints out the imported modules:

```sh
(env1) [murashka@dev3 test1]$ cat myscript.py
import pandas
import flask
import matplotlib

modules = dir()
print(f'modules imported: {modules}')

(env1) [murashka@dev3 test1]$ python ./myscript.py
modules imported: ['__annotations__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'flask', 'matplotlib', 'pandas']
```



- export the conda environment


```sh
(env1) [murashka@dev3 test1]$ conda env export > environment.yml
```

(env1) [murashka@dev3 test1]$ cat environment.yml
name: env1
channels:
  - bioconda
  - defaults
  - conda-forge
dependencies:
  - _libgcc_mutex=0.1=main
  - _openmp_mutex=4.5=1_gnu
  - blas=1.0=mkl
  - bottleneck=1.3.2=py39hdd57654_1
  - brotli=1.0.9=he6710b0_2
  - ca-certificates=2021.7.5=h06a4308_1
  - certifi=2021.5.30=py39h06a4308_0
  - click=8.0.1=pyhd3eb1b0_0
  - cycler=0.10.0=py39h06a4308_0
  - dataclasses=0.8=pyh6d0b6a4_7
  - dbus=1.13.18=hb2f20db_0
  - expat=2.4.1=h2531618_2
  - flask=1.1.2=pyhd3eb1b0_0
  - fontconfig=2.13.1=h6c09931_0
  - fonttools=4.25.0=pyhd3eb1b0_0
  - freetype=2.10.4=h5ab3b9f_0
  - glib=2.69.1=h5202010_0
  - gst-plugins-base=1.14.0=h8213a91_2
  - gstreamer=1.14.0=h28cd5cc_2
  - icu=58.2=he6710b0_3
  - importlib-metadata=4.8.1=py39h06a4308_0
  - intel-openmp=2021.3.0=h06a4308_3350
  - itsdangerous=2.0.1=pyhd3eb1b0_0
  - jinja2=3.0.1=pyhd3eb1b0_0
  - jpeg=9d=h7f8727e_0
  - kiwisolver=1.3.1=py39h2531618_0
  - lcms2=2.12=h3be6417_0
  - ld_impl_linux-64=2.35.1=h7274673_9
  - libffi=3.3=he6710b0_2
  - libgcc-ng=9.3.0=h5101ec6_17
  - libgomp=9.3.0=h5101ec6_17
  - libpng=1.6.37=hbc83047_0
  - libstdcxx-ng=9.3.0=hd4cf53a_17
  - libtiff=4.2.0=h85742a9_0
  - libuuid=1.0.3=h1bed415_2
  - libwebp-base=1.2.0=h27cfd23_0
  - libxcb=1.14=h7b6447c_0
  - libxml2=2.9.12=h03d6c58_0
  - lz4-c=1.9.3=h295c915_1
  - markupsafe=2.0.1=py39h27cfd23_0
  - matplotlib=3.4.2=py39h06a4308_0
  - matplotlib-base=3.4.2=py39hab158f2_0
  - mkl=2021.3.0=h06a4308_520
  - mkl-service=2.4.0=py39h7f8727e_0
  - mkl_fft=1.3.0=py39h42c9631_2
  - mkl_random=1.2.2=py39h51133e4_0
  - munkres=1.0.7=py_1
  - ncurses=6.2=he6710b0_1
  - numexpr=2.7.3=py39h22e1b3c_1
  - numpy=1.20.3=py39hf144106_0
  - numpy-base=1.20.3=py39h74d4b33_0
  - olefile=0.46=pyhd3eb1b0_0
  - openjpeg=2.4.0=h3ad879b_0
  - openssl=1.1.1l=h7f8727e_0
  - pandas=1.3.2=py39h8c16a72_0
  - pcre=8.45=h295c915_0
  - pillow=8.3.1=py39h2c7a002_0
  - pip=21.2.4=py37h06a4308_0
  - pyparsing=2.4.7=pyhd3eb1b0_0
  - pyqt=5.9.2=py39h2531618_6
  - python=3.9.7=h12debd9_1
  - python-dateutil=2.8.2=pyhd3eb1b0_0
  - pytz=2021.1=pyhd3eb1b0_0
  - qt=5.9.7=h5867ecd_1
  - readline=8.1=h27cfd23_0
  - setuptools=58.0.4=py39h06a4308_0
  - sip=4.19.13=py39h2531618_0
  - six=1.16.0=pyhd3eb1b0_0
  - sqlite=3.36.0=hc218d9a_0
  - tk=8.6.10=hbc83047_0
  - tornado=6.1=py39h27cfd23_0
  - tzdata=2021a=h5d7bf9c_0
  - werkzeug=2.0.1=pyhd3eb1b0_0
  - wheel=0.37.0=pyhd3eb1b0_1
  - xz=5.2.5=h7b6447c_0
  - zipp=3.5.0=pyhd3eb1b0_0
  - zlib=1.2.11=h7b6447c_3
  - zstd=1.4.9=haebb681_0
prefix: /wynton/home/admins/murashka/miniconda3/envs/env1

---

Now that you have your Python code (myscript.py) and the exported environment yaml file, the next step is to upload those to Github:

You can manually create the repository and files or you can do it from the command line.

The new repository will have 

- myscript.py
- environment.yml


- The last file that is needed is a Singularity definition file, create a file using your preferred text editor, in this example it is named Singularity.def:

The post section of the defition file will use wget to fetch the environment.yml file. 

```sh
Bootstrap: docker

From: continuumio/miniconda3

%environment

%post
    wget https://raw.githubusercontent.com/murashka-ucsf/singularity_conda/main/environment.yml

    ENV_NAME=$(head -1 environment.yml | cut -d' ' -f2)
    echo ". /opt/conda/etc/profile.d/conda.sh" >> $SINGULARITY_ENVIRONMENT
    echo "conda activate $ENV_NAME" >> $SINGULARITY_ENVIRONMENT

    . /opt/conda/etc/profile.d/conda.sh
    conda env create -f environment.yml -p /opt/conda/envs/$ENV_NAME

    mkdir /code; cd /code
    wget https://raw.githubusercontent.com/murashka-ucsf/singularity_conda/main/myscript.py

%runscript
    exec "$@"
```
    
---

- Using the `--remote` option for the `singularity build` command, you can use the Remote Builder


Assuming you have a valid access token (if not generate one and store it under ~/.singularity/remote.yaml)

If you token is expired you will see a message similar to:
```sh
(env1) [murashka@dev3 test]$ singularity build --remote test.sif Singularity
FATAL:   While performing build: failed to post request to remote build service: Failed to verify auth token in request: auth: failed to validate token signature: token is expired (401 Unauthorized)
```

Otherwise the Remote Builder should be building the container image, which if everything works, will be downloaded to the directory you ran the command from.


```sh
(env1) [murashka@dev3 test]$ singularity build --remote test.sif Singularity
INFO:    Access Token Verified!
INFO:    Token stored in /root/.singularity/remote.yaml
INFO:    Remote "default" now in use.
INFO:    Starting build...
Getting image source signatures
Copying blob sha256:33847f680f63fb1b343a9fc782e267b5abdbdb50d65d4b9bd2a136291d67cf75
Copying blob sha256:f5a80bcd14133fe8e0166900eb4bfb714939510e490403e82f3a32776cd41a8f
Copying blob sha256:8d0d14d1334a21b14dcb9a9bbb16aa692282173db137856ce8c315a05e3397c7
Copying config sha256:d17c4c40058acc065bdf9a9f48332b636390f4a4f5401e0fe6d30c0fe28ee672
Writing manifest to image destination
Storing signatures
2021/09/21 23:40:34  info unpack layer: sha256:33847f680f63fb1b343a9fc782e267b5abdbdb50d65d4b9bd2a136291d67cf75
2021/09/21 23:40:35  info unpack layer: sha256:f5a80bcd14133fe8e0166900eb4bfb714939510e490403e82f3a32776cd41a8f
2021/09/21 23:40:37  info unpack layer: sha256:8d0d14d1334a21b14dcb9a9bbb16aa692282173db137856ce8c315a05e3397c7
INFO:    Running post scriptlet
+ wget https://raw.githubusercontent.com/murashka-ucsf/singularity_conda/main/environment.yml
--2021-09-21 23:40:42--  https://raw.githubusercontent.com/murashka-ucsf/singularity_conda/main/environment.yml
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.109.133, 185.199.110.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 157 [text/plain]
Saving to: ‘environment.yml’

     0K                                                       100% 10.1M=0s

2021-09-21 23:40:42 (10.1 MB/s) - ‘environment.yml’ saved [157/157]

+ head -1+  environment.ymlcut -d  -f2

+ ENV_NAME=test01
+ echo . /opt/conda/etc/profile.d/conda.sh
+ echo conda activate test01
+ . /opt/conda/etc/profile.d/conda.sh
+ export CONDA_EXE=/opt/conda/bin/conda
+ export _CE_M=
+ export _CE_CONDA=
+ export CONDA_PYTHON_EXE=/opt/conda/bin/python
+ [ -z  ]
+ export CONDA_SHLVL=0
+ [ -n  ]
+ dirname /opt/conda/bin/conda
+ dirname /opt/conda/bin
+ PATH=/opt/conda/condabin:/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
+ export PATH
+ [ -z x ]
+ conda env create -f environment.yml -p /opt/conda/envs/test01
+ local cmd=env
+ __conda_exe env create -f environment.yml -p /opt/conda/envs/test01
+ __add_sys_prefix_to_path
+ [ -n  ]
+ dirname /opt/conda/bin/conda
+ SYSP=/opt/conda/bin
+ dirname /opt/conda/bin
+ SYSP=/opt/conda
+ [ -n  ]
+ PATH=/opt/conda/bin:/opt/conda/condabin:/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
+ export PATH
+ /opt/conda/bin/conda env create -f environment.yml -p /opt/conda/envs/test01
Collecting package metadata (repodata.json): ...working... done
Solving environment: ...working... done

Downloading and Extracting Packages
icu-68.1             | 13.0 MB   | ########## | 100%
libgfortran5-11.2.0  | 1.7 MB    | ########## | 100%
nspr-4.30            | 233 KB    | ########## | 100%
libclang-11.1.0      | 19.2 MB   | ########## | 100%
freetype-2.10.4      | 890 KB    | ########## | 100%
itsdangerous-2.0.1   | 17 KB     | ########## | 100%
fontconfig-2.13.1    | 357 KB    | ########## | 100%
lcms2-2.12           | 443 KB    | ########## | 100%
pyqtwebengine-5.12.1 | 174 KB    | ########## | 100%
glib-2.68.4          | 440 KB    | ########## | 100%
olefile-0.46         | 32 KB     | ########## | 100%
libopenblas-0.3.17   | 9.2 MB    | ########## | 100%
tk-8.6.11            | 3.3 MB    | ########## | 100%
libopus-1.3.1        | 255 KB    | ########## | 100%
libstdcxx-ng-11.2.0  | 4.2 MB    | ########## | 100%
pyqt-5.12.3          | 21 KB     | ########## | 100%
sqlite-3.36.0        | 1.4 MB    | ########## | 100%
xorg-libxau-1.0.9    | 13 KB     | ########## | 100%
pthread-stubs-0.4    | 5 KB      | ########## | 100%
pyqt-impl-5.12.3     | 5.9 MB    | ########## | 100%
nss-3.69             | 2.1 MB    | ########## | 100%
_libgcc_mutex-0.1    | 3 KB      | ########## | 100%
libxml2-2.9.12       | 772 KB    | ########## | 100%
dataclasses-0.8      | 10 KB     | ########## | 100%
libogg-1.3.4         | 206 KB    | ########## | 100%
python_abi-3.9       | 4 KB      | ########## | 100%
krb5-1.19.2          | 1.4 MB    | ########## | 100%
openjpeg-2.4.0       | 444 KB    | ########## | 100%
mysql-common-8.0.25  | 1.6 MB    | ########## | 100%
libtiff-4.3.0        | 668 KB    | ########## | 100%
qt-5.12.9            | 99.5 MB   | ########## | 100%
openssl-1.1.1l       | 2.1 MB    | ########## | 100%
libcblas-3.9.0       | 11 KB     | ########## | 100%
pillow-8.3.2         | 701 KB    | ########## | 100%
libvorbis-1.3.7      | 280 KB    | ########## | 100%
liblapack-3.9.0      | 11 KB     | ########## | 100%
werkzeug-2.0.1       | 219 KB    | ########## | 100%
gst-plugins-base-1.1 | 2.6 MB    | ########## | 100%
python-dateutil-2.8. | 240 KB    | ########## | 100%
tzdata-2021a         | 121 KB    | ########## | 100%
expat-2.4.1          | 182 KB    | ########## | 100%
gstreamer-1.18.5     | 2.0 MB    | ########## | 100%
libpng-1.6.37        | 306 KB    | ########## | 100%
matplotlib-base-3.4. | 7.3 MB    | ########## | 100%
pyqt5-sip-4.19.18    | 310 KB    | ########## | 100%
pip-21.2.4           | 1.1 MB    | ########## | 100%
kiwisolver-1.3.2     | 79 KB     | ########## | 100%
libgfortran-ng-11.2. | 19 KB     | ########## | 100%
libedit-3.1.20191231 | 121 KB    | ########## | 100%
jbig-2.1             | 43 KB     | ########## | 100%
python-3.9.7         | 27.5 MB   | ########## | 100%
certifi-2021.5.30    | 141 KB    | ########## | 100%
lerc-2.2.1           | 213 KB    | ########## | 100%
libglib-2.68.4       | 3.1 MB    | ########## | 100%
matplotlib-3.4.3     | 7 KB      | ########## | 100%
libpq-13.3           | 2.7 MB    | ########## | 100%
_openmp_mutex-4.5    | 22 KB     | ########## | 100%
markupsafe-2.0.1     | 22 KB     | ########## | 100%
pandas-1.3.3         | 13.0 MB   | ########## | 100%
readline-8.1         | 295 KB    | ########## | 100%
libevent-2.1.10      | 1.1 MB    | ########## | 100%
libgomp-11.2.0       | 428 KB    | ########## | 100%
libgcc-ng-11.2.0     | 892 KB    | ########## | 100%
ca-certificates-2021 | 136 KB    | ########## | 100%
gettext-0.19.8.1     | 3.6 MB    | ########## | 100%
six-1.16.0           | 14 KB     | ########## | 100%
libiconv-1.16        | 1.4 MB    | ########## | 100%
numpy-1.21.2         | 6.2 MB    | ########## | 100%
jpeg-9d              | 264 KB    | ########## | 100%
libblas-3.9.0        | 12 KB     | ########## | 100%
ncurses-6.2          | 985 KB    | ########## | 100%
setuptools-58.0.4    | 958 KB    | ########## | 100%
libdeflate-1.7       | 67 KB     | ########## | 100%
xz-5.2.5             | 343 KB    | ########## | 100%
tornado-6.1          | 646 KB    | ########## | 100%
libwebp-base-1.2.1   | 845 KB    | ########## | 100%
libllvm11-11.1.0     | 29.1 MB   | ########## | 100%
wheel-0.37.0         | 31 KB     | ########## | 100%
lz4-c-1.9.3          | 179 KB    | ########## | 100%
cycler-0.10.0        | 9 KB      | ########## | 100%
pyparsing-2.4.7      | 60 KB     | ########## | 100%
libffi-3.4.2         | 60 KB     | ########## | 100%
zlib-1.2.11          | 106 KB    | ########## | 100%
pyqtchart-5.12       | 253 KB    | ########## | 100%
mysql-libs-8.0.25    | 1.8 MB    | ########## | 100%
jinja2-3.0.1         | 99 KB     | ########## | 100%
click-8.0.1          | 146 KB    | ########## | 100%
libxkbcommon-1.0.3   | 581 KB    | ########## | 100%
pcre-8.45            | 253 KB    | ########## | 100%
zstd-1.5.0           | 490 KB    | ########## | 100%
glib-tools-2.68.4    | 86 KB     | ########## | 100%
xorg-libxdmcp-1.1.3  | 19 KB     | ########## | 100%
alsa-lib-1.2.3       | 560 KB    | ########## | 100%
dbus-1.13.6          | 572 KB    | ########## | 100%
ld_impl_linux-64-2.3 | 667 KB    | ########## | 100%
libuuid-2.32.1       | 28 KB     | ########## | 100%
libxcb-1.13          | 395 KB    | ########## | 100%
pytz-2021.1          | 239 KB    | ########## | 100%
flask-2.0.1          | 70 KB     | ########## | 100%
Preparing transaction: ...working... done
Verifying transaction: ...working... done
Executing transaction: ...working... done
#
# To activate this environment, use
#
#     $ conda activate /opt/conda/envs/test01
#
# To deactivate an active environment, use
#
#     $ conda deactivate

+ mkdir /code
+ cd /code
+ wget https://raw.githubusercontent.com/murashka-ucsf/singularity_conda/main/myscript.py
--2021-09-21 23:42:50--  https://raw.githubusercontent.com/murashka-ucsf/singularity_conda/main/myscript.py
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.111.133, 185.199.110.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 100 [text/plain]
Saving to: ‘myscript.py’

     0K                                                       100% 6.09M=0s

2021-09-21 23:42:50 (6.09 MB/s) - ‘myscript.py’ saved [100/100]

INFO:    Adding environment to container
INFO:    Adding runscript
INFO:    Creating SIF file...
INFO:    Build complete: /tmp/image-817988753
WARNING: Skipping container verification
854.9MiB / 854.9MiB [======================================] 100 % 64.7 MiB/s 0s

Library storage: using 854.91 MiB out of 11.00 GiB quota (7.6% used)
Container URL: https://cloud.sylabs.io/library/murashka/remote-builds/rb-614a6d6ba267b3f6a3832f35
INFO:    Build complete: test.sif
```

```sh
(env1) [murashka@dev3 test]$ ls -l
total 760036
-rw-r--r--. 1 murashka wynton-admins       100 Sep 21 16:34 myscript.py
-rw-r--r--. 1 murashka wynton-admins       616 Sep 21 16:37 Singularity
-rwxr-xr-x. 1 murashka wynton-admins 896438272 Sep 21 16:46 test.sif
```



```sh
(env1) [murashka@dev3 test]$ singularity shell ./test.sif
Singularity> ls -l /
total 1
drwxr-xr-x.   2 root     root           1128 Jul 23 05:34 bin
drwxr-xr-x.   2 root     root              3 Jun 13 03:30 boot
drwxrwxr-x.   2 root     root             34 Sep 21 16:42 code
drwxr-xr-x.  22 root     root           4200 Aug 30 12:19 dev
lrwxrwxrwx.   1 root     root             36 Sep 21 16:40 environment -> .singularity.d/env/90-environment.sh
-rw-rw-r--.   1 root     root            157 Sep 21 16:40 environment.yml
drwxr-xr-x.  41 root     root           1489 Sep 21 16:40 etc
drwxr-xr-x.   2 root     root              3 Jun 13 03:30 home
drwxr-xr-x.   8 root     root            117 Jul 23 05:34 lib
drwxr-xr-x.   2 root     root             43 Jul 20 17:00 lib64
drwxr-xr-x.   2 root     root              3 Jul 20 17:00 media
drwxr-xr-x.   2 root     root              3 Jul 20 17:00 mnt
drwxr-xr-x.   3 root     root             28 Jul 23 05:35 opt
dr-xr-xr-x. 855 root     root              0 Aug 27 04:21 proc
drwx------.   3 root     root             78 Sep 21 16:40 root
drwxr-xr-x.   3 root     root             39 Jul 20 17:00 run
drwxr-xr-x.   2 root     root           1063 Jul 23 05:34 sbin
lrwxrwxrwx.   1 root     root             24 Sep 21 16:40 singularity -> .singularity.d/runscript
drwxr-xr-x.   2 root     root              3 Jul 20 17:00 srv
dr-xr-xr-x.  13 root     root              0 Aug 27 11:21 sys
drwxrwxrwt. 179 root     root          14320 Sep 21 16:47 tmp
drwxr-xr-x.  10 root     root            150 Jul 20 17:00 usr
drwxr-xr-x.  11 root     root            160 Jul 20 17:00 var
drwxr-xr-x.   3 murashka wynton-admins    60 Sep 21 16:47 wynton
```


```sh
Singularity> ls -l /code
-rw-rw-r--. 1 root root 100 Sep 21 16:42 myscript.py
```

```
Singularity> python
Python 3.9.7 | packaged by conda-forge | (default, Sep 14 2021, 01:17:55)
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
```

even if you deactivated the environment, if you enter the Singularity container using the `singularity shell` command

All the dependencies needed for myscript.py should be present. Verify with `conda list` and it will show all the packages in the environment:

```sh
Singularity> conda list
# packages in environment at /opt/conda/envs/test01:
#
# Name                    Version                   Build  Channel
_libgcc_mutex             0.1                 conda_forge    conda-forge
_openmp_mutex             4.5                       1_gnu    conda-forge
alsa-lib                  1.2.3                h516909a_0    conda-forge
ca-certificates           2021.5.30            ha878542_0    conda-forge
certifi                   2021.5.30        py39hf3d152e_0    conda-forge
click                     8.0.1            py39hf3d152e_0    conda-forge
cycler                    0.10.0                     py_2    conda-forge
dataclasses               0.8                pyhc8e2a94_3    conda-forge
dbus                      1.13.6               h48d8840_2    conda-forge
expat                     2.4.1                h9c3ff4c_0    conda-forge
flask                     2.0.1              pyhd8ed1ab_0    conda-forge
fontconfig                2.13.1            hba837de_1005    conda-forge
freetype                  2.10.4               h0708190_1    conda-forge
gettext                   0.19.8.1          h73d1719_1006    conda-forge
glib                      2.68.4               h9c3ff4c_1    conda-forge
glib-tools                2.68.4               h9c3ff4c_1    conda-forge
gst-plugins-base          1.18.5               hf529b03_0    conda-forge
gstreamer                 1.18.5               h76c114f_0    conda-forge
icu                       68.1                 h58526e2_0    conda-forge
itsdangerous              2.0.1              pyhd8ed1ab_0    conda-forge
jbig                      2.1               h7f98852_2003    conda-forge
jinja2                    3.0.1              pyhd8ed1ab_0    conda-forge
jpeg                      9d                   h36c2ea0_0    conda-forge
kiwisolver                1.3.2            py39h1a9c180_0    conda-forge
krb5                      1.19.2               hcc1bbae_0    conda-forge
lcms2                     2.12                 hddcbb42_0    conda-forge
ld_impl_linux-64          2.36.1               hea4e1c9_2    conda-forge
lerc                      2.2.1                h9c3ff4c_0    conda-forge
libblas                   3.9.0           11_linux64_openblas    conda-forge
libcblas                  3.9.0           11_linux64_openblas    conda-forge
libclang                  11.1.0          default_ha53f305_1    conda-forge
libdeflate                1.7                  h7f98852_5    conda-forge
libedit                   3.1.20191231         he28a2e2_2    conda-forge
libevent                  2.1.10               hcdb4288_3    conda-forge
libffi                    3.4.2                h9c3ff4c_2    conda-forge
libgcc-ng                 11.2.0               h1d223b6_8    conda-forge
libgfortran-ng            11.2.0               h69a702a_8    conda-forge
libgfortran5              11.2.0               h5c6108e_8    conda-forge
libglib                   2.68.4               h174f98d_1    conda-forge
libgomp                   11.2.0               h1d223b6_8    conda-forge
libiconv                  1.16                 h516909a_0    conda-forge
liblapack                 3.9.0           11_linux64_openblas    conda-forge
libllvm11                 11.1.0               hf817b99_2    conda-forge
libogg                    1.3.4                h7f98852_1    conda-forge
libopenblas               0.3.17          pthreads_h8fe5266_1    conda-forge
libopus                   1.3.1                h7f98852_1    conda-forge
libpng                    1.6.37               h21135ba_2    conda-forge
libpq                     13.3                 hd57d9b9_0    conda-forge
libstdcxx-ng              11.2.0               he4da1e4_8    conda-forge
libtiff                   4.3.0                hf544144_1    conda-forge
libuuid                   2.32.1            h7f98852_1000    conda-forge
libvorbis                 1.3.7                h9c3ff4c_0    conda-forge
libwebp-base              1.2.1                h7f98852_0    conda-forge
libxcb                    1.13              h7f98852_1003    conda-forge
libxkbcommon              1.0.3                he3ba5ed_0    conda-forge
libxml2                   2.9.12               h72842e0_0    conda-forge
lz4-c                     1.9.3                h9c3ff4c_1    conda-forge
markupsafe                2.0.1            py39h3811e60_0    conda-forge
matplotlib                3.4.3            py39hf3d152e_0    conda-forge
matplotlib-base           3.4.3            py39h2fa2bec_0    conda-forge
mysql-common              8.0.25               ha770c72_2    conda-forge
mysql-libs                8.0.25               hfa10184_2    conda-forge
ncurses                   6.2                  h58526e2_4    conda-forge
nspr                      4.30                 h9c3ff4c_0    conda-forge
nss                       3.69                 hb5efdd6_0    conda-forge
numpy                     1.21.2           py39hdbf815f_0    conda-forge
olefile                   0.46               pyh9f0ad1d_1    conda-forge
openjpeg                  2.4.0                hb52868f_1    conda-forge
openssl                   1.1.1l               h7f98852_0    conda-forge
pandas                    1.3.3            py39hde0f152_0    conda-forge
pcre                      8.45                 h9c3ff4c_0    conda-forge
pillow                    8.3.2            py39ha612740_0    conda-forge
pip                       21.2.4             pyhd8ed1ab_0    conda-forge
pthread-stubs             0.4               h36c2ea0_1001    conda-forge
pyparsing                 2.4.7              pyh9f0ad1d_0    conda-forge
pyqt                      5.12.3           py39hf3d152e_7    conda-forge
pyqt-impl                 5.12.3           py39h0fcd23e_7    conda-forge
pyqt5-sip                 4.19.18          py39he80948d_7    conda-forge
pyqtchart                 5.12             py39h0fcd23e_7    conda-forge
pyqtwebengine             5.12.1           py39h0fcd23e_7    conda-forge
python                    3.9.7           hb7a2778_1_cpython    conda-forge
python-dateutil           2.8.2              pyhd8ed1ab_0    conda-forge
python_abi                3.9                      2_cp39    conda-forge
pytz                      2021.1             pyhd8ed1ab_0    conda-forge
qt                        5.12.9               hda022c4_4    conda-forge
readline                  8.1                  h46c0cb4_0    conda-forge
setuptools                58.0.4           py39hf3d152e_1    conda-forge
six                       1.16.0             pyh6c4a22f_0    conda-forge
sqlite                    3.36.0               h9cd32fc_1    conda-forge
tk                        8.6.11               h27826a3_1    conda-forge
tornado                   6.1              py39h3811e60_1    conda-forge
tzdata                    2021a                he74cb21_1    conda-forge
werkzeug                  2.0.1              pyhd8ed1ab_0    conda-forge
wheel                     0.37.0             pyhd8ed1ab_1    conda-forge
xorg-libxau               1.0.9                h7f98852_0    conda-forge
xorg-libxdmcp             1.1.3                h7f98852_0    conda-forge
xz                        5.2.5                h516909a_1    conda-forge
zlib                      1.2.11            h516909a_1010    conda-forge
zstd                      1.5.0                ha95c52a_0    conda-forge
```

and if you run the myscript.py, all it's should work:

```sh
Singularity> python ./myscript.py
modules imported: ['__annotations__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'flask', 'matplotlib', 'pandas']
```
