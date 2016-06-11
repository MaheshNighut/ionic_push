////////////////////////////IONIC push ANDROID/////////////////////////////////////////////////////////////////////
ionic start pushCall
ionic login
ionic upload


after successful upload you can open ionic io and you wull see your project live
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////
                                             GOOGLE CONSOLE
//open google console
1-create project
2-use google api
    1-mobile APIs
    2-select google cloud messaging and eneble it
    3- go to credential and create API key
//after that add following plugin
ionic add ionic-platform-web-client
ionic plugin add phonegap-plugin-push --variable SENDER_ID="<your gcm number>"
(dont remove quotes while adding gcm number)

//add platfom

ionic platform add android
ionic io init
ionic config set dev_push true

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
                                              IONIC IO
go to setting
	1-create api key	
	2-go to certificate and create security profile name edit id click on android and  add GCM key
	and save it.
	3-after this again  edit on your profile and save Android Keystore ,use following command
	"keytool -genkey -v -keystore MAHESH.keystore -alias rigel -keyalg RSA -keysize 2048 -validity 10000"
BUT BEFORE THAT OPEN NEW command prompt aand we have to go to the bin directory of our java sdk
so-cd C:\Program Files\Java\jdk1.7.0\bin 
and then press enter now you are in bin folder and this time run above command without changing it 
we have given the name Mahesh so after running above cammand it will create one file in your bin directory named "mahesh"  
of type
keytool
just go to ionic io  go into setting and edit on profile and add keystore by giving path to the file we created and enter the
 password and enter the 
alise name as "rigel"
(if your password are same for both ten also it is ok i am kind of lazy thats y  have same password)
-save it
(now there is nothing to do in ionic io dashboard)
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
		                                                    	INDEX.HTML
	//add this code to app.js

	angular.module('starter', ['ionic'])
 
	.run(function($ionicPlatform) {
  	$ionicPlatform.ready(function() {
   	 var push = new Ionic.Push({
      "debug": true
    	});
 
 	   push.register(function(token) {
      console.log("My Device token:",token.token);
      push.saveToken(token);  // persist the token in the Ionic Platform
    	});
  	});
	})

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
                                     POSTMAN
//to test wether your configure correctly with ionic io open launch postman
//and then do the following things:

	1-create collection give it a valid name
	2-in body click on text and select Application/json
	it will add header automatically
 	3-add another header	 
	key as Authorization
	value as Bearer followed by your api token from ionic io
	4-select "raw " as the format of our json
	2-in body section of your collection write
	following code
	{
	"tokens": ["DEV_DEVICE_TOKEN"],
    	"profile": "PROFILE_NAME",
    	"notification":
         {
        "message": "This is my demo push!"
         }
	}


//now it will prompt message on browser
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
to make it work on mobile do the following things

1-open ionic io dashboard
2-go to setting 


ionic config set gcm_key   <your-gcm-project-number>	
ionic config set dev_push false
ionic build android 

install your app in mobile and send the notification from postman 
again just change the token and send it
do the following things
1-first run your app in your mobile
2-after that connect it to the pc/laptop via cable
3-in your mobile open "developer mode"
(in some mobile at first you will not see developer option ,
to see that developer option just click on "about phone " more than four times and you will get massage 
"debugger mode on" after you will have that "developer option" in your mobile just above the "about phone")
4-after that in your pc type this URL
" chrome://inspect/#devices"
you will see your phone and inspect option there
to open our ceated app in debugger mode you should open your app in mobile then only you can see your app 
on pc browser.
5- click on inspect go into console and copy that device token 
6-open postman and just change the token and send it(see postman section abobe)

you will get notification on your mobile(make sure you have internet plan activated ) 

(Mahesh Sampat Nighut)

