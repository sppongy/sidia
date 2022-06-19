```
          _____                    _____                    _____                   _____                    _____          
         /\    \                  /\    \                  /\    \                 /\    \                  /\    \         
        /::\    \                /::\    \                /::\    \               /::\    \                /::\    \        
       /::::\    \               \:::\    \              /::::\    \              \:::\    \              /::::\    \       
      /::::::\    \               \:::\    \            /::::::\    \              \:::\    \            /::::::\    \      
     /:::/\:::\    \               \:::\    \          /:::/\:::\    \              \:::\    \          /:::/\:::\    \     
    /:::/__\:::\    \               \:::\    \        /:::/  \:::\    \              \:::\    \        /:::/__\:::\    \    
    \:::\   \:::\    \              /::::\    \      /:::/    \:::\    \             /::::\    \      /::::\   \:::\    \   
  ___\:::\   \:::\    \    ____    /::::::\    \    /:::/    / \:::\    \   ____    /::::::\    \    /::::::\   \:::\    \  
 /\   \:::\   \:::\    \  /\   \  /:::/\:::\    \  /:::/    /   \:::\ ___\ /\   \  /:::/\:::\    \  /:::/\:::\   \:::\    \ 
/::\   \:::\   \:::\____\/::\   \/:::/  \:::\____\/:::/____/     \:::|    /::\   \/:::/  \:::\____\/:::/  \:::\   \:::\____\
\:::\   \:::\   \::/    /\:::\  /:::/    \::/    /\:::\    \     /:::|____\:::\  /:::/    \::/    /\::/    \:::\  /:::/    /
 \:::\   \:::\   \/____/  \:::\/:::/    / \/____/  \:::\    \   /:::/    / \:::\/:::/    / \/____/  \/____/ \:::\/:::/    / 
  \:::\   \:::\    \       \::::::/    /            \:::\    \ /:::/    /   \::::::/    /                    \::::::/    /  
   \:::\   \:::\____\       \::::/____/              \:::\    /:::/    /     \::::/____/                      \::::/    /   
    \:::\  /:::/    /        \:::\    \               \:::\  /:::/    /       \:::\    \                      /:::/    /    
     \:::\/:::/    /          \:::\    \               \:::\/:::/    /         \:::\    \                    /:::/    /     
      \::::::/    /            \:::\    \               \::::::/    /           \:::\    \                  /:::/    /      
       \::::/    /              \:::\____\               \::::/    /             \:::\____\                /:::/    /       
        \::/    /                \::/    /                \::/____/               \::/    /                \::/    /        
         \/____/                  \/____/                  ~~                      \/____/                  \/____/         
                                                                                                                            


```                    

<h1 style="text-align: center"> SIDIA  A SImple MeDIA server </h1>

[Info](Info)
>[Applications](Applications)\
[Folder Structure](Folder-structure)

[Installation](installation)
>[Docker](Docker)\
[Permissions](Permissions)\
[Notes](Notes)

---
## Info
### Applications
```
${APP}			${USE}				${PORT}
Sonnar			TV show manager			8989
Radarr			Movie Manager			7878
Lidarr			Music Manager			8686
Readarr			Book Manager			8787
Prowlarr		Index Manager			9696
qBittorrent		Torrenting Client		8080
Jellyfin		Media Center/Viewer		8096
Flame			Startpage			5005
```
---
### Folder-structure
```
/data
├── torrents
│  ├── movies
│  ├── music
│  └── tv
├── usenet
│  ├── movies
│  ├── music
│  └── tv
└── media
   ├── movies
   ├── music
   └── tv
/docker
├── appdata
│   ├── radarr
│   ├── sonarr
│   ├── lidarr
│   ├── readarr
│   ├── prowlarr
│   ├── qbittorrent
│   ├── jellyfin
│   └── flame
└── sidia
    ├── docker-compose.yml
    ├── .env
    └── README.md
```
---
## Installation
### Docker
we'll use docker-compose to manage our docker containers
>make sure to check over the env_example file
```
# turn example into actual env file
mv env_example .env

# compose and run as deamon
docker-compose up -d"
```
### Permissions
> you'll need to change this if you decided to use a different folder in the env file
```
sudo chown -R $USER:$USER /data
sudo chmod -R a=,a+rX,u+w,g+w /data
```
---
## App Setup
### Star apps(sonarr, radarr, lidarr, readarr)
Adding indexers is done through prowlarr\
To add a download client simply go to setting/download clients/ and then choose qbittorent. the "host" is qbittorrent
and the port is whatever you chose in the env file (default is 8080) 
### qBittorrent 
The default credentials are
```
user: admin
pass: adminadmin
```
### Prowlarr
Add indexers of your choice\
to add prowlarr to other apps go to settings/apps and select the app you would like to add it to\
it will ask for an api key that you can find in settings/general in whatever app you chose
### Jellyfin
You will be prompted with a setup wizard upon visiting jellyfin\
You will be givin the option to add your libraries,
> these libraries will by default be /data/media/{movies\shows\music\books}

### Flame
You can add applications/bookmarks to flame by going to http://localhost:5005/applications\
Settings will be found at http://localhost:5005/settings
> if you changed the port for flame in the env file then substitute that for 5005

---
## Notes
you can access all the apps at http://localhost:<zero-width space>${PORT}/
> localhost should only be used for users accessing the webui\
apps will communicate with eachother through the docker network
```
what goes in your browser		http://localhost:8989 
what goes in application settings	http://sonnar:8989
```
