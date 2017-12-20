# spfx-kendo
By Balamurugan Kailasam  |  September 8, 2016 1:30 pm  |  1.69K views 
https://collab365.community/o365-spfx-using-kendoui-on-the-sharepoint-framework/
Categories: Development, Framework

One of the key drivers for the SharePoint Framework is to give developers the ability to implement SharePoint solutions using tools and languages that have become widespread in the community. In this post, we will illustrate how to utilise Kendo UI by Progress components within the SharePoint Framework client web parts. If you don’t know, Kendo UI is a fantastic set of controls that allows developers to build business applications by using rich UI capabilities. Before looking into the example, you may want to check out the following links to get a deeper undestanding of what problems Kendo UI solves:

**Why it makes sense to use Kendo UI:**
-	70+ responsive UI components that integrate with the SharePoint REST API.
   http://www.telerik.com/kendo-ui/ui-for-office-365-sharepoint 
-	Built-in Office 365 theme.
-	Built-in export functionality to most common office formats, such as Excel, PDF and image files.
-	Compliance with widely-recognized accessibility standards (WAI-ARIA, WCAG 2.0 and Section 508).
-  Out-of-the-box support with the KO 
-  NPM support 
-  Third-party tools support and Framework support – Require, TypeScript etc. 

## Setup the SPFX environment and create a basic client web part:
In this example, I have used the Drop 2 version of the SPFX components. If you have Drop 1 installed then you will need to upgrade.
Create a new Client Webpart using Yeoman SharePoint Generator and the Knockout template option.

## Install the Kendo UI NPM Package:
Run “npm install –save kendo-ui-core” on the terminal from the SPFX solution folder to install the Kendo UI Core components. (Note: the professional version of the Kendo UI can be downloaded as mentioned here).

## Install jQuery NPM Package:
Kendo UI components depends on jQuery, so we have to install jQuery using the “npm i –save query” command from the terminal to setup the dependencies.

## Install Typings for jQuery and Kendo UI:
1. We have to install the typings for Kendo UI and jQuery so that TypeScript can build the package without any errors.
2. Run “tsd install jquery –save” from the terminal to install the jQuery typings.
3. Run “tsd install kendo-ui –save” from the terminal to install the Kendo UI typings.
4. If the “tsd” is not installed, it can be installed by running “npm i -g tsd”.
5. Run “npm list -g –depth=0” to list all the top level packages.

## Dependencies:
After installing Kendo UI and jQuery, the dependencies in the package.json are updated as below.

1:   "dependencies": {
2:      "@microsoft/sp-client-base": "~0.2.0",
3:      "@microsoft/sp-client-preview": "~0.2.0",
4:      "@types/kendo-ui": "^2016.1.32",
5:      "jquery": "^3.1.0",
6:      "kendo-ui-core": "^2016.2.727",
7:      "knockout": "3.4.0"
8:    },

## Configure the Knockout template 
and Properties to render the “DateCreated” property:

Setup a new property “DateCreated” within the SPFX ClientWebParts within the <SPFXWebPart>WebPartProp.ts as below:

1:  export interface IKendouiWebPartProps {
2:    dateCreated: string;
3:  }

Amend the Knockout template to render the new “dateCreated” property as a writeable (text) and read-only(label):

   1:  <div data-bind="attr: {class:cssClass}">
   2:    <div data-bind="attr: {class:containerClass}">
   3:      <div data-bind="attr: {class:rowClass}">
   4:        <div class='ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1'>
   5:          <span class='ms-font-xl ms-fontColor-white'>
   6:            SharePoint Framework custom properties using Kendo UI
   7:          </span>
   8:          <p class='ms-font-l ms-fontColor-white'>
   9:            Customize SharePoint experiences using Web Parts.
  10:          </p>  
  11:          <input id='ts' data-bind="value: dateCreated">
  12:          <p class='ms-font-l ms-fontColor-white'>
  13:            <p class='ms-font-l ms-fontColor-white'>
  14:            Date Created:
  15:          </p> 
  16:          <p class='ms-font-l ms-fontColor-white' data-bind="text:dateCreated">
  17:          </p>
  18:          <a data-bind="attr: {class:buttonClass}"}
  19:            href='https://github.com/SharePoint/sp-dev-docs/wiki'>
  20:            <span class='ms-Button-label'>Learn more</span>
  21:          </a>
  22:        </div>
  23:      </div>
  24:    </div>
  25:  </div>

## Modify the <SPFX>WebPart.ts to bind the control with Kendo UI:
Import jQuery, Kendo UI Core and the Module loader

   1:  import * as jquery from 'jquery'; 
   2:  import 'kendo-ui-core';
   3:  import ModuleLoader from '@microsoft/sp-module-loader';

Load the Kendo UI css on the constructor using the module loader.

   1:  public constructor(context: IWebPartContext) {
   2:     super(context);
   3:     this._id = _instance++;
   4:     ...
   5:    ModuleLoader.loadCss('https://kendo.cdn.telerik.com/2016.2.714/styles/kendo.common.min.css');
   6:    ModuleLoader.loadCss('https://kendo.cdn.telerik.com/2016.1.112/styles/kendo.default.min.css');
   7:  
   8:     ...
   9:   
  10:    }

Overwrite the Render method to initialise the Kendo UI DatePicker control.

1:   public render(): void {
2:      $('#ts').kendoDatePicker();
3:   }


## Build and deploy the package:
Kendo UI date picker is displayed and when the date is changed the KO binding updates the content as well.
In the example above we’ve shown how to use the Kendo UI date picker component. However, as you can imagine, 
this can be easily extended to use any other UI component from Kendo UI Professional.

