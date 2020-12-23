# Generated by: Neurodocker version 0.7.0+0.gdc97516.dirty
# Latest release: Neurodocker version 0.7.0
# Timestamp: 2020/12/23 22:23:59 UTC
# 
# Thank you for using Neurodocker. If you discover any issues
# or ways to improve this software, please submit an issue or
# pull request on our GitHub repository:
# 
#     https://github.com/ReproNim/neurodocker

Bootstrap: docker
From: neurodebian:buster

%post
apt-get update -qq
apt-get install -y -q --no-install-recommends neurodebian-freeze
nd_freeze  20201222T174247Z
apt-get clean
rm -rf /var/lib/apt/lists/*

su - root

export ND_ENTRYPOINT="/neurodocker/startup.sh"
apt-get update -qq
apt-get install -y -q --no-install-recommends \
    apt-utils \
    bzip2 \
    ca-certificates \
    curl \
    locales \
    unzip
apt-get clean
rm -rf /var/lib/apt/lists/*
sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen
dpkg-reconfigure --frontend=noninteractive locales
update-locale LANG="en_US.UTF-8"
chmod 777 /opt && chmod a+s /opt
mkdir -p /neurodocker
if [ ! -f "$ND_ENTRYPOINT" ]; then
  echo '#!/usr/bin/env bash' >> "$ND_ENTRYPOINT"
  echo 'set -e' >> "$ND_ENTRYPOINT"
  echo 'export USER="${USER:=`whoami`}"' >> "$ND_ENTRYPOINT"
  echo 'if [ -n "$1" ]; then "$@"; else /usr/bin/env bash; fi' >> "$ND_ENTRYPOINT";
fi
chmod -R 777 /neurodocker && chmod a+s /neurodocker

apt-get update -qq
apt-get install -y -q --no-install-recommends \
    vim \
    wget \
    strace \
    time \
    ncdu \
    gnupg \
    curl \
    procps \
    datalad \
    pigz \
    less \
    tree \
    git-annex-standalone \
    python3-nibabel \
    python3-nipype \
    virtualenv \
    shellcheck \
    python3-dcmstack \
    python3-funcsigs \
    python3-etelemetry \
    python3-pytest \
    dcmtk \
    python3-pip \
    python3-wheel \
    python3-setuptools \
    python3-datalad \
    python3-filelock \
    dcm2niix \
    python3-pytest \
    python3-nose \
    heudiconv=0.9.0-1~nd100+1
apt-get clean
rm -rf /var/lib/apt/lists/*

:

curl -sL https://deb.nodesource.com/setup_9.x | bash - 

apt-get update -qq
apt-get install -y -q --no-install-recommends \
    nodejs \
    npm
apt-get clean
rm -rf /var/lib/apt/lists/*

npm install -g bids-validator@1.5.8

mkdir /afs /inbox

test "$(getent passwd reproin)" || useradd --no-user-group --create-home --shell /bin/bash reproin
su - reproin

echo '{
\n  "pkg_manager": "apt",
\n  "instructions": [
\n    [
\n      "base",
\n      "neurodebian:buster"
\n    ],
\n    [
\n      "ndfreeze",
\n      {
\n        "date": "20201222T174247Z"
\n      }
\n    ],
\n    [
\n      "user",
\n      "root"
\n    ],
\n    [
\n      "_header",
\n      {
\n        "version": "generic",
\n        "method": "custom"
\n      }
\n    ],
\n    [
\n      "install",
\n      [
\n        "vim",
\n        "wget",
\n        "strace",
\n        "time",
\n        "ncdu",
\n        "gnupg",
\n        "curl",
\n        "procps",
\n        "datalad",
\n        "pigz",
\n        "less",
\n        "tree",
\n        "git-annex-standalone",
\n        "python3-nibabel",
\n        "python3-nipype",
\n        "virtualenv",
\n        "shellcheck",
\n        "python3-dcmstack",
\n        "python3-funcsigs",
\n        "python3-etelemetry",
\n        "python3-pytest",
\n        "dcmtk",
\n        "python3-pip",
\n        "python3-wheel",
\n        "python3-setuptools",
\n        "python3-datalad",
\n        "python3-filelock",
\n        "dcm2niix",
\n        "python3-pytest",
\n        "python3-nose",
\n        "heudiconv=0.9.0-1~nd100+1"
\n      ]
\n    ],
\n    [
\n      "run",
\n      ":"
\n    ],
\n    [
\n      "run",
\n      "curl -sL https://deb.nodesource.com/setup_9.x | bash - "
\n    ],
\n    [
\n      "install",
\n      [
\n        "nodejs",
\n        "npm"
\n      ]
\n    ],
\n    [
\n      "run",
\n      "npm install -g bids-validator@1.5.8"
\n    ],
\n    [
\n      "run",
\n      "mkdir /afs /inbox"
\n    ],
\n    [
\n      "user",
\n      "reproin"
\n    ],
\n    [
\n      "entrypoint",
\n      "/usr/bin/heudiconv \"$@\""
\n    ]
\n  ]
\n}' > /neurodocker/neurodocker_specs.json

%environment
export LANG="en_US.UTF-8"
export LC_ALL="en_US.UTF-8"
export ND_ENTRYPOINT="/neurodocker/startup.sh"

%runscript
/usr/bin/heudiconv "$@"
