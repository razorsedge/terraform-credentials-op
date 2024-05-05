# terraform-credentials-op
A [Terraform credentials helper](https://developer.hashicorp.com/terraform/internals/credentials-helpers) for [1Password](https://1password.com/).

> Credentials helpers offer an alternative approach that allows you to customize how Terraform obtains credentials using an external program, which can then directly access an existing secrets management system in your organization.

## Installation:

1. Requires [jq](https://jqlang.github.io/jq/) to be installed.
2. Requires [1Password CLI](https://developer.1password.com/docs/cli/get-started/) to be installed and logged in to your account.
```
op signin
```

3. Download the `terraform-credentials-op` file from this repository, and copy it to your global plugins path `~/.terraform.d/plugins`.
```
# Run the following in a Bourne compatible shell (Linux and MacOS):
mkdir -p ~/.terraform.d/plugins/ && \
wget https://raw.githubusercontent.com/razorsedge/terraform-credentials-op/main/terraform-credentials-op \
 -O ~/.terraform.d/plugins/terraform-credentials-op && \
chmod +x ~/.terraform.d/plugins/terraform-credentials-op
```
4. Edit [your Terraform CLI configuration](https://www.terraform.io/docs/commands/cli-config.html) to enable the helper:
```
# Run the following in a Bourne compatible shell (Linux and MacOS):
echo "credentials_helper "op" {}" >>~/.terraformrc
```

## Usage:

1. Use [`terraform login`](https://www.terraform.io/docs/commands/login.html) to create a Terraform Cloud token and store it in your keychain.

```
$ terraform login
Terraform will request an API token for app.terraform.io using your browser.

If login is successful, Terraform will store the token in the configured
"op" credentials helper for use by subsequent commands.

Do you want to proceed?
  Only 'yes' will be accepted to confirm.

  Enter a value: yes


---------------------------------------------------------------------------------

Terraform must now open a web browser to the tokens page for app.terraform.io.

If a browser does not open this automatically, open the following URL to proceed:
    https://app.terraform.io/app/settings/tokens?source=terraform-login


---------------------------------------------------------------------------------

Generate a token using your browser, and copy-paste it into this prompt.

Terraform will store the token in the configured "op" credentials helper
for use by subsequent commands.

Token for app.terraform.io:
  Enter a value:


Retrieved token for user xxxxxx


---------------------------------------------------------------------------------

                                          -
                                          -----                           -
                                          ---------                      --
                                          ---------  -                -----
                                           ---------  ------        -------
                                             -------  ---------  ----------
                                                ----  ---------- ----------
                                                  --  ---------- ----------
   Welcome to Terraform Cloud!                     -  ---------- -------
                                                      ---  ----- ---
   Documentation: terraform.io/docs/cloud             --------   -
                                                      ----------
                                                      ----------
                                                       ---------
                                                           -----
                                                               -


   New to TFC? Follow these steps to instantly apply an example configuration:

   $ git clone https://github.com/hashicorp/tfc-getting-started.git
   $ cd tfc-getting-started
   $ scripts/setup.sh

```
2. You can remove the stored token with [`terraform logout`](https://www.terraform.io/docs/commands/logout.html).
```
$ terraform logout
Removing the stored credentials for app.terraform.io from the configured
"op" credentials helper.

Success! Terraform has removed the stored API token for app.terraform.io.

```
