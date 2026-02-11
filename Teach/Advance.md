-  CancellationToken
    
-  GlobalUsing
    
-  DTO
    
-  https => api
    
-  https => client
    
-  Interface / Repository
    
-  Move `component.ts` code to a `service`
    
-  Save `user` on the browser and stay logged-in
    
-  Home => Show and hide `logout` button with signal
    
-  Home => Move `ts` code to `ngOnInit()`
    
-  Switch login-register and logout places with signal
    
-  Design Navbar
    
    -  Move `ts` code to `ngOnInit()`
        
    -  Move `Login`, `Register` and `Logout` buttons to `Navbar`
        
    -  menu with Photo location
        
-  API cleanup => ExtensionMethods
    
    -  ApplicationServiceExtensions.cs => AddApplicationServices
        
    -  IdentityServiceExtensions.cs => AddIdentityServices
        
    -  RepositoryServiceExtensions.cs => AddRepositoryServices
        
-  [[JWT (Token)]]
    
    -  `jwt.interceptor.ts` => Fix `showAllUsers()` error `401-Unathorized` in `Home` by sending the `token`
        
-  [Client-Side Vs. Server-Side Rendering](https://www.searchenginejournal.com/client-side-vs-server-side/482574/) CSR vs SSR
    
-  jwt interceptor
    
-  client => Create environments and place `baseApiUrl` in `environment.development`
    
-  Mappers
    
-  CalculateAge() for UserDto -- [[DateTimeExtensions]]
    
-  `Count()` for `List` and `Any()` for `IEnumerable`
    
-  [[Claim Principal]]
    
    -  `TokenService` change `DateTime.Now` to `DateTime.UtcNow`
        
    -  Add `ValidateLifetime = true` to `IdentityServiceExtensions` class
        
    -  `UserController` => simplify `ClaimPrincipalExtensions.GetUserId(User)` to `User.GetUserId()`
        
    -  `ClaimPrincipalExtensions` rename `user` to `principal`
        
-  Create these components
    
    -  `ServerErrorComponent` => `path: 'server-error'` design for any server error
        
    -  `MemberListComponent` => `path: 'members'` to show members
        
-  Basic `authGuard` with `MatSnackBar`
    
-  Modify the `Register` component
    
    -  Add `Range` to `DateOfBirth` in `RegisterDto` to prevent `1/1/1`
        
    -  Convert Angular `Date` to C# `DateOnly` for DateOfBirth
        
    -  Add all properties to the component
        
    -  unsubscribe
        
-  Create `backend` folder
    
    -  Move `api` to `backend`
        
    -  Move `match-finder.sln` to `backend` folder
        
-  Photo Upload (API)
    
    -  `image-processing` project
        
        -  From `Solution Explorer` create a `new Empty web, empty` project called `image-processing`. (Credit to Iman!)
            
        -  Add required libraries from `Nuget Gallery` to `image-processing.csproj`
            
            ```C#
            "SkiaSharp"
            "SkiaSharp.NativeAssets.Linux"
            ```
            
        -  Uninstall above libraries from `api.csproj` (if installed)
            
        -  From `_resources folder` import the given folders into `image-processing` project's folder (`Helpers`, `Interfaces`, `Services`)
            
    -  `api` project
        
        -  Add a `Photo` record/model
            
        -  Create an endpoint `AddPhoto` in `UserController` which takes a file
            
            -  Validate file (`minSize`, `maxSize`) and `fileType` to be image
                
        -  Create an `UploadPhotoAsync` method in `UserRepository` and `IUserRepository`
            
            -  Add `Photo` creation in `_Mapper`
                
        -  Add `wwwroot` folder to `api` folder
            
        -  In `api` => `Program.cs` Add `app.UseStaticFiles();` before `app.UseCors();`
            
        -  Add a reference of `image-processing` project to `api`
            
        -  Add these items to `api`'s `globalUsings.cs`
            
            ```C#
            global using image_processing.Interfaces;
            global using image_processing.Services;
            global using image_processing.Helpers;
            ```
            
        -  Add all new services to `RepositoryServiceExtensions`
            
        -  Make `PhotoService` to inherit from `PhotoStandardSize`
            
    -  Test Photo upload with `postman`
        
    -  Test the photo URL in the browser
        
    -  Check `MongoDbCompass` doc
        
-  Setup `member-card` (teach `@input`)
    
-  Photo Upload (client)
    
    -  In `userController` rename `fileInput` to `file` due to the `ng2-file-upload` requirement
        
    -  Create `user-edit` component under `components/user` folder
        
    -  Move `photo-editor` to `components/user`
        
    -  Inject `accountService` to get the `loggedInUser`
        
    -  Inject `memberService` to get `getMemberByEmail()`
        
    -  Send this member to `photo-edit.component.ts` using `@Input`
        
    -  Create `photo-editor` component
        
    -  Install `"ng2-file-upload"`
        
    -  Explain `user-edit.component.html` causing `photo-editor` not reloading on refresh
        
    -  Set `navbar/profile` photo on the first upload
        
        -  `api` and `client` => Add `gender` & `profilePhotoUrl` to `LoggedInUser` model
            
        -  `api` => `Mappers` => initialize `Gender` and `ProfilePhotoUrl`
            
        -  In `photo-editor-component.ts` setup `setNavbarProfilePhoto()`
            
        -  Use `profilePhotoUrl` in `loggedInUserSig` (e.g., `navbar`)
            
        -  Make it round with `border-radius: 50%`
            
-  Set another photo as main
    
    -  API
        
        -  Create appropriate `Controller endpoint` and `Repository method`
            
        -  Test in `Postman`
            
        -  Remove unnecessary `<string>` from `ActionResult`
            
    -  Client
        
        -  Create `UpdateResult` model
            
        -  Add `setMainPhoto()` in `user.service`
            
        -  Use it in `photo-editor` component
            
        -  Add `Set profile` button in `DOM`
            
        -  Set `loggedInUser` again
            
-  Delete photo
    
    -  Create appropriate `Controller endpoint` and `Repository method`
        
    -  Add `DeletePhotoFromDisk()` in `IPhotoService` and `PhotoService`
        
    -  Add `deletePhoto()` in `user.service`
        
    -  Use `deletePhoto()` in `photo-editor` component
        
    -  Add `delete` button in `DOM`
        
    -  Test in `Postman`
        
-  Update `LastActive` with `IAsyncActionFilter`
    
    -  Delete line 72 of `AccountRepository`
        
    -  Create `LogUserActivity` class
        
    -  Implement `UpdateLastActive()`
        
    -  Use it in `LogUserActivity`
        
    -  Add it in `ApplicationServiceExtensions`
        
    -  Add `[ServiceFilter(typeof(LogUserActivity))]` to `BaseApiController`
        
-  Setup `user-edit`
    
    -  API
        
        -  Create `UserUpdateDto.cs`
            
        -  Create `UpdateUserAsync()`
            
        -  Update `IUserRepository`
            
        -  Test with `Postman`
            
    -  Client
        
        -  Implement `updateUser()`
            
-  Loading using `ngx-spinner`
    
    -  Install `ngx-spinner`
        
    -  Setup style in `angular.json`
        
    -  Create `LoadingService.ts`
        
    -  Create `LoadingInterceptor`
        
    -  Register in `appConfig`
        
    -  Use in `app-component`
        
-  Complete navbar links
    
    -  `MatTabsModule`
        
    -  Links list
        
    -  Use in DOM and style
        
-  Error Handling
    
    -  Client
        
        -  Add `error.interceptor`
            
        -  Explain `modelStateErrors`
            
        -  Ensure routing matches `app.routes`
            
        -  Update `app.config`
            
        -  Design error components
            
    -  API
        
        -  Use `ExceptionController`
            
        -  Create `ExceptionMiddleware`
            
        -  Create `ApiException` record
            
        -  Register in `Program.cs`
            
-  Fix `User Since / Created` in `user-edit`
    
-  Encapsulation with traditional `Properties/props`
    
    -  Class with parameter-less constructor
        
    -  Class with constructor (1 parameter)
        
    -  Class with constructor (2 parameters)
        
    -  Full prop with conditions
        
    -  Short prop without default value
        
    -  Short prop with default value
        
-  Pagination
    
    -  API
        
        -  Create `PagedList`
            
        -  Create `PaginationParams`
            
        -  Add `HttpExtensions`
            
        -  Create `PaginationHeader`
            
        -  Adjust `GetAll` in `MemberController`
            
        -  Test in `Postman`
            
    -  Client
        
        -  Create `pagination.ts`
            
        -  Create `paginatedResult.ts`
            
        -  Modify `MemberService`
            
        -  Use in `member-list`
            
        -  Implement Angular Material `Paginator`
            
        -  Create `PaginationHandler` in `extensions` folder
            
            -  Rename `result` to `body`
                
            -  Implement `getPaginatedResult<T>(...)`
                
            -  Use anywhere needed
                
-  Handle Users by `AspNetCore.Identity.MongoDbCore`
    
    -  API Setup
        
        -  Rename `MongoDbSettings` to `MyMongoDbSettings`
            
        -  Rename `IMongoDbSettings` to `IMyMongoDbSettings`
            
        -  Rename files
            
        -  Update `appsettings.development.json`
            
        -  Install `AspNetCore.Identity.MongoDbCore`
            
    -  Create/Login user
        
        -  Add `AppRole` model
            
        -  Update `IdentityServiceExtension`
            
        -  Convert `AppUser` to `class`
            
        -  Add `[CollectionName("users")]`
            
        -  Inherit from `MongoIdentityUser<ObjectId>`
            
        -  Remove duplicated props
            
        -  Update `Mapper`
            
        -  Convert `LoggedInDto` to `class`
            
        -  Use `UserManager<AppUser>` in `AccountRepository`
            
        -  Convert all `ObjectId` to `string`
            
        -  Fix errors
            
        -  Test Register/Login in `Postman`
            
    -  Assign Roles
        
        -  Drop old database
            
        -  Create `SeedController`
            
        -  Run in `Postman`
            
        -  Create policies in `IdentityServiceExtensions`
            
        -  Add roles to token in `TokenService`
            
        -  Create `AdminController` & `AdminRepository`
            
        -  Apply `RequiredAdminRole`
            
        -  Create `UserWithRoleDto`
            
        -  Create `GetUsersWithRoles()`
            
        -  Adjust `AdminRepository`
            
        -  Test policy with `admin@a.com` and `a@a.com`
            
        -  Create `SuspendMember()`
            
        -  Create `DeleteMember()`
            
        -  Add more role management methods
            
    -  Client
        
        -  Add `403` handling in `errorInterceptor`
            
        -  Create `AdminService`
            
        -  Create `AdminPanelComponent`
            
        -  Test role-based UI
            
        -  Hide parts based on roles
            
            -  Create `setLoggedInUserRoles()`
                
            -  Decode token with `atob`
                
            -  Update `loggedInUserSig`
                
            -  Hide admin tab using `@if / @else if`
                
        -  Manually test route protection `localhost:4200/admin`