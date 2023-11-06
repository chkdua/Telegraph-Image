#Telegraph-Image
Free image hosting solution, Flickr/imgur alternative. Use Cloudflare Pages and Telegraph.

[English](README-EN.md)|中文

## How to deploy

### Prepare in advance
The only thing you need to prepare in advance is a Cloudflare account (if you need to deploy on your own server without relying on Cloudflare, please refer to [#46](https://github.com/cf-pages/Telegraph-Image/issues/46 ) )

### Step by step tutorial
In 3 simple steps, you can deploy this project and have your own drawing bed

1. Download or Fork this repository (Note: Please use fork currently, there are problems with deployment when using download [#14](https://github.com/cf-pages/Telegraph-Image/issues/14))

2. Open Cloudflare Dashboard, enter the Pages management page, select Create Project, if you choose to fork this repository in the first step, select `Connect to Git Provider`, if you choose to download this repository in the first step, then Select `Direct Upload`
![1](https://telegraph-image.pages.dev/file/8d4ef9b7761a25821d9c2.png)

3. Enter the project name as prompted on the page, select the git repository to be connected (the first step is to select fork) or upload the warehouse file you just downloaded (the first step is to download this repository), and click `Deploy Site`. Deployment ready

## Features
1. Unlimited image storage, you can upload an unlimited number of images

2. There is no need to purchase a server, it is hosted on Cloudflare’s network. When the usage does not exceed Cloudflare’s free quota, it is completely free.

3. There is no need to purchase a domain name. You can use the free second-level domain name `*.pages.dev` provided by Cloudflare Pages. It also supports binding custom domain names.

4. Supports image review API, which can be turned on as needed. Once turned on, bad pictures will be automatically blocked and will no longer be loaded.

5. Supports background image management, you can preview uploaded images online, add whitelists, blacklists and other operations

### Bind custom domain name
In the custom domain of pages, bind the domain name that exists in cloudflare. The domain name hosted by cloudflare will automatically modify the dns record.
![2](https://telegraph-image.pages.dev/file/29546e3a7465a01281ee2.png)

### Enable image review
1. Please go to https://moderatecontent.com/ to register and get a free API key for moderating image content

2. Open the management page of Cloudflare Pages, click `Settings`, `Environment Variables`, `Add Environment Variables`

3. Add a `variable name` as `ModerateContentApiKey`, `value` as the `API key` you just obtained in the first step, click `Save`.

Note: Since the changes will take effect during the next deployment, you may also need to enter the `Deployment` page and redeploy the project.

After turning on image review, the first image loading will be slow because the review takes time. Subsequent image loading will not be affected due to the cache.
![3](https://telegraph-image.pages.dev/file/bae511fb116b034ef9c14.png)

### limit
1. Since image files are actually stored in Telegraph, Telegraph limits the uploaded image size to a maximum of 5MB.

2. Due to the use of Cloudflare's network, the loading speed of images may not be guaranteed in some areas.

3. The free version of Cloudflare Function has a daily limit of 100,000 requests (that is, the total number of uploads or loading images cannot exceed 100,000 times). If it exceeds the limit, you may need to purchase a paid package of Cloudflare Function. If the image management function is turned on, there will also be a number of KV operations. limit, if it exceeds the limit, you need to purchase a paid package

### grateful
Ideas and code provided by Hostloc @feixiang and @wulaca

## Update log
January 18, 2023--Update of image management function

1. Support image management function, which is turned off by default. If you want to turn it on, please go to the background after deployment and click `Settings`->`Function`->`KV Namespace Binding`->`Edit Binding`->` Fill in the variable name: `img_url` `KV namespace` Select the KV storage space you created in advance, open it and visit http(s)://your domain name/admin to open the background management page
| variable name | KV namespace |
| ----------- | ----------- |
| img_url | Select the KV storage space created in advance |

![](https://im.gurl.eu.org/file/a0c212d5dfb61f3652d07.png)
![](https://im.gurl.eu.org/file/48b9316ed018b2cb67cf4.png)

2. A new login verification function has been added to the backend management page. It is turned off by default. If you want to enable it, please go to the backend after deployment and click `Settings`->`Environment Variables`->`Define variables for the production environment`->`Edit variables ` Add the variables shown in the following table to enable login verification
| variable name | value |
| ----------- | ----------- |
|BASIC_USER = | <backend management page login user name>|
|BASIC_PASS = | <Backend management page login user password>|

![](https://im.gurl.eu.org/file/dff376498ac87cdb78071.png)

Of course, you can also not set these two values, so that no verification is required when accessing the backend management page and the login step is skipped directly. This design allows you to use it in conjunction with Cloudflare Access to support email verification code login and Microsoft account login. Functions such as Github account login can be integrated with the original login method on your domain name. There is no need to remember an additional set of backend account passwords. For how to add Cloudflare Access, please refer to the official documentation. Note that the protected paths include /admin and /api/ manage/*

3. Statistics on the total number of new pictures
When the picture management function is turned on, the number of pictures in the record can be viewed at the top of the background

![](https://im.gurl.eu.org/file/b7a37c08dc2c504199824.png)

4. Added image file name search
When the image management function is turned on, you can use the image file name in the background search box to quickly search and locate the images that need to be managed.

![](https://im.gurl.eu.org/file/faf6d59a7d4a48a555491.png)

5. Added picture status display
When the picture management function is turned on, the current status of the picture can be viewed in the background { "ListType": "None", "TimeStamp": 1673984678274 }
ListType represents whether the picture is currently in the black and white list, None means that it is neither in the black list nor the white list, White means that it is in the white list, Block means that it is in the black list, and TimeStamp is the timestamp when the picture was first loaded, if it is turned on Image review API, the results of the image review will also be displayed here and marked with Label

![](https://im.gurl.eu.org/file/6aab78b83bbd8c249ee29.png)

6. Added blacklist function
When the image management function is turned on, images can be manually added to the blacklist in the background. Images added to the blacklist will not load normally.

![](https://im.gurl.eu.org/file/fb18ef006a23677a52dfe.png)

7. Added whitelist function
When the image management function is turned on, images can be manually added to the whitelist in the background. Images added to the whitelist will be loaded normally anyway, and the results of the image review API can be bypassed.

![](https://im.gurl.eu.org/file/2193409107d4f2bcd00ee.png)

8. Added record deletion function
When the image management function is turned on, the image record can be manually deleted in the background, that is, the image will no longer be displayed in the background unless someone uploads and loads the image again. Note that since the image is stored on telegraph's server, we cannot delete the original uploaded image. The loading of images can only be blocked through the blacklist function in point 6 above.

9. New program running mode: whitelist mode
When the image management function is turned on, in addition to the default mode, this update also adds a new operating mode. In this mode, only images added to the whitelist will be loaded, and uploaded images need to be reviewed and approved. to prevent the loading of bad images to the greatest extent. If you want to enable it, please set the environment variable: WhiteList_Mode=="true"

10. Added background image preview function
When the image management function is turned on, images loaded through your domain name can be previewed in the background. Click on the image to enlarge, reduce, rotate and other operations.

![](https://im.gurl.eu.org/file/740cd5a69672de36133a2.png)

## It has been deployed, how to update it?
In fact, the update is very simple. You only need to refer to the above update content, first enter the Cloudflare Pages backend, set the environment variables you need to use in advance and bind them to the KV namespace, then go to Github and select the warehouse you have forked before. Sync fork`->`Update branch`. Wait a moment. Cloudflare Pages will automatically deploy the latest code after detecting that your warehouse has been updated.

## Some restrictions:
Cloudflare KV only has 1,000 free write quotas per day. Each new image loaded will occupy this write quota. If this quota is exceeded, the image management background will not be able to record newly loaded images.

Up to 100,000 free read operations per day. This quota will be occupied every time an image is loaded (in the absence of caching, if your domain name is cached in Cloudflare, the quota will be occupied only when the cache misses), exceeding the black and white list Other functions may fail

There are a maximum of 1,000 free deletions per day. Each picture record will occupy this quota. If the limit is exceeded, picture records cannot be deleted.

There is a maximum of 1,000 free listing operations per day. Every time the background/admin is opened or refreshed, this quota will be occupied. If it exceeds the limit, background image management will be performed.

In most cases, the free quota is basically enough, and can be slightly exceeded. If it is exceeded, it will be deactivated immediately. Each quota is calculated separately. If an operation exceeds the free quota, only that operation will be deactivated. It does not affect other functions, that is, even if my free writing quota is used up, my reading and writing functions are not affected, and the pictures can be loaded normally, but I cannot see new pictures in the picture management background.

If your free quota is not enough, you can purchase the paid version of Cloudflare Workers from Cloudflare. It starts at $5 per month and is charged according to your usage. There is no quota limit mentioned above.

In addition, changes made to environment variables will take effect the next time you deploy. If you change the `environment variables` and turn a certain function on or off, please remember to redeploy.

![](https://im.gurl.eu.org/file/b514467a4b3be0567a76f.png)

### Sponsorship
This project is tested with BrowserStack.

This project is supported by [Cloudflare](https://www.cloudflare.com/).
