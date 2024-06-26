---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "lastpass Provider"
subcategory: ""
description: |-
  
---

# Lastpass Provider

The Lastpass provider is used to read, manage, or destroy secrets inside Lastpass. Goodbye secret .tfvars files 👋

⚠️ **Warning**: This provider uses an unofficial LastPass API. With that comes the unfortunate risk of Lastpass releasing breaking changes without previous notice.

If you use two-factor authentication (recommended) you must remember to set the one-time password: 

```bash
$ LASTPASS_ONETIME_PASSWORD=017968 terraform plan
```

If you enable `trust` you will only need to set the one-time password during first login. Subsequent logins to not require multifactor authentication.

## Example Usage

```hcl
terraform {
  required_providers {
    random = {
      source = "hashicorp/random"
      version = "3.1.0"
    }
    lastpass = {
      source = "neticdk/lastpass"
      version = ">= 1.0.0"
    }
  }
}

provider lastpass {
  baseurl = "https://lastpass.eu"
  trust = true
  enable_2fa = true
}

resource "random_password" "pw" {
  length = 32
  special = false
}

resource "lastpass_secret" "mysecret" {
    name = "My site"
    username = "foobar"
    password = random_password.pw.result
    share = "Shared-TeamX"
    url = "https://example.com"
    notes = <<EOF
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam sed elit nec orci
cursus rhoncus. Morbi lacus turpis, volutpat in lobortis vel, mattis nec magna.
Cras gravida libero vitae nisl iaculis ultrices. Fusce odio ligula, pharetra ac
viverra semper, consequat quis risus.
EOF
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **username** (String) Lastpass login e-mail. Env `LASTPASS_USER`
- **password** (String, Sensitive) Lastpass login password. Env `LASTPASS_PASSWORD`

### Optional

- **baseurl** (String) Base URL https://lastpass.com or https://lastpass.eu. 
  - Env variable `LASTPASS_BASEURL`
  - Default `https://lastpass.com`
- **configdir** (String) Path where the provider stores its trust ID. Env 
  - Env variable `LASTPASS_CONFIGDIR`
  - Default `$HOME/.terraform-provider-lastpass`
- **enable_2fa** (Boolean) enable two-factor authentication: LastPass Authenticator, Google Authenticator, Microsoft Authenticator, YubiKey, Transakt, Duo Security, or Sesame. 
  - Env variable `LASTPASS_ENABLE_2FA`
  - Default `true`
- **onetime_password** (String, Sensitive) one-time password for 2fa.
  - Env variable `LASTPASS_ONETIME_PASSWORD`
- **trust** (Boolean) Trust will cause subsequent logins to not require multifactor authentication. Trust lasts for 30 days.
  - Env variable `LASTPASS_TRUST`
  - Default `false`
