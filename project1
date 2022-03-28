import pickle

 
password = "pass123"
 
Start = """\nWelcome to EasyMeals, our restaurant management system!
Choose one of the following options to proceed:
[M] Menu: Order and view our menu!
[A] Admin panel: Edit and view the menu, past orders and customers!
[Q] Quit
"""
 
AdminTab = """\n \nWelcome to the admin panel!\n Choose one of the following options to proceed:\n
[M] Menu: View and edit the restaurant menu.
[F] Food items: View and edit the food items available.
[O] Orders: View previous orders & bills.
[C] Customers: View all customers.
[P] Password: Edit & update the password for the admin panel.
[B] Back to main menu
"""
 
MenuTab = """\n \nWelcome to the Menu!"""
 
Admin_MenuTab = """Do you want to edit the menu?\nPlease choose one of the following options to proceed:\n
[A] Add: Add a food item to the menu.
[R] Remove: Remove a food item from the menu.
[B] Back to the admin panel
"""
 
FoodItem = """Do you want to edit the food items?\nPlease choose one of the following options to proceed:\n
[C] Create: Create a new food item.
[E] Edit: Edit an existing food item.
[R] Remove: Remove an existing food item.
[B] Back to the admin panel
"""
 
# name, price, desc, special, spicy, egg
menu = [1, 2, 3]
orders = {}
data = {'menu': menu, 'orders': orders, 'food': food}
food = {1: ["Caesar Salad", 100, "Roasted Turkey, baby greens, chopped eggs, red onions, avacado, bacon, grated parmesan cheese and tomatoes, served with your choice of dressing."],
       2: ["Chicken Pesto Pizza", 200, "Grilled Chickens, diced tomatoes, mozzarella cheese, and mushrooms with pesto sauce."],
       3: ["Spaghetti Bolognese", 150, "Spaghetti long pasta with slow cooked mince meat sauce made with non- alcoholic wine, plum tomatoes, celery, onions, seasoned with nutmeg."]}


def sys_in():
   global data, menu, orders, food
   with open('/content/drive/My Drive/easymeals.dat', 'wb') as F:
       try:
           file_data = pickle.load(F)
           data = file_data
           menu = data['menu']
           orders = data['orders']
           food = data['food']
       except:
           pickle.dump(data, F)
 
def update():
   global data
   data['menu'] = menu
   data['orders'] = orders
   data['food'] = food
   with open('/content/drive/My Drive/easymeals.dat', 'wb+') as F:
       pickle.dump(data, F)
 
def add_menu():
   print("\nHere are all the food items:")
   display_all_food_items()
   add_index = int(input("Enter the item number of the food item to be added: "))
   if add_index in menu:
       print("The food item is already present in the menu.")
   else:
       if add_index in food:
           menu.append(add_index)
           print("Food item added!")
       else:
           print("Invalid item number.")
   return 0
 
def remove_menu():
   remove_index = int(input("Enter the item number of the food item to be removed: "))
   if remove_index in menu:
       menu.remove(remove_index)
       print("Food item removed!")
   else:
       print("Invalid item number.")
   return 0
 
def admin_menu():
   print("Here is the current menu:")
   display_menu()
   while True:
       print(Admin_MenuTab)
       choice = input("Enter your choice: ").upper()
       if choice == 'A':
           add_menu()
       elif choice == 'R':
           remove_menu()
       elif choice == 'B':
           return 0
       else:
           print("\nPlease choose only one of A/R/B.\n")
 
def admin_create_food_item():
   food_item_arr = []
   food_item_arr.append(input("Enter the name of the food item: "))
   food_item_arr.append(int(input("Enter the price of the food item in rupees: ")))
   food_item_arr.append(input("Enter the description of the food item: "))
   food[len(food)+1] = food_item_arr
   print("\nFood item added!\n")
   return 0
 
def admin_edit_food_item():
   item = int(input("Enter the item number of the food item to be edited: "))
   if item in food:
       print("Here is the current food item: ")
       display_food_item(food[item])
       print("Please enter the following information: ")
       food_item_arr = []
       food_item_arr.append(input("Enter the name of the food item: "))
       food_item_arr.append(int(input("Enter the price of the food item in rupees: ")))
       food_item_arr.append(input("Enter the description of the food item: "))
       food[item] = food_item_arr
       print("\nFood item updated!\n")
   else:
       print("Invalid item number.")
   return 0
 
def admin_remove_food_item():
   item = int(input("Enter the item number of the food item to be removed: "))
   if item in menu:
       menu.remove(item)
   if item in food:
       food.pop(item)
       print("\nFood item removed!\n")
   else:
       print("Invalid item number.")
   return 0
 
def admin_fooditems():
   print("\nHere are all the existing food items:")
   display_all_food_items()
   while True:
       print(FoodItem)
       choice = input("Enter your choice: ").upper()
       if choice == 'C':
           admin_create_food_item()
       elif choice == 'E':
           admin_edit_food_item()
       elif choice == 'R':
           admin_remove_food_item()
       elif choice == 'B':
           return 0
       else:
           print("\nPlease choose only one of C/E/R/B.")
 
def admin_orders():
   grand_grand_total = 0
   for order in orders:
       print("Order #" + str(order) + ":")
       generate_bill(orders[order])
       grand_grand_total += orders[order]["total"]
       print("\n")
   print("Number of orders:", len(orders))
   print("Total across all orders: ₹" + str(grand_grand_total))
   return 0
 
def admin_customers():
   all_customers = []
   for order in orders:
       if orders[order]["name"] not in all_customers:
           all_customers.append(orders[order]["name"])
   if len(all_customers) == 0:
       print("There are no customers!")
       return 0
   print("List of customers: ")
   n = 1
   for customer in all_customers:
       print(str(n) + ". " + customer)
       n += 1
   return 0
 
def reset_password():
   global password
   print("Current password is: " + password)
   new_pass = input("Enter new password: ")
   print("Your password has been reset")
   password = new_pass
   return 0
 
def admin_panel():
   while True:
       pass_in = input("Enter password for admin: ")
       if pass_in == password:
           break
       else:
           choice = input("\nSorry, that was incorrect. Do you want to try again? [Y: Yes, N: No]: ").upper()
           print()
           if choice == "Y":
               continue
           else:
               return
   while True:
       print(AdminTab)
       choice = input("Enter your choice: ").upper()
       if choice == 'M':
           admin_menu()
           update()
       elif choice == 'F':
           admin_fooditems()
           update()
       elif choice == 'O':
           admin_orders()
           update()
       elif choice == 'C':
           admin_customers()
           update()
       elif choice == 'P':
           reset_password()
           update()
       elif choice == 'B':
           return 0
       else:
           print("\nPlease choose only one of M/F/O/C/P/B.")
 
def display_food_item(food_item):
   print("["+str(food_item)+"]", food[food_item][0], end=" ")
   print()
   print(food[food_item][2])
   print("Cost: ₹" + str(food[food_item][1]))
   print()
  
def display_all_food_items():
   print("Number of food items:", len(food))
   print()
   for food_item in food:
       display_food_item(food_item)
   print()
   return 0
 
def display_menu():
   print("Number of items in our menu:", len(menu))
   print()
   for food_item in menu:
       display_food_item(food_item)
   print()
   return 0
 
def generate_bill(order):
   print("-"*60)
   print("Name:", order["name"])
   print("Mobile Number:", order["number"])
   print("-"*60)
   n = 1
   for item in order["order"]:
       print(str(n) + ". " + str(food[item[0]][0]) + ":  " + str(item[1]) + " serving(s) worth ₹" + str(item[1]*food[item[0]][1]))
       n += 1
   print("-"*60)
   print("Grand Total: ₹" + str(order["total"]))
   print("-"*60)
   return 0
 
def take_order():
   order_spec = {}
   name = input("Please enter your name: ")
   mobile_no = int(input("Please enter your mobile number: "))
   counter = {}
   for item in menu:
       counter[item] = 0
   order_spec["name"] = name
   order_spec["number"] = mobile_no
   order_spec["order"] = []
   total = 0
   while True:
       while True:
           item = int(input("Enter the item you wish to order: "))
           if item in menu:
               break
           else:
               print("That item is not available in our menu, please try again.")
       quantity = int(input("Enter the desired quantity: "))
       if quantity == 1:
           print(str(quantity) + " serving of " + food[item][0] + " has been added.")
       else:
           print(str(quantity) + " servings of " + food[item][0] + " have been added.")
       total += quantity*food[item][1]
       print("Order total is now ₹" + str(total))
       print()
       counter[item] += quantity
       more = False
       while True:
           choice = input("Do you want to add more items? [Y - Yes, N - No]: ").upper()
           if choice == 'Y':
               more = True
               break
           elif choice == 'N':
               more = False
               break
           else:
               print("\nPlease choose only one of Y/N.")
       if not more:
           break
   for x in counter:
       if counter[x] != 0:
           order_spec["order"].append([x, counter[x]])
   order_spec["total"] = total
   orders[len(orders)+1] = order_spec
   print("\nYour order has been placed! Here is your bill: ")
   generate_bill(order_spec)
   return 0
 
def menu_panel():
   print(MenuTab)
   display_menu()
   while True:
       choice = input("Do you want to place an order? [Y - Yes, N - No]: ").upper()
       if choice == 'Y':
           break
       elif choice == 'N':
           return 0
       else:
           print("\nPlease choose only one of Y/N.\n")
   take_order()
   print("Thank you!\n")
 
while True:
   sys_in()
   print(Start)
   choice = input("Enter your choice: ").upper()
   if choice == 'A':
       admin_panel()
       update()
   elif choice == 'M':
       menu_panel()
       update()
   elif choice == 'Q':
       break
   else:
       print("\nPlease choose only one of A/M/Q.")
