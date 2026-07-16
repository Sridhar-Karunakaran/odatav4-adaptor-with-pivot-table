<div align="center">
  <h1>Syncfusion® React Pivot Table – OData V4 Adaptor Quick Start</h1>

  <p>
    A production-ready quick start that connects the <strong>Syncfusion® React Pivot Table</strong> to an <strong>ASP.NET Core OData V4</strong> backend using the <strong>ODataV4Adaptor</strong> of the <code>DataManager</code> — enabling remote data binding, server-side query processing, and full CRUD operations over standard OData endpoints.
  </p>

  <p>
    <a href="https://react.dev/"><img src="https://img.shields.io/badge/React-19%2B-61DAFB?style=for-the-badge&logo=react&logoColor=white" alt="React"></a>
    <a href="https://dotnet.microsoft.com/apps/aspnet"><img src="https://img.shields.io/badge/.NET-10.0%2B-512BD4?style=for-the-badge&logo=dotnet&logoColor=white" alt=".NET"></a>
    <a href="https://www.odata.org/"><img src="https://img.shields.io/badge/OData-V4-7AB023?style=for-the-badge&logo=odata&logoColor=white" alt="OData V4"></a>
    <a href="https://www.syncfusion.com/react-components/react-pivot-table"><img src="https://img.shields.io/badge/Syncfusion-EJ2-FF9C00?style=for-the-badge&logo=syncfusion&logoColor=white" alt="Syncfusion"></a>
    <a href="https://github.com/SyncfusionExamples/odatav4-adaptor-with-pivot-table/blob/master/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License"></a>
  </p>
</div>

---

## 📑 Table of Contents

- [🚀 Quick Overview](#-quick-overview)
- [✨ Key Features](#-key-features)
- [🛠️ Prerequisites](#-prerequisites)
- [📂 Project Structure](#-project-structure)
- [🏗️ Architecture & Data Flow](#-architecture--data-flow)
- [⚙️ Installation & Setup](#-installation--setup)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Backend – ASP.NET Core OData V4 Service](#2-backend--aspnet-core-odata-v4-service)
  - [3. Frontend – React Pivot Table](#3-frontend--react-pivot-table)
- [▶️ Running the Application](#-running-the-application)
- [🧪 Testing CRUD Operations](#-testing-crud-operations)
- [🔍 OData Query Options Reference](#-odata-query-options-reference)
- [🔧 Troubleshooting](#-troubleshooting)
- [📖 API Reference](#-api-reference)
- [🤝 Contributing](#-contributing)
- [📜 License & Support](#-license--support)
- [📚 Related Resources](#-related-resources)

---

## 🚀 Quick Overview

This project demonstrates how to bind the **Syncfusion® React Pivot Table** to a remote **ASP.NET Core OData V4** service using the [`ODataV4Adaptor`](https://ej2.syncfusion.com/react/documentation/data/adaptors/odatav4-adaptor) of the [`DataManager`](https://ej2.syncfusion.com/react/documentation/data/getting-started). The ODataV4Adaptor is purpose-built for REST endpoints that follow the [OData V4 protocol](https://www.odata.org/documentation/), enabling standardized querying, filtering, sorting, paging, and CRUD operations.

| Component          | Technology                              | Purpose                                                          |
| ------------------ | --------------------------------------- | ---------------------------------------------------------------- |
| 🎨 Frontend        | React 19+ + Syncfusion® EJ2             | Render the interactive Pivot Table UI                            |
| ⚙️ Backend         | ASP.NET Core 10.0 (OData 9.4)           | Serve OData V4 endpoints with `[EnableQuery]` support            |
| 🔌 Adaptor         | `ODataV4Adaptor`                        | Bridge between Pivot Table and OData service over standard URLs  |
| 📊 Sample Data     | In-memory `OrdersDetails` list          | Simulate order records for the Pivot Table                       |

> 💡 The ODataV4Adaptor is ideal when you want server-side query processing (filtering, sorting, paging) using a standardized open protocol — eliminating the need to write custom REST query conventions.

---

## ✨ Key Features

- 📊 **Remote Data Binding** – Connects the Pivot Table to an OData V4 endpoint over HTTP.
- 🔄 **Full CRUD Support** – Insert, update, and delete records directly from the Pivot Table drill-through grid using `POST`, `PATCH`, and `DELETE` verbs.
- 🎨 **Standard OData Querying** – All filter, sort, page, and aggregation logic is delegated to the server using `$filter`, `$orderby`, `$skip`, `$top`, and `$count` query options.
- 🗂️ **Standardized Response Format** – Returns OData-compliant JSON with `value` and `@odata.count` for client-side parsing.
- 🔑 **Primary Key Configuration** – Uses `OrderID` as the primary key (via the `[Key]` attribute) for unique record identification.
- 🌐 **CORS-Enabled** – Preconfigured to allow cross-origin requests from the React dev server.
- 🛡️ **Property Casing Preservation** – Uses `DefaultContractResolver` to keep PascalCase fields like `OrderID`, `ShipCountry`.
- ⚡ **Drill-Through Editing** – Double-click a pivot cell to add, edit, or delete underlying records in a pop-up grid.
- 📦 **Ready-to-Run** – Clone, build, and start both projects — no database setup required (in-memory sample data).

---

## 🛠️ Prerequisites

Make sure the following software and packages are installed on your machine before running the project.

| Software / Package                              | Version      | Purpose                                                            |
| ----------------------------------------------- | ------------ | ------------------------------------------------------------------ |
| 🟢 Node.js                                      | 18.x or later| Runtime for the React development server                           |
| ⚛️ React                                        | 19.x or later| Build the Pivot Table client                                       |
| 🟣 .NET SDK                                     | 10.0 or later| Build and run the ASP.NET Core OData V4 service                    |
| 🧑‍💻 Visual Studio / VS Code                    | Latest       | Configure and run the backend API                                  |
| 📦 `@syncfusion/ej2-react-pivotview`            | Latest       | React Pivot Table component                                        |
| 📦 `@syncfusion/ej2-data`                       | Latest       | `DataManager` and `ODataV4Adaptor`                                 |
| 📦 `Microsoft.AspNetCore.OData`                 | 9.4.1+       | OData V4 server-side support (query parsing, EDM, formatting)      |
| 📦 `Microsoft.AspNetCore.Mvc.NewtonsoftJson`    | 10.0.9+      | Preserve original property casing during JSON serialization        |

---

## 📂 Project Structure

```
odatav4-adaptor-with-pivot-table/
├── 📁 Client/                              # React frontend (Pivot Table)
│   ├── 📁 public/
│   │   ├── index.html
│   │   ├── manifest.json
│   │   └── robots.txt
│   ├── 📁 src/
│   │   ├── App.css                         # Component styles (Syncfusion Tailwind3 theme)
│   │   ├── App.js                          # Pivot Table with ODataV4Adaptor configuration
│   │   ├── App.test.js
│   │   ├── datasource.js                   # Local pivot sample data (not used by the OData endpoint)
│   │   ├── index.css
│   │   ├── index.js                        # React entry point
│   │   ├── reportWebVitals.js
│   │   └── setupTests.js
│   └── package.json                        # React dependencies & scripts
│
├── 📁 ODataV4Adaptor/                      # ASP.NET Core OData V4 backend
│   ├── 📁 Controllers/
│   │   └── PivotController.cs              # OData endpoints: GET, GET(key), POST, PATCH(key), DELETE(key)
│   ├── 📁 Models/
│   │   └── OrdersDetails.cs                # Order data model + sample data
│   ├── 📁 Properties/
│   │   └── launchSettings.json             # Default ports: https 7181, http 5092
│   ├── appsettings.Development.json
│   ├── appsettings.json
│   ├── ODataV4Adaptor.csproj               # Project file (targets net10.0)
│   ├── ODataV4Adaptor.http                 # Endpoint testing file
│   └── Program.cs                          # OData + Newtonsoft.Json + CORS configuration
│
├── 📄 README.md                            # You are here
```

---

## 🏗️ Architecture & Data Flow

The application is split into two processes that communicate over HTTP using the OData V4 protocol.

```
┌──────────────────────────────────┐         ┌──────────────────────────────────────┐
│  React Client (localhost:3000)   │         │  ASP.NET Core OData V4 Backend       │
│                                  │         │  (https://localhost:7181)            │
│  ┌────────────────────────────┐  │         │                                      │
│  │  PivotViewComponent        │  │         │  ┌──────────────────────────────┐    │
│  │  (Syncfusion EJ2)          │  │         │  │ PivotController : ODataCtrl  │    │
│  └─────────────┬──────────────┘  │         │  │  • GET    /odata/Pivot      │    │
│                │                 │         │  │  • GET    /odata/Pivot({k}) │    │
│  ┌─────────────▼──────────────┐  │  HTTP   │  │  • POST   /odata/Pivot      │    │
│  │  DataManager               │──┼────────▶│  │  • PATCH  /odata/Pivot({k}) │    │
│  │  url: /odata/Pivot         │  │  OData  │  │  • DELETE /odata/Pivot({k}) │    │
│  │  adaptor: ODataV4Adaptor   │  │   V4    │  └────────────┬─────────────────┘    │
│  └────────────────────────────┘  │         │               │                      │
│                                  │         │  ┌────────────▼─────────────────┐    │
│                                  │         │  │ [EnableQuery]                │    │
│                                  │         │  │ OrdersDetails.GetAllRecords()│    │
│                                  │         │  │ (in-memory list)             │    │
│                                  │         │  └──────────────────────────────┘    │
└──────────────────────────────────┘         └──────────────────────────────────────┘
```

**Step-by-step request flow (initial load):**

1. The React `DataManager` issues `GET https://localhost:7181/odata/Pivot` to the backend.
2. The request passes through the OData middleware registered in `Program.cs`.
3. `PivotController.Get()` returns `OrdersDetails.GetAllRecords().AsQueryable()` decorated with `[EnableQuery]`.
4. ASP.NET Core OData serializes the data into the OData-compliant envelope:
   ```json
   {
     "value": [ { "OrderID": 10001, "...": "..." }, ... ],
     "@odata.count": 2
   }
   ```
5. The `ODataV4Adaptor` parses the response and feeds the records into the Pivot Table.

**Step-by-step request flow (CRUD from drill-through):**

| User action              | HTTP verb | URL template                  | Controller method            |
| ------------------------ | --------- | ----------------------------- | ---------------------------- |
| Double-click pivot cell  | `GET`     | `/odata/Pivot?...`            | `Get()`                      |
| Add new record           | `POST`    | `/odata/Pivot`                | `Post(addRecord)`            |
| Edit existing record     | `PATCH`   | `/odata/Pivot({key})`         | `Patch(key, updatedOrder)`   |
| Delete record            | `DELETE`  | `/odata/Pivot({key})`         | `Delete(key)`                |

> 🔑 The `OrderID` field is marked as the primary key by the `[Key]` attribute on the model and by the `beginDrillThrough` event in `App.js`. The ODataV4Adaptor uses this key when generating URLs for `PATCH` and `DELETE`.

---

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/SyncfusionExamples/odatav4-adaptor-with-pivot-table.git
cd odatav4-adaptor-with-pivot-table
```

### 2. Backend – ASP.NET Core OData V4 Service

The backend project lives in the `ODataV4Adaptor/` folder.

#### 2.1 Restore dependencies

```bash
cd ODataV4Adaptor
dotnet restore
```

#### 2.2 Verify the required NuGet packages

Open `ODataV4Adaptor.csproj` and confirm the following package references are present:

```xml
<!-- filepath: ODataV4Adaptor/ODataV4Adaptor.csproj -->
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net10.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.Mvc.NewtonsoftJson" Version="10.0.9" />
    <PackageReference Include="Microsoft.AspNetCore.OData" Version="9.4.1" />
    <PackageReference Include="Microsoft.AspNetCore.OpenApi" Version="10.0.9" />
  </ItemGroup>

</Project>
```

- **`Microsoft.AspNetCore.OData`** – Adds OData V4 query parsing, EDM model creation, and response formatting (`$filter`, `$orderby`, `$top`, `$skip`, `$count`).
- **`Microsoft.AspNetCore.Mvc.NewtonsoftJson`** – Preserves PascalCase property names (`OrderID`, `ShipCountry`) during JSON serialization.

If any are missing, add them with:

```bash
dotnet add package Microsoft.AspNetCore.OData --version 9.4.1
dotnet add package Microsoft.AspNetCore.Mvc.NewtonsoftJson --version 10.0.9
```

#### 2.3 Inspect the configuration

`Program.cs` configures the OData service, JSON serialization, and CORS:

```csharp
// filepath: ODataV4Adaptor/Program.cs
using Newtonsoft.Json.Serialization;
using Microsoft.OData.ModelBuilder;
using ODataV4Adaptor.Models;
using Microsoft.AspNetCore.OData;

var builder = WebApplication.CreateBuilder(args);

// Create an ODataConventionModelBuilder to build the OData model.
var modelBuilder = new ODataConventionModelBuilder();

// Register the "Pivot" entity set with the OData model builder.
// "Pivot" will be the name used in URLs (e.g., /odata/Pivot).
modelBuilder.EntitySet<OrdersDetails>("Pivot");

builder.Services.AddMvc().AddNewtonsoftJson(options =>
{
  options.SerializerSettings.ContractResolver = new DefaultContractResolver();
});

builder.Services.AddCors(options =>
{
  options.AddDefaultPolicy(policy =>
  {
    policy.AllowAnyOrigin()
          .AllowAnyMethod()
          .AllowAnyHeader();
  });
});

builder.Services.AddControllers();

// Register OData services and route components under the "odata" prefix.
builder.Services.AddControllers().AddOData(
    options => options
        .Count()                                                  // Enables $count
        .AddRouteComponents("odata", modelBuilder.GetEdmModel()));// "odata" is the URL prefix

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.MapOpenApi();
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();
app.UseCors();

app.Run();
```

> 🔒 **Production CORS:** Replace `AllowAnyOrigin()` with `policy.WithOrigins("https://yourdomain.com")`.

#### 2.4 Inspect the OData model

```csharp
// filepath: ODataV4Adaptor/Models/OrdersDetails.cs
using System.ComponentModel.DataAnnotations;

namespace ODataV4Adaptor.Models
{
    public class OrdersDetails
    {
        public static List<OrdersDetails> order = new List<OrdersDetails>();

        public OrdersDetails() { }

        public OrdersDetails(int OrderID, string CustomerId, int EmployeeId, string ShipCountry)
        {
            this.OrderID = OrderID;
            this.CustomerID = CustomerId;
            this.EmployeeID = EmployeeId;
            this.ShipCountry = ShipCountry;
        }

        public static List<OrdersDetails> GetAllRecords()
        {
            if (order.Count() == 0)
            {
                int code = 10000;
                for (int i = 1; i < 2; i++)
                {
                    order.Add(new OrdersDetails(code + 1, "ALFKI", i + 0, "Denmark"));
                    order.Add(new OrdersDetails(code + 2, "ANATR", i + 2, "Brazil"));
                    code += 5;
                }
            }
            return order;
        }

        [Key]
        public int? OrderID { get; set; }       // Primary key — used for CRUD key handling
        public string? CustomerID { get; set; }
        public int? EmployeeID { get; set; }
        public string? ShipCountry { get; set; }
    }
}
```

> ℹ️ The sample currently seeds only two records. Uncomment the additional `order.Add(...)` lines (or expand the loop) to populate more data for the Pivot Table.

#### 2.5 Inspect the OData controller

```csharp
// filepath: ODataV4Adaptor/Controllers/PivotController.cs
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.OData.Query;
using Microsoft.AspNetCore.OData.Routing.Controllers;
using ODataV4Adaptor.Models;

namespace ODataV4Adaptor.Server.Controllers
{
    [Route("[controller]")]
    [ApiController]
    public class PivotController : ODataController
    {
        // READ: Get all orders
        [HttpGet]
        [EnableQuery]
        public IActionResult Get()
        {
            var data = OrdersDetails.GetAllRecords().AsQueryable();
            return Ok(data);
        }

        // READ: Get single order by key
        [HttpGet("{key}")]
        [EnableQuery]
        public IActionResult Get(int key)
        {
            var order = OrdersDetails.GetAllRecords().FirstOrDefault(o => o.OrderID == key);
            if (order == null) return NotFound();
            return Ok(order);
        }

        // CREATE: Insert new order
        [HttpPost]
        [EnableQuery]
        public IActionResult Post([FromBody] OrdersDetails addRecord)
        {
            if (addRecord == null) return BadRequest("Order cannot be null");
            OrdersDetails.GetAllRecords().Insert(0, addRecord);
            return Created(addRecord);
        }

        // UPDATE: Modify existing order
        [HttpPatch("{key}")]
        public IActionResult Patch(int key, [FromBody] OrdersDetails updatedOrder)
        {
            if (updatedOrder == null) return BadRequest("Order data cannot be null");

            var existingOrder = OrdersDetails.GetAllRecords().FirstOrDefault(o => o.OrderID == key);
            if (existingOrder == null) return NotFound();

            existingOrder.CustomerID  = updatedOrder.CustomerID  ?? existingOrder.CustomerID;
            existingOrder.EmployeeID  = updatedOrder.EmployeeID  ?? existingOrder.EmployeeID;
            existingOrder.ShipCountry = updatedOrder.ShipCountry ?? existingOrder.ShipCountry;

            return Ok(existingOrder);
        }

        // DELETE: Remove order
        [HttpDelete("{key}")]
        public IActionResult Delete(int key)
        {
            var order = OrdersDetails.GetAllRecords().FirstOrDefault(o => o.OrderID == key);
            if (order == null) return NotFound();

            OrdersDetails.GetAllRecords().Remove(order);
            return NoContent();
        }
    }
}
```

> The `[EnableQuery]` attribute is **mandatory** for OData query functionality. Without it, the server returns the full data set and ignores `$filter`, `$orderby`, `$top`, `$skip`, and `$count`.

### 3. Frontend – React Pivot Table

The React client lives in the `Client/` folder.

#### 3.1 Install npm dependencies

```bash
cd ../Client
npm install
```

#### 3.2 Verify the API URL

Open `src/App.js` and ensure the `url` in the `DataManager` points to your backend port. The default in this repo is `https://localhost:7181` (HTTPS profile from `launchSettings.json`).

```jsx
// filepath: Client/src/App.js
import * as React from 'react';
import { PivotViewComponent } from '@syncfusion/ej2-react-pivotview';
import { DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import './App.css';

function App() {
    // Configure DataManager with ODataV4Adaptor.
    const data = new DataManager({
        url: 'https://localhost:7181/odata/Pivot',   // 👈 Update this if your backend uses a different port
        adaptor: new ODataV4Adaptor(),
    });

    const editSettings = {
        allowEditing: true,    // Enables the Edit button and allows users to modify existing records
        allowAdding: true,     // Enables the Add button and allows users to create new records
        allowDeleting: true,   // Enables the Delete button and allows users to remove records
        mode: 'Normal'         // Uses Normal mode (popup dialog) for editing; other options: 'Dialog', 'Batch'
    };

    const dataSourceSettings = {
        dataSource: data,
        expandAll: false,
        rows: [{ name: 'ShipCountry' }],
        columns: [{ name: 'OrderID' }],
        values: [{ name: 'EmployeeID' }],
        formatSettings: [{ name: 'Freight', format: 'N0' }],
    };

    let pivotObj;

    // Configure beginDrillThrough event to set the primary key for CRUD operations
    function beginDrillThrough(args) {
        for (var i = 0; i < args.gridObj.columns.length; i++) {
            if (args.gridObj.columns[i].field === "OrderID") {
                // Mark this column as the primary key so DataManager uses it for CRUD key handling
                args.gridObj.columns[i].isPrimaryKey = true;
            } else {
                args.gridObj.columns[i].visible = true;
                if (args.gridObj.columns[i].field === 'OrderDate' || args.gridObj.columns[i].field === 'ShippedDate') {
                    args.gridObj.columns[i].editType = 'datetimepickeredit';
                }
            }
        }
    }

    return (
        <div className='control-section' style={{ margin: 100 }}>
            <PivotViewComponent
                ref={d => pivotObj = d}
                id='PivotView'
                height={350}
                width={700}
                editSettings={editSettings}
                beginDrillThrough={beginDrillThrough}
                dataSourceSettings={dataSourceSettings}>
            </PivotViewComponent>
        </div>
    );
}

export default App;
```

---

## ▶️ Running the Application

You need **two terminals** — one for the backend OData service and one for the React client.

### ▶️ Start the Backend (Terminal 1)

```bash
cd ODataV4Adaptor
dotnet run
```

The API starts on the URLs defined in `Properties/launchSettings.json`:

- 🔒 HTTPS: `https://localhost:7181` (recommended)
- 🌐 HTTP:  `http://localhost:5092`

**Verify it works:**

- 🌐 Open `https://localhost:7181/odata/Pivot` in your browser.
- ✅ You should see an OData-compliant JSON envelope:
  ```json
  {
    "value": [
      { "OrderID": 10001, "CustomerID": "ALFKI", "EmployeeID": 1, "ShipCountry": "Denmark" },
      { "OrderID": 10002, "CustomerID": "ANATR", "EmployeeID": 3, "ShipCountry": "Brazil" }
    ],
    "@odata.count": 2
  }
  ```

> 📝 Note the port number in the terminal output and update the `url` in `Client/src/App.js` if it differs from `https://localhost:7181`.

### ▶️ Start the Frontend (Terminal 2)

```bash
cd Client
npm start
```

The React app opens at `http://localhost:3000` by default. 🎉

You should see the Pivot Table populated with aggregated **EmployeeID** values, grouped by **ShipCountry** (rows) and **OrderID** (columns).

### ✅ Verify in the Browser

1. Open the browser's **Developer Tools** (F12) → **Network** tab.
2. Reload the page.
3. You should see a `GET https://localhost:7181/odata/Pivot` request with status `200` and an OData response containing `value` and `@odata.count`.
4. The Pivot Table renders the aggregated data automatically.

---

## 🧪 Testing CRUD Operations

The Pivot Table supports full CRUD through its built-in **drill-through editing** grid.

| Step | Action                                                                                                  | Expected Network Request                                  |
| ---- | ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| 1️⃣  | **Double-click** any pivot cell to open the drill-through grid showing underlying source records.       | `GET /odata/Pivot`                                        |
| ➕ 2️⃣ | Click **Add**, fill in the new row fields, then click **Update**.                                       | `POST https://localhost:7181/odata/Pivot`                 |
| ✏️ 3️⃣ | Click **Edit** on an existing row, change a field, then click **Update**.                                | `PATCH https://localhost:7181/odata/Pivot({key})`         |
| 🗑️ 4️⃣ | Click **Delete** on a row to remove it.                                                                  | `DELETE https://localhost:7181/odata/Pivot({key})`        |
| 🔁 5️⃣ | The Pivot Table automatically refreshes to display the updated aggregated data from the backend.        | New `GET /odata/Pivot`                                    |

> 🔑 The `OrderID` column is automatically marked as the primary key inside the `beginDrillThrough` event, so `PATCH` and `DELETE` operations know which record to target. On the server, the same key is identified by the `[Key]` attribute on `OrdersDetails.OrderID`.

---

## 🔍 OData Query Options Reference

The ODataV4Adaptor emits the standard OData V4 query options below. All of them are processed server-side by ASP.NET Core OData when the `[EnableQuery]` attribute is present.

| Query option | Purpose                              | Example                                                       |
| ------------ | ------------------------------------ | ------------------------------------------------------------- |
| `$filter`    | Filter records by a boolean expression| `/odata/Pivot?$filter=ShipCountry eq 'Denmark'`               |
| `$orderby`   | Sort by one or more fields           | `/odata/Pivot?$orderby=OrderID desc`                          |
| `$top`       | Take the first N records             | `/odata/Pivot?$top=5`                                         |
| `$skip`      | Skip the first N records             | `/odata/Pivot?$skip=10&$top=10`                               |
| `$count`     | Include total record count           | `/odata/Pivot?$count=true`                                    |
| `$select`    | Project a subset of fields           | `/odata/Pivot?$select=OrderID,CustomerID`                     |
| `$expand`    | Include related entities (not used in this sample) | `/odata/Pivot?$expand=...`                          |

**OData filter operators you can use with `$filter`:**

| Operator | Meaning     | Example                                              |
| -------- | ----------- | ---------------------------------------------------- |
| `eq`     | equals      | `ShipCountry eq 'Denmark'`                           |
| `ne`     | not equals  | `ShipCountry ne 'Denmark'`                           |
| `gt`     | greater than| `OrderID gt 10005`                                   |
| `lt`     | less than   | `OrderID lt 10010`                                   |
| `and`    | logical AND | `ShipCountry eq 'Denmark' and OrderID gt 10005`      |
| `or`     | logical OR  | `ShipCountry eq 'Denmark' or ShipCountry eq 'Germany'` |

**Querying features that benefit the Pivot Table:**

- **Filtering** – The Pivot Table sends `$filter` whenever the user applies filters via the field list or filter dialog.
- **Sorting** – Sort headers (e.g., `OrderID desc`) are translated to `$orderby`.
- **Paging / virtualization** – Page-based requests are translated to `$skip` and `$top`. The `@odata.count` field is required for accurate page counts (enabled by `.Count()` in `Program.cs`).
- **Aggregation** – The Pivot Table aggregates client-side from the records returned by OData, so it works seamlessly over the standard `value` array.
- **Grouping** – The Pivot Table composes group keys from the field values; the server returns all records and the client groups/aggregates them.

> ℹ️ The current `Program.cs` only enables `.Count()`. If you need the server to handle `$filter`, `$orderby`, `$top`, and `$skip` directly (which `[EnableQuery]` already does), no additional changes are required. To restrict available query capabilities, chain `.Select()`, `.Filter()`, `.OrderBy()`, `.Expand()`, or `.SetMaxTop(...)` in the OData registration.

---

## 🔧 Troubleshooting

| ❓ Issue                                | 🔍 Symptom                                                                                                       | ✅ Resolution                                                                                                                |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 🚫 Empty Pivot Table                    | Pivot loads with no errors but no rows or values appear.                                                          | Ensure the API returns OData-compliant JSON (`{ value, @odata.count }`) and that field names match `dataSourceSettings`.     |
| 404 Not Found                           | Network tab shows a 404 response when the Pivot Table loads.                                                     | Confirm the backend is running, the entity set is named `Pivot`, and the URL is `https://<port>/odata/Pivot`.                |
| 💥 500 Internal Server Error            | The Pivot Table fails and the browser shows a server error.                                                      | Check the terminal/Visual Studio output for stack traces. Common causes: missing `[EnableQuery]`, null body, or model issues. |
| 🌐 CORS Blocked                         | Console shows `Access to XMLHttpRequest ... has been blocked by CORS policy`.                                    | Verify CORS is configured in `Program.cs` and `app.UseCors()` is called.                                                     |
| 💾 CRUD operations not saving           | The edit dialog closes but changes are not reflected in the data.                                                | Confirm `OrderID` is the primary key (`[Key]` attribute + `isPrimaryKey` in `beginDrillThrough`).                            |
| 🔤 Property casing mismatch             | Pivot appears empty or shows "field not found" even though the API returns data.                                 | Ensure `DefaultContractResolver` is registered in `Program.cs` so PascalCase fields like `OrderID` are preserved.             |
| 📉 Only 2 records visible               | Pivot shows just the two seeded records from the loop bound `1..2`.                                              | Uncomment additional `order.Add(...)` lines in `OrdersDetails.GetAllRecords()` or increase the loop bound.                   |
| 🔒 SSL/TLS certificate error            | Console shows `net::ERR_CERT_AUTHORITY_INVALID` or browser warns about an untrusted certificate.                 | Run `dotnet dev-certs https --clean` then `dotnet dev-certs https --trust`. Or switch to the `http` profile (port `5092`).    |
| ❌ Missing OData package                 | Build error: "The type or namespace name 'OData' could not be found".                                            | Install `Microsoft.AspNetCore.OData` 9.4.1 via NuGet.                                                                       |
| 🔁 `[EnableQuery]` ignored              | The server returns the full set even when `$filter` is sent.                                                      | Ensure the `[EnableQuery]` attribute is applied to the controller method and the OData route is registered in `Program.cs`.   |

---

## 📖 API Reference

The backend exposes the following OData V4 endpoints through `PivotController`. All endpoints follow standard OData conventions; query options like `$filter`, `$orderby`, `$top`, `$skip`, and `$count` are processed by the framework when `[EnableQuery]` is present.

| Method   | Route                       | Purpose                                        | Request Body            | Response                          |
| -------- | --------------------------- | ---------------------------------------------- | ----------------------- | --------------------------------- |
| `GET`    | `/odata/Pivot`              | Retrieve all order records (with OData query)  | —                       | `{ value: [...], @odata.count }`  |
| `GET`    | `/odata/Pivot({key})`       | Retrieve a single order by primary key         | —                       | Single `OrdersDetails` object     |
| `POST`   | `/odata/Pivot`              | Insert a new order                             | `OrdersDetails` JSON    | `201 Created`                     |
| `PATCH`  | `/odata/Pivot({key})`       | Update an existing order (matched by `OrderID`)| `OrdersDetails` JSON    | `200 OK`                          |
| `DELETE` | `/odata/Pivot({key})`       | Remove an order by primary key                 | —                       | `204 No Content`                  |

The `OrdersDetails` model exposes the following fields:

| Field         | Type        | Description                                |
| ------------- | ----------- | ------------------------------------------ |
| `OrderID`     | `int?`      | Unique order identifier (primary key)      |
| `CustomerID`  | `string?`   | Identifier of the customer                 |
| `EmployeeID`  | `int?`      | Identifier of the handling employee        |
| `ShipCountry` | `string?`   | Destination country                        |

> ℹ️ The model currently exposes only four fields. To bind richer Pivot Table configurations (e.g., `ShipCity`, `Freight`, `OrderDate`, `ShipName`, `ShippedDate`, `ShipAddress`, `Verified`) as referenced in the Pivot Table configuration, add the corresponding properties to `OrdersDetails` and re-seed sample data in `GetAllRecords()`. The `datasource.js` file in the React client contains a richer local-data reference but is **not** used by the OData service in this sample.

---

## 🤝 Contributing

Contributions are welcome and appreciated! 💖

1. 🍴 **Fork** the repository.
2. 🌿 **Create** a feature branch: `git checkout -b feature/my-awesome-change`
3. 💾 **Commit** your changes: `git commit -m "Add my awesome change"`
4. 📤 **Push** to your branch: `git push origin feature/my-awesome-change`
5. 🔁 **Open** a Pull Request describing the change and its motivation.

### 📋 Contribution Guidelines

- Follow the existing code style in both the React and ASP.NET Core projects.
- Keep changes focused — one feature or fix per pull request.
- Update or add documentation (`README.md`, `odatav4-adaptor.md`) when behavior changes.
- Test your changes locally against both the backend and frontend before submitting.

---

## 📜 License & Support

### 📄 License

This project is released under the **MIT License**. You are free to use, modify, and distribute the code in personal and commercial projects. See the [LICENSE](LICENSE) file for full text.

### 🛟 Support

- 📘 **Documentation:** [Syncfusion® React Pivot Table Docs](https://ej2.syncfusion.com/react/documentation/pivotview/getting-started)
- 💬 **Community forum:** [Syncfusion® Community](https://www.syncfusion.com/forums)
- 🐛 **Bug reports & feature requests:** [GitHub Issues](https://github.com/SyncfusionExamples/odatav4-adaptor-with-pivot-table/issues)
- 📧 **Direct support:** [Syncfusion® Support Portal](https://www.syncfusion.com/support) (for licensed users)
- 📖 **OData V4 Adaptor Guide:** [ODataV4Adaptor Documentation](https://ej2.syncfusion.com/react/documentation/data/adaptors/odatav4-adaptor)

> ⭐ If this project helped you, please consider giving it a **star** on GitHub — it helps others discover it!

---

## 📚 Related Resources

- 🔗 [Web API Adaptor with Pivot Table](https://github.com/SyncfusionExamples/webapi-adaptor-with-pivot-table) — Companion sample using `WebApiAdaptor` for ASP.NET Web API.
- 🔗 [UrlAdaptor with Pivot Table](https://github.com/SyncfusionExamples/url-adaptor-with-pivot-table) — Companion sample using `UrlAdaptor` for custom REST endpoints.
- 📘 [PivotTable Data Binding](https://ej2.syncfusion.com/react/documentation/pivotview/data-binding)
- 📘 [DataManager Getting Started](https://ej2.syncfusion.com/react/documentation/data/getting-started)
- 📘 [ODataV4Adaptor Reference](https://ej2.syncfusion.com/react/documentation/data/adaptors/odatav4-adaptor)
- 📘 [PivotTable Editing](https://ej2.syncfusion.com/react/documentation/pivotview/editing)
- 📘 [PivotTable Drill-Through](https://ej2.syncfusion.com/react/documentation/pivotview/drill-through)
- 📘 [OData V4 Official Documentation](https://www.odata.org/documentation/)
- 📘 [ASP.NET Core OData](https://learn.microsoft.com/en-us/odata/webapi-8/overview)

---

<div align="center">
  <sub>Built with ❤️ using <a href="https://react.dev/">React</a>, <a href="https://dotnet.microsoft.com/">.NET</a> and the <a href="https://www.odata.org/">OData V4</a> standard by the <a href="https://www.syncfusion.com/">Syncfusion®</a> team.</sub>
</div>
