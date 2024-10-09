namespace MianMenu.Models
{
    public class MenuItem
    {
        public int ID { get; set; }
        public int? ParentID { get; set; }
        public string DisplayText { get; set; }
        public string URL { get; set; }
        public IEnumerable<MenuItem> TopLevelItems { get; set; }
        public List<MenuItem> Children { get; set; } = new List<MenuItem>();
    }
}




















//using Application.Models;
//using MianMenu.Models;
//using Microsoft.AspNetCore.Mvc;
//using System.Collections.Generic;
//using System.Linq;

//namespace Application.Controllers
//{
//    public class MenuItemsController : Controller
//    {
//        private readonly ApplicationDbContext _context;

//        public MenuItemsController(ApplicationDbContext context)
//        {
//            _context = context;
//        }

//        public IActionResult Index()
//        {
//            var menuItems = _context.MenuItems.ToList();
//            var model = BuildMenuTree(menuItems);
//            return View(model);
//        }

//        [HttpPost]
//        public IActionResult Create(MenuItem newItem)
//        {
//            if (newItem.ParentID == 0)
//            {
//                newItem.ParentID = null;
//            }
//            _context.MenuItems.Add(newItem);
//            _context.SaveChanges();
//            return RedirectToAction("Index");
//        }

//        private List<MenuItem> BuildMenuTree(List<MenuItem> menuItems)
//        {
//            var menuMap = new Dictionary<int, MenuItem>();
//            var rootItems = new List<MenuItem>();

//            foreach (var menuItem in menuItems)
//            {
//                menuMap[menuItem.ID] = menuItem;
//                menuItem.Children = new List<MenuItem>(); // Assuming MenuItem has a Children property
//            }

//            foreach (var menuItem in menuItems)
//            {
//                if (menuItem.ParentID.HasValue && menuMap.ContainsKey(menuItem.ParentID.Value))
//                {
//                    menuMap[menuItem.ParentID.Value].Children.Add(menuItem);
//                }
//                else
//                {
//                    rootItems.Add(menuItem);
//                }
//            }

//            return rootItems;
//        }

//        public IActionResult Create()
//        {
//            var model = new MenuItem
//            {
//                TopLevelItems = GetAllMenuItems()
//            };
//            return View(model);
//        }

//        private IEnumerable<MenuItem> GetAllMenuItems()
//        {
//            var items = _context.MenuItems.ToList();
//            var parentIds = items.Select(i => i.ParentID).Distinct().Where(id => id.HasValue).Select(id => id.Value);
//            var topLevelItems = items.Where(i => !parentIds.Contains(i.ID)).ToList();
//            return topLevelItems;
//        }
//    }
//}



























using MianMenu.Models;
using Microsoft.EntityFrameworkCore;

namespace Application.Models
{
    public class ApplicationDbContext : DbContext
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }

        public DbSet<MenuItem> MenuItems { get; set; }
    }
}

















@model Application.Models.MenuItems
h2>Create new menu item</h2>

<form asp-action="Create" method="post">

<div class="form-group">

<label asp-for="DisplayText">Title:</label>

<input asp-for="DisplayText" class="form-control" />

</div>



<div class="form-group">

  <label asp-for="URL">URL:</label>

  <input asp-for="URL" class="form-control" />

</div>



<div class="form-group">

<label asp-for="ParentID">Parent menu item:</label>

<select asp-for="ParentID" class="form-control">

<option value=""> >-- None  -<< 
    @foreach (var item in Models.TopLevelItems)

{ <option value="@item.ID">@item.DisplayText</option>

}

</select>
</div>
<Button type="submit" class="btn btn-primary"></Button>
</form>


















# menuitems
