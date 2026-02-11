Create a `class` called `BaseApiController.cs`
```C#
namespace api.Controllers;

[ApiController]
[Route("api/[controller]")]
//use ControllerBase for api
//use Controller     for Views and/or api
public class BaseApiController : ControllerBase {

}
```

Now you can inherit from this `BaseApiController` class in all your **Controllers**. 
No need to add these to each Controller:
* `[ApiController]`
* [Route("api/[controller]")]