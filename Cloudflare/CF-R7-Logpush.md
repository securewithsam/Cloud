
![image](https://github.com/securewithsam/Cloud/assets/85324643/ca9b9206-f9e4-4047-8983-e5097f9ec23c)

![image](https://github.com/securewithsam/Cloud/assets/85324643/ce1e8cc2-3dab-45d1-bf4f-9e8a77308d8c)

![image](https://github.com/securewithsam/Cloud/assets/85324643/246c4368-c634-4db5-aab2-cb1b0d173eca)

![image](https://github.com/securewithsam/Cloud/assets/85324643/0ae0909c-0d72-480b-ab58-c19f1a372351)

![image](https://github.com/securewithsam/Cloud/assets/85324643/67308a61-817a-46fa-8317-95ff4255cbdd)


##### Then go to cloudflare , and hit Validate Access
![image](https://github.com/securewithsam/Cloud/assets/85324643/34fb55e9-a22c-449c-8704-346d15fae7da)


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
