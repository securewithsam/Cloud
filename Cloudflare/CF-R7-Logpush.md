
![image](https://github.com/securewithsam/Cloud/assets/85324643/ca9b9206-f9e4-4047-8983-e5097f9ec23c)

![image](https://github.com/securewithsam/Cloud/assets/85324643/ce1e8cc2-3dab-45d1-bf4f-9e8a77308d8c)

![image](https://github.com/securewithsam/Cloud/assets/85324643/246c4368-c634-4db5-aab2-cb1b0d173eca)

![image](https://github.com/securewithsam/Cloud/assets/85324643/0ae0909c-0d72-480b-ab58-c19f1a372351)

![image](https://github.com/securewithsam/Cloud/assets/85324643/561e86e0-514b-4e12-bfb8-25906c55222c)


##### After this go to S3 Bucket and edit the policy , after its saved, you will receive a ownership token , copy and paste as seen below and validate .

![image](https://github.com/securewithsam/Cloud/assets/85324643/bf6cdc1d-8d08-4b6e-b5f4-16be83040a6a)


```sh
{
	"Version": "2012-10-17",
	"Id": "Policy150667777792",
	"Statement": [
		{
			"Sid": "Stmt1506627777918",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::3917777777948:user/cloudflare-logpush"
			},
			"Action": "s3:PutObject",
			"Resource": "arn:aws:s3:::cc-cac-cf-r7-logpush-dev/*"
		}
	]
}

```


![image](https://github.com/securewithsam/Cloud/assets/85324643/a2607337-702b-4961-b4f3-2eb61931a461)

![image](https://github.com/securewithsam/Cloud/assets/85324643/704408b1-3578-4282-abe5-8c56f4bbcf2c)

![image](https://github.com/securewithsam/Cloud/assets/85324643/f44670e2-6afb-405a-9e36-67b6b1cd9e62)

![image](https://github.com/securewithsam/Cloud/assets/85324643/e58fe95b-ee6f-40ff-9b84-3e6044198cf0)



##### After the validation is success , you will receive a ownership token in the S3 bucket , click download and copy paste the token 
![image](https://github.com/securewithsam/Cloud/assets/85324643/4e87b5af-7cb9-48a3-950f-579be6631780)

![image](https://github.com/securewithsam/Cloud/assets/85324643/bf6cdc1d-8d08-4b6e-b5f4-16be83040a6a)




### Testing for multiuser access

```sh
{
	"Version": "2012-10-17",
	"Id": "Policy1506627184792",
	"Statement": [
		{
			"Sid": "Stmt1506627150918",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::391854517948:user/cloudflare-logpush"
			},
			"Action": "s3:PutObject",
			"Resource": "arn:aws:s3:::ec-cac-cf-r7-logpush-dev/*"
		},
		{
			"Sid": "Statement1",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::478958651604:user/svct-aawwssraapiid7"
			},
			"Action": "s3:GetObject",
			"Resource": "arn:aws:s3:::cc-eac-cf-r7-logspush-devst/*"
		}
	]
}
```

#### Adding Event source in Rapid7 

![image](https://github.com/securewithsam/Cloud/assets/85324643/886be7f3-0d0f-47fa-984a-41c9bdfbf30e)

![image](https://github.com/securewithsam/Cloud/assets/85324643/f0b7e179-13e5-4639-8c62-fc00d8528739)
![image](https://github.com/securewithsam/Cloud/assets/85324643/7cb68207-8efb-46a4-9725-e3926158464c)
![image](https://github.com/securewithsam/Cloud/assets/85324643/d3378dbf-d543-4e80-b2ad-6506c7517980)

![image](https://github.com/securewithsam/Cloud/assets/85324643/3f6bbe81-4b1e-4771-ad86-8ef113e29bc4)
![image](https://github.com/securewithsam/Cloud/assets/85324643/8205f18e-c4b7-4245-bfe5-b7540923ad17)







