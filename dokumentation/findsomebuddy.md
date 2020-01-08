<!-- SUBTITLE: A quick summary of Findsomebuddy -->

# Findsomebuddy Dokumentation

## Server Data

Host : 9215458.campusvps.de
IP : 185.158.212.77


## Database

Download FSB Dump here : [Fsb](/uploads/fsb.sql "Fsb")

## Dokumentation
Download Doc File : [Fsb Android Apies](/uploads/fsb-android-apies.docx "Fsb Android Apies")

Download complete Doku : [20190106 En Fsb Doku Collection V 1](/uploads/20190106-en-fsb-doku-collection-v-1.docx "20190106 En Fsb Doku Collection V 1")

Application REST Doku : [Application Rest Doc](/uploads/application-rest-doc.docx "Application Rest Doc")


## Environment

Dev : https://findsomebuddy.de/api/v2 

Live : https://findsomebuddy.de/api/v1 



### Test Environment

For Developing and Testing we have /api/v2

It is a different application AND Database.

Please see example on Schreenshot

![Manual Calls](/uploads/manual-calls.png "Manual Calls")



**Authentication :** 

In the Header Section, use 

*Authorization : Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTAyNywiZW1haWwiOiJqaGFuaWhhc2hlbWlAZ21haWwuY29tIiwiaWF0IjoxNDkwNDU1MTU4fQ.5SkXcqORLxFGU-hlak3GLW6rkybOECX5dJz4LlGoZmM*





## routes.js

```javascript
var Routes = new Array();

Routes.push({
	method : "GET",
	path  : "/api/v1/all-notifications",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/notification_controller', request, reply).all();
		},
        auth: {
            strategy: 'token',
			mode : "try"
        }		
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/auth/facebook",
	handler : function(request, reply){
		return helper.controller('api/api_authenticate', request, reply).facebook();
	}
})

Routes.push({
	method : "POST",
	path  : "/api/v1/signup",
	handler : function(request, reply){
		return helper.controller('api/api_authenticate', request, reply).signup();
	}
})


Routes.push({
	method : "POST",
	path  : "/api/v1/signin",
	handler : function(request, reply){
		return helper.controller('api/api_authenticate', request, reply).signin();
	}
})

Routes.push({
	method : "POST",
	path  : "/api/v1/forgot-password",
	handler : function(request, reply){
		return helper.controller('api/api_authenticate', request, reply).forgotPassword();
	}
})

Routes.push({
	method : "GET",
	path  : "/password_reminder/{token}",
	handler : function(request, reply){
		return helper.controller('api/api_authenticate', request, reply).formUpdatePassword();
	}
})

Routes.push({
	method : "POST",
	path  : "/password_reminder/{token}",
	handler : function(request, reply){
		return helper.controller('api/api_authenticate', request, reply).updatePassword();
	}
})

Routes.push({
	method : "POST",
	path  : "/api/v1/users/{user_id}/invite/{friend_id}/game/{game_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/invitation_controller', request, reply).store();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "PUT",
	path  : "/api/v1/invitation/{invitation_id}/{type}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/invitation_controller', request, reply).update();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "GET",
	path  : "/api/v1/users",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/user_controller', request, reply).index();
		},
        auth: {
            strategy: 'token',
			mode : 'try'
        }
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/users/{user_id}/avatar",
	config : {

        payload: {
            output: 'stream',
            maxBytes: 50000000,
            parse: true,
            allow: 'multipart/form-data'
        },		
		handler : function(request, reply){
			return helper.controller('api/user_controller', request, reply).uploadAvatar();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

server.route({
    method: 'GET',
    path: '/{param*}',
    handler: {
        directory: {
            path: base_dir+'/public',
            listing: true
        }
    }
});

Routes.push({
	method : "POST",
	path  : "/api/v1/users",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/user_controller', request, reply).store();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "GET",
	path  : "/api/v1/users/{user_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/user_controller', request, reply).show();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "PUT",
	path  : "/api/v1/users/{user_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/user_controller', request, reply).update();
		},
        auth: {
            strategy: 'token'
        }		
	}
});


Routes.push({
	method : "GET",
	path  : "/api/v1/users/{user_id}/sports",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/user_sport_controller', request, reply).index();
		},
        auth: {
            strategy: 'token'
        }		
	}	
});


Routes.push({
	method : "POST",
	path  : "/api/v1/users/{user_id}/sports",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/user_sport_controller', request, reply).store();
		},
        auth: {
            strategy: 'token'
        },
        payload: {
            output: 'data',   // These are default options
            parse: true       // These are default options
        }
	}	
});


Routes.push({
	method : "DELETE",
	path  : "/api/v1/users/{user_id}/sports/{sport_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/user_sport_controller', request, reply).destroy();
		},
        auth: {
            strategy: 'token'
        }		
	}	
});


// Sports
Routes.push({
	method : "GET",
	path  : "/api/v1/sports",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/sport_controller', request, reply).index();
		}	
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/sports",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/sport_controller', request, reply).store();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "DELETE",
	path  : "/api/v1/sports/{sport_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/user_controller', request, reply).destroy();
		},
        auth: {
            strategy: 'token'
        }		
	}
});


Routes.push({
	method : "GET",
	path  : "/api/v1/sports/types",
	config : {
		handler : function(request, reply){
			return helper.controller('api/sport_controller', request, reply).get_sport_types();
		},
		auth: {
			strategy: 'token'
		}
	}
});
// end



// Locations
Routes.push({
	method : "GET",
	path  : "/api/v1/users/{user_id}/locations",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/location_controller', request, reply).index();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/users/{user_id}/locations",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/location_controller', request, reply).store();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "DELETE",
	path  : "/api/v1/users/{user_id}/locations/{location_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/location_controller', request, reply).destroy();
		},
        auth: {
            strategy: 'token'
        }		
	}
});
// end


// Games
Routes.push({
	method : "GET",
	path  : "/api/v1/users/{user_id}/games",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/game_controller', request, reply).index();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "GET",
	path  : "/api/v1/games/{game_id}",
	config : {
		handler : function(request, reply){
			return helper.controller('api/game_controller', request, reply).show();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/games",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/game_controller', request, reply).store();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/games/{game_id}/notification",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/game_controller', request, reply).notification();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "PUT",
	path  : "/api/v1/games/{game_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/game_controller', request, reply).update();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/games/{game_id}/sendRequest",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/game_controller', request, reply).attachRequest();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "DELETE",
	path  : "/api/v1/games/{game_id}/leave",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/game_controller', request, reply).leave();
		},
        auth: {
            strategy: 'token'
        }		
	}
});
// end



// Requests
Routes.push({
	method : "GET",
	path  : "/api/v1/requests/{request_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/request_controller', request, reply).show();
		},
        auth: {
            strategy: 'token'
        }		
	}
});	

Routes.push({
	method : "PUT",
	path  : "/api/v1/requests/{request_id}/{request_status}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/request_controller', request, reply).update();
		},
        auth: {
            strategy: 'token'
        }		
	}
});	
// end

Routes.push({
	method : "GET",
	path  : "/api/v1/filter/sports/{id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/filter_controller', request, reply).bySport();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "GET",
	path  : "/api/v1/filter",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/filter_controller', request, reply).custom();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "GET",
	path  : "/api/v1/notifications",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/notification_controller', request, reply).index();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "GET",
	path  : "/api/v1/notifications/seenAll",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/notification_controller', request, reply).seen();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "GET",
	path  : "/api/v1/notifications/count",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/notification_controller', request, reply).count();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "GET",
	path  : "/api/v1/chat/games/{game_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/chat_controller', request, reply).index();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/chat/games/{game_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/chat_controller', request, reply).store();
		},
        auth: {
            strategy: 'token'
        }		
	}
});


Routes.push({
	method : "GET",
	path  : "/api/v1/venues/{venue_id}",
	config : {
		handler : function(request, reply){
			return helper.controller('api/venue_controller', request, reply).show();
		},
        auth: {
            strategy: 'token'
        }
	}
});







Routes.push({
	method : "GET",
	path  : "/api/v1/venues",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/venue_controller', request, reply).index();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/venues",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/venue_controller', request, reply).store();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "PUT",
	path  : "/api/v1/venues/{venue_id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/venue_controller', request, reply).update();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "POST",
	path  : "/api/v1/venues/{id}/photos",
	config : {	
        payload: {
            output: 'stream',
            maxBytes: 50000000,
            parse: true,
            allow: 'multipart/form-data'
        },		
		handler : function(request, reply){
			return helper.controller('api/venue_controller', request, reply).upload();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "DELETE",
	path  : "/api/v1/venues/{id}",
	config : {	
		handler : function(request, reply){
			return helper.controller('api/venue_controller', request, reply).destroy();
		},
        auth: {
            strategy: 'token'
        }		
	}
});

Routes.push({
	method : "GET",
	path  : "/test/gcm",
	config : {	
		handler : function(request, reply){
			helper.send_gcm({
				tokens : [request.query.gcm],
				from : 1,
				to : 1,
				message  : 'Test GCM',
				title : 'test gcm by fsb',
				body : 'Test GCM',
				type : 'message',
				seen : 0,
				target_id : 0
			}, function(err, response){
				return reply({
					err : err,
					res : response
				})
				console.log('info', err);
				console.log('info', response);						
			});			
		}	
	}
});


Routes.push({
	method : "POST",
	path  : "/admin/signin",
	handler : function(request, reply){
		return helper.controller('admin/api_authenticate', request, reply).signin();
	}
})


module.exports = Routes;

```


## Examples

![Createsport](/uploads/fsb/createsport.png "Createsport")

![Updatename](/uploads/fsb/updatename.png "Updatename")


## Pictures

UPDATE 
   files
SET 
   path = REPLACE(path,'http://localhost:8580','https;//findsomebuddy.de')
WHERE 
   path like '%http://localhost:8580%';
	 
	 


## Test Enviroment OAUTH


### Developing



Testsite for Login and Oauth for FSB : https://findsomebuddy.de/auth/

User  : fsbauth, password : fVQ/{*}jFmp:t95R

For Testing the Response of the Login Header, you can use this Site to see  what repsonse is delivering.

Have a look in console. After hopy out the token in out of the input Prompt.
( All these steps are made in the app of course)
Have a look in code! Comment exactly how done in node js!

![Test Fsb Auth](/uploads/fsbauth/test-fsb-auth.png "Test Fsb Auth")



### Signin

Now you can sign in, passing the firebase token in the REST signin Call!

![Test Fsb Auth 2](/uploads/fsbauth/test-fsb-auth-2.png "Test Fsb Auth 2")

..and get the small token at end of response


### Using as Beaerer

The token has an time out, so after limited time it has to be replaced!

![Test Fsb Auth 3](/uploads/fsbauth/test-fsb-auth-3.png "Test Fsb Auth 3")


## Upload Image

### 1. Upload Image

![1 Uploadimage](/uploads/fsb/1-uploadimage.png "1 Uploadimage")


### 2. Show Image


![Photos](/uploads/fsb/photos.png "Photos")







	 

