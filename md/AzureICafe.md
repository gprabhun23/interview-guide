**1. What is the difference between an Azure Tenant and Azure Subscription?**  
- Azure Tenant represents an instance of Azure Active Directory, used to manage users and applications across an organization.  
- Azure Subscription provides access to Azure services and resources with billing tied to it.  
- A tenant can have multiple subscriptions, but a subscription can only belong to one tenant.  
- In my project, I linked multiple Azure subscriptions under a single tenant for unified user management.  

**2. What is the difference between Azure API Apps, Logic Apps, Web Apps, and Azure Functions?**  
- API Apps are designed for hosting and managing APIs with built-in API management features.  
- Logic Apps provide workflow automation and integration without writing code.  
- Web Apps are used to host and manage web applications on Azure App Service.  
- I used Azure Functions in my project to execute serverless background tasks triggered by events.  

**3. What is Azure CDN (Content Delivery Network) and why use it?**  
- Azure CDN distributes content globally to reduce latency and improve load times.  
- It caches content at strategically located edge servers closer to users.  
- It supports static content like images, videos, or JavaScript files.  
- In my project, we used Azure CDN to cache large media files for a global video streaming application.  

**4. What is the difference between Azure AD Application Permissions and Delegated Permissions?**  
- Application Permissions are used by applications to access resources without user interaction.  
- Delegated Permissions are used to access resources on behalf of a signed-in user.  
- Application Permissions are ideal for backend services, while Delegated Permissions are for client apps.  
- I used Delegated Permissions for an Angular app requiring user consent to access Microsoft Graph.  

**5. What are ARM Templates in Azure?**  
- ARM Templates are JSON files used to define and deploy Azure infrastructure.  
- They enable declarative infrastructure management and support versioning.  
- They support parameterization for reusable templates across environments.  
- In my project, I used an ARM template to provision a Cosmos DB account and a web app in a single deployment.  

**6. When would you use Azure CLI vs PowerShell? Explain.**  
- Azure CLI is better for cross-platform scripting and is lightweight.  
- PowerShell integrates well with Windows-based environments and supports automation tasks.  
- Both can manage Azure resources, but the choice depends on the environment and language preference.  
- I used Azure CLI in a CI/CD pipeline for deploying microservices to Azure Kubernetes Service.  

**7. What is the rule of thumb for choosing the ideal partitioning key in Cosmos DB?**  
- Choose a key with high cardinality to distribute data evenly across partitions.  
- The key should minimize cross-partition queries for better performance.  
- Avoid keys that lead to hot partitions or uneven distribution.  
- In my project, we used the `userId` field as the partition key for a multi-tenant application.  

**8. What is WebJob in Azure?**  
- WebJobs are background tasks associated with Azure App Service.  
- They support running continuously or on-demand with manual or scheduled triggers.  
- They are ideal for recurring tasks like data processing or cleanup.  
- I used WebJobs to process and archive log files from a web application nightly.  

**9. Is there a way to view deployed files in Azure?**  
- Yes, use Kudu (Advanced Tools) in Azure App Service to access the deployed files.  
- Navigate to `https://<appname>.scm.azurewebsites.net` for the Kudu interface.  
- It provides tools for file exploration, debugging, and deployment logs.  
- In one project, I used Kudu to verify if a configuration file was correctly deployed to a staging environment.  

**10. When would you use Azure Storage Queues vs Azure Service Bus?**  
- Use Azure Storage Queues for simple, lightweight, and scalable messaging.  
- Use Azure Service Bus for advanced features like dead-letter queues and transactional messages.  
- Service Bus is better for enterprise-grade integration scenarios.  
- I used Service Bus to implement reliable communication between microservices requiring guaranteed delivery.  

**11. What is RU (Request Unit) in Cosmos DB?**  
- RU (Request Unit) measures throughput in Cosmos DB for operations.  
- It abstracts compute, memory, and IOPS costs into a single unit.  
- Provision RUs based on workload requirements to ensure performance.  
- In my project, I allocated 400 RUs to a collection handling moderate read/write operations.  

**12. What is the difference between Azure Queue Storage and Azure Service Bus with regards to dead-letter queues & poison messages?**  
- Azure Queue Storage lacks built-in dead-letter queues; you must implement custom logic.  
- Azure Service Bus includes native dead-letter queues for message processing issues.  
- Service Bus also supports automatic handling of poison messages.  
- I used Service Bus dead-letter queues to diagnose failures in message processing for an e-commerce application.  

**13. Explain the difference between Event vs Message Services in the context of Azure Services.**  
- Events are lightweight notifications indicating state changes (e.g., Azure Event Grid).  
- Messages contain raw data for processing, often between applications (e.g., Azure Service Bus).  
- Use events for broadcast notifications and messages for reliable data delivery.  
- In my project, Event Grid was used to notify microservices of database changes.  

**14. What’s the difference between Azure SQL Database and Azure SQL Managed Instance?**  
- Azure SQL Database is a fully managed PaaS for single databases or elastic pools.  
- Azure SQL Managed Instance provides near 100% compatibility with on-premises SQL Server.  
- Use Managed Instance for migrating legacy applications; SQL Database is better for cloud-native apps.  
- I used SQL Managed Instance to lift and shift an on-premises ERP system to Azure.  

**15. How to do a transaction with two collections on Azure CosmosDB?**  
- Cosmos DB supports multi-document transactions within a single logical partition.  
- Use stored procedures for cross-collection operations within the same partition.  
- Cross-partition transactions require custom handling or external frameworks.  
- In my project, I created a stored procedure to update inventory and order records atomically.  

```csharp
function updateDocuments(order, inventory) {
    var context = getContext();
    var collection = context.getCollection();
    
    var isAccepted = collection.createDocument(collection.getSelfLink(), order, function(err) {
        if (err) throw new Error("Failed to create order");
    });
    if (!isAccepted) throw new Error("Order creation was not accepted");

    isAccepted = collection.replaceDocument(inventory._self, inventory, function(err) {
        if (err) throw new Error("Failed to update inventory");
    });
    if (!isAccepted) throw new Error("Inventory update was not accepted");
}
```  


**16. What is Azure Web PubSub Service? When shall you use it?**  
- Azure Web PubSub Service enables real-time web communication over WebSocket.  
- It's suitable for scenarios requiring low-latency updates, like chat apps or live dashboards.  
- It supports multiple client protocols and integrations with existing systems.  
- I used Web PubSub to deliver live score updates for a sports application.  

**17. What Is Azure Resource Manager (ARM)?**  
- ARM is the deployment and management service for Azure resources.  
- It uses declarative templates for creating, updating, or deleting resources.  
- ARM ensures resource dependency management and consistent deployments.  
- In my project, I used ARM to deploy a full-stack application, including a web app and database.  

**18. How can I test my ARM template before deploying it?**  
- Use the `az deployment what-if` command to preview changes without deploying.  
- Validate the template structure using `az deployment validate`.  
- Deploy in a test environment first to ensure correctness.  
- I used `az deployment what-if` to identify potential misconfigurations before deploying a staging environment.  

**19. What is a Logical Partition in Cosmos DB?**  
- A logical partition groups data with the same partition key for efficient querying.  
- It provides a scope for transactions and local indexing.  
- Each logical partition can store up to 20GB of data in Cosmos DB.  
- I used the `orderId` as a partition key in an e-commerce project to group all order-related items together.  

**20. When would you use Azure Event Grid vs Azure Service Bus and vice versa?**  
- Use Event Grid for event-driven architectures with high throughput and low latency.  
- Service Bus is better for message-driven architectures with guaranteed delivery.  
- Event Grid is ideal for broadcasting events, while Service Bus handles complex workflows.  
- In one project, Event Grid was used to notify microservices of resource changes, while Service Bus handled order processing.  

**21. What’s the difference between Logical and Physical partitions in Cosmos DB?**  
- Logical partitions group data based on partition key; they are user-defined.  
- Physical partitions are managed by Cosmos DB and store logical partitions.  
- Physical partitions can span multiple logical partitions for scalability.  
- In a multi-tenant app, logical partitions represented tenants, while physical partitions were abstracted by Cosmos DB.  

**22. Explain the difference between At-most-once vs At-least-once message processing in Azure Service Bus.**  
- At-most-once ensures no duplicate message delivery but may drop messages.  
- At-least-once ensures every message is processed but may result in duplicates.  
- Use at-most-once for idempotent operations and at-least-once for critical tasks.  
- I implemented at-least-once processing to ensure reliable order placement in a retail system.  

**23. What does "Cosmos DB automatically indexes the documents" mean? Explain.**  
- Cosmos DB indexes all data by default for efficient queries.  
- This eliminates the need for manual index management.  
- You can customize indexing policies to include or exclude specific fields.  
- I disabled indexing for large blobs in a document to optimize query performance in a logging system.  

**24. Name some pros and cons of using GUID as Partition Key in Cosmos DB.**  
- Pros: Ensures high cardinality, avoids hot partitions, and distributes data evenly.  
- Cons: Difficult to query by GUID and lacks semantic meaning.  
- It's suitable for scenarios prioritizing write scalability over query efficiency.  
- In one project, I used GUIDs for write-intensive logs to achieve even partitioning.  

**25. Using Azure Functions, can I reference and use NuGet packages in my C# function?**  
- Yes, NuGet packages can be referenced by adding them to the `function.proj` file.  
- Use the `#r` directive for package references in the script-based approach.  
- Ensure the package version aligns with the Azure Functions runtime.  
- I referenced `Azure.Storage.Blobs` in an Azure Function to process uploaded files.  

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net6.0</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Azure.Storage.Blobs" Version="12.12.0" />
  </ItemGroup>
</Project>
```  

**26. What are Web Role, Worker Role, and VM Role in Azure?**  
- Web Role is for hosting web applications using IIS.  
- Worker Role runs background tasks independent of IIS.  
- VM Role provides OS-level control for custom software installations.  
- I used Worker Roles for data processing tasks in an IoT solution.  

**27. What is the difference between an API App and a Web App?**  
- API Apps specialize in hosting APIs with enhanced API management.  
- Web Apps focus on hosting and managing full-stack web applications.  
- Both run on Azure App Service but have distinct optimizations.  
- I deployed an API App to manage backend services for a mobile application.  

**28. What are On Demand WebJobs, Scheduled WebJobs, and Triggered WebJobs in Azure?**  
- On Demand WebJobs run manually via Azure portal or API.  
- Scheduled WebJobs run at specified intervals using CRON expressions.  
- Triggered WebJobs are invoked by external events like queue messages.  
- In my project, Scheduled WebJobs generated daily reports for analytics.  

**29. What are the differences between Classic and Storage Accounts in Azure?**  
- Classic accounts use older deployment models with limited scalability.  
- Storage accounts support the ARM model and advanced features.  
- Modern storage accounts integrate with Azure RBAC and diagnostic logs.  
- I migrated classic accounts to ARM-based accounts for better governance and security.  

**30. What to use: many small Azure Storage Blob containers vs one really large container with tons of blobs?**  
- Use many small containers for better organization and access control.  
- Use a large container for simpler management when blobs have uniform access patterns.  
- Consider performance implications for scenarios with high throughput.  
- I opted for separate containers to segregate media files by department in a media management system.  

**31. How would you choose between Azure Blob Storage vs Azure File Service?**  
- Use Azure Blob Storage for unstructured data like media files, backups, or logs.  
- Use Azure File Service for file shares that require SMB protocol and directory structures.  
- Blob Storage offers more scalability, while File Service supports lift-and-shift scenarios.  
- I used Azure File Service to provide shared storage for legacy applications during migration.  

**32. What is the difference between an Azure Web App and an Azure Web Role?**  
- Azure Web App is a PaaS offering to host web applications with built-in scaling and monitoring.  
- Azure Web Role is part of the deprecated Cloud Services model used to host IIS-based apps.  
- Web Apps are easier to manage and integrate with modern Azure services.  
- I migrated a Web Role-based application to Azure Web App for improved manageability and features.  

**33. When to choose Worker Role vs Web Jobs on Azure?**  
- Worker Roles are standalone VMs for intensive background tasks (deprecated).  
- WebJobs run within the App Service environment for lightweight background processing.  
- WebJobs integrate better with modern services and are easier to deploy and scale.  
- I used WebJobs for periodic data synchronization in a SaaS platform.  

**34. Explain the use of Claim Check Pattern in Azure Event Grid.**  
- The Claim Check Pattern offloads large payloads to storage while sending a lightweight reference in events.  
- It improves performance and avoids size limits in messaging systems.  
- Combine Event Grid with Blob Storage to implement this pattern.  
- I used this pattern to send metadata in events while storing detailed logs in Azure Blob Storage.  

**35. Compare Azure WebJobs vs Azure Function. When to use one?**  
- WebJobs are ideal for long-running tasks tied to an App Service.  
- Azure Functions are event-driven, scalable, and suitable for serverless architectures.  
- Use WebJobs for simpler scenarios and Functions for flexibility and scalability.  
- I used Azure Functions to handle real-time event processing in an IoT project.  

**36. When shall we use Azure Table Storage over Azure SQL?**  
- Use Table Storage for key-value or NoSQL data requiring high scalability.  
- Azure SQL is better for relational data and complex queries.  
- Table Storage is cost-effective for large, simple datasets.  
- I used Table Storage to log IoT telemetry data for cost efficiency and speed.  

**37. What is the difference between Keys and Secrets in Azure Key Vault?**  
- Keys are used for encryption, signing, and cryptographic operations.  
- Secrets store sensitive information like connection strings or passwords.  
- Keys have cryptographic features, while secrets are for secure storage and retrieval.  
- I stored database connection strings as secrets in Azure Key Vault for secure access.  

**38. How is Azure App Services different from Azure Functions?**  
- Azure App Services is a PaaS offering for web apps, APIs, and mobile backends.  
- Azure Functions is a serverless compute service for running event-driven tasks.  
- App Services offer broader hosting options, while Functions are lightweight and cost-efficient.  
- I used App Services for hosting a multi-tenant SaaS platform and Functions for event processing.  

**39. What is the equivalent of a Windows Service on Azure?**  
- Azure Functions or WebJobs can act as equivalents for background tasks.  
- Azure VMs can host traditional Windows Services for legacy applications.  
- Azure Container Instances can also run custom services in isolated environments.  
- I replaced a legacy Windows Service with an Azure Function for processing uploaded files.  

**40. What data schema shall you use for Event Grid events?**  
- Follow the CloudEvents schema for standardization and interoperability.  
- Include minimal metadata for routing and processing efficiency.  
- Store large payloads externally using the Claim Check Pattern.  
- I designed custom events with CloudEvents schema to standardize inter-service communication.  

**41. What are main considerations when creating Azure Service Bus queues/topics?**  
- Define message size, retention policies, and maximum queue size.  
- Use sessions for ordered message processing and dead-letter queues for fault handling.  
- Configure access policies for secure message handling.  
- I created Service Bus queues with custom TTL settings to optimize resource usage for temporary messages.  

**42. Explain the difference between Scheduled vs Deferred messages in Azure Service Bus.**  
- Scheduled messages are delayed for a specific time before becoming available for consumption.  
- Deferred messages are postponed by the receiver and require a sequence number to be retrieved.  
- Scheduled messages are set at sending time; deferred messages require manual retrieval logic.  
- I used scheduled messages to delay notifications in a time-sensitive workflow.  

**43. Explain the use of Express Entities in Azure Service Bus.**  
- Express entities optimize performance by storing messages in memory temporarily.  
- They are suitable for lightweight, high-throughput scenarios.  
- Persistent storage is sacrificed for speed, so use them for non-critical workloads.  
- I used express queues in a high-velocity telemetry pipeline where message loss was tolerable.  

**44. Why should you keep Azure Event Grid events as small as possible?**  
- Small events reduce latency and improve throughput.  
- They prevent exceeding size limits and reduce processing overhead.  
- Use external storage for large payloads to adhere to size constraints.  
- I implemented compact events for notifying clients of file uploads, with URLs pointing to storage locations.  

**45. How would you get Azure Event Grid events in Angular/React client?**  
- Use Azure SignalR or Web PubSub to forward events to clients in real time.  
- Poll a custom API or use WebSocket for direct communication.  
- Implement subscription verification for secure Event Grid integration.  
- I forwarded Event Grid events via Web PubSub to display live updates in an Angular dashboard.  

**46. What are pros and cons of Azure Web PubSub vs SignalR?**  
- Web PubSub offers native WebSocket support, high scalability, and integration flexibility.  
- SignalR simplifies development but is tightly coupled with the .NET ecosystem.  
- Web PubSub is more suitable for diverse clients and lightweight architectures.  
- I used Web PubSub for a multi-platform chat application requiring WebSocket-based communication.  

**47. Explain the use of Bounded Staleness consistency model in Cosmos DB.**  
- Ensures reads lag behind writes by a defined staleness window or operation count.  
- Provides a balance between strong consistency and high availability.  
- Suitable for scenarios tolerating delayed reads with globally distributed systems.  
- I used Bounded Staleness to sync a global inventory system while maintaining high write throughput.  

**48. How would you choose/design a multi-tenant architecture with Azure Cosmos DB?**  
- Use partition keys to isolate tenant data for scalability and cost-efficiency.  
- Leverage shared throughput databases for cost sharing among tenants.  
- Implement RBAC for secure tenant-level access.  
- I designed a multi-tenant platform using `tenantId` as the partition key to segregate customer data.  

**49. Compare ARM Templates vs Azure CLI for Azure deployments.**  
- ARM Templates are declarative and reusable; ideal for complex, repeatable deployments.  
- Azure CLI is imperative and better for ad-hoc or interactive resource management.  
- ARM Templates ensure consistency; CLI offers flexibility for quick changes.  
- I used ARM Templates to define a standardized infrastructure for a development environment.  

**50. What is the difference between Azure Active Directory and Azure Active Directory Domain Services?**  
- Azure AD is a cloud-based identity and access management service for apps.  
- Azure AD Domain Services provides domain-join, LDAP, and NTLM/Kerberos authentication.  
- Use Azure AD for modern apps and Domain Services for legacy apps requiring on-prem-style authentication.  
- I used Azure AD for SSO in a modern web application and Domain Services for legacy ERP integration.  

**51. Name some advantages and disadvantages of Azure CDNs.**  
- Advantages: Improved performance, global availability, and reduced latency for static assets.  
- Disadvantages: Costs increase with traffic, and changes to content may take time to propagate.  
- CDNs are ideal for serving static assets like images, videos, or scripts.  
- I implemented Azure CDN to optimize content delivery for a high-traffic e-commerce website.  

**52. Cosmos DB vs Azure Table Storage vs Azure SQL Database: what to choose?**  
- Cosmos DB: For globally distributed, low-latency applications with NoSQL flexibility.  
- Azure Table Storage: For key-value pairs in cost-effective scenarios with simple querying.  
- Azure SQL Database: For relational data requiring strong consistency and complex querying.  
- I used Cosmos DB for a multi-region chat app, Table Storage for logs, and SQL for transactional data.  

**53. How would you choose between Azure Table Storage vs MongoDB?**  
- Azure Table Storage is simpler, cost-effective, and integrates natively with Azure services.  
- MongoDB offers advanced querying, aggregation, and indexing capabilities.  
- Use Table Storage for lightweight key-value scenarios and MongoDB for complex NoSQL workloads.  
- I chose Table Storage for a logging system and MongoDB for a social media analytics platform.  

**54. Explain the difference between Block Blobs, Append Blobs, and Page Blobs in Azure.**  
- Block Blobs: Optimized for sequential uploads; ideal for text and media files.  
- Append Blobs: Specialized for append-only operations; suitable for logging.  
- Page Blobs: Optimized for random read/write operations; used for virtual disks.  
- I used Append Blobs to collect real-time telemetry data from IoT devices.  

**55. When should I use Azure SQL vs Azure Table Storage?**  
- Use Azure SQL for relational data, transactional requirements, and complex querying.  
- Use Table Storage for simple key-value storage with high scalability and low cost.  
- Azure SQL ensures data integrity, while Table Storage excels in high-throughput scenarios.  
- I stored product catalogs in SQL for querying and session data in Table Storage for scalability.  

**56. What is the difference between Enterprise Application and App Registration in Azure?**  
- Enterprise Application represents an instance of an app in a tenant for SSO.  
- App Registration is a template to define app permissions and properties.  
- Enterprise Apps are tenant-specific, while App Registrations can be multi-tenant.  
- I created an App Registration for a multi-tenant API and used Enterprise Apps for client onboarding.  

**57. Explain Optimistic Concurrency Control (OCC) and how it is implemented in Cosmos DB.**  
- OCC ensures data consistency by using ETags to detect changes.  
- Updates fail if the ETag doesn’t match, indicating a conflict.  
- Suitable for scenarios with low contention and high performance.  
- I used OCC in a collaborative editing app to prevent overwrites of concurrent updates.  

```csharp
var itemResponse = await container.ReadItemAsync<MyItem>(id, partitionKey);
var item = itemResponse.Resource;
item.SomeField = "Updated Value";
await container.ReplaceItemAsync(item, id, new PartitionKey(item.PartitionKey), new ItemRequestOptions { IfMatchEtag = itemResponse.ETag });
```  

**58. Why are Azure Resource Groups associated with a specific region?**  
- Resource Groups store metadata about resources and their locations.  
- Associating with a region ensures optimal performance and latency.  
- Resources within a group can span regions, but group metadata resides in one region.  
- I deployed a global app with all resources in a group based in the `East US` region for performance reasons.  

**59. How to define an Environment Variable on Azure using Azure CLI?**  
- Use `az webapp config appsettings set` for Azure App Service environment variables.  
- CLI allows defining key-value pairs for app-specific configurations.  
- These settings override environment variables at runtime.  
- I set `DatabaseConnectionString` using the following command for a production deployment.  

```bash
az webapp config appsettings set --name MyWebApp --resource-group MyResourceGroup --settings DatabaseConnectionString="Server=tcp:mydb.database.windows.net;..."
```  

**60. When would you use Azure Event Grid vs Azure Service Bus?**  
- Event Grid is for reactive event-driven architectures with high throughput.  
- Service Bus is for command-style messaging and reliable workflows.  
- Event Grid suits publish-subscribe models, while Service Bus handles complex messaging patterns.  
- I used Event Grid for resource change notifications and Service Bus for order processing in an e-commerce system.  

**61. What’s the difference between Logical and Physical partitions in Cosmos DB?**  
- Logical partitions group data by a partition key; users define them.  
- Physical partitions are Azure-managed, storing one or more logical partitions.  
- Physical partitions scale automatically as data volume grows.  
- I used `userId` as a logical partition to segregate user data, while physical partitions handled scalability transparently.  

**62. Explain the difference between Scheduled vs Deferred messages in Azure Service Bus.**  
- Scheduled messages delay visibility until a set time, useful for time-based actions.  
- Deferred messages are manually postponed by the receiver and retrieved using a sequence number.  
- Scheduled messages are ideal for reminders; deferred messages help manage workflows.  
- I scheduled messages for payment retries and deferred error-handling messages in a payment gateway.  

**63. Explain the use of Express Entities in Azure Service Bus.**  
- Express entities store messages in memory for faster processing.  
- They are suitable for scenarios where durability is not critical.  
- Message retention is limited compared to standard entities.  
- I used express queues for low-latency telemetry in a monitoring system.  

**64. Why should you keep Azure Event Grid events as small as possible?**  
- Small events reduce latency and minimize processing overhead.  
- Large events may hit size limits and require external storage.  
- Smaller payloads are easier to transmit and process in real time.  
- I sent metadata in Event Grid events and stored detailed data in Blob Storage to optimize performance.  

**65. How would you get Azure Event Grid events in Angular/React client?**  
- Use Azure Web PubSub or SignalR to push events to the frontend in real time.  
- Implement a WebSocket or polling strategy for receiving events.  
- Secure the endpoint using Event Grid subscriptions and shared keys.  
- I built a React app that consumed Event Grid notifications via a SignalR hub for live updates.  