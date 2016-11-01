hugo-s3-deploy
=========

This Ansible role will generate all static artifacts using [Hugo](https://gohugo.io) and sync with an Amazon S3 bucket.

Requirements
------------
You'll need the following stuff to get started:

* ansible >= 2.1.x
* aws-cli >= 1.11.x
* hugo >= 0.17
* [Amazon AWS account](https://aws.amazon.com/free)

**Note:** before you run `ansible-playbook`, make sure `boto` has access to your AWS profile (~ for example by exporting the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables).

TL;DR
------------

See [this](https://www.foobar-it.com/2016/09/03/hello-hugo/) blog post.

Use a playbook like this:

```sh
---
  - name: Deploy Hugo to Amazon AWS
    hosts: localhost
    gather_facts: true

    vars:
      website_domain: foobar-it.com
      verbose_output: true

    roles:
      - role: hugo-s3-deploy
        hugo_base_path: ../www
        s3_website_domain: "{{ website_domain }}"
        verbose: "{{ verbose_output }}"
        tags:
          - deploy
```

Run:

```sh
$ ansible-playbook -i localhost site.yml
```

Where: `site.yml` contains the contents I pasted above.

As a result, all static artifacts are generated and synched to the Amazon S3 bucket. I used a naming convention that translates `s3_website_domain` to a S3 bucketname. In this case: `foobar-it.com` leads to `www-foobar-it-com`.


License
-------

BSD
