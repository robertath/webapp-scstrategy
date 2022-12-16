# webapp-scstrategy

LFS, Git actions in CI &amp; CD

1. Created a repository on git

2. Application basic setup

```
mkdir websolution-scstrategy
cd websolution-scstrategy
git init
git remote add origin [url]
notepad .gitignore
git add .
git status //check if temp files was ignored
git commit -m "Application basic setup"
git push -u orgin main
```
3. Install Git LFS and upload file reference to reposiroty
Download: https://git-lfs.github.com/
```
git lfs track *.mp4
notepad .gitattributes //check if file was created and *.mp4 was added
git add .
git commig -m "Setup LFS, add .mp4 attribute"
git push -u origin main
```
4. Setup actions workflow
- on web tab Actions, select NET workflow
- configure your dotnet.yml file
- create resource group on azure
```
az login
az group create -l northeurope -n webapp-scstrategy
az appservice plan create -g webapp-scstrategy -n webapp-scstrategy-plan -sku S1
az webapp create --resource-group webapp-scstrategy --plan webapp-scstrategy-plan --name webapp-scstrategy-app --runtime "DOTNETCORE|6.0"
```
- go to az portal, webapp-scstrategy-app and download publish file on `Get Publish Profile`
- go to git repo web portal, security tab and create a new secret agent, past the content of the downloaded file of previous step and save as AZURE_WEBAPP_PUBLISH_PROFILE
- commit and push your dotnet.yml file
- check your app on web brownser

5. Create CD pipeline
- setup new repo
```
git remote add azdevops https://azmariauehara@dev.azure.com/azmariauehara/websolution-scstrategy/_git/websolution-scstrategy
git push -u azdevops --all
//if got an error and 
git config http.version HTTP/1.1
```

6. Delete large file
```
git filter-branch --index-filter "git rm --cached --irnog unmatch 'websolution\webapp\wwwroot\video\file.mp4;'"
```


