---
# ----------------------------------------------------------------------------
#
#     ***     AUTO GENERATED CODE    ***    Type: DCL     ***
#
# ----------------------------------------------------------------------------
#
#     This file is managed by Magic Modules (https:#github.com/GoogleCloudPlatform/magic-modules)
#     and is based on the DCL (https:#github.com/GoogleCloudPlatform/declarative-resource-client-library).
#     Changes will need to be made to the DCL or Magic Modules instead of here.
#
#     We are not currently able to accept contributions to this file. If changes
#     are required, please file an issue at https:#github.com/hashicorp/terraform-provider-google/issues/new/choose
#
# ----------------------------------------------------------------------------
subcategory: "RecaptchaEnterprise"
layout: "google"
page_title: "Google: google_recaptcha_enterprise_key"
description: |-
The RecaptchaEnterprise Key resource
---

# google_recaptcha_enterprise_key

The RecaptchaEnterprise Key resource

## Example Usage - android_key
A basic test of recaptcha enterprise key that can be used by Android apps
```hcl
resource "google_recaptcha_enterprise_key" "primary" {
  display_name = "display-name-one"

  android_settings {
    allow_all_package_names = true
    allowed_package_names   = []
  }

  labels = {
    label-one = "value-one"
  }

  project = "my-project-name"

  testing_options {
    testing_score = 0.8
  }
}


```
## Example Usage - ios_key
A basic test of recaptcha enterprise key that can be used by iOS apps
```hcl
resource "google_recaptcha_enterprise_key" "primary" {
  display_name = "display-name-one"

  ios_settings {
    allow_all_bundle_ids = true
    allowed_bundle_ids   = []
  }

  labels = {
    label-one = "value-one"
  }

  project = "my-project-name"

  testing_options {
    testing_score = 1
  }
}


```
## Example Usage - minimal_key
A minimal test of recaptcha enterprise key
```hcl
resource "google_recaptcha_enterprise_key" "primary" {
  display_name = "display-name-one"
  labels       = {}
  project      = "my-project-name"

  web_settings {
    integration_type  = "SCORE"
    allow_all_domains = true
  }
}


```
## Example Usage - web_key
A basic test of recaptcha enterprise key that can be used by websites
```hcl
resource "google_recaptcha_enterprise_key" "primary" {
  display_name = "display-name-one"

  labels = {
    label-one = "value-one"
  }

  project = "my-project-name"

  testing_options {
    testing_challenge = "NOCAPTCHA"
    testing_score     = 0.5
  }

  web_settings {
    integration_type              = "CHECKBOX"
    allow_all_domains             = true
    allowed_domains               = []
    challenge_security_preference = "USABILITY"
  }
}


```
## Example Usage - web_score_key
A basic test of recaptcha enterprise key with score integration type that can be used by websites
```hcl
resource "google_recaptcha_enterprise_key" "primary" {
  display_name = "display-name-one"

  labels = {
    label-one = "value-one"
  }

  project = "my-project-name"

  testing_options {
    testing_score = 0.5
  }

  web_settings {
    integration_type  = "SCORE"
    allow_all_domains = true
    allow_amp_traffic = false
    allowed_domains   = []
  }
}


```

## Argument Reference

The following arguments are supported:

* `display_name` -
  (Required)
  Human-readable display name of this key. Modifiable by user.
  


- - -

* `android_settings` -
  (Optional)
  Settings for keys that can be used by Android apps.
  
* `ios_settings` -
  (Optional)
  Settings for keys that can be used by iOS apps.
  
* `labels` -
  (Optional)
  See [Creating and managing labels](https://cloud.google.com/recaptcha-enterprise/docs/labels).
  
* `project` -
  (Optional)
  The project for the resource
  
* `testing_options` -
  (Optional)
  Options for user acceptance testing.
  
* `web_settings` -
  (Optional)
  Settings for keys that can be used by websites.
  


The `android_settings` block supports:
    
* `allow_all_package_names` -
  (Optional)
  If set to true, it means allowed_package_names will not be enforced.
    
* `allowed_package_names` -
  (Optional)
  Android package names of apps allowed to use the key. Example: 'com.companyname.appname'
    
The `ios_settings` block supports:
    
* `allow_all_bundle_ids` -
  (Optional)
  If set to true, it means allowed_bundle_ids will not be enforced.
    
* `allowed_bundle_ids` -
  (Optional)
  iOS bundle ids of apps allowed to use the key. Example: 'com.companyname.productname.appname'
    
The `testing_options` block supports:
    
* `testing_challenge` -
  (Optional)
  For challenge-based keys only (CHECKBOX, INVISIBLE), all challenge requests for this site will return nocaptcha if NOCAPTCHA, or an unsolvable challenge if UNSOLVABLE_CHALLENGE. Possible values: TESTING_CHALLENGE_UNSPECIFIED, NOCAPTCHA, UNSOLVABLE_CHALLENGE
    
* `testing_score` -
  (Optional)
  All assessments for this Key will return this score. Must be between 0 (likely not legitimate) and 1 (likely legitimate) inclusive.
    
The `web_settings` block supports:
    
* `allow_all_domains` -
  (Optional)
  If set to true, it means allowed_domains will not be enforced.
    
* `allow_amp_traffic` -
  (Optional)
  If set to true, the key can be used on AMP (Accelerated Mobile Pages) websites. This is supported only for the SCORE integration type.
    
* `allowed_domains` -
  (Optional)
  Domains or subdomains of websites allowed to use the key. All subdomains of an allowed domain are automatically allowed. A valid domain requires a host and must not include any path, port, query or fragment. Examples: 'example.com' or 'subdomain.example.com'
    
* `challenge_security_preference` -
  (Optional)
  Settings for the frequency and difficulty at which this key triggers captcha challenges. This should only be specified for IntegrationTypes CHECKBOX and INVISIBLE. Possible values: CHALLENGE_SECURITY_PREFERENCE_UNSPECIFIED, USABILITY, BALANCE, SECURITY
    
* `integration_type` -
  (Required)
  Required. Describes how this key is integrated with the website. Possible values: SCORE, CHECKBOX, INVISIBLE
    
## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `projects/{{project}}/keys/{{name}}`

* `create_time` -
  The timestamp corresponding to the creation of this Key.
  
* `name` -
  The resource name for the Key in the format "projects/{project}/keys/{key}".
  
## Timeouts

This resource provides the following
[Timeouts](/docs/configuration/resources.html#timeouts) configuration options:

- `create` - Default is 10 minutes.
- `update` - Default is 10 minutes.
- `delete` - Default is 10 minutes.

## Import

Key can be imported using any of these accepted formats:

```
$ terraform import google_recaptcha_enterprise_key.default projects/{{project}}/keys/{{name}}
$ terraform import google_recaptcha_enterprise_key.default {{project}}/{{name}}
$ terraform import google_recaptcha_enterprise_key.default {{name}}
```



