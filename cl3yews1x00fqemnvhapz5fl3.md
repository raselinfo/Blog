## Chrome Extension Development Quick Guide By RaselOfficial

Hello Developers, This is [Rasel Hossain](https://raselofficial.com). And in this article, I will give a quick introduction to chrome extension development. I divide this article into 7 Parts.

1. Introduction
2. Create your first extension
3. Chrome Api’s
4. Chrome Notification
5. Chrome Context Menu
6. Context Event
7. Chrome Badge

You can also take this article as Cheat Sheet. So let's start 🥰

## Introduction
### What is Chrome Extension?
- Chrome extension is a small program that is installed in your chrome browser to customize a web browser.
- Chrome extensions are software programs, build on web technologies (such as HTML, CSS, and JS) that enable the users to customize browser features.

## How to start building a chrome extension?
- As I said we need web technology to build the chrome extension. So here we can use HTML, CSS, JS or we can choose a js library like React, Jquery
- We also need a common file named manifest.json where we will write details about our chrome extension.
- After that, we need to save our chrome extension with a .crx zipped file. So that people can download our extension from the chrome web store.

## Types of the browser extension
- Brower Action ( Can Acces at all times)
- Page Action (Only Accessible on a certain page)
- Unnoticeable Action ( It runs in the background)

## Create your first extension
### Step 1: Create a manifest.json file 
- Manifest is a JSON file. Where you can write the name, version, manifest version, and so on for your extension.
- The manifest version must be an integer and it should be 2 or 3.
- The version of your application must be 1-4 and dot-separated
- **Description: **Write about the extension
- **Icons:** Define icons for your extension. Google recommends you should provide three icons of different sizes like 128X128, 48X48 and 16X16
- **Browser Action or Action:** Browser action specific that our extension is browser action extension but in manifest version 3 this key is replaced by “action”. And in the action object, we can tell the default title, icon, popup, etc.
- **Options Page:** The options page is used to permit the users to maintain the setting of your extension

```
manifest.json

{
  "name": "demo extension",
  "version": "1.0",
  "manifest_version": 3,
  "description": "Demo extension is here",
  "icons": {
    "16": "/images/image16.png",
    "48": "/images/image48.png",
    "128": "/images/image128.png"
  },
  "action": {
    "default_icon": "/images/image48.png",
    "default_title": "Demo Extension",
    "default_popup": "popup.html"
  },
  "options_page": "options.html",
  "background": {
    "service_worker": "eventPage.js"
  },
  
  "permissions": ["storage", "notifications", "contextMenus"]
}
```

### Step 2: Add Javascript for interactivity
### Step 3: Add CSS for styling


 
## Chrome Api’s
**Note: All chrome APIs are asynchronous**

**Storage:** Chrome storage API can help you to store, retrieve, and track changes to user data. But before using this storage API we have to give the permission

```
manifest.json
{
  "permissions": ["storage"]
}
```
```
Example of Chrome Storage API: 

chrome.storage.set({ key: value }, () => {
    console.log('value is set to ' + value)
})
chrome.storage.get(['key'], (result) => {
    console.log('value is set to ' + result.key)
})
```
- If we want to track the storage changes we can use chrome storage onChanged event.

```
Example of Chrome Storage Event: 

chrome.storage.onChanged.addListener((changes,storageName)=>{
    
})
```
## Chrome Notification
- Chrome notifications come with different flavor links basic, image, list, and progress. All chrome notifications have a title, message, and small icon. To use chrome notification you should give the permission

```
manifest.json
{
 "permissions": ["notifications"]
}
```
```
Example of Chrome Notification :  

chrome.notifications.create("notificationId", {
    type: "basic",
    iconUrl: "/images/image128.png",
    title: "Ths is title",
    message: "This is message"
})
```
## Chrome Context Menu
- A chrome context menu is a menu that appears when you click the right mouse button which offers you to set or get some data. To use the context menu we need to write the background option for this event. And also we have to give the context menus permission.

```
manifest.json
{
"background": {
    "service_worker": "eventPage.js"
},
"permissions": ["contextMenus"]
}
```
- To declare a context menu you can call chrome context menus API and pass the options.

```
Example of Chrome Context Menu:  

const contextmenuItem = {
    "id": "spendMoney",
    "title": "SpendMoney",
    "contexts": ["selection"]
}
chrome.contextMenus.create(contextmenuItem)
```
## Context Event
- This event is typically triggered by clicking the right mouse button

```
Example of Chrome Context Menu Event:  

chrome.contextMenus.onClicked.addListener((contextInfo) => {

})
```
## Chrome Badge
- If you want to use the badge in your chrome extension. you can use Chrome Badge features.

```
Example of Chrome Badge:  

chrome.action.setBadgeText({ text: "Badge Text" })
```

Thanks for reading 😍