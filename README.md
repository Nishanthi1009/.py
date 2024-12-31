class Donor:
    def __init__(self, name, age, organ, blood_group): 
        self.name = name
        self.age = age
        self.organ = organ
        self.blood_group = blood_group

class Recipient:
    def __init__(self, name, age, organ_needed, blood_group): 
        self.name = name
        self.age = age
        self.organ_needed = organ_needed
        self.blood_group = blood_group

class DonationManagementSystem:
    def __init__(self): 
        self.donors = []
        self.recipients = []

    def add_donor(self, donor): 
        self.donors.append(donor)

    def add_recipient(self, recipient): 
        self.recipients.append(recipient)

    def match_donor_recipient(self): 
        return [(donor, recipient) for recipient in self.recipients for donor in self.donors if recipient.organ_needed == donor.organ and self.is_blood_group_compatible(donor.blood_group, recipient.blood_group)]

    def is_blood_group_compatible(self, donor_blood_group, recipient_blood_group): 
        compatible_groups = {
            "O-": ["O-", "O+", "A-", "A+", "B-", "B+", "AB-", "AB+"],
            "O+": ["O+", "A+", "B+", "AB+"],
            "A-": ["A-", "A+", "AB-", "AB+"],
            "A+": ["A+", "AB+"],
            "B-": ["B-", "B+", "AB-", "AB+"],
            "B+": ["B+", "AB+"],
            "AB-": ["AB-", "AB+"],
            "AB+": ["AB+"]
        }
        return recipient_blood_group in compatible_groups[donor_blood_group]

if __name__ == "__main__": 
    system = DonationManagementSystem() 
    while True: 
        print("1. Enter number of donors") 
        print("2. Enter donor details") 
        print("3. Enter number of recipients") 
        print("4. Enter recipient details") 
        print("5. Match donors with recipients") 
        print("6. Exit") 
        choice = int(input("Enter your choice: ")) 
        if choice == 1: 
            num_donors = int(input("Enter the number of donors: ")) 
        elif choice == 2: 
            system.donors.extend([
                Donor(
                    input("Enter donor's name: "), 
                    int(input("Enter donor's age: ")), 
                    input("Enter organ donated: "), 
                    input("Enter donor's blood group: ")
                ) for _ in range(num_donors)
            ]) 
        elif choice == 3: 
            num_recipients = int(input("Enter the number of recipients: ")) 
        elif choice == 4: 
            system.recipients.extend([
                Recipient(
                    input("Enter recipient's name: "), 
                    int(input("Enter recipient's age: ")), 
                    input("Enter organ needed: "), 
                    input("Enter recipient's blood group: ")
                ) for _ in range(num_recipients)
            ]) 
        elif choice == 5: 
            matches = system.match_donor_recipient() 
            print("Matches:") 
            for donor, recipient in matches: 
                print(f"Donor: {donor.name}, Recipient: {recipient.name}") 
        elif choice == 6: 
            break 
        else: 
            print("Invalid choice. Please enter a valid choice.")
