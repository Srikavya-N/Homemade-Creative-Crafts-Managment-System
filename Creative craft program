import sys

# ---------------- Sample Product Catalog ----------------
PRODUCTS = {
    "regular": [
        {"id": 1, "name": "Handmade Painting", "price": 800},
        {"id": 2, "name": "Craft Basket", "price": 500},
        {"id": 3, "name": "Photo Frame", "price": 300}
    ],
    "gift": {
        "chocolates": {"id": 4, "name": "Assorted Chocolates", "price": 450},
        "frames": {"id": 5, "name": "Gift Frame", "price": 350},
        "paintings": {"id": 6, "name": "Mini Painting", "price": 700},
        "crafts": {"id": 7, "name": "Decorative Crafts", "price": 400},
        "handloom": {"id": 8, "name": "Handloom Scarf", "price": 600}
    }
}

# ---------------- Global Cart ----------------
CART = []


# ---------------- Order Functions ----------------
def show_products(category="regular"):
    print("\n--- Available Products ---")
    if category == "regular":
        for p in PRODUCTS["regular"]:
            print(f"{p['id']}. {p['name']} - ₹{p['price']}")
    else:
        for k, v in PRODUCTS["gift"].items():
            print(f"{v['id']}. {v['name']} ({k}) - ₹{v['price']}")


def add_to_cart(username):
    pid = int(input("Enter product ID to add: "))
    qty = int(input("Enter quantity: "))
    for p in PRODUCTS["regular"]:
        if p["id"] == pid:
            CART.append({"username": username, "name": p["name"], "price": p["price"], "qty": qty})
            print(f"Added {qty} x {p['name']} to {username}'s cart.")
            return
    for v in PRODUCTS["gift"].values():
        if v["id"] == pid:
            CART.append({"username": username, "name": v['name'], "price": v['price'], "qty": qty})
            print(f"Added {qty} x {v['name']} to {username}'s cart.")
            return
    print("Invalid product ID.")


def show_cart(username=None):
    if not CART:
        print("\nCart is empty.")
        return 0
    print("\n--- Order Summary ---")
    total = 0
    for idx, item in enumerate(CART, start=1):
        if username and item["username"] != username:
            continue
        subtotal = item["price"] * item["qty"]
        print(f"{idx}. {item['name']} x {item['qty']} (by {item['username']}) = ₹{subtotal}")
        total += subtotal
    print(f"Total Amount: ₹{total}")
    return total


def modify_order(username):
    show_cart(username)
    idx = int(input("Enter item number to modify: ")) - 1
    user_items = [i for i, item in enumerate(CART) if item["username"] == username]

    if 0 <= idx < len(user_items):
        actual_idx = user_items[idx]
        new_qty = int(input("Enter new quantity: "))
        if new_qty <= 0:
            removed_item = CART.pop(actual_idx)
            print(f"{removed_item['name']} removed from {username}'s cart.")
        else:
            CART[actual_idx]["qty"] = new_qty
            print(f"{username}'s item quantity updated.")
    else:
        print("Invalid item.")


def cancel_order(username):
    global CART
    CART = [item for item in CART if item["username"] != username]
    print(f"{username}'s order cancelled.")


def place_order(username):
    total = show_cart(username)
    if total == 0:
        return

    confirm = input("Do you want to confirm the order? (yes/no): ").lower()
    if confirm != "yes":
        print("Order not confirmed.")
        return

    print("\n--- Payment ---")
    print("1. Online")
    print("2. Cash on Delivery (COD)")
    choice = input("Choose payment option: ")

    if choice == "1":
        print("Redirecting to Online Payment Gateway... (simulated)")
    else:
        print("Cash on Delivery selected.")

    print(f"✅ Order placed successfully by {username}!")


# ---------------- Main Flows ----------------
def gift_flow(username):
    purpose = input("Enter purpose of gift (e.g. birthday, anniversary): ")
    budget = int(input("Enter budget: "))

    print("\nSuggestions based on purpose & budget:")
    for k, v in PRODUCTS["gift"].items():
        if v["price"] <= budget:
            print(f"- {v['name']} ({k}) - ₹{v['price']}")

    show_products("gift")
    add_to_cart(username)


def regular_flow(username):
    show_products("regular")
    add_to_cart(username)


# ---------------- Login/Register ----------------
def login_or_register():
    print("Welcome to Homemade Arts & Crafts Ordering System")
    print("1. Login")
    print("2. Register")
    choice = input("Choose option: ")

    username = input("Enter your username: ")

    if choice == "1":
        print(f"✅ {username}, you have logged in successfully!")
    elif choice == "2":
        print(f"✅ {username}, you have registered successfully!")
    else:
        print(f"⚠ Invalid choice. Continuing as guest ({username}).")

    return username


# ---------------- Main Program ----------------
def main():
    username = login_or_register()  # Ask at the start

    while True:
        print(f"\n--- Main Menu ({username}) ---")
        print("1. Regular Purchase")
        print("2. Gift Purchase")
        print("3. View Order")
        print("4. Modify Order")
        print("5. Cancel Order")
        print("6. Place Order")
        print("7. Exit")

        choice = input("Choose option: ")

        if choice == "1":
            regular_flow(username)
        elif choice == "2":
            gift_flow(username)
        elif choice == "3":
            show_cart(username)
        elif choice == "4":
            modify_order(username)
        elif choice == "5":
            cancel_order(username)
        elif choice == "6":
            place_order(username)
        elif choice == "7":
            print(f"Bye Thank you ! Have a Nice Day 🙂 , {username}!")
            sys.exit()
        else:
            print("Invalid option.")


if __name__ == "__main__":
    main()