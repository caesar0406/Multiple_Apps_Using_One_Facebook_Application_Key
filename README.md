For Facebook login implementation in our iOS app, we need to do some setting in our iOS project.

First, install the Facebook SDK with cocoapods or other way.<br />
**pod 'FacebookCore'**<br />
**pod 'FacebookLogin'**<br />
**pod 'FacebookShare'**<br />

We can build the project first to test if "pod install" (or your special method) is OK for your project.
If there is anything wrong after project building, maybe you can try this: <br />

replace "**pod 'FacebookShare'**" with "**pod 'FacebookShare', :git => 'https://github.com/1amageek/facebook-sdk-swift**"<br />

This should be Facebook issue and I don't know when will they will fix it.<br />

------------------------install SDK finish-------------------------<br />
<br />
Now, Facebook SDK is ready in your project.<br />
Follow [Facebook Server Site](https://developers.facebook.com/docs/facebook-login/ios/) to setting your Facebook server setting.<br />
<br />
Then, open your info.plist file with source code and add following code in it.<br /><br />
\<key\>LSApplicationQueriesSchemes\</key\><br />
\<array\><br />
　\<string\>fbapi\</string\><br />
　\<string\>fb-messenger-api\</string\><br />
　\<string\>fbauth2\</string\><br />
　\<string\>fbshareextension\</string\><br />
\</array\><br />
<br />
This the white scheme list with Facebook App communication.
<br /><br />
\<key\>CFBundleURLTypes\</key\><br />
\<array\><br />
　\<dict\><br />
　　\<key\>CFBundleURLSchemes\</key\><br />
　　\<array\><br />
　　　\<string\>fb + "**Your Facebook App ID**"\</string\><br />
　　\</array\><br />
　\</dict\><br />
\</array\><br />
\<key\>FacebookAppID\</key\><br />
\<string\>"**Your Facebook App ID**"\</string\><br />
\<key\>FacebookDisplayName\</key\><br />
\<string\>"**Your Login string**"\</string\><br />
<br />
Replace the bold string with your own setting.<br />
This is the scheme code for Facebook to call your App back after the Facebook auth 2.0 procedure.<br />
<br />
Ignore the real code implementation, your project should be ready for Facebook login.<br />
However, if multiple Apps using the same Facebook application number(ID), Facebook will be getting into chaos with the same scheme rule "fb + **Your Facebook App ID**\" when callback.<br />
From the Facebook server setting, all your App use the same scheme setting.<br />
<br />
One way to fix this issue is using "**FacebookUrlSchemeSuffix**".<br />
This is the scheme tail for Facebook to verify which App sent login request.<br />
To implement this method, you need to do some adjust with the setting above.<br />
First, decide one unique key string for your own App identify.<br />
Then, add the following setting in your info.plist.<br /><br />
\<key\>FacebookUrlSchemeSuffix\</key\><br />
\<string\>"**Your App identify key string**"\</string\><br /><br />
Secondly, adjust the setting above:<br />
replace "\<string\>fb + "**Your Facebook App ID**"\</string\>" with "\<string\>fb + "**Your Facebook App ID**" + "**Your App identify key string**"\</string\>"<br />
<br />
Thus, Facebook will call back your own scheme Url "fb + "**Your Facebook App ID**" + "**Your App identify key string**"\" after auth. 2.0 procedure. Your App will never be lost after call out Facebook.







