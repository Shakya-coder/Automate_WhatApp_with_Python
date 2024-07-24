#Code by R K Shakya

import pywhatkit
import datetime
import re

# Function to read contacts from VCF file
def read_vcf(vcf_file):
    contacts = {}
    with open(vcf_file, 'r') as file:
        lines = file.readlines()
        name = None
        phone = None
        for line in lines:
            if line.startswith("FN:"):
                name = line.strip().replace("FN:", "").lower()
            elif line.startswith("TEL;"):
                phone = line.strip().replace("TEL;TYPE=CELL:", "")
                if name and phone:
                    contacts[name] = phone
                    name = None
                    phone = None
    return contacts

# Function to send WhatsApp message
def send_whatsapp_message(phone_number, message, hour, minute):
    pywhatkit.sendwhatmsg(f"+{phone_number}", message, hour, minute)

# Function to handle sending messages immediately
def send_message_now(phone_number, message):
    current_time = datetime.datetime.now()
    send_whatsapp_message(phone_number, message, current_time.hour, current_time.minute + 1)

# Function to handle sending messages at a scheduled time
def send_message_at_time(phone_number, message):
    try:
        hour = int(input("Enter the hour (24-hour format): "))
        minute = int(input("Enter the minute: "))
        if 0 <= hour < 24 and 0 <= minute < 60:
            send_whatsapp_message(phone_number, message, hour, minute)
        else:
            print("Invalid time format. Please enter hour between 0-23 and minute between 0-59.")
    except ValueError:
        print("Invalid input. Please enter numeric values for hour and minute.")

# Main function to handle the message command
def main():
    # Load contacts from VCF file
    contacts = read_vcf('Enter_the_path_to_ur_contacts_vcf_file.vcf')
    
    # Get user input
    contact_name = input("Enter the name or phone number to whom you want to send a message: ").strip().lower()
    if contact_name in contacts:
        phone_number = contacts[contact_name]
    else:
        phone_number = contact_name  # Assume it's a phone number if not found in contacts
    
    message = input("Write the message you want to send: ").strip()
    
    # Ask user if they want to send the message now or later
    option = input("Do you want to send this message now or set a time?\n1. Now\n2. Set time\nChoose an option (1 or 2): ").strip()
    
    if option == "1":
        send_message_now(phone_number, message)
    elif option == "2":
        send_message_at_time(phone_number, message)
    else:
        print("Invalid option. Please choose 1 or 2.")


if __name__ == "__main__":
    main()
