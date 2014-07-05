wheelshop
=========

A pypi compatible index where you can point pip install


Install
-------

It is designed to run on AWS with Autoscaling Groups (ASG). It works with [dynpacker](https://github.com/livesystems/dynpacker) and can be made into an AMI with the following command

```bash
#!/bin/bash
git clone . packaging/
cd packaging; tar -czvf  ../app.tar.gz *; cd ..
python -m dynpacker "${BASE_AMI}" "${BASE_AMI_DESCRIPTION}" "${BASE_AMI_VERSION}-${BASE_AMI_REVISION}" "wheelshop" "0.1" 1 "app.tar.gz" "${GIT_CHECKOUT_SHA1}" "${CI_PROJECT_REPONAME}" "${CI_BUILD_NUM}" -d "web" -s "python server.py"
rm -r packaging/
```

The resulting AMI will be compatible with the Netflix naming scheme, so it works perfectly with e.g. [Asgard](http://github.com/netflix/Asgard)

It expects the wheels to be uploaded to an S3 bucket - you must specify the name with the $WHEELSHOP_S3_BUCKET environment variable.
