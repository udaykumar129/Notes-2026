
# Testing Life Cycle Configuration for S3 Buckets in rook-ceph

- Create a bucket in USDC East with life cycle snippet and without snippet
- check if we are creating it with snippet is actually deleting it or not
- used following snippet for creating with life cycle snippet

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
