<!-- markdownlint-disable -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 2.0 |
| <a name="requirement_local"></a> [local](#requirement\_local) | >= 1.2 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 2.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_dns"></a> [dns](#module\_dns) | cloudposse/route53-alias/aws | 0.12.0 |
| <a name="module_logs"></a> [logs](#module\_logs) | cloudposse/s3-log-storage/aws | 0.21.0 |
| <a name="module_origin_label"></a> [origin\_label](#module\_origin\_label) | cloudposse/label/null | 0.24.1 |
| <a name="module_this"></a> [this](#module\_this) | cloudposse/label/null | 0.24.1 |

## Resources

| Name | Type |
|------|------|
| [aws_cloudfront_distribution.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudfront_distribution) | resource |
| [aws_cloudfront_origin_access_identity.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudfront_origin_access_identity) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_acm_certificate_arn"></a> [acm\_certificate\_arn](#input\_acm\_certificate\_arn) | Existing ACM Certificate ARN | `string` | `""` | no |
| <a name="input_additional_tag_map"></a> [additional\_tag\_map](#input\_additional\_tag\_map) | Additional tags for appending to tags\_as\_list\_of\_maps. Not added to `tags`. | `map(string)` | `{}` | no |
| <a name="input_aliases"></a> [aliases](#input\_aliases) | List of aliases. CAUTION! Names MUSTN'T contain trailing `.` | `list(string)` | `[]` | no |
| <a name="input_allowed_methods"></a> [allowed\_methods](#input\_allowed\_methods) | List of allowed methods (e.g. ` GET, PUT, POST, DELETE, HEAD`) for AWS CloudFront | `list(string)` | <pre>[<br>  "DELETE",<br>  "GET",<br>  "HEAD",<br>  "OPTIONS",<br>  "PATCH",<br>  "POST",<br>  "PUT"<br>]</pre> | no |
| <a name="input_attributes"></a> [attributes](#input\_attributes) | Additional attributes (e.g. `1`) | `list(string)` | `[]` | no |
| <a name="input_cache_policy_id"></a> [cache\_policy\_id](#input\_cache\_policy\_id) | ID of the cache policy attached to the cache behavior | `string` | `null` | no |
| <a name="input_cached_methods"></a> [cached\_methods](#input\_cached\_methods) | List of cached methods (e.g. ` GET, PUT, POST, DELETE, HEAD`) | `list(string)` | <pre>[<br>  "GET",<br>  "HEAD"<br>]</pre> | no |
| <a name="input_comment"></a> [comment](#input\_comment) | Comment for the origin access identity | `string` | `"Managed by Terraform"` | no |
| <a name="input_compress"></a> [compress](#input\_compress) | Whether you want CloudFront to automatically compress content for web requests that include Accept-Encoding: gzip in the request header (default: false) | `bool` | `false` | no |
| <a name="input_context"></a> [context](#input\_context) | Single object for setting entire context at once.<br>See description of individual variables for details.<br>Leave string and numeric variables as `null` to use default value.<br>Individual variable settings (non-null) override settings in context object,<br>except for attributes, tags, and additional\_tag\_map, which are merged. | `any` | <pre>{<br>  "additional_tag_map": {},<br>  "attributes": [],<br>  "delimiter": null,<br>  "enabled": true,<br>  "environment": null,<br>  "id_length_limit": null,<br>  "label_key_case": null,<br>  "label_order": [],<br>  "label_value_case": null,<br>  "name": null,<br>  "namespace": null,<br>  "regex_replace_chars": null,<br>  "stage": null,<br>  "tags": {}<br>}</pre> | no |
| <a name="input_custom_error_response"></a> [custom\_error\_response](#input\_custom\_error\_response) | List of one or more custom error response element maps | <pre>list(object({<br>    error_caching_min_ttl = string<br>    error_code            = string<br>    response_code         = string<br>    response_page_path    = string<br>  }))</pre> | `[]` | no |
| <a name="input_custom_header"></a> [custom\_header](#input\_custom\_header) | List of one or more custom headers passed to the origin | <pre>list(object({<br>    name  = string<br>    value = string<br>  }))</pre> | `[]` | no |
| <a name="input_custom_origins"></a> [custom\_origins](#input\_custom\_origins) | One or more custom origins for this distribution (multiples allowed). See documentation for configuration options description https://www.terraform.io/docs/providers/aws/r/cloudfront_distribution.html#origin-arguments | <pre>list(object({<br>    domain_name = string<br>    origin_id   = string<br>    origin_path = string<br>    custom_headers = list(object({<br>      name  = string<br>      value = string<br>    }))<br>    custom_origin_config = object({<br>      http_port                = number<br>      https_port               = number<br>      origin_protocol_policy   = string<br>      origin_ssl_protocols     = list(string)<br>      origin_keepalive_timeout = number<br>      origin_read_timeout      = number<br>    })<br>    s3_origin_config = object({<br>      origin_access_identity = string<br>    })<br>  }))</pre> | `[]` | no |
| <a name="input_default_root_object"></a> [default\_root\_object](#input\_default\_root\_object) | Object that CloudFront return when requests the root URL | `string` | `"index.html"` | no |
| <a name="input_default_ttl"></a> [default\_ttl](#input\_default\_ttl) | Default amount of time (in seconds) that an object is in a CloudFront cache | `number` | `60` | no |
| <a name="input_delimiter"></a> [delimiter](#input\_delimiter) | Delimiter to be used between `namespace`, `environment`, `stage`, `name` and `attributes`.<br>Defaults to `-` (hyphen). Set to `""` to use no delimiter at all. | `string` | `null` | no |
| <a name="input_distribution_enabled"></a> [distribution\_enabled](#input\_distribution\_enabled) | Set to `true` if you want CloudFront to begin processing requests as soon as the distribution is created, or to false if you do not want CloudFront to begin processing requests after the distribution is created. | `bool` | `true` | no |
| <a name="input_dns_aliases_enabled"></a> [dns\_aliases\_enabled](#input\_dns\_aliases\_enabled) | Set to false to prevent dns records for aliases from being created | `bool` | `true` | no |
| <a name="input_enabled"></a> [enabled](#input\_enabled) | Set to false to prevent the module from creating any resources | `bool` | `null` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment, e.g. 'uw2', 'us-west-2', OR 'prod', 'staging', 'dev', 'UAT' | `string` | `null` | no |
| <a name="input_forward_cookies"></a> [forward\_cookies](#input\_forward\_cookies) | Specifies whether you want CloudFront to forward cookies to the origin. Valid options are all, none or whitelist | `string` | `"none"` | no |
| <a name="input_forward_cookies_whitelisted_names"></a> [forward\_cookies\_whitelisted\_names](#input\_forward\_cookies\_whitelisted\_names) | List of forwarded cookie names | `list(string)` | `[]` | no |
| <a name="input_forward_headers"></a> [forward\_headers](#input\_forward\_headers) | Specifies the Headers, if any, that you want CloudFront to vary upon for this cache behavior. Specify `*` to include all headers. | `list(string)` | `[]` | no |
| <a name="input_forward_query_string"></a> [forward\_query\_string](#input\_forward\_query\_string) | Forward query strings to the origin that is associated with this cache behavior | `bool` | `false` | no |
| <a name="input_geo_restriction_locations"></a> [geo\_restriction\_locations](#input\_geo\_restriction\_locations) | List of country codes for which CloudFront either to distribute content (whitelist) or not distribute your content (blacklist) | `list(string)` | `[]` | no |
| <a name="input_geo_restriction_type"></a> [geo\_restriction\_type](#input\_geo\_restriction\_type) | Method that use to restrict distribution of your content by country: `none`, `whitelist`, or `blacklist` | `string` | `"none"` | no |
| <a name="input_id_length_limit"></a> [id\_length\_limit](#input\_id\_length\_limit) | Limit `id` to this many characters (minimum 6).<br>Set to `0` for unlimited length.<br>Set to `null` for default, which is `0`.<br>Does not affect `id_full`. | `number` | `null` | no |
| <a name="input_is_ipv6_enabled"></a> [is\_ipv6\_enabled](#input\_is\_ipv6\_enabled) | State of CloudFront IPv6 | `bool` | `true` | no |
| <a name="input_label_key_case"></a> [label\_key\_case](#input\_label\_key\_case) | The letter case of label keys (`tag` names) (i.e. `name`, `namespace`, `environment`, `stage`, `attributes`) to use in `tags`.<br>Possible values: `lower`, `title`, `upper`.<br>Default value: `title`. | `string` | `null` | no |
| <a name="input_label_order"></a> [label\_order](#input\_label\_order) | The naming order of the id output and Name tag.<br>Defaults to ["namespace", "environment", "stage", "name", "attributes"].<br>You can omit any of the 5 elements, but at least one must be present. | `list(string)` | `null` | no |
| <a name="input_label_value_case"></a> [label\_value\_case](#input\_label\_value\_case) | The letter case of output label values (also used in `tags` and `id`).<br>Possible values: `lower`, `title`, `upper` and `none` (no transformation).<br>Default value: `lower`. | `string` | `null` | no |
| <a name="input_log_bucket_fqdn"></a> [log\_bucket\_fqdn](#input\_log\_bucket\_fqdn) | Optional fqdn of logging bucket, if not supplied a bucket will be generated. | `string` | `""` | no |
| <a name="input_log_expiration_days"></a> [log\_expiration\_days](#input\_log\_expiration\_days) | Number of days after which to expunge the objects | `number` | `90` | no |
| <a name="input_log_force_destroy"></a> [log\_force\_destroy](#input\_log\_force\_destroy) | Applies to log bucket created by this module only. If true, all objects will be deleted from the bucket on destroy, so that the bucket can be destroyed without error. These objects are not recoverable. | `bool` | `false` | no |
| <a name="input_log_glacier_transition_days"></a> [log\_glacier\_transition\_days](#input\_log\_glacier\_transition\_days) | Number of days after which to move the data to the glacier storage tier | `number` | `60` | no |
| <a name="input_log_include_cookies"></a> [log\_include\_cookies](#input\_log\_include\_cookies) | Include cookies in access logs | `bool` | `false` | no |
| <a name="input_log_prefix"></a> [log\_prefix](#input\_log\_prefix) | Path of logs in S3 bucket | `string` | `""` | no |
| <a name="input_log_standard_transition_days"></a> [log\_standard\_transition\_days](#input\_log\_standard\_transition\_days) | Number of days to persist in the standard storage tier before moving to the glacier tier | `number` | `30` | no |
| <a name="input_logging_enabled"></a> [logging\_enabled](#input\_logging\_enabled) | When true, access logs will be sent to a newly created s3 bucket | `bool` | `true` | no |
| <a name="input_max_ttl"></a> [max\_ttl](#input\_max\_ttl) | Maximum amount of time (in seconds) that an object is in a CloudFront cache | `number` | `31536000` | no |
| <a name="input_min_ttl"></a> [min\_ttl](#input\_min\_ttl) | Minimum amount of time that you want objects to stay in CloudFront caches | `number` | `0` | no |
| <a name="input_name"></a> [name](#input\_name) | Solution name, e.g. 'app' or 'jenkins' | `string` | `null` | no |
| <a name="input_namespace"></a> [namespace](#input\_namespace) | Namespace, which could be your organization name or abbreviation, e.g. 'eg' or 'cp' | `string` | `null` | no |
| <a name="input_ordered_cache"></a> [ordered\_cache](#input\_ordered\_cache) | An ordered list of cache behaviors resource for this distribution. List from top to bottom in order of precedence. The topmost cache behavior will have precedence 0.<br>The fields can be described by the other variables in this file. For example, the field 'lambda\_function\_association' in this object has<br>a description in var.lambda\_function\_association variable earlier in this file. The only difference is that fields on this object are in ordered caches, whereas the rest<br>of the vars in this file apply only to the default cache. Put value `""` on field `target_origin_id` to specify default s3 bucket origin. | <pre>list(object({<br>    target_origin_id = string<br>    path_pattern     = string<br><br>    allowed_methods          = list(string)<br>    cached_methods           = list(string)<br>    cache_policy_id          = string<br>    origin_request_policy_id = string<br>    compress                 = bool<br><br>    viewer_protocol_policy = string<br>    min_ttl                = number<br>    default_ttl            = number<br>    max_ttl                = number<br><br>    forward_query_string  = bool<br>    forward_header_values = list(string)<br>    forward_cookies       = string<br><br>    lambda_function_association = list(object({<br>      event_type   = string<br>      include_body = bool<br>      lambda_arn   = string<br>    }))<br>  }))</pre> | `[]` | no |
| <a name="input_origin_domain_name"></a> [origin\_domain\_name](#input\_origin\_domain\_name) | The DNS domain name of your custom origin (e.g. website) | `string` | `""` | no |
| <a name="input_origin_http_port"></a> [origin\_http\_port](#input\_origin\_http\_port) | The HTTP port the custom origin listens on | `number` | `"80"` | no |
| <a name="input_origin_https_port"></a> [origin\_https\_port](#input\_origin\_https\_port) | The HTTPS port the custom origin listens on | `number` | `443` | no |
| <a name="input_origin_keepalive_timeout"></a> [origin\_keepalive\_timeout](#input\_origin\_keepalive\_timeout) | The Custom KeepAlive timeout, in seconds. By default, AWS enforces a limit of 60. But you can request an increase. | `number` | `60` | no |
| <a name="input_origin_path"></a> [origin\_path](#input\_origin\_path) | An optional element that causes CloudFront to request your content from a directory in your Amazon S3 bucket or your custom origin. It must begin with a /. Do not add a / at the end of the path. | `string` | `""` | no |
| <a name="input_origin_protocol_policy"></a> [origin\_protocol\_policy](#input\_origin\_protocol\_policy) | The origin protocol policy to apply to your origin. One of http-only, https-only, or match-viewer | `string` | `"match-viewer"` | no |
| <a name="input_origin_read_timeout"></a> [origin\_read\_timeout](#input\_origin\_read\_timeout) | The Custom Read timeout, in seconds. By default, AWS enforces a limit of 60. But you can request an increase. | `number` | `60` | no |
| <a name="input_origin_request_policy_id"></a> [origin\_request\_policy\_id](#input\_origin\_request\_policy\_id) | ID of the origin request policy attached to the cache behavior | `string` | `null` | no |
| <a name="input_origin_ssl_protocols"></a> [origin\_ssl\_protocols](#input\_origin\_ssl\_protocols) | The SSL/TLS protocols that you want CloudFront to use when communicating with your origin over HTTPS | `list(string)` | <pre>[<br>  "TLSv1",<br>  "TLSv1.1",<br>  "TLSv1.2"<br>]</pre> | no |
| <a name="input_parent_zone_id"></a> [parent\_zone\_id](#input\_parent\_zone\_id) | ID of the hosted zone to contain this record (or specify `parent_zone_name`) | `string` | `""` | no |
| <a name="input_parent_zone_name"></a> [parent\_zone\_name](#input\_parent\_zone\_name) | Name of the hosted zone to contain this record (or specify `parent_zone_id`) | `string` | `""` | no |
| <a name="input_price_class"></a> [price\_class](#input\_price\_class) | Price class for this distribution: `PriceClass_All`, `PriceClass_200`, `PriceClass_100` | `string` | `"PriceClass_100"` | no |
| <a name="input_regex_replace_chars"></a> [regex\_replace\_chars](#input\_regex\_replace\_chars) | Regex to replace chars with empty string in `namespace`, `environment`, `stage` and `name`.<br>If not set, `"/[^a-zA-Z0-9-]/"` is used to remove all characters other than hyphens, letters and digits. | `string` | `null` | no |
| <a name="input_stage"></a> [stage](#input\_stage) | Stage, e.g. 'prod', 'staging', 'dev', OR 'source', 'build', 'test', 'deploy', 'release' | `string` | `null` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | Additional tags (e.g. `map('BusinessUnit','XYZ')` | `map(string)` | `{}` | no |
| <a name="input_trusted_signers"></a> [trusted\_signers](#input\_trusted\_signers) | List of AWS account IDs (or self) that you want to allow to create signed URLs for private content | `list(string)` | `[]` | no |
| <a name="input_viewer_minimum_protocol_version"></a> [viewer\_minimum\_protocol\_version](#input\_viewer\_minimum\_protocol\_version) | The minimum version of the SSL protocol that you want CloudFront to use for HTTPS connections. | `string` | `"TLSv1"` | no |
| <a name="input_viewer_protocol_policy"></a> [viewer\_protocol\_policy](#input\_viewer\_protocol\_policy) | allow-all, redirect-to-https | `string` | `"redirect-to-https"` | no |
| <a name="input_web_acl_id"></a> [web\_acl\_id](#input\_web\_acl\_id) | ID of the AWS WAF web ACL that is associated with the distribution | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_cf_aliases"></a> [cf\_aliases](#output\_cf\_aliases) | Extra CNAMEs of AWS CloudFront |
| <a name="output_cf_arn"></a> [cf\_arn](#output\_cf\_arn) | ARN of CloudFront distribution |
| <a name="output_cf_domain_name"></a> [cf\_domain\_name](#output\_cf\_domain\_name) | Domain name corresponding to the distribution |
| <a name="output_cf_etag"></a> [cf\_etag](#output\_cf\_etag) | Current version of the distribution's information |
| <a name="output_cf_hosted_zone_id"></a> [cf\_hosted\_zone\_id](#output\_cf\_hosted\_zone\_id) | CloudFront Route 53 Zone ID |
| <a name="output_cf_id"></a> [cf\_id](#output\_cf\_id) | ID of CloudFront distribution |
| <a name="output_cf_origin_access_identity"></a> [cf\_origin\_access\_identity](#output\_cf\_origin\_access\_identity) | A shortcut to the full path for the origin access identity to use in CloudFront |
| <a name="output_cf_status"></a> [cf\_status](#output\_cf\_status) | Current status of the distribution |
| <a name="output_logs"></a> [logs](#output\_logs) | Logs resource |
<!-- markdownlint-restore -->
