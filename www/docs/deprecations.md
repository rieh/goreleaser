---
title: Deprecation notices
---

This page is used to list deprecation notices across GoReleaser.

Deprecated options will be removed after ~6 months from the time they were
deprecated.

You can check your use of deprecated configurations by running:

```console
$ goreleaser check
```

## Active deprecation notices

None at this time.

<!--

Template for new deprecations:

### property

> since yyyy-mm-dd

Description.

=== "Before"

    ``` yaml
    foo: bar
    ```

=== "After"
    ``` yaml
    foo: bar
    ```

-->

## Expired deprecation notices

The following options were deprecated in the past and were already removed.

### puts

> since 2019-11-15, removed 2020-04-14 (v0.132.0)

The HTTP upload support was extended to also accept `POST` as a method,
so the name `puts` kind of lost its meaning.

=== "Before"

    ``` yaml
    puts:
    - ...
    ```

=== "After"
    ``` yaml
    uploads:
    - ...
    ```

Also note that secrets environment variable name prefixes have changed from
`PUT_` to `UPLOAD_`.

### nfpms.name_template

> since 2019-11-15, removed 2020-04-14 (v0.132.0)

The `name_template` field was deprecated in favor of a more clear one,
`file_name_template`.

=== "Before"
    ``` yaml
    nfpms:
    - name_template: foo
    ```


=== "After"
    ``` yaml
    nfpms:
    - file_name_template: foo
    ```

### blob

> since 2019-08-02, removed 2020-03-22 (v0.130.0)

Blob was deprecated in favor of its plural form.
It was already accepting multiple inputs, but its pluralized now so its more
clear.

=== "Before"
    ```yaml
    blob:
      # etc
    ```

=== "After"
    ```yaml
    blobs:
      # etc
    ```

### sign

> since 2019-07-20, removed 2020-03-22 (v0.130.0)

Sign was deprecated in favor of its plural form.

=== "Before"
    ```yaml
    sign:
      # etc
    ```

=== "After"
    ```yaml
    signs:
      -
        # etc
    ```

### brew

> since 2019-06-09, removed 2020-01-26 (v0.125.0)

Brew was deprecated in favor of its plural form.

Change this:

=== "Before"
    ```yaml
    brew:
      # etc
    ```

=== "After"
    ```yaml
    brews:
      -
        # etc
    ```

### s3

> since 2019-06-09, removed 2020-01-07 (v0.125.0)

S3 was deprecated in favor of the new `blob`, which supports S3, Azure Blob and
GCS.

=== "Before"
    ```yaml
    s3:
    -
      # etc
    ```

=== "After"
    ```yaml
    blobs:
    -
      provider: s3
      # etc
    ```

ACLs should be set on the bucket, the `acl` option does not exist anymore.

### archive

> since 2019-04-16, removed 2019-12-27 (v0.124.0)

We now allow multiple archives, so the `archive` statement will be removed.

=== "Before"
    ```yaml
    archive:
      format: zip
    ```

=== "After"
    ```yaml
    archives:
      - id: foo
        format: zip
    ```

### snapcraft

> since 2019-05-27, removed 2019-12-27 (v0.124.0)

We now allow multiple Snapcraft configs, so the `snapcraft` statement will be removed.

=== "Before"
    ```yaml
    snapcraft:
      publish: true
      # ...
    ```

=== "After"
    ```yaml
    snapcrafts:
      -
        publish: true
        # ...
    ```

### nfpm

> since 2019-05-07, removed 2019-12-27 (v0.124.0)

We now allow multiple NFPM config, so the `nfpm` statement will be removed.

=== "Before"
    ```yaml
    nfpm:
      formats:
        - deb
    ```

=== "After"
    ```yaml
    nfpms:
      -
        formats:
          - deb
    ```

### docker.binary

> since 2018-10-01, removed 2019-08-02 (v0.114.0)

You can now create a Docker image with multiple binaries.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      binary: foo
    ```

=== "After"
    ```yaml
    dockers:
    - image: foo/bar
      binaries:
      - foo
    ```

### docker.image

> since 2018-10-20, removed 2019-08-02 (v0.114.0)

This property was deprecated in favor of more flexible `image_templates`.
The idea is to be able to define several images and tags using templates instead of just one image with tag templates.
This flexibility allows images to be pushed to multiple registries.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      tag_templates:
        - '{{ .Tag }}'
    ```

=== "After"
    ```yaml
    dockers:
    - image_templates:
        - 'foo/bar:{{ .Tag }}'
    ```

### docker.tag_templates

> since 2018-10-20, removed 2019-08-02 (v0.114.0)

This property was deprecated in favor of more flexible `image_templates`.
The idea is to be able to define several images and tags using templates instead of just one image with tag templates.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      tag_templates:
        - '{{ .Tag }}'
    ```

=== "After"
    ```yaml
    dockers:
    - image_templates:
        - 'foo/bar:{{ .Tag }}'
    ```

### git.short_hash

> since 2018-10-03, removed 2019-01-19 (v0.98.0)

This property was being used to tell GoReleaser to use short git hashes
instead of the full ones. This has been removed in favor of specific
template variables (`.FullCommit` and `.ShortCommit`).

=== "Before"
    ```yaml
    git:
      short_hash: true

    fake:
      foo_template: 'blah {{ .Commit }}'
    ```

=== "After"
    ```yaml
    fake:
      foo_template: 'blah {{ .ShortCommit }}'
    ```

### fpm

> since 2018-02-17, removed 2017-08-15 (v0.83.0)

FPM is deprecated in favor of nfpm, which is a simpler alternative written
in Go. The objective is to remove the ruby dependency thus simplify the
CI/CD pipelines.

Just replace the `fpm` keyword by `nfpm` in your `goreleaser.yaml` file.

=== "Before"
    ```yaml
    fpm:
      # ...
    ```

=== "After"
    ```yaml
    nfpm:
      # ...
    ```

### docker.tag_template

> since 2018-01-19, removed 2017-08-15 (v0.83.0)

This property was deprecated in favor of the pluralized `tag_templates`.
The idea is to be able to define several tags instead of just one.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      tag_template: '{{ .Tag }}'
    ```

=== "After"
    ```yaml
    dockers:
    - image: foo/bar
      tag_templates:
        - '{{ .Tag }}'
    ```

### docker.latest

> since 2018-01-19, removed 2017-08-15 (v0.83.0)

The `latest` field in Docker config is deprecated in favor of the newer
`tag_templates` field.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      latest: true
    ```

=== "After"
    ```yaml
    dockers:
    - image: foo/bar
      tag_templates:
        - '{{ .Tag }}'
        - latest
    ```