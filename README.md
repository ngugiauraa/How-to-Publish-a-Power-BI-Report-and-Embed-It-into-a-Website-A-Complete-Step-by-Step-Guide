# How-to-Publish-a-Power-BI-Report-and-Embed-It-into-a-Website-A-Complete-Step-by-Step-Guide
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/by2nr47sk7cb3brstet5.jpg)
Microsoft Power BI is one of the most powerful business intelligence tools available today. Developed by Microsoft, it allows users to connect to hundreds of data sources, transform raw data using Power Query, create stunning interactive visualizations, and build sophisticated DAX measures for advanced analytics. Whether you are a data analyst in retail, finance, healthcare, or marketing, Power BI turns complex datasets into actionable insights that can be shared across teams.

The publishing and embedding process is the bridge between your local report development in Power BI Desktop and making that report available to end users on the web. Publishing uploads your .pbix file to the Power BI Service (the cloud-based platform at app.powerbi.com), where it becomes a live, refreshable report. Once published, you can generate an embed code — an HTML iframe snippet — that lets you seamlessly integrate the interactive report directly into any website, intranet portal, SharePoint page, or custom web application.

This process is not only straightforward but also highly secure when done correctly. It supports scheduled data refreshes, row-level security (RLS), and collaboration. However, it requires a Power BI Pro or Premium Per User (PPU) license for full sharing and embedding capabilities (free licenses can only publish to “My Workspace” with limited options). In this comprehensive 1,600+ word guide, we will walk through every step with detailed instructions, real-world best practices, troubleshooting tips, and high-quality screenshots to ensure you can successfully publish and embed your reports.

### Prerequisites Before You Begin

Before starting, ensure you have:
- Power BI Desktop installed (latest version from the Microsoft Store or official download page).
- A Microsoft 365 account with Power BI Pro or Premium licensing.
- A completed .pbix report file ready for publishing (with proper data modeling, relationships, and visuals).
- Access to the Power BI Service (sign in at app.powerbi.com).
- For website embedding: basic HTML knowledge or access to a CMS like WordPress, Wix, or Squarespace that supports custom HTML/iframes.

Note: If your report uses DirectQuery or Import mode with large datasets, Premium capacity is recommended for better performance and larger refresh limits.

### Step 1: Creating a Workspace in Power BI Service

Workspaces are collaborative containers in the Power BI Service. They act like folders where you can store reports, dashboards, datasets, and dataflows. Unlike “My Workspace” (personal space), shared workspaces allow team members with appropriate licenses to collaborate securely. Creating a dedicated workspace is the recommended first step for professional publishing.

**Detailed step-by-step instructions:**
1. Open your web browser and navigate to [app.powerbi.com](https://app.powerbi.com). Sign in with your work or school Microsoft account.
2. On the left navigation pane, click **Workspaces**.
3. At the bottom of the Workspaces list, click the **+ Create a workspace** button.
4. In the “Create a workspace” pane that appears on the right:
   - Enter a unique **Workspace name** (e.g., “Sales Analytics Team”).
   - Add an optional **Description**.
   - Optionally upload a custom **Icon** (recommended for branding).
   - Under **Advanced** settings, you can enable Premium capacity if available (for larger datasets and AI visuals).
5. Click **Apply** or **Create**.

The new workspace will appear in your list. You can now invite team members via the workspace settings (Manage access) and assign roles: Admin, Member, Contributor, or Viewer.

**Why this matters**: Workspaces enable governance, version history, and controlled sharing. Without one, your published report stays isolated in My Workspace.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/euxnbx97rz2iwek4wbjl.jpg)

### Step 2: Uploading and Publishing Your Report

With the workspace ready, it is time to publish the report from Power BI Desktop to the cloud.

**Detailed step-by-step instructions:**
1. Open your .pbix file in Power BI Desktop.
2. Go to **File > Publish > Publish to Power BI**.
3. In the “Publish to Power BI” dialog, sign in if prompted.
4. Select your newly created workspace from the dropdown list.
5. Click **Select** (or **Publish** in some versions).
6. Power BI will upload the file, compress datasets if necessary, and publish. You will see a success message with a direct link: “Open report in Power BI Service.”
7. Click the link to view the live report in the browser.

Once published, the report becomes a cloud asset. You can schedule automatic data refreshes under **Settings > Dataset > Scheduled refresh** (up to 8 times/day for Pro, 48 for Premium). If your model uses gateway connections for on-premises data, configure the On-premises Data Gateway first.

**Best practice tip**: Always use a dedicated workspace and publish under a service principal account in enterprise environments to avoid license conflicts.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nyq1lkuhi8v94kkd9ygv.jpg)

### Step 3: Generating the Embed Code in Power BI Service

Now that the report is live in the service, generate the embed code for website integration.

**Detailed step-by-step instructions:**
1. In the Power BI Service, navigate to your workspace and open the published report.
2. At the top-right of the report canvas, click the **... (ellipsis)** menu.
3. Select **Embed > Embed in website or portal** (this is the standard public-embed option; for secure enterprise embedding, use Power BI Embedded API later).
4. A new pane opens displaying the embed code: an HTML `<iframe>` snippet with your report’s unique URL, width, height, and parameters.
5. Customize options if needed:
   - **Allow filters** (to show slicers).
   - **Show navigation** (page tabs).
   - **Fit to page** or fixed dimensions.
6. Click **Copy** to copy the entire iframe code to your clipboard.
7. (Optional) For more control, use **Embed > Secure embed** or generate an embed token via the Power BI REST API for authenticated scenarios.

**Important security note**: The default “Embed in website or portal” makes the report publicly accessible (anyone with the link can view it). For sensitive data, use row-level security, publish to a private app, or implement Power BI Embedded with Azure AD authentication.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kxt16az9cstz40zirkb8.jpg)

### Step 4: Embedding the Report on a Website

Embedding is as simple as pasting the iframe code into your website’s HTML.

**Detailed step-by-step instructions:**
1. Open your website’s HTML editor (or CMS code block):
   - For static HTML sites: edit the .html file.
   - For WordPress: add a Custom HTML block.
   - For SharePoint: use the Embed web part.
2. Paste the copied iframe code inside the `<body>` section where you want the report to appear. Example code:

```html
<iframe 
  width="100%" 
  height="800" 
  src="https://app.powerbi.com/reportEmbed?reportId=xxxxxxxx&groupId=yyyyyyyy" 
  frameborder="0" 
  allowFullScreen="true">
</iframe>
```

3. Adjust `width` and `height` for responsiveness (use CSS media queries or `width="100%"` with a container div).
4. Add styling for seamless integration:

```html
<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" 
    src="YOUR_EMBED_URL" 
    frameborder="0" 
    allowfullscreen>
  </iframe>
</div>
```

5. Save and publish the page. Test the embed on desktop and mobile devices.
6. Optional enhancements:
   - Add JavaScript to handle report events (e.g., filtering via postMessage API).
   - For production websites, consider Power BI Embedded (Azure service) for custom authentication and branding removal.

**Troubleshooting common issues**:
- Blank iframe: Check browser CORS policy or embed URL parameters.
- “Report not found”: Verify workspace permissions.
- Slow loading: Optimize your data model and use Direct Lake mode if on Premium.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1c3i8f1kbvnrew9npj82.jpg)

### Advanced Considerations and Best Practices

For enterprise-scale embedding, move beyond simple iframes to Power BI Embedded capacity in Azure. This allows you to embed reports into custom applications without requiring viewers to have Power BI licenses. You generate embed tokens programmatically via REST APIs and can white-label the experience completely.

Always implement:
- Row-level security (RLS) to show users only their data.
- Automatic page refresh settings.
- Usage monitoring via the Power BI admin portal.
- Mobile-optimized layouts (Power BI reports automatically adapt, but test thoroughly).

Common pitfalls include exceeding dataset size limits (1 GB for Pro, 10 GB+ for Premium) and forgetting to set up gateway refreshes for on-premises sources.

### Conclusion: Key Insights

Publishing a Power BI report and embedding it into a website democratizes data access, turning static PDFs into live, interactive experiences. The entire process — from workspace creation to iframe integration — can be completed in under 15 minutes once you are familiar with the UI. The combination of Power BI Desktop’s authoring power and the Service’s cloud scalability makes it an unbeatable solution for organizations of any size.

Key insights to remember:
1. Always publish to a shared workspace for collaboration and governance.
2. Use “Embed in website or portal” for quick public sharing; upgrade to Power BI Embedded for secure, licensed-free viewing.
3. Test embeds across devices and browsers before going live.
4. Monitor performance and security — a well-embedded report can drive business decisions instantly.
5. Keep your data model optimized; poor modeling causes slow embeds regardless of hosting.

By following this guide, you now have the complete technical knowledge to publish professional-grade Power BI reports and seamlessly integrate them into any website. Start experimenting today — your next data-driven web experience is just a few clicks away.

This article is also available on:

- Medium: [ngugiauraa]()

- Dev.to: [ngugiauraa](https://dev.to/ngugiauraa/how-to-publish-a-power-bi-report-and-embed-it-into-a-website-a-complete-step-by-step-guide-o5f)

- Linkedin:  [Jesse Ngugi]()
 


