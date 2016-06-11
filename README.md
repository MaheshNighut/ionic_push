ionic start pushCall
ionic login
ionic upload
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
ionic plugin add phonegap-plugin-push --variable SENDER_ID="991785317233"
(dont remove quotes while adding gcm number)

//add platfom

ionic platform add android
ionic io init
ionic config set dev_push true

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
                                                    //open ionic io dashboard
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
