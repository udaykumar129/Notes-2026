
# Testing Life Cycle Configuration for S3 Buckets in rook-ceph

- Create a bucket in USDC East with life cycle snippet and without snippet
- check if we are creating it with snippet is actually deleting it or not
- used following snippet for creating with life cycle snippet - udayk-lifecycle is the bucket name

```
apiVersion: objectbucket.io/v1alpha1
kind: ObjectBucketClaim
metadata:
  annotations:

  finalizers:
  - objectbucket.io/finalizer
  generation: 4
  labels:
    bucket-provisioner: rook-ceph.ceph.rook.io-bucket
  name: udayk-lifecycle
  namespace: rook-ceph

spec:
  bucketName:
  generateBucketName: udayk-lifecycle

  storageClassName: rook-ceph-bucket
  additionalConfig:
    maxSize: "5G"
    bucketLifecycle: |
      {
        "Rules": [
          {
            "ID": "ExpireAfter1Days",
            "Status": "Enabled",
            "Prefix": "",
            "Expiration": {
              "Days": 1
            }
          }
        ]
      }
```

```
   AWS_ACCESS_KEY_ID: ZAPZ3C3KX9DHGFU00KN9
   AWS_SECRET_ACCESS_KEY: wuJreSkQhLomDgNPltg9wdp7ioaDzLcKylSQnWIr
   BUCKET_HOST: https://rook-ceph-objstore-east.kus.logistics.corp
   BUCKET_NAME: udayk-lifecycle-826f298a-e722-4311-8c01-f2f467fba135
   BUCKET_PORT: "80"
   BUCKET_REGION: usdc-east
```
```
mc alias set udayk-lifecycle https://rook-ceph-objstore-east.kus.logistics.corp ZAPZ3C3KX9DHGFU00KN9 wuJreSkQhLomDgNPltg9wdp7ioaDzLcKylSQnWIr
mc cp LoggingUtil-0.0.1.jar udayk-lifecycle/udayk-lifecycle-826f298a-e722-4311-8c01-f2f467fba135
mc cp newsupportbundle.zip udayk-lifecycle/udayk-lifecycle-826f298a-e722-4311-8c01-f2f467fba135
mc cp test-file-2 udayk-lifecycle/udayk-lifecycle-826f298a-e722-4311-8c01-f2f467fba135
mc cp test-file-1 udayk-lifecycle/udayk-lifecycle-826f298a-e722-4311-8c01-f2f467fba135
mc ls udayk-lifecycle/udayk-lifecycle-826f298a-e722-4311-8c01-f2f467fba135
```
- used following snippet for creating without life cycle snippet - udayk-no-lifecycle is the bucket name

```
apiVersion: objectbucket.io/v1alpha1
kind: ObjectBucketClaim
metadata:
  annotations:

  finalizers:
  - objectbucket.io/finalizer
  generation: 4
  labels:
    bucket-provisioner: rook-ceph.ceph.rook.io-bucket
  name: udayk-no-lifecycle
  namespace: rook-ceph

spec:
  bucketName:
  generateBucketName: udayk-no-lifecycle

  storageClassName: rook-ceph-bucket
  additionalConfig:
    maxSize: "5G"
```

```
   AWS_ACCESS_KEY_ID: B59PE1ARTUMUHU25KPK4
   AWS_SECRET_ACCESS_KEY: kuUPvUCC2BXYG4KHSWDIBgrQCVjM5yUDxzCrADNU
   BUCKET_HOST: https://rook-ceph-objstore-east.kus.logistics.corp
   BUCKET_NAME: udayk-no-lifecycle-72514acf-51a0-453c-8b38-691144f8287c
   BUCKET_PORT: "80"
   BUCKET_REGION: usdc-east
```

```
mc alias set udayk-no-lifecycle https://rook-ceph-objstore-east.kus.logistics.corp B59PE1ARTUMUHU25KPK4 kuUPvUCC2BXYG4KHSWDIBgrQCVjM5yUDxzCrADNU
mc cp LoggingUtil-0.0.1.jar udayk-no-lifecycle/udayk-no-lifecycle-72514acf-51a0-453c-8b38-691144f8287c
mc cp newsupportbundle.zip udayk-no-lifecycle/udayk-no-lifecycle-72514acf-51a0-453c-8b38-691144f8287c
mc cp test-file-2 udayk-no-lifecycle/udayk-no-lifecycle-72514acf-51a0-453c-8b38-691144f8287c
mc cp test-file-1 udayk-no-lifecycle/udayk-no-lifecycle-72514acf-51a0-453c-8b38-691144f8287c
mc ls udayk-no-lifecycle/udayk-no-lifecycle-72514acf-51a0-453c-8b38-691144f8287c
```

- After creating the bucket without life cycle - i have created life cycle rule like this by patching exising bucket

```
kubectl patch obc udayk-no-lifecycle -n rook-ceph --type=merge -p '
spec:
  additionalConfig:
    bucketLifecycle: |
      {
        "Rules": [
          {
            "ID": "ExpireAfter1Days",
            "Status": "Enabled",
            "Prefix": "",
            "Expiration": {
              "Days": 1
            }
          }
        ]
      }'
'
```
