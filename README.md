[HttpPost]

[Route("Registration")]

O references

public ActionResult Registration (UserDTO userDTO)

if(!ModelState.IsValid)

,

return BadRequest(ModelState); }

var objUser dbContext.Users.FirstOrDefault(x => x. Email userDTO. Email);

if (objUser null)

{ dbContext. Users.Add(new User

,

FirstName userDTO. FirstName, LastName userDTO. LastName, Email userDTO. Email, Password userDTO. Password

,

else

10;

dbContext. SaveChanges(); return Ok("User registered successfully");

return BadRequest("User already exists with the same email address.")









[HttpPast]

[Route("Login")]

public ActionResult LegininginDTO LeginATO)

var user dbContext. Users.FirstOrDefault(xx. Email if(user != null) LoginDTO. Email && Password LoginDTO. Password);

return Ok(user);

return BuContent();

[HttpGet]

[Route("GetUsers")]

public ActionResult GetUsers()

return ok(dbContext.Users. ToList())

1

[Route("Getüser")]

public ActionResult GetUser(int id)

var user dbContext. Users.FirstOrDefault(x x.UserId

if (user null) return ok):

else

return ReContent();
