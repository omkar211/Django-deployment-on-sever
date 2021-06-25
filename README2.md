                                        ''' Django Application Deployment Manual'''
        
ONLY FOR LINUX DISTRIBUTIONS<br/>
      
<br>To deploy the codebase on server following commands:<br/>
           Open host Terminal <br/>
1.`python manage.py check --deploy`<br/>
  1.1 run this command before deploying your project and make sure no warnings and errors.<br/>
  1.2 If  you find any error or any warning ,then take care of below dependencies.<br/>
      
        SECURE_HSTS_SECONDS = 3600
        SECURE_CONTENT_TYPE_NOSNIFF = True
        SECURE_HSTS_PRELOAD = True
        SECURE_HSTS_INCLUDE_SUBDOMAINS = True
        SECURE_BROWSER_XSS_FILTER = True
        SECURE_SSL_REDIRECT = True
        SESSION_COOKIE_SECURE = True
        CSRF_COOKIE_SECURE = True
        X_FRAME_OPTIONS = 'DENY'
        DEBUG = False
---
1. Install the Python latest version 3.6.8 <br/>
2. Install the Virtual Environment using 2.1 command <br/>
   2.1 `pip install virtualenv`
3. Create Virtual Environment using 3.1 command <br/>
   3.1 `python -m virtualenv env_name`
4. Generate the SSH key using 4.2 command <br/>
   4.1 Generate it .so host can communicate with another host and share resources.<br/>
   4.2 `ssh-keygen`<br/>
   4.3 `cat ~/.ssh/id_rsa.pub` or search where you have given path<br/>
   4.4 And 4.2 command generates two keys one is public and another one is private,copy the 
           public key, using 4.3 command and paste it "Add an SSH key".<br/>
5. Ready to clone your Application/project in server/host using 5.1 command<br/>
   5.1 `git clone "url.git"`
6. Go inside the project and activate the virtualenv by using 6.1 command<br/>
   6.1 `source /virtualenv_name/bin/activate`
7. After that install all the requirements/packages using 7.1 command (file extension should be in filename.txt)<br/>
   7.1 `pip install -r requirements.txt`
   
---
                                     CHANGES in Setting.py 
    
    
1. Set environment path<br/>
   1.1 `os.environment["HOME"]="/home/domain_name"`<br/>
   1.2 When 1.1 `return True` .All the settings will starts-up for the server in setting.py <br/>
2. BASE_DIR - It has contained home path or root path of django-application<br/>

3. Set media root  and static root path<br/>
  3.1 ``media_root=os.path.join(BASE_DIR,"media/)``// path of where media directory stored<br/>
  3.2 ``media_root=os.path.join(BASE_DIR,"static/)``// path of where statics directory stored

4. Tell the django application ,Request can come from only these domains or IP Address for that
   set the 4.1 variable <br/>
   4.1  ``ALLOWED_HOST=["google.com","domain_name","ip_address"]``
   4.2 let say if request come from IP Address or Domain_name  that is not included in
           ALLOW_HOSTS.so that request will not be proceed for further process.<br/>
5.  Make sure ``DEBUG = False`` When Application is running on server<br/>
6.  Configure the EMAIL environment<br/>
   6.1  
       
         """ SMTP Server settings """
         EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
         EMAIL_HOST = 'mail.xyz.in'
         EMAIL_USE_SSL = False
         EMAIL_PORT = 587
         EMAIL_HOST_USER = 'inf@xyx.in'
         EMAIL_HOST_PASSWORD = 'Pass123'

7. Set the DATABASE configuration<br/>
    7.1  
           
            if Server == True:
                DATABASES = {
                    'default': {
                        'ENGINE': 'django.db.backends.mysql',
                        'NAME': 'Database_name',
                        'USER': 'User_name',
                        'PASSWORD': 'User_password',
                        'HOST': 'localhost',
                        'PORT': '',
                        'OPTIONS': {
                            'sql_mode': 'traditional',
                        }
                    }
                }
           
      
8. Set the CORS_ORIGIN_WHITELIST (Cross-Origin Resource Sharing), because No other domains or 
   or IP Addresses can access the data  except given in CORS_ORIGIN_WHITELIST.<br/>
  
   8.1 
                
                CORS_ORIGIN_WHITELIST = [
                    "http://localhost:4200",
                    "https://domain_name"
                   ]
                   
9. LOGGING : for containing all the logs of Application<br/>
   9.1 In header set the log file path variable name is "filename"<br/>
   9.2   
          
           handlers': {
                'file': {
                    'level': 'DEBUG',
                    'class': 'logging.handlers.RotatingFileHandler',
                    'filename': '/home/Application_name/python_log/requests.log' if Server == True else '/opt/python/log/requests.log',
                    'formatter': 'verbose'
                },
           

10. nohup command [command-argument ...]
        
       10.1 The nohup command, short for no hang-up is used to run a process 
        in the background. A process that has been ‘nohuped’ will continue 
        to run even if the terminal from which it was run is closed. In effect,
        nohup disconnects the process from the terminal.
                      
              `  swagger is Not mandatory `      
11. swagger<br/>
    11.1 OpenAPI Documentation Generator for Django REST Framework.<br/>
    11.2 for Installation run the command 11.3.<br/>
    11.3 `pip install django-rest-swagger`<br/>
    11.4 Also include swagger app in setting.py in INSTALLED_APP<br/>
    
           INSTALLED_APPS = [
              'rest_framework_swagger',
           ]
           
    11.5 Import the url of swagger <br/>
         11.5.1 swagger provides defaut url method<br/>
         11.5.2 `` from rest_framework_swagger.views import get_swagger_view``  include it in root urls.py<br/>
         11.5.3 `schema_view = get_swagger_view(title='Application_name API')` use this method to get default url<br/>
         11.5.4 and include it in :- <br/>
                    
                    urlpatterns = [
                           url('api_documentation', schema_view)
                           ]
                   
12. To run the server<br/>
    12.1 ``nohup python manage.py runsslserver 0.0.0.0:8001 --certificate cert_file_path --key ssl_key_path &`` to run a server<br/>
    12.2 check if "port"8001 is empty or not in 12.1 command ,if not run on another port. and make sure a port you chose should not be a reserved port.<br/>
# Author
- OMKAR SHARMA 
