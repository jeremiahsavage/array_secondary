# array_secondary

--
to use:
```
$ git clone https://github.com/jeremiahsavage/array_secondary.git
$ cd array_secondary
$ cwltool --debug array_secondary_tool.cwl.yaml --bam_path test.bam
```

--
without fix:
```
[jeremiah@wireless-s1-no-150-23-125 array_secondary]$ cwltool --debug array_secondary_tool.cwl.yaml --bam_path test.bam
/home/jeremiah/miniconda2/bin/cwltool 1.0.20160427142240
Parsed job order from command line: {
    "bam_path": [
        {
            "path": "test.bam", 
            "class": "File"
        }
    ], 
    "id": "array_secondary_tool.cwl.yaml", 
    "job_order": null
}
[job 139716192343440] initializing from file:///home/jeremiah/code/array_secondary/array_secondary_tool.cwl.yaml
[job 139716192343440] {
    "bam_path": [
        {
            "path": "test.bam", 
            "class": "File"
        }
    ], 
    "job_order": null
}
[job 139716192343440] path mappings is {
    "test.bam": [
        "/home/jeremiah/code/array_secondary/test.bam", 
        "/var/lib/cwl/job629133257_array_secondary/test.bam"
    ]
}
[job 139716192343440] command line bindings is [
    {
        "shellQuote": false, 
        "position": [
            1, 
            0
        ], 
        "valueFrom": null, 
        "do_eval": "${ var bai_list = \"\"; for (var i = 0; i < inputs.bam_path.length; i ++) { bai_list += \" cat \" + inputs.bam_path[i].path.slice(0,-4)+\".bai\" + \" >> bai.list && \" } return bai_list.slice(0,-3) }"
    }
]
['docker', 'pull', 'alpine']
Using default tag: latest
Trying to pull repository docker.io/library/alpine ... latest: Pulling from library/alpine

Digest: sha256:ea0d1389812f43e474c50155ec4914e1b48792d420820c15cab28c0794034950
Status: Image is up to date for docker.io/alpine:latest

[job 139716192343440] /home/jeremiah/code/array_secondary$ docker run -i --volume=/home/jeremiah/code/array_secondary/test.bam:/var/lib/cwl/job629133257_array_secondary/test.bam:ro --volume=/home/jeremiah/code/array_secondary:/var/spool/cwl:rw --volume=/tmp/tmpJmhURg:/tmp:rw --workdir=/var/spool/cwl --read-only=true --user=1000 --rm --env=TMPDIR=/tmp alpine /bin/sh -c  cat /var/lib/cwl/job629133257_array_secondary/test.bai >> bai.list 
cat: can't open '/var/lib/cwl/job629133257_array_secondary/test.bai': No such file or directory
[job 139716192343440] completed permanentFail
[job 139716192343440] {
    "bai_list": {
        "size": 0, 
        "path": "/home/jeremiah/code/array_secondary/bai.list", 
        "checksum": "sha1$da39a3ee5e6b4b0d3255bfef95601890afd80709", 
        "class": "File"
    }
}
Final process status is permanentFail
[job 139716192343440] Removing temporary directory /tmp/tmpJmhURg
Workflow error, try again with --debug for more information:
  Process status is ['permanentFail']
Traceback (most recent call last):
  File "/home/jeremiah/miniconda2/lib/python2.7/site-packages/cwltool/main.py", line 612, in main
    eval_timeout=args.eval_timeout
  File "/home/jeremiah/miniconda2/lib/python2.7/site-packages/cwltool/main.py", line 191, in single_job_executor
    raise workflow.WorkflowException(u"Process status is %s" % (final_status))
WorkflowException: Process status is ['permanentFail']
[jeremiah@wireless-s1-no-150-23-125 array_secondary]$ 
```

with fix:
```
(p2_fix)[jeremiah@wireless-s1-no-150-23-125 array_secondary]$ cwltool --debug array_secondary_tool.cwl.yaml --bam_path test.bam
/home/jeremiah/.virtualenvs/p2_fix/bin/cwltool 1.0
Parsed job order from command line: {
    "bam_path": [
        {
            "path": "test.bam", 
            "class": "File"
        }
    ], 
    "id": "array_secondary_tool.cwl.yaml", 
    "job_order": null
}
[job array_secondary_tool.cwl.yaml] initializing from file:///home/jeremiah/code/array_secondary/array_secondary_tool.cwl.yaml
[job array_secondary_tool.cwl.yaml] {
    "bam_path": [
        {
            "path": "test.bam", 
            "class": "File"
        }
    ], 
    "job_order": null
}
[job array_secondary_tool.cwl.yaml] path mappings is {
    "test.bam": [
        "/home/jeremiah/code/array_secondary/test.bam", 
        "/var/lib/cwl/job596286556_array_secondary/test.bam"
    ], 
    "test.bai": [
        "/home/jeremiah/code/array_secondary/test.bai", 
        "/var/lib/cwl/job596286556_array_secondary/test.bai"
    ]
}
[job array_secondary_tool.cwl.yaml] command line bindings is [
    {
        "shellQuote": false, 
        "position": [
            1, 
            0
        ], 
        "valueFrom": null, 
        "do_eval": "${ var bai_list = \"\"; for (var i = 0; i < inputs.bam_path.length; i ++) { bai_list += \" cat \" + inputs.bam_path[i].path.slice(0,-4)+\".bai\" + \" >> bai.list && \" } return bai_list.slice(0,-3) }"
    }
]
['docker', 'pull', 'alpine']
Using default tag: latest
Trying to pull repository docker.io/library/alpine ... latest: Pulling from library/alpine
Digest: sha256:ea0d1389812f43e474c50155ec4914e1b48792d420820c15cab28c0794034950
Status: Image is up to date for docker.io/alpine:latest

[job array_secondary_tool.cwl.yaml] /home/jeremiah/code/array_secondary$ docker \
    run \
    -i \
    --volume=/home/jeremiah/code/array_secondary/test.bam:/var/lib/cwl/job596286556_array_secondary/test.bam:ro \
    --volume=/home/jeremiah/code/array_secondary/test.bai:/var/lib/cwl/job596286556_array_secondary/test.bai:ro \
    --volume=/home/jeremiah/code/array_secondary:/var/spool/cwl:rw \
    --volume=/tmp/tmpZ8H2H6:/tmp:rw \
    --workdir=/var/spool/cwl \
    --read-only=true \
    --user=1000 \
    --rm \
    --env=TMPDIR=/tmp \
    --env=HOME=/var/spool/cwl \
    alpine \
    /bin/sh \
    -c \
     cat /var/lib/cwl/job596286556_array_secondary/test.bai >> bai.list 
[job array_secondary_tool.cwl.yaml] completed success
[job array_secondary_tool.cwl.yaml] {
    "bai_list": {
        "size": 11, 
        "path": "/home/jeremiah/code/array_secondary/bai.list", 
        "checksum": "sha1$4ed0e43723bf017d533a5ba129b2984af534b34c", 
        "class": "File"
    }
}
Final process status is success
[job array_secondary_tool.cwl.yaml] Removing temporary directory /tmp/tmpZ8H2H6
{
    "bai_list": {
        "size": 11, 
        "path": "/home/jeremiah/code/array_secondary/bai.list", 
        "checksum": "sha1$4ed0e43723bf017d533a5ba129b2984af534b34c", 
        "class": "File"
    }
}
(p2_fix)[jeremiah@wireless-s1-no-150-23-125 array_secondary]$ 
```