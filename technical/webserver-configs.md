<!-- TITLE: Webserver Configs -->
<!-- SUBTITLE: A quick summary of Webserver Configs -->

# Webserver Configs

## Apache 

## Nginx

# Wiki js Fix
There was really a Problem to config nginx and apache for the wikijs. Nginx always calling bad gateway if we set the proxy pass to https and another port then 443, but we have do, because apache is listen to 443, too.
So i wrote some code hard in the wikijs instance : 


```batchfile
[root@petitcoderoot server]# grep -rn vendor.js
views/auth/login.pug:21:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')
views/error-notexist.pug:21:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')
views/configure/index.pug:16:    script(type='text/javascript', src='/js/vendor.js')
views/layout.pug:26:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')
views/error.pug:21:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')
views/error-forbidden.pug:21:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')


[root@petitcoderoot server]# grep -rn app.js
views/auth/login.pug:22:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')
views/error-notexist.pug:22:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')
views/layout.pug:27:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')
views/error.pug:22:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')
views/error-forbidden.pug:22:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')

```


I wrote the Url : https://wiki.petitcode.com/js/vendor.js hard in the Files which are be greped. So i garanty of right serving of the vendor.js and the app.js!
Else there is no css loading.

