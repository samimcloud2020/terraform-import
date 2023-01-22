# terraform-import
Let start import.
( so one look manually name of cloudtrail, its help for import)
resource "aws_cloudtrail" "foobar" {
  name                          = "unknown"
  s3_bucket_name                = "unknown"
  s3_key_prefix                 = "unknown"
}
-----------------------------------------------------------------------------------------

C:\Users\BSNL\terrafomsamim\import>terraform import aws_cloudtrail.foobar samim-cloudtrail-21012023
aws_cloudtrail.foobar: Importing from ID "samim-cloudtrail-21012023"...
aws_cloudtrail.foobar: Import prepared!
  Prepared aws_cloudtrail for import
aws_cloudtrail.foobar: Refreshing state... [id=samim-cloudtrail-21012023]

Import successful!

The resources that were imported are shown above. These resources are now in
your Terraform state and will henceforth be managed by Terraform.
---------------------------------------------------------------------------------------------
after that you see terraform.tfstate file cretaed and most option it retrived from aws.

-----------------------------------------------------------------------------
let check by terraform plan that any destroy of resourece will happen.

C:\Users\BSNL\terrafomsamim\import>terraform plan
aws_cloudtrail.foobar: Refreshing state... [id=samim-cloudtrail-21012023]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # aws_cloudtrail.foobar must be replaced
-/+ resource "aws_cloudtrail" "foobar" {
      ~ arn                           = "arn:aws:cloudtrail:us-east-1:291222035571:trail/samim-cloudtrail-21012023" -> (known after apply)
      ~ home_region                   = "us-east-1" -> (known after apply)
      ~ id                            = "samim-cloudtrail-21012023" -> (known after apply)
      ~ include_global_service_events = false -> true
      ~ name                          = "samim-cloudtrail-21012023" -> "unknown" # forces replacement   <---------------FORCE REPLACEMENT SEEN
      ~ s3_bucket_name                = "cloudtrail-samim-rourkela" -> "unknown"
      ~ s3_key_prefix                 = "prefix" -> "unknown"
      - tags                          = {} -> null
      ~ tags_all                      = {} -> (known after apply)
        # (4 unchanged attributes hidden)
    }

Plan: 1 to add, 0 to change, 1 to destroy.   <--------------------------------------SEE ONE DESTROY SEEN

──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.


NOW LET ADD THE NAME OF CLOUDTRAIL

resource "aws_cloudtrail" "foobar" {
  name                          = "samim-cloudtrail-21012023"   <-----------------------------ADDED manually in main.tf
  s3_bucket_name                = "unknown"
  s3_key_prefix                 = "unknown"
}

-------------------------------------------------------------------------------------------------------------------
let now do terraform plan

C:\Users\BSNL\terrafomsamim\import>terraform plan
aws_cloudtrail.foobar: Refreshing state... [id=samim-cloudtrail-21012023]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  ~ update in-place

Terraform will perform the following actions:

  # aws_cloudtrail.foobar will be updated in-place
  ~ resource "aws_cloudtrail" "foobar" {
        id                            = "samim-cloudtrail-21012023"
      ~ include_global_service_events = false -> true
        name                          = "samim-cloudtrail-21012023"
      ~ s3_bucket_name                = "cloudtrail-samim-rourkela" -> "unknown"     <----------------------let set in main.tf
      ~ s3_key_prefix                 = "prefix" -> "unknown"
        tags                          = {}
        # (7 unchanged attributes hidden)
    }

Plan: 0 to add, 1 to change, 0 to destroy.   <-----------

──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
--------------------------------------------------------------------------------

resource "aws_cloudtrail" "foobar" {
  name                          = "samim-cloudtrail-21012023"
  s3_bucket_name                = "cloudtrail-samim-rourkela"
  s3_key_prefix                 = "unknown"
}

C:\Users\BSNL\terrafomsamim\import>terraform plan
aws_cloudtrail.foobar: Refreshing state... [id=samim-cloudtrail-21012023]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  ~ update in-place

Terraform will perform the following actions:

  # aws_cloudtrail.foobar will be updated in-place
  ~ resource "aws_cloudtrail" "foobar" {
        id                            = "samim-cloudtrail-21012023"
      ~ include_global_service_events = false -> true
        name                          = "samim-cloudtrail-21012023"
      ~ s3_key_prefix                 = "prefix" -> "unknown"            <-----------------------let set in main.tf
        tags                          = {}
        # (8 unchanged attributes hidden)
    }

Plan: 0 to add, 1 to change, 0 to destroy.  <---------
------------------------------------------------------------
resource "aws_cloudtrail" "foobar" {
  name                          = "samim-cloudtrail-21012023"
  s3_bucket_name                = "cloudtrail-samim-rourkela"
  s3_key_prefix                 = "prefix"
}

C:\Users\BSNL\terrafomsamim\import>terraform plan
aws_cloudtrail.foobar: Refreshing state... [id=samim-cloudtrail-21012023]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  ~ update in-place

Terraform will perform the following actions:

  # aws_cloudtrail.foobar will be updated in-place
  ~ resource "aws_cloudtrail" "foobar" {
        id                            = "samim-cloudtrail-21012023"
      ~ include_global_service_events = false -> true               <-----------------------------its false to true, let add in main.tf
        name                          = "samim-cloudtrail-21012023"
        tags                          = {}
        # (9 unchanged attributes hidden)
    }

Plan: 0 to add, 1 to change, 0 to destroy.

resource "aws_cloudtrail" "foobar" {
  name                          = "samim-cloudtrail-21012023"
  s3_bucket_name                = "cloudtrail-samim-rourkela"
  s3_key_prefix                 = "prefix"
  include_global_service_events = "false"
}

---------------------again do terraform plan--------------------
C:\Users\BSNL\terrafomsamim\import>terraform plan
aws_cloudtrail.foobar: Refreshing state... [id=samim-cloudtrail-21012023]

No changes. Your infrastructure matches the configuration.

Terraform has compared your real infrastructure against your configuration and found no differences, so no changes are needed.

