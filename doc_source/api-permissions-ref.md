# AWS Data Exchange API permissions: actions and resources reference<a name="api-permissions-ref"></a>

Use the following table as a reference when you are setting up [Access control](access-control.md) and writing a permissions policy that you can attach to an AWS Identity and Access Management \(IAM\) identity \(identity\-based policies\)\. The table lists each AWS Data Exchange API operation, the actions for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field\. You specify the resource value in the policy's `Resource` field\. 

**Note**  
To specify an action, use the `dataexchange:` prefix followed by the API operation name \(for example, `dataexchange:CreateDataSet`\)\.


**AWS Data Exchange API and required permissions for actions**  

| AWS Data Exchange API operations | Required permissions \(API actions\) | Resources | Conditions | 
| --- | --- | --- | --- | 
| CreateDataSet | dataexchange:CreateDataSet | N/A |  `aws:TagKeys` `aws:RequestTag`  | 
| GetDataSet | dataexchange:GetDataSet | Data set |  aws:RequestTag | 
| UpdateDataSet | dataexchange:UpdateDataSet | Data set |  aws:RequestTag | 
| DeleteDataSet | dataexchange:DeleteDataSet | Data set | aws:RequestTag | 
| ListDataSets | dataexchange:ListDataSets | N/A | N/A | 
| CreateRevision | dataexchange:CreateRevision | Data set |  `aws:TagKeys` `aws:RequestTag`  | 
| GetRevision | dataexchange:GetRevision |  Revision  | aws:RequestTag | 
| DeleteRevision | dataexchange:DeleteRevision |  Revision  | aws:RequestTag | 
| ListDataSetRevisions | dataexchange:ListDataSetRevisions | Data set | aws:RequestTag | 
| ListRevisionAssets | dataexchange:ListRevisionAssets |  Revision  | aws:RequestTag | 
| CreateEventAction | dataexchange:CreateEventAction | N/A | N/A | 
| UpdateEventAction | dataexchange:UpdateEventAction |  EventAction  | N/A | 
| GetEventAction | dataexchange:GetEventAction |  EventAction  | N/A | 
| ListEventActions | dataexchange:ListEventActions | N/A | N/A | 
| DeleteEventAction | dataexchange:DeleteEventAction |  EventAction  | N/A | 
| CreateJob | dataexchange:CreateJob | N/A | dataexchange:JobType | 
| GetJob | dataexchange:GetJob | Job | dataexchange:JobType | 
| StartJob\*\* | dataexchange:StartJob | Job | dataexchange:JobType | 
| CancelJob | dataexchange:CancelJob | Job | dataexchange:JobType | 
| ListJobs | dataexchange:ListJobs | N/A | N/A | 
| ListTagsForResource | dataexchange:ListTagsForResource |  Revision  | aws:RequestTag | 
| TagResource | dataexchange:TagResource |  Revision  |  `aws:TagKeys` `aws:RequestTag`  | 
| UnTagResource | dataexchange:UnTagResource |  Revision  |  `aws:TagKeys` `aws:RequestTag`  | 
| UpdateRevision | dataexchange:UpdateRevision |  Revision  | aws:RequestTag | 
| DeleteAsset | dataexchange:DeleteAsset |  Asset  | N/A | 
| GetAsset | dataexchange:GetAsset |  Asset  | N/A | 
| UpdateAsset | dataexchange:UpdateAsset |  Asset  | N/A | 
| SendApiAsset | dataexchange:SendApiAsset |  Asset  | N/A | 

**\*\*** Additional IAM permissions might be needed depending on the type of the job you are starting\. See the following table for the AWS Data Exchange job types and associated additional IAM permissions\. For more information about jobs, see [Jobs in AWS Data Exchange](jobs.md)\.

**Note**  
Currently, the `SendApiAsset` operation is not supported for the following SDKs:  
AWS SDK for \.NET
AWS SDK for C\+\+
SDK for Java 2\.x


**AWS Data Exchange job type permissions for `StartJob`**  

| Job type | Additional IAM permissions needed | 
| --- | --- | 
| IMPORT\_ASSETS\_FROM\_S3 | dataexchange:CreateAsset | 
| IMPORT\_ASSET\_FROM\_SIGNED\_URL | dataexchange:CreateAsset | 
| IMPORT\_ASSETS\_FROM\_API\_GATEWAY\_API | dataexchange:CreateAsset | 
| IMPORT\_ASSETS\_FROM\_REDSHIFT\_DATA\_SHARES | dataexchange:CreateAsset, redshift:AuthorizeDataShare | 
| EXPORT\_ASSETS\_TO\_S3 | dataexchange:GetAsset | 
| EXPORT\_ASSETS\_TO\_SIGNED\_URL | dataexchange:GetAsset | 
| EXPORT\_REVISIONS\_TO\_S3 | dataexchange:GetRevision | 

You can scope data set actions to the revision or asset level through the use of wildcards, as in the following example\.

```
arn:aws:dataexchange:us-east-1:123456789012:data-sets/99EXAMPLE23c7c272897cf1EXAMPLE7a/revisions/*/assets/*
```

Some AWS Data Exchange actions can only be performed on the AWS Data Exchange console\. These actions are integrated with AWS Marketplace functionality\. The actions require the AWS Marketplace permissions shown in the following table\.


**AWS Data Exchange console\-only actions for subscribers**  

| Console action | IAM permission | 
| --- | --- | 
| Subscribe to a product | aws\-marketplace:Subscribe | 
| Send subscription verification request | aws\-marketplace:Subscribe | 
| Enable subscription auto\-renew | aws\-marketplace:Subscribe | 
| Disable subscription auto\-renew | aws\-marketplace:Unsubscribe | 
| List active subscriptions | aws\-marketplace:ViewSubscriptions | 
| View subscription | aws\-marketplace:ViewSubscriptions | 
| List subscription verification requests | aws\-marketplace:ListAgreementRequests | 
| View subscription verification request | aws\-marketplace:GetAgreementRequest | 
| Cancel subscription verification request | aws\-marketplace:CancelAgreementRequest | 


**AWS Data Exchange console\-only actions for providers**  

| Console action | IAM permission | 
| --- | --- | 
| Publish product |  `aws-marketplace:StartChangeSet` `aws-marketplace:DescribeChangeSet` `dataexchange:PublishDataSet`  | 
| Unpublish product |  `aws-marketplace:StartChangeSet` `aws-marketplace:DescribeChangeSet`  | 
| Edit product |  `aws-marketplace:StartChangeSet` `aws-marketplace:DescribeChangeSet`  | 
| Create custom offer |  `aws-marketplace:StartChangeSet` `aws-marketplace:DescribeChangeSet`  | 
| Edit custom offer |  `aws-marketplace:StartChangeSet` `aws-marketplace:DescribeChangeSet`  | 
| View product details |  `aws-marketplace:DescribeEntity` `aws-marketplace:ListEntities`  | 
| View product's custom offer | aws\-marketplace:DescribeEntity | 
| View product dashboard |  `aws-marketplace:ListEntities` `aws-marketplace:DescribeEntity`  | 
| List products to which a data set or revision has been published |  `aws-marketplace:ListEntities` `aws-marketplace:DescribeEntity`  | 
| List subscription verification requests | aws\-marketplace:ListAgreementApprovalRequests | 
| Approve subscription verification requests | aws\-marketplace:AcceptAgreementApprovalRequest | 
| Decline subscription verification requests | aws\-marketplace:RejectAgreementApprovalRequest | 
| Delete information from subscription verification requests | aws\-marketplace:UpdateAgreementApprovalRequest | 
| View subscription details | aws\-marketplace:SearchAgreements`aws-marketplace:GetAgreementTerms` | 