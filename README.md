import json
import os

# Define the filename for storing contacts
CONTACTS_FILE = "contacts.json"

# Load contacts from the file
def load_contacts():
    if os.path.exists(CONTACTS_FILE):
        with open(CONTACTS_FILE, "r") as file:
            return json.load(file)
    return []

# Save contacts to the file
def save_contacts(contacts):
    with open(CONTACTS_FILE, "w") as file:
        json.dump(contacts, file, indent=4)

# Add a new contact
def add_contact(contacts):
    name = input("Enter contact name: ")
    phone = input("Enter phone number: ")
    email = input("Enter email address: ")
    contacts.append({"name": name, "phone": phone, "email": email})
    save_contacts(contacts)
    print("Contact added successfully!")

# View all contacts
def view_contacts(contacts):
    if not contacts:
        print("No contacts found.")
    else:
        for i, contact in enumerate(contacts, 1):
            print(f"{i}. Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")

# Edit an existing contact
def edit_contact(contacts):
    view_contacts(contacts)
    index = int(input("Enter the contact number to edit: ")) - 1
    if 0 <= index < len(contacts):
        print("Enter new details (leave blank to keep current value):")
        name = input(f"Name ({contacts[index]['name']}): ") or contacts[index]['name']
        phone = input(f"Phone ({contacts[index]['phone']}): ") or contacts[index]['phone']
        email = input(f"Email ({contacts[index]['email']}): ") or contacts[index]['email']
        contacts[index] = {"name": name, "phone": phone, "email": email}
        save_contacts(contacts)
        print("Contact updated successfully!")
    else:
        print("Invalid contact number.")

# Delete a contact
def delete_contact(contacts):
    view_contacts(contacts)
    index = int(input("Enter the contact number to delete: ")) - 1
    if 0 <= index < len(contacts):
        contacts.pop(index)
        save_contacts(contacts)
        print("Contact deleted successfully!")
    else:
        print("Invalid contact number.")

# Main program loop
def main():
    contacts = load_contacts()
    
    while True:
        print("\nContact Manager")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Edit Contact")
        print("4. Delete Contact")
        print("5. Exit")
        
        choice = input("Choose an option: ")
        
        if choice == "1":
            add_contact(contacts)
        elif choice == "2":
            view_contacts(contacts)
        elif choice == "3":
            edit_contact(contacts)
        elif choice == "4":
            delete_contact(contacts)
        elif choice == "5":
            print("Exiting the program.")
            break
        else:
            print("Invalid option. Please try again.")

if __name__ == "__main__":
    main()
