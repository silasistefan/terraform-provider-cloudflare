---
layout: "cloudflare"
page_title: "Cloudflare: cloudflare_logpush_job"
sidebar_current: "docs-cloudflare-logpush-job"
description: |-
  Provides a resource which manages Cloudflare logpush jobs.
---

# cloudflare_logpush_job

Provides a resource which manages Cloudflare logpush jobs.

## Example Usage

```hcl
resource "cloudflare_logpush_job" "example_job" {
  enabled = true
  name = "My logpush job"
  logpull_options = "fields=RayID,ClientIP,EdgeStartTimestamp&timestamps=rfc3339"
  destination_conf = "s3://my-bucket-path?region=us-west-2"
  ownership_challenge = "00000000000000000"
}
```

## Argument Reference

The following arguments are supported:

* `desitination_conf` - (Required) Uniquely identifies a resource (such as an s3 bucket) where data will be pushed. Additional configuration parameters supported by the destination may be included.
* `ownership_challenge` - (Required) Ownership challenge token to prove destination ownership. See [https://developers.cloudflare.com/logs/tutorials/tutorial-logpush-curl/](https://developers.cloudflare.com/logs/tutorials/tutorial-logpush-curl/)

## Import

Logpush jobs can be imported using a composite ID formed of zone ID and logpush job ID, e.g.

```
$ terraform import cloudflare_logpush_job.example_job d41d8cd98f00b204e9800998ecf8427e/1
```

where:

* `d41d8cd98f00b204e9800998ecf8427e` - zone ID as returned by the API
* `1` - logpush job ID as returned by the [API](https://api.cloudflare.com/#logpush-jobs-list-logpush-jobs)
