## 1.Installing Yarn on Ubuntu/Debian
first youll need to configure the repository
```shell
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```
then, you can simply
```shell
sudo apt update && sudo apt install yarn
```

## 2.Starting new project
`npm init` or `npm init -y` | `yarn init`

## 3.Add a Dependency/Package/Module
`npm install <package-name>` or `npm i <package-name>` | `yarn add <package-name>`

>- ### Direct Dependency
> 	 `npm i <package-name> --save` or `npm i <package-name> -S` | `yarn add <package-name>`
>- ### Dev Dependency
> 	 `npm i <package-name> --save-dev` or `npm i <package-name> -D` | `yarn add <package-name> --dev`
>- ### Global Dependency
> 	 `npm i <package-name> -g` | `yarn global add <package-name>`
  
## 4.Update Dependency/Package/Module
`npm update <package-name>` | `yarn upgrade <package-name>`

## 5.Update
`npm update` | `yarn upgrade`

## 6.Uninstall Dependency/Package/Module
`npm uninstall <package-name>` | `yarn remove <package-name>`

## 7.Install all Dependencies of Project
`npm i` | `yarn` or `yarn install`
