    <h1>Mars Landing Lumen Component</h1>

    <div class="section">
        <h2>Description</h2>
        <p>
            Lumen is a custom ServiceNow Workspace component designed by <strong>Jon DeLuna</strong> under <strong>Mars Landing Media LLC</strong>.
            This component bridges the gap between Workspace and Service Portal, enabling users to embed a Service Portal page into a Workspace seamlessly. 
            It allows for interaction with and display of data from the current record in real-time, providing a dynamic and integrated user experience.
        </p>
    </div>

    <div class="section">
        <h2>Features</h2>
        <ul>
            <li><strong>Seamless Embedding:</strong> Embeds Service Portal pages within Workspace.</li>
            <li><strong>Dynamic Record Handling:</strong> Automatically populates record data based on the current Workspace context.</li>
            <li><strong>Real-Time Updates:</strong> Monitors record changes and updates dynamically.</li>
            <li><strong>Interactive Functionality:</strong> Synchronizes updates between Workspace and Service Portal.</li>
            <li><strong>Customizable Parameters:</strong> Properties like <strong>Table</strong> and <strong>Record ID</strong> can still be manually edited.</li>
        </ul>
    </div>

    <div class="section">
        <h2>Component Details</h2>
        <h3>Workspace Component Properties</h3>
        <ul>
            <li><strong>Table (parameter = 'table'):</strong> Automatically populated with the current Workspace record's table but can be manually overridden.</li>
            <li><strong>Record ID (parameter = 'record'):</strong> Automatically populated with the current Workspace record's SysId but is editable.</li>
            <li><strong>Frame URL (Portal View/Page):</strong> Base URL for the Service Portal page (e.g., <code>/mars_landing?id=lumen_demo</code>).</li>
            <li><strong>Parameters (JSON) (parameter = 'paramjson'):</strong> Reserved for future enhancements.</li>
        </ul>
    </div>

    <div class="section">
        <h2>Installation</h2>
        <h3>Step 1: Download and Install the Update Set</h3>
        <ul>
            <li>Download the <code>marslanding_lumen</code> update set from <a href="<insert_github_url_here>" target="_blank">GitHub</a>.</li>
            <li>Import and commit the update set through <strong>Retrieved Update Sets</strong> in your ServiceNow instance.</li>
        </ul>
        <h3>Step 2: Add the Component in UI Builder</h3>
        <ul>
            <li>Open <strong>UI Builder</strong> and edit the desired page.</li>
            <li>Search for the component named <strong>Mars Landing Lumen</strong> in the component library.</li>
            <li>Drag and drop the component onto your page.</li>
            <li>Configure the component properties:
                <ul>
                    <li><strong>Frame URL (Portal View/Page):</strong> Set the URL for the embedded Service Portal page (e.g., <code>/mars_landing?id=lumen_demo</code>).</li>
                    <li><strong>Table:</strong> Automatically populated with the current Workspace record’s table but can be manually overridden.</li>
                    <li><strong>Record ID:</strong> Automatically populated with the current Workspace record’s SysId but can be manually overridden.</li>
                </ul>
            </li>
        </ul>
    </div>

    <div class="section">
        <h2>Example Configuration for Demo</h2>
        <h3>Service Portal Setup</h3>
        <ul>
            <li>Create a new Service Portal with the URL: <code>/mars_landing</code>.</li>
            <li>Do not assign a theme to the portal to ensure a clean embed.</li>
            <li>Add a demo page named <code>lumen_demo</code> within the <code>mars_landing</code> Service Portal.</li>
        </ul>
        <h3>Component Configuration Example</h3>
        <p>
            <strong>Table:</strong> <code>incident</code><br>
            <strong>Record ID:</strong> <code>12345</code> (example SysId)<br>
            <strong>Frame URL:</strong> <code>/mars_landing?id=lumen_demo</code>
        </p>
    </div>

    <div class="section">
        <h2>Portal Widget Example</h2>
        <h3>Server-Side Script</h3>
        <pre><code>(function() {
    data.tbl = $sp.getParameter('table');
    data.rcd = $sp.getParameter('record');

    var getData = new GlideRecord(data.tbl);
    getData.get(data.rcd);

    data.recNumber = getData.number.toString();
    data.openedFor = getData.opened_for.name.toString();
    data.shortDescription = getData.short_description.toString();
})();</code></pre>

        <h3>Client-Side Script</h3>
        <pre><code>api.controller=function($scope,spUtil) {
    var c = this;

    c.getRcd = String($scope.data.rcd);

    var getRcd = String($scope.data.rcd);
    var getTbl = String($scope.data.tbl);

    spUtil.recordWatch($scope,getTbl,"sys_id="+getRcd,function(name){
        $scope.$apply();
        spUtil.update($scope);
    });
};</code></pre>

        <h3>HTML Template</h3>
        <pre><code>&lt;div&gt;
    &lt;div id="header"&gt;
        &lt;table width="100%"&gt;
            &lt;tr&gt;
                &lt;td width="20%"&gt;&lt;svg width="48" height="48"&gt;...&lt;/svg&gt;&lt;/td&gt;
                &lt;td width="80%" style="display: flex; align-items: center; justify-content: center;"&gt;
                    &lt;h3&gt;MARS LANDING MEDIA LLC&lt;/h3&gt;
                &lt;/td&gt;
            &lt;/tr&gt;
        &lt;/table&gt;
    &lt;/div&gt;
    &lt;div id="recData"&gt;
        &lt;div&gt;&lt;label&gt;Table From Workspace parameter:&lt;/label&gt;&lt;span&gt;{{data.tbl}}&lt;/span&gt;&lt;/div&gt;
        &lt;div&gt;&lt;label&gt;SysId From Workspace parameter:&lt;/label&gt;&lt;span&gt;{{data.rcd}}&lt;/span&gt;&lt;/div&gt;
        &lt;div&gt;&lt;label&gt;Record Number:&lt;/label&gt;&lt;span&gt;{{data.recNumber}}&lt;/span&gt;&lt;/div&gt;
        &lt;div&gt;&lt;label&gt;Opened For:&lt;/label&gt;&lt;span&gt;{{data.openedFor}}&lt;/span&gt;&lt;/div&gt;
        &lt;div&gt;&lt;label&gt;Short Description:&lt;/label&gt;&lt;span&gt;{{data.shortDescription}}&lt;/span&gt;&lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;</code></pre>
    </div>

    <div class="section">
        <h2>Author</h2>
        <p>Developed by <strong>Jon DeLuna</strong> under <strong>Mars Landing Media LLC</strong>.</p>
    </div>

    <div class="section">
        <h2>License</h2>
        <p>This project is licensed under the MIT License. See the <code>LICENSE</code> file for details.</p>
    </div>

