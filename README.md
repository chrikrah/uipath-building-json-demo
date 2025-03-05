![Overview](README.png)

===

### How to create a custom class

# Step 1: Create a New C# Class Library
We need to create a C# Class Library (instead of a Console App) because UiPath can import and use DLL files.

Using Visual Studio
Open Visual Studio.
Click File → New → Project.
Select Class Library (.NET Framework).
Name it MyUiPathLibrary and click Create.
Make sure the Target Framework is .NET Framework 4.6.1 or higher (this is required for UiPath).


# Step 2: Install Newtonsoft.Json
Since we will use JSON serialization, install Newtonsoft.Json:

Using NuGet Package Manager:

Open Tools → NuGet Package Manager → Manage NuGet Packages for Solution.
Search for Newtonsoft.Json.
Install the latest version.
Using .NET CLI:

sh
Copy
Edit
dotnet add package Newtonsoft.Json

# Step 3: Define Your C# Class
Modify Class1.cs (Rename to UserGroup.cs)
Inside UserGroup.cs, add the following code:


```
using System;
using System.Collections.Generic;
using Newtonsoft.Json;

namespace MyUiPathLibrary
{
    public class UserGroup
    {
        public string Name { get; set; }
        public int Age { get; set; }
        public Address Address { get; set; }
        public List<string> Users { get; set; }

        public UserGroup()
        {
            Address = new Address();
            Users = new List<string>();
        }

        public string ToJson()
        {
            return JsonConvert.SerializeObject(this, Formatting.Indented);
        }
    }

    public class Address
    {
        public string Street { get; set; }
        public string City { get; set; }
    }
}
```

# Step 4: Build the DLL
Click Build → Build Solution (Ctrl+Shift+B).
Once built, locate the DLL:
php-template
Copy
Edit
<YourProjectFolder>\bin\Debug\MyUiPathLibrary.dll
Copy the MyUiPathLibrary.dll file to a safe location.

# Step 5: Import the DLL into UiPath
Open UiPath Studio.
Go to "Manage Packages".
Click "Settings" → "Add Custom Package Source".
Set the source path to where you copied MyUiPathLibrary.dll.
Click Add.
Search for MyUiPathLibrary in Manage Packages.
Install it and Import the Namespace.
