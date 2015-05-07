Tapewriter(EC2 tag management tool)
====

## Overview
Tapewriter is a tool to manage EC2 Tags.

## Description
EC2 Tags managed from JSON file.

This tool can be the following usage.

- current tag export
- tags
    - update
    - append
    - delete


## Requirement
- python 2.7~
- boto
- ansicolor

## Install
```
$ git clone xxx
```

## Usage
### options
```
-a --aws_access_key KEY           (default: ~/.aws/credentials or ~/.boto or /etc/boto.cfg)
-s --aws_secret_key KEY           (default: ~/.aws/credentials or ~/.boto or /etc/boto.cfg)
-c --credentials CREDENTIALS_FILE (default: ~/.aws/credentials or ~/.boto or /etc/boto.cfg)
-p --profile PROFILE_NAME         (default: default)
-r --region REGION_NAME           (default: all region, description: エクスポート対象となるregionを指定)
   --export EXPORT_FILE_NAME      (default: STDOUT, description: エクスポートの実行)
   --apply FILE_NAME              (default: None, description: タグを適用)
   --filter FILTER                (default: {}, description: エクスポート時に指定したタグのフィルタリングを実施)
   --dry-run                      (default: false, description: dry-run)
```

### run
export to file from all region

```
$ tapewriter --export example.json
```

export to stdout from all region

```
$ tapewriter --export
```

export to stdout(use tag filter)

```
$ tapewriter --export --filter '{"Env":"dev", "Role":"app"}'
```

specified region

```
$ tapewriter -r ap-northeast-1 --export
```

specified credentials

```
$ tapewriter -c ./my_credential
```

check apply tag

```
$ tapewriter -r ap-northeast-1 --apply example.json --dry-run
```

apply tag

```
$ tapewriter -r ap-northeast-1 --apply example.json
```


## JSON Format
```
{
  "instances": [
    {
      "id": "i-11111111",
      "region": "ap-northeast-1",
      "tags": {
        "Env": "dev",
        "Hostname": "www",
        "Name": "hoge"
      }
    },
    {
      "id": "i-22222222",
      "region": "ap-northeast-1",
      "tags": {
        "Env": "dev",
        "Hostname": "db",
        "Name": "fuga"
      }
    },
    {
      "id": "i-33333333",
      "region": "us-east-1",
      "tags": {
        "Env": "release",
        "Name": "piyo"
      }
    }
  ]
}
```

## Notice
- The following regions will be excluded.
    - cn-north-1
    - us-gov-west-1
- Operation is slow, if using export to all regions. This problem will be resolved, You use -r or --region option.

## Licence

MIT

## Author

[og732](https://github.com/om732)
