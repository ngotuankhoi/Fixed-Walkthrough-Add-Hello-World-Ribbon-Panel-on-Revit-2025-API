# Walkthrough: Add Hello World Ribbon Panel (Fixed for .NET Core 8 in Revit 2025 API)

### Create a New Project
Complete the following steps to create a new project:

#### 1. Create a C# project in Visual Studio using the Class Library template.
  - Chose: `Class Library - A Project for a class library that targets .NET or NET Standard)`.

#### 2. Type AddPanel as the project name.
  - Leave other default and click Next.
  - Chose: `Framework - .NET 8.x (Long Term Support)` and click Create.
  
#### 3. Add references to the RevitAPI.dll and RevitAPIUI.dll.
  - In the Solution Explorer panel. Right click on `Dependencies` and click `Add Project Reference...` to open Reference Manager.
  - Click `Browse...` and go to `\Program Files\Autodesk\Revit 2025\`
  - Chose RevitAPI.dll and RevitAPIUI.dll and click Add and click OK.
  - Click RevitAPI.dll and RevitAPIUI.dll and chose 'No' in Properties > Copy Local.

#### 4. Add NuGet Packages:
  - In the Solution Explorer panel. Right click and chose `Manage Nuget Packages...`
  - In the Browse tab, search and install `Microsoft.Windows.Compatibility` and `System.Windows.Extensions`.

#### 5. Modify `.csproj` file:
  - In Visual Studio, in the Solution Explorer, right click on project title and pick `Edit Project File` to see projet .csproj file (AddPanel.csproj).
  - For ensure it is set up correctly for a class library targeting .NET 8.0 with WPF support. Focus on tag <PropertyGroup>.
    ```
    <Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

      <PropertyGroup>
        <TargetFramework>net8.0-windows</TargetFramework>
        <OutputType>Library</OutputType>
        <UseWPF>true</UseWPF>
      </PropertyGroup>
    
      <ItemGroup>
        <!-- Add Revit API DLL references here if not added via NuGet -->
      </ItemGroup>

    </Project>
    ```

#### 6. Code Adjustments:
  - See in `CsAddPanel.cs` file follow code this project files.

#### 7. Use `Build Solution` to build `AddPanel.dll`.
  - File located on local project folder: `C:\Users\[user]\source\repos\AddPanel\AddPanel\bin\Debug\net8.0-windows\`.

#### 8. Create manifest file:
  - Right click on the Solution Explorer and chose Add > New Item...
  - Chose `Application Manifest File (Windows Only)` and change Name to `HelloWorldRibbon.addin`. And lick Add button.
  - Put code in the `HelloWorldRibbon.addin` follow:
    ```
    <?xml version="1.0" encoding="utf-8" standalone="no"?>
      <RevitAddIns>
          <AddIn Type="Application">
              <Name>HelloWorldRibbon</Name>
              <Assembly>C:\Users\[user]\source\repos\AddPanel\AddPanel\bin\Debug\net8.0-windows\AddPanel.dll</Assembly>
              <AddInId>604b1052-f742-4951-8576-c261d1789108</AddInId>
              <FullClassName>Walkthrough.CsAddPanel</FullClassName>
              <VendorId>NAME</VendorId>
              <VendorDescription>Your Company Information</VendorDescription>
          </AddIn>
      </RevitAddIns>
    ```
  - Ensure that the path specified in <Assembly> correctly points to project folder DLL. If the path is incorrect, Revit won’t be able to find your add-in.
  - Ensure the <AddInId> is unique to avoid conflicts with other add-ins. Use `Tool > Create GUID` to create new ID if necessary.
  - Copy and paste `HelloWorldRibbon.addin` in `C:\ProgramData\Autodesk\Revit\Addins\2025\`.

#### 9. Run Revit and see add-in in the `Add-ins` ribbon table.
  - Chose `Always Load` when system asked.
  - Open or create new Revit project and click on the `NewRibbonPanel` name to see final result.
