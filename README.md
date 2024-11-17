# Mars Landing Media - Lumen: Service Portal Inside Workspace
Developer: Jon DeLuna
## Description

Lumen is a custom ServiceNow Workspace component designed by **Jon DeLuna** under **Mars Landing Media LLC**. This component bridges the gap between Workspace and Service Portal, enabling users to embed a Service Portal page into a Workspace seamlessly. It allows for interaction with and display of data from the current record in real-time, providing a dynamic and integrated user experience.

## Features

- **Seamless Embedding**: Embeds Service Portal pages within Workspace.
- **Dynamic Record Handling**: Automatically populates record data based on the current Workspace context.
- **Real-Time Updates**: Monitors record changes and updates dynamically.
- **Interactive Functionality**: Synchronizes updates between Workspace and Service Portal.
- **Customizable Parameters**: While automatically populated, properties like **Table** and **Record ID** can still be manually edited for customization.

## Component Details

### Workspace Component Properties

- **Table (parameter = 'table')**: Represents the name of the table associated with the current Workspace record. This field is **automatically populated** but can be manually overridden if needed.
- **Record ID (parameter = 'record')**: Refers to the SysId of the current record in the Workspace. This field is also **automatically populated** but is editable for custom scenarios.
- **Frame URL (Portal View/Page)**: Defines the base URL for the Service Portal page. Example: `/mars_landing?id=lumen_demo`.
- **Parameters (JSON) (parameter = 'paramjson')**: Currently unused in this example setup. Reserved for future enhancements or custom use cases.

## Example Configuration for Demo

### Service Portal Setup
1. Create a new Service Portal with the URL: `/mars_landing`.
2. Do not assign a theme to the portal to ensure a clean embed.
3. Add a demo page named `lumen_demo` within the `mars_landing` Service Portal.

### Component Configuration Example
In your Workspace component configuration interface:
- **Table**: `incident`
- **Record ID**: `12345` (example SysId)
- **Frame URL**: `/mars_landing?id=lumen_demo`

These configurations will render the embedded Service Portal with the record context.

## Installation

### Step 1: Download and Install the Update Set
1. Download the `marslanding_lumen` update set.
2. Import and commit the update set through **Retrieved Update Sets** in your ServiceNow instance.

### Step 2: Add the Component in UI Builder
1. Open **UI Builder** and edit the desired page.
2. Search for the component named **Mars Landing Lumen** in the component library.
3. Drag and drop the component onto your page.
4. Configure the component properties:
   - **Frame URL (Portal View/Page)**: Set the URL for the embedded Service Portal page (e.g., `/mars_landing?id=lumen_demo`).
   - **Table**: Automatically populated with the current Workspace record’s table but can be manually overridden.
   - **Record ID**: Automatically populated with the current Workspace record’s SysId but can be manually overridden.

## Portal Widget Example

The following Service Portal widget example is for **illustrative purposes only**. It demonstrates how to interact with Workspace parameters and dynamically render record data.

### Server-Side Script
```javascript
(function() {
    data.tbl = $sp.getParameter('table');
    data.rcd = $sp.getParameter('record');

    var getData = new GlideRecord(data.tbl);
    getData.get(data.rcd);

    data.recNumber = getData.number.toString();
    data.openedFor = getData.opened_for.name.toString();
    data.shortDescription = getData.short_description.toString();
})();
```
### Client-Side Script
```javascript
api.controller=function($scope,spUtil) {
    var c = this;

    c.getRcd = String($scope.data.rcd);

    var getRcd = String($scope.data.rcd);
    var getTbl = String($scope.data.tbl);

    spUtil.recordWatch($scope,getTbl,"sys_id="+getRcd,function(name){
        $scope.$apply();
        spUtil.update($scope);
    });
};
```


### HTML Template
```html
<div>
  
<div id="header">
<table width="100%">
  <tr>
  <td width="20%"><svg width="48" height="48" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="m16.59 14a24.69 24.69 0 0 1 11.06-6.52c6.56-1.63 11.81-1 15.37 1.25s4.63 4.37 4.63 4.37l2.35-1.75s-2.31-5.5 2.57-6.81 5.81 2.69 5.62 5.81-2.35 3.75-3.19 3.88a9.11 9.11 0 0 1 -2.69-.44l-2.68 4a15.54 15.54 0 0 1 1.48 6.21 37.51 37.51 0 0 1 -.11 5.58s3.59 1.5 3.71 1.5 2.92-1 3.92-.17.71 1.59.71 1.59 2 0 1.54 1.75a2.75 2.75 0 0 1 -1.67 2.08 1.16 1.16 0 0 1 .5 1.54 2.64 2.64 0 0 1 -3.27 1.13 6.39 6.39 0 0 1 -2.33-3.17 8 8 0 0 1 -.29-1.54l-3.17-1s-2.58 8.62-3.71 12.16-1.79 5.84-1.79 5.84 3.87 0 4.33 1.91.42 4.92 0 5.21-5 .67-8.41.67-4.54-.79-4.5-1.33 0-7.55-.25-7.67a16.22 16.22 0 0 0 -4 0c-1.67.16-2.88.62-2.92 1s.25 7.29 0 7.75-6.25.95-10.17 1-4.58 0-4.58-.42-.67-5 .63-5.71a19 19 0 0 1 4.7-1s-2.87-7.83-4.29-11.75-2.37-6.92-2.37-6.92l-3.25.97s.29 1.62-.5 2.21-2.25 1-3 0a2.48 2.48 0 0 1 -.34-2.09 2.75 2.75 0 0 1 -1.33-2.41c.21-1.46.79-2 1.13-2.17a2.63 2.63 0 0 1 .87-.08s.87-1.63 2.1-1.3a1.59 1.59 0 0 1 1.3 1.34l2.25-.84a16.34 16.34 0 0 1 -.13-7 11.6 11.6 0 0 1 2.29-5.25l-4.41-4.62a5.46 5.46 0 0 1 -4.13.92c-2.17-.55-4.17-2.71-2.44-6s7.27-3.59 8.63-1.71 0 4.33 0 4.33z" fill="#1d1d1b"></path> <path d="m8.32 31.37-.55-.87s.21-1 1.05-.63 1 1.59 1.12 1.54 2.5-.95 2.63-.7.54 2.41.54 2.41-4 1-4 1.25.33 1.63-.21 2.09-1.33.5-1.5.16-.29-1.16 0-1.21.58-.2.58-.33-.08-.71-.08-.71-1 .34-1.5-.21-.92-2.08-.4-2.45a1.38 1.38 0 0 1 1.54-.09c.19.25.78-.25.78-.25z" fill="#ddc07c"></path> <path d="m12.15 31.41c.08.13.29.71.08.84a2.35 2.35 0 0 1 -.79.12s-.37-.54-.21-.66a4.31 4.31 0 0 1 .92-.3z" fill="#1d1d1b"></path> <path d="m8.48 6c1.73-.32 3.21.41 3.46 2s-1.83 4-3.25 4.58-3.33.46-4.12-.75-1.05-4.92 3.91-5.83z" fill="#fab900"></path> <path d="m12 11.21a37.25 37.25 0 0 1 4 3.79 5 5 0 0 1 -.75 1.29s-4.25-3.67-4.1-3.88.85-1.2.85-1.2z" fill="#ddc07c"></path> <path d="m52.9 5.75c1.41-.46 3.83-.21 4.37 3.08s-1.5 4.54-3.54 4.13a3.52 3.52 0 0 1 -2.87-3.88c.08-1.83.87-2.96 2.04-3.33z" fill="#fab900"></path> <path d="m50.52 12.16c.13.17 1.21 1 1.09 1.17s-2.29 3-2.29 3a19.78 19.78 0 0 1 -1-2.21c.04-.12 2.2-1.96 2.2-1.96z" fill="#ddc07c"></path> <path d="m25.27 9.71c2.44-1.12 8.67-1.92 13-1.25s8.73 5.87 9.73 9.54a50.26 50.26 0 0 1 1.34 7.58s-3.63-2.16-3.8-2-.2.75-.08.84 3.79 1.66 3.88 2 0 2.58 0 2.58a33.71 33.71 0 0 0 -3.63-1.58c-.08.12-.46.62 0 .75a22.81 22.81 0 0 1 3.46 2c0 .16-.33 2.7-.33 2.7s-2.75-1.54-2.88-1.5-.29.59-.12.63 2.87 1.67 2.83 1.92-3.67 11.83-3.81 11.87a21.14 21.14 0 0 1 -2.17-.92s-.33.59-.17.67 2.13.87 2 1.08-.38 1-.38 1a13.08 13.08 0 0 0 -2.33-1.08c-.13.12-.34.42-.13.58a23.7 23.7 0 0 1 2.32 1.09c0 .16 0 .83-.12.83a22.27 22.27 0 0 0 -2.52-1.04c-.21.08-.46.5-.21.66s2.46 1.09 2.42 1.34a5.33 5.33 0 0 1 -.38.87 22.57 22.57 0 0 0 -2.25-1.29c-.12 0-.29.62-.17.71a13.53 13.53 0 0 1 2 1.29c0 .12-2.66.29-2.7.62a1.91 1.91 0 0 0 0 .92c.08.17 3 0 4.83.25s2.63.21 2.71.67.29 3.29 0 3.37-5.71 0-7.08-.08-2.13-.33-2.13-.58-.08-7.75-.29-8-3.25-.63-5.71-.5a14 14 0 0 0 -4.46 1 8.58 8.58 0 0 0 -1.29-1.05c-.17 0-.58.3-.46.5s1.25 1.13 1.25 1.25a4 4 0 0 1 -.08.5 20.39 20.39 0 0 0 -3-1.87c-.17.12-.37.62-.17.75a29.24 29.24 0 0 1 3.13 2.33c0 .21.08 1.21.08 1.21s-2.62-1.75-2.79-1.5-.21.79-.08.88 2.79 1.25 2.83 1.54a22.45 22.45 0 0 1 0 3.75c-.16.21-10.62 1-10.75.58s-.12-3.5.17-3.71 6.46-1 6.54-1.21.08-.75-.12-.79-1.38 0-1.42-.08-5.54-14.13-6.75-19.21-1.67-11.83 1.97-16.62 5.27-5.42 8.27-6.79z" fill="#8ec480"></path> <g fill="#1d1d1b"> <path d="m33.32 11.62c.33 0 .33 1 .2 1a11.13 11.13 0 0 0 -6.79 1.88c-3.37 2.33-3.75 3.17-4 3.08s-.7-.25-.62-.46a14.07 14.07 0 0 1 11.17-5.54z"></path> <path d="m43.9 14.91a5.07 5.07 0 0 1 2.17 1.21c0 .21 0 .59-.21.46a16.21 16.21 0 0 1 -2-1c-.09-.17-.17-.5.04-.67z"></path> <path d="m44.57 17.71s2.79 1.12 3 1.7.33.71.08.67a18.75 18.75 0 0 1 -3.17-1.58c-.04-.21-.04-.71.09-.79z"></path> <path d="m45.07 20.83a19.27 19.27 0 0 1 3.08 1.71c.08.29.37.71 0 .54a28.64 28.64 0 0 1 -3.21-1.54 3.11 3.11 0 0 1 .13-.71z"></path> </g> <path d="m51.19 30.58c.17.08 3.58 1.54 3.71 1.58s2-.87 3-.58.75.83.66 1.08-.37.75-.16.92.21.29.33.29.54-.62.88-.41a1.16 1.16 0 0 1 .12 1.54 5.3 5.3 0 0 1 -1.58 1.21c-.17 0-.25.5-.08.62s1.08.42.87.79a1.58 1.58 0 0 1 -2.42.46c-1.2-1-1.58-3.67-1.62-3.87a2.43 2.43 0 0 0 -.5-.92 35.91 35.91 0 0 1 -3.5-1.13c0-.16.29-1.58.29-1.58z" fill="#ddc07c"></path> <path d="m32.57 39.08c.16 0 3.66.42 6.2-.83s4.09-3.25 4.42-3.17.79.58.71.75a10 10 0 0 1 -4.63 4.17c-3.16 1.41-6.29 1.54-6.54 1.29s-.58-2.13-.16-2.21z" fill="#1d1d1b"></path> <path d="m30.69 18.16c3.71-.82 9.08.21 11.17 4.63s1.54 10.33-3.29 13.08-11.3 2.67-14.3-.21-5.16-14.91 6.42-17.5z" fill="#1d1d1b"></path> <path d="m30.93 19.49c3.2-.71 7.84.18 9.64 4s1.33 8.92-2.84 11.29-9.73 2.3-12.34-.18-4.46-12.88 5.54-15.11z" fill="#e6e4da"></path> <path d="m31.46 25a3 3 0 0 1 2.38 5.35c-1.46.83-3.41.81-4.32-.06a3.27 3.27 0 0 1 1.94-5.29z" fill="#1d1d1b"></path> <path d="m32.23 26a1.6 1.6 0 0 1 1.59.46c.41.5-1 1.66-1.17 1.58s-1.17-1.63-.42-2.04z" fill="#e6e4da"></path> </g></svg></td>
  <td width="80%" style="display: flex; align-items: center; justify-content: center;"><h3>MARS LANDING MEDIA LLC</h3></td>
  </tr>
  </table>  
</div> 
  
<div id="recData">
   <div><label style="margin-right:3px;">Table From Workspace parameter:</label><span>{{data.tbl}}</span></div>
 <div><label style="margin-right:3px;">SysId From Workspace parameter:</label><span>{{data.rcd}}</span></div>
 <div><label style="margin-right:3px;">Record Number:</label><span>{{data.recNumber}}</span></div>
 <div><label style="margin-right:3px;">Opened For:</label><span>{{data.openedFor}}</span></div>
 <div><label style="margin-right:3px;">Short Description:</label><span>{{data.shortDescription}}</span></div>
</div>  
  
  
<div id="message">
    This portal widget can be configured to display or interact with the workspace record data.
    Workspace is always listening to the record, so as soon as you update it from the portal widget it should refresh workspace.
</div>
  
</div>
```

### CSS
```css
label {font-weight: bold;}
#recData{margin-top:50px;}
#message{margin-top:50px;}
```


