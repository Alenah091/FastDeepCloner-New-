## Object to interface converter
You could convert any object to an interface, even AnonymousTypes with easy. 
the object offcouse wont need to be inherited from the interface, the library will do this instead.

Example
```csharp
    // 
    public interface IUserGroup
    {
        string Name { get; set; }
    }

    public interface IUser
    {
        string Name { get; set; }
        
        // As you can see class user dose not have FirstName, but still
        // not all properties have to match the class, the library will handle only found property and add the extra one 
        // to the new created object
        string FirstName { get; set; }
        
        // You cant inc none interface in the operations 
        // So if you choose to have class Role in user, then you have to inc it in the interface as Interface and not class
        IUserGroup Role { get; set; }
    }
   
    
    public class User
    {
        public string Name { get; set; } = "sdjh";

        public int PasswordLength { get; set; } = 6;
        
        public Role Role { get; set; } = new Role();
    }
    
    public class Role
    {
        public string Name { get; set; } = "Test";
        
         public string RoleType { get; set; } = "Admin";
    }
```

Now you could simple convert User to IUser with easy.

```csharp
  User user = new User() { Name="Test" };
  IUser iUser = user.ActAsInterface<IUser>();
  
  // You could even use a AnonymousType
  IUser iUser = new { Name= "Test" }.ActAsInterface<IUser>();
  
  // as for list or ObservableCollection
  var lst = new List<User>();
  List<IUser> iUserList = lst.ActAsInterface<List<IUser>>();
  // Or 
  ObservableCollection<IUser> iUserList = lst.ActAsInterface<ObservableCollection<IUser>>();
  
```

