# Getting Started

login
```bash
gcloud init
# for cli
gcloud auth login
# for ADC
gcloud auth application-default login
```

config
```bash
# core/account
gcloud config set account <email>
gcloud config unset account <email>
# auth/impersonate_service_account
gcloud config set auth/impersonate_service_account <email>
gcloud config unset auth/impersonate_servcice_account <email>
```

# Services

artifact registry
```bash
gcloud auth print-access-token | nerd login -u oauth2accesstoken --password-stdin https://<location>-docker.pkg.dev
```

kms
```bash
# craete keyring
gcloud kms keyrings create "keyring" --location "global"

# create encryption key
gcloud kms keys create "key" --location "global" --keyring "keyring" --purpose "encryption"

# list keys
gcloud kms keys list --location "global" --keyring "keyring"

# encrypt file using encryption key
gcloud kms encrypt --location "global" --keyring "keyring" --key "quickstart" --plaintext-file /path/to/file --ciphertext-file /path/to/output

# decrypt file using encryption key
gcloud kms decrypt --location "global" --keyring "keyring" --key "key" --ciphertext-file /path/to/file --plaintext-file /path/to/output

# list key versions
gcloud kms keys versions list --location "global" --keyring "keyring" --key "key"

# schedule for destroy for a key version
gcloud kms keys versions destroy key-version --location "global" --keyring "keyring" --key "key"
```

# Extras

gcsfuse
```bash
# clone from official repo
git clone --depth 1 https://github.com/GoogleCloudPlatform/gcsfuse.git
# build image
docker build -t gcsfuse .
# run with docker
docker run --rm -it --name gcsfuse -h gcsfuse --privileged -v /path/to/local:/gcs:rw,rshared gcsfuse
# run with shell
docker run --rm -it --name gcsfuse -h gcsfuse --privileged -v /path/to/local:/gcs:rw,rshared --entrypoint ash gcsfuse
# inside container
gcsfuse <bucket> /path/to/local
```

# IAM

[predefined roles](https://cloud.google.com/iam/docs/understanding-roles)
[full resource names](https://cloud.google.com/iam/docs/full-resource-names)

cloudrun/cloudbuild service agent required roles
```
storage.objectUser
artifactregistry.writer
logging.logWriter
iam.serviceAccountUser
```

impersonation
```bash
gcloud storage buckets list --impersonate-service-account <service-account>
```
