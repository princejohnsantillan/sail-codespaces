# Running Laravel Sail on Github Codespaces

### Let's set this up from the beginning

1. Create a Laravel project using sail and make sure to add the devcontainer flag.

    ```curl -s https://laravel.build/sail-codespaces?devcontainer | bash```
    
2. There are 2 main components here to make this happen. 
    - ./devcontainer/devcontainer.json : This is where we can tell Codespaces how to create the container for us.
    - docker-compose.yml : This defines what our container will look like.
    
3. Let's tweak the docker-compose.yml file first. 
    - Make sure there are no references to the vendor folder. Codespaces starts off with an empty repo, therefore there is no vendor folder to look into.
        - Run ```php artisan sail:publish``` this will copy the dockerfile that sail is using into a new docker folder on your repo.
        - Copy to your repo any other files that docker-compose.yml is referencing from the vendor folder
    - Make sure that all variables in your docker-compose.yml file exists in the .env.example file. Alternatively, you should provide a default value. Eg. 
    ```${WWWGROUP:-1000}``` and ```${WWWUSER:-1000}```
    
4. Now let's tweak the devcontainer.json file.
    - Duding the initializeCommand lifecyle make sure to copy .env.example to an .env file. This will ensure that docker-compose.yml has all the variables it needs.
    - Expose the ports your services are using.
    - Here's a sample of how it might look: ![image](https://user-images.githubusercontent.com/60916966/206878564-28c9cc9b-ebd1-4ae0-9d36-d3f1ee927afd.png)

