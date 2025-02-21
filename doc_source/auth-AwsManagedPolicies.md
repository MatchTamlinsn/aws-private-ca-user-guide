# AWS managed policies<a name="auth-AwsManagedPolicies"></a>

AWS Private CA includes a set of predefined AWS managed policies for AWS Private CA administrators, users, and auditors\. Understanding these policies can help you implement [Customer managed policies](auth-CustManagedPolicies.md)\.

Choose any of the policies listed below to see details and sample policy code\.

## AWSPrivateCAFullAccess<a name="AWSPrivateCAFullAccess"></a>

Grants unrestricted administrative control\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Action":[
            "acm-pca:*"
         ],
         "Resource":"*"
      }
   ]
}
```

## AWSPrivateCAReadOnly<a name="AWSPrivateCAFullAccess"></a>

Grants access limited to read\-only API operations\.

```
{
   "Version":"2012-10-17",
   "Statement":{
      "Effect":"Allow",
      "Action":[
         "acm-pca:DescribeCertificateAuthority",
         "acm-pca:DescribeCertificateAuthorityAuditReport",
         "acm-pca:ListCertificateAuthorities",
         "acm-pca:GetCertificateAuthorityCsr",
         "acm-pca:GetCertificateAuthorityCertificate",
         "acm-pca:GetCertificate",
         "acm-pca:ListPermissions",
         "acm-pca:ListTags"
      ],
      "Resource":"*"
   }
}
```

## AWSPrivateCAPrivilegedUser<a name="AWSPrivateCAFullAccess"></a>

Grants ability to issue and revoke CA certificates\. This policy has no other administrative capabilities and no ability to issue end\-entity certificates\. Permissions are mutually exclusive with the **User** policy\. 

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Action":[
            "acm-pca:IssueCertificate"
         ],
         "Resource":"arn:aws:acm-pca:*:*:certificate-authority/*",
         "Condition":{
            "StringLike":{
               "acm-pca:TemplateArn":[
                  "arn:aws:acm-pca:::template/*CACertificate*/V*"
               ]
            }
         }
      },
      {
         "Effect":"Deny",
         "Action":[
            "acm-pca:IssueCertificate"
         ],
         "Resource":"arn:aws:acm-pca:*:*:certificate-authority/*",
         "Condition":{
            "StringNotLike":{
               "acm-pca:TemplateArn":[
                  "arn:aws:acm-pca:::template/*CACertificate*/V*"
               ]
            }
         }
      },
      {
         "Effect":"Allow",
         "Action":[
            "acm-pca:RevokeCertificate",
            "acm-pca:GetCertificate",
            "acm-pca:ListPermissions"
         ],
         "Resource":"arn:aws:acm-pca:*:*:certificate-authority/*"
      },
      {
         "Effect":"Allow",
         "Action":[
            "acm-pca:ListCertificateAuthorities"
         ],
         "Resource":"*"
      }
   ]
}
```

## AWSPrivateCAUser<a name="AWSPrivateCAUser"></a>

Grant ability to issue and revoke end\-entity certificates\. This policy has no administrative capabilities and no ability to issue CA certificates\. Permissions are mutually exclusive with the **PrivilegedUser** policy\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Action":[
            "acm-pca:IssueCertificate"
         ],
         "Resource":"arn:aws:acm-pca:*:*:certificate-authority/*",
         "Condition":{
            "StringLike":{
               "acm-pca:TemplateArn":[
                  "arn:aws:acm-pca:::template/EndEntityCertificate/V*"
               ]
            }
         }
      },
      {
         "Effect":"Deny",
         "Action":[
            "acm-pca:IssueCertificate"
         ],
         "Resource":"arn:aws:acm-pca:*:*:certificate-authority/*",
         "Condition":{
            "StringNotLike":{
               "acm-pca:TemplateArn":[
                  "arn:aws:acm-pca:::template/EndEntityCertificate/V*"
               ]
            }
         }
      },
      {
         "Effect":"Allow",
         "Action":[
            "acm-pca:RevokeCertificate",
            "acm-pca:GetCertificate",
            "acm-pca:ListPermissions"
         ],
         "Resource":"arn:aws:acm-pca:*:*:certificate-authority/*"
      },
      {
         "Effect":"Allow",
         "Action":[
            "acm-pca:ListCertificateAuthorities"
         ],
         "Resource":"*"
      }
   ]
}
```

## AWSPrivateCAAuditor<a name="AWSPrivateCAAuditor"></a>

Grant access to read\-only API operations and permission to generate a CA audit report\. 

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Action":[
            "acm-pca:CreateCertificateAuthorityAuditReport",
            "acm-pca:DescribeCertificateAuthority",
            "acm-pca:DescribeCertificateAuthorityAuditReport",
            "acm-pca:GetCertificateAuthorityCsr",
            "acm-pca:GetCertificateAuthorityCertificate",
            "acm-pca:GetCertificate",
            "acm-pca:ListPermissions",
            "acm-pca:ListTags"
         ],
         "Resource":"arn:aws:acm-pca:*:*:certificate-authority/*"
      },
      {
         "Effect":"Allow",
         "Action":[
            "acm-pca:ListCertificateAuthorities"
         ],
         "Resource":"*"
      }
   ]
}
```

## Updates to AWS managed policies for AWS Private CA<a name="managed-policy-updates"></a>

In the following table, view details about updates to AWS managed policies for AWS Private CA since the service began tracking these changes\. For automatic alerts about all changes to AWS Private CA, subscribe to the RSS feed on the [Document History](dochistory.md) page\.


**Managed policy changes**  

| Change | Description  | Date | 
| --- | --- | --- | 
|  `AWSPrivateCAUser` policy added\.  |  Replaces `AWSCertificateManagerPrivateCAUser`\. Functionality is unchanged\.  |  September 27, 2022  | 
|  `AWSCertificateManagerPrivateCAUser` policy deprecated\.  |  Policy has out\-of\-date service name\.  |  September 27, 2022  | 