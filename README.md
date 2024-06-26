# terraform-provider-lastpass 
[![release](https://img.shields.io/github/release/neticdk/terraform-provider-lastpass.svg?style=flat-square)](https://github.com/neticdk/terraform-provider-lastpass/releases/latest) [![Go Report Card](https://goreportcard.com/badge/github.com/neticdk/terraform-provider-lastpass)](https://goreportcard.com/report/github.com/neticdk/terraform-provider-lastpass) [![GoDoc](https://godoc.org/github.com/github.com/neticdk/terraform-provider-lastpass/lastpass?status.svg)](https://godoc.org/github.com/neticdk/terraform-provider-lastpass/lastpass)

<img src="https://www.vectorlogo.zone/logos/terraformio/terraformio-ar21.svg" width="400px">

The Lastpass provider is used to read, manage, or destroy secrets inside Lastpass. Goodbye secret .tfvars files 👋

⚠️ **Warning**: This provider uses an unofficial LastPass API. With that comes the unfortunate risk of Lastpass releasing breaking changes without previous notice.

```hcl
terraform {
  required_providers {
    random = {
      source = "hashicorp/random"
      version = "3.1.0"
    }
    lastpass = {
      source = "neticdk/lastpass"
      version = "~> 1.0"
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

data "lastpass_secret" "mysecret" {
    id = resource.lastpass_secret.mysecret.id
}

```

Documentation and examples can be found inside the Terraform registry:

- [Terraform Registry](https://registry.terraform.io/providers/neticdk/lastpass/latest)
- [Documentation](https://registry.terraform.io/providers/neticdk/lastpass/latest/docs)
 
## License

[Apache](LICENSE)
