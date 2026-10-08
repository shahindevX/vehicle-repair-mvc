# Vehicle Repair MVC

A **vehicle repair management web app** built with **ASP.NET MVC 5 (.NET Framework 4.8)** and **Entity Framework 6 (Code First)**. It lets a repair shop record vehicles, assign a service type, attach a photo, and list the replacement parts used with their costs. Create and edit forms open in modal dialogs and save through AJAX, so the page never reloads.

## Features

- **Vehicle repair records** – registration number, repair date, owner phone, repaired / pending status
- **Service types** – full CRUD (Engine Repair, Brake Service, Oil Change, Electrical Repair, Tire Service, Body Work are seeded by default)
- **Repair parts** – add multiple parts (name and cost) to each vehicle, and add or remove them while editing
- **Image upload** – attach a photo to each vehicle (saved with a unique GUID filename, with a `noimage.png` fallback)
- **AJAX modals** – create, edit and delete vehicles without leaving the page (jQuery and Bootstrap)
- **Validation** – server-side data annotations through a dedicated `VehicleViewModel`, plus anti-forgery tokens on POST actions
- **Code First migrations** – database schema and seed data are created from the models

## Tech Stack

| Layer | Technology |
| --- | --- |
| Framework | ASP.NET MVC 5.2, .NET Framework 4.8 |
| Language | C# |
| ORM | Entity Framework 6.4 (Code First Migrations) |
| Database | SQL Server LocalDB |
| Front end | Razor views, Bootstrap 5.3, jQuery 3.7 |

## Data Model

```
ServiceType 1 ──< Vehicle 1 ──< RepairPart
```

| Entity | Main fields |
| --- | --- |
| `ServiceType` | `ServiceTypeId`, `ServiceTypeName` |
| `Vehicle` | `VehicleId`, `VehicleRegNo`, `RepairDate`, `OwnerPhone`, `IsRepaired`, `ImageUrl`, `ServiceTypeId` (FK) |
| `RepairPart` | `RepairPartId`, `PartName`, `PartCost`, `VehicleId` (FK) |

## Project Structure

```
VehicleRepairMVC/
├── Controllers/      # Home, Vehicles, ServiceTypes
├── Models/           # Vehicle, ServiceType, RepairPart
├── ViewModels/       # VehicleViewModel (form binding and validation)
├── DAL/              # AppDbContext (EF6 DbContext)
├── Migrations/       # EF Code First migrations and seed data
├── Views/            # Razor views and shared partials (create / edit modals)
├── Content/ Scripts/ # Bootstrap and jQuery
└── images/           # Uploaded vehicle photos
```

## Getting Started

### Prerequisites

- Windows with **Visual Studio 2019 / 2022** (ASP.NET and web development workload)
- **.NET Framework 4.8** developer pack
- **SQL Server LocalDB** (installed with Visual Studio)

### Run locally

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   ```
2. Open `VehicleRepairMVC_Solution.sln` in Visual Studio.
3. Restore NuGet packages (this happens automatically on build).
4. Open **Tools → NuGet Package Manager → Package Manager Console** and create the database:
   ```
   Update-Database
   ```
5. Press **F5**. The home page opens, and the vehicle list is at `/Vehicles`.

### Database connection

The default connection string in `Web.config` uses LocalDB:

```xml
<add name="AppDbContext"
     connectionString="server=(LocalDB)\MSSQLLocalDB; database=VehicleRepairDB; Trusted_Connection=true"
     providerName="System.Data.SqlClient" />
```

Change the server name here if you use a full SQL Server instance.

## Routes

| Route | Description |
| --- | --- |
| `/` | Home page |
| `/Vehicles` | Repair records list with modal create, edit and delete |
| `/ServiceTypes` | Manage service types (list, details, create, edit, delete) |

## Possible Improvements

- Add authentication and roles (admin and mechanic)
- Search, filter and paging on the vehicle list
- Total repair cost per vehicle
- Validate uploaded file type and size
- Migrate to ASP.NET Core

## License

Add a license of your choice (for example MIT), or remove this section.

