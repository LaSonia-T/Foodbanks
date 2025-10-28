START
DISPLAY "Welcome to the Food Assistance Finder App!"

SET attempts = 0
SET max_attempts = 3

WHILE attempts < max_attempts:
    PROMPT user to enter a ZIP code
    STORE input as user_zip

    IF user_zip is not numeric OR length is not 5:
        DISPLAY "Invalid ZIP code. Please enter a 5-digit number."
        INCREMENT attempts by 1
        CONTINUE loop

    SEARCH database for resources matching user_zip

    IF results found:
        DISPLAY "Here are the food assistance resources near you:"
        FOR each resource in results:
            DISPLAY resource name, address, hours, contact info
        BREAK loop
    ELSE:
        DISPLAY "No resources found for that ZIP code."
        ASK user: "Would you like to try another ZIP code? (yes/no)"
        IF user answers "yes":
            INCREMENT attempts by 1
            CONTINUE loop
        ELSE:
            DISPLAY "Thank you for using the Food Assistance Finder."
            BREAK loop

IF attempts == max_attempts:
    DISPLAY "Maximum attempts reached. Please try again later."

END

# Food Assistance Finder Program
# Purpose: Help users find food assistance resources by ZIP code.
# This program asks the user for their ZIP code, checks a database of resources,
# and displays available food assistance options. It also handles invalid input
# and allows multiple attempts.

# Example database of food resources (in a real app, this could come from an API or file)
resources = {
    "76548": [
        {"name": "Harker Heights Food Care Center", 
         "address": "123 Main St", 
         "hours": "Mon-Fri 9am-5pm", 
         "contact": "555-123-4567"}
    ],
    "76541": [
        {"name": "Killeen Community Pantry", 
         "address": "456 Oak Ave", 
         "hours": "Tue-Sat 10am-4pm", 
         "contact": "555-987-6543"}
    ]
}

print("Welcome to the Food Assistance Finder App!")

# Track number of attempts
attempts = 0
max_attempts = 3

# Loop until user finds results or runs out of attempts
while attempts < max_attempts:
    user_zip = input("Enter your 5-digit ZIP code: ")

    # Validate input (must be 5 digits and numeric)
    if not user_zip.isdigit() or len(user_zip) != 5:
        print("Invalid ZIP code. Please enter a 5-digit number.")
        attempts += 1
        continue  # Ask again

    # Search for resources in the database
    if user_zip in resources:
        print("\nFood assistance resources in your area:")
        for r in resources[user_zip]:
            print(f"- {r['name']} | {r['address']} | {r['hours']} | Contact: {r['contact']}")
        break  # Exit loop once results are found
    else:
        print("No resources found for that ZIP code.")
        try_again = input("Would you like to try another ZIP code? (yes/no): ").lower()
        if try_again == "yes":
            attempts += 1
            continue
        else:
            print("Thank you for using the Food Assistance Finder. Stay safe!")
            break

# If user runs out of attempts
if attempts == max_attempts:
    print("Maximum attempts reached. Please try again later.")

