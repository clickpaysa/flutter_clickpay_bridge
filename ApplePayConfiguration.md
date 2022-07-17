# Steps to configure Apple Pay with ClickPay

Follow the steps to help you easily configure your Apple Pay with ClickPay

1. Generate CSR via [ClickPay Portal](https://merchant.clickpay.com.sa)

	* Navigate to ClickPay [Certificate Management](https://merchant.clickpay.com.sa/merchant/developers/certs).
	![](https://user-images.githubusercontent.com/103630680/179389595-244bc23b-a36d-4a23-b993-c0748f19e7d6.png)
	* Click on ➕ to add a request for certificate.
	![](https://user-images.githubusercontent.com/103630680/179389657-6fa68dbe-e258-408c-9ae5-edf87c343281.png)
	* Wait the proccess to be finished, then download the certificate file. 
	![](https://user-images.githubusercontent.com/103630680/179389693-5edf80d9-0012-4369-9ac3-737243e1f564.png)
2. Create Apple Pay certificate via your account on [Apple Developer](http://developer.apple.com)
	* Navigate to the Certificates, Identifiers & Profiles, then click on **Add** certificate button.
	![](https://user-images.githubusercontent.com/69899730/106731619-58ccd800-6618-11eb-8f38-c4917aca5cf9.jpg)
	* Check the option **Apple Pay Payment Processing Certificate** under the section **Services**, then click on **Continue** button.
	![](https://user-images.githubusercontent.com/69899730/106731955-caa52180-6618-11eb-853f-5757e9b7420a.jpg)
	* Choose the **Merchant ID** from the dropdown list, then click on **Continue** button.
	![](https://user-images.githubusercontent.com/69899730/106731628-5a969b80-6618-11eb-9968-8ac35dff97d8.jpg)
	* Click on **Create Certificate** button under the section **Apple Pay Payment Processing Certificate**.
	![](https://user-images.githubusercontent.com/69899730/106731960-cbd64e80-6618-11eb-8785-ba599f2f2ddc.jpg)
	* Click on **Choose File** to select the certificate file you downloaded from ClickPay portal in step 1, then clikc on **Continue** button.
	![](https://user-images.githubusercontent.com/69899730/106731964-cd077b80-6618-11eb-9a9e-d065c74ce244.jpg)
	* Download your certificate to your Mac, then double click the **.cer** file to install in **Keychain Access**.
	![](https://user-images.githubusercontent.com/69899730/106732177-0b049f80-6619-11eb-86b9-9ddee2b6c35e.jpg)
	
3. Upload your certificate to ClickPay portal.
	* Navigate to [ClickPay Certificate Management](https://merchant.clickpay.com.sa/merchant/developers/certs).
		
	* Enter the **Merchant ID** under the section **COMPLETE CERTIFICATE REQUEST**, then choose the **.cer** file you downloaded in step 2 and click on **Save** button.
	![](https://user-images.githubusercontent.com/103630680/179389841-b9aea585-8857-41f6-8872-4a8a62cfdd0b.png)
	* Congratulations, Your certificate request completed successfully, your ClickPay profile is now ready for doing payment using Apple Pay.
	
