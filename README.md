<b>Lumen:</b> ServiceNow Workspace Component
Description
Lumen is a custom ServiceNow Workspace component designed by Jon DeLuna under Mars Landing Media LLC. This component bridges the gap between Workspace and Service Portal, enabling users to embed a Service Portal page into a Workspace seamlessly. It allows for interaction with and display of data from the current record in real-time, providing a dynamic and integrated user experience.

Features
Seamless Embedding: Embeds Service Portal pages within Workspace.
Dynamic Record Handling: Automatically populates record data based on the current Workspace context.
Real-Time Updates: Monitors record changes and updates dynamically.
Interactive Functionality: Synchronizes updates between Workspace and Service Portal.
Customizable Parameters: While automatically populated, properties like Table and Record ID can still be manually edited for customization.
Component Details
Workspace Component Properties
Table (parameter = 'table'): Represents the name of the table associated with the current Workspace record. This field is automatically populated but can be manually overridden if needed.
Record ID (parameter = 'record'): Refers to the SysId of the current record in the Workspace. This field is also automatically populated but is editable for custom scenarios.
Frame URL (Portal View/Page): Defines the base URL for the Service Portal page. Example: /mars_landing?id=lumen_demo.
Parameters (JSON) (parameter = 'paramjson'): Currently unused in this example setup. Reserved for future enhancements or custom use cases.
Example Configuration for Demo
Service Portal Setup
Create a new Service Portal with the URL: /mars_landing.
Do not assign a theme to the portal to ensure a clean embed.
Add a demo page named lumen_demo within the mars_landing Service Portal.
Component Configuration Example
In your Workspace component configuration interface:

Table: incident
Record ID: 12345 (example SysId)
Frame URL: /mars_landing?id=lumen_demo
These configurations will render the embedded Service Portal with the record context.

Installation
Step 1: Download and Install the Update Set
Download the marslanding_lumen update set from GitHub.
Import and commit the update set through Retrieved Update Sets in your ServiceNow instance.
Step 2: Add the Component in UI Builder
Open UI Builder and edit the desired page.
Search for the component named Mars Landing Lumen in the component library.
Drag and drop the component onto your page.
Configure the component properties:
Frame URL (Portal View/Page): Set the URL for the embedded Service Portal page (e.g., /mars_landing?id=lumen_demo).
Table: Automatically populated with the current Workspace record’s table but can be manually overridden.
Record ID: Automatically populated with the current Workspace record’s SysId but can be manually overridden.
Portal Widget Example
The following Service Portal widget example is for illustrative purposes only. It demonstrates how to interact with Workspace parameters and dynamically render record data.
