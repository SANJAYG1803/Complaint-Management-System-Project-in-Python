# Complaint-Management-System-Project-in-Python
The Complaint Management System is a Python project that provides a graphical user interface (GUI) using the Tkinter library. It allows users to submit complaints, view a list of existing complaints, and update the status of a complaint. The system utilizes a simple in-memory data structure to store and manage the complaints. 

import tkinter as tk
from tkinter import messagebox

complaints = [
    {"id": 1, "title": "Network Issue", "description": "Slow internet connection", "status": "Open"},
    {"id": 2, "title": "Bug in Software", "description": "Application crashes frequently", "status": "Open"},
    {"id": 3, "title": "Payment Error", "description": "Incorrect billing amount", "status": "Resolved"}
]

def submit_complaint():
    title = title_entry.get()
    description = description_text.get("1.0", "end-1c")
    complaints.append({"id": len(complaints) + 1, "title": title, "description": description, "status": "Open"})
    messagebox.showinfo("Success", "Complaint submitted successfully!")
    refresh_complaint_list()

def update_status():
    selected_complaint = complaint_listbox.get(complaint_listbox.curselection())
    if selected_complaint:
        complaint_id = int(selected_complaint.split(":")[0])
        new_status = status_entry.get()
        for complaint in complaints:
            if complaint["id"] == complaint_id:
                complaint["status"] = new_status
                break
        refresh_complaint_list()
        messagebox.showinfo("Success", "Complaint status updated successfully.")

def refresh_complaint_list():
    complaint_listbox.delete(0, tk.END)
    for complaint in complaints:
        complaint_listbox.insert(tk.END, f"{complaint['id']}: {complaint['title']} - {complaint['status']}")

window = tk.Tk()
window.title("Complaint Management System")

title_label = tk.Label(window, text="Complaint Title:")
title_label.pack()

title_entry = tk.Entry(window)
title_entry.pack()

description_label = tk.Label(window, text="Complaint Description:")
description_label.pack()

description_text = tk.Text(window, height=5)
description_text.pack()

submit_button = tk.Button(window, text="Submit", command=submit_complaint)
submit_button.pack()

complaint_listbox = tk.Listbox(window)
complaint_listbox.pack()

refresh_complaint_list()

status_label = tk.Label(window, text="New Status:")
status_label.pack()

status_entry = tk.Entry(window)
status_entry.pack()

update_button = tk.Button(window, text="Update Status", command=update_status)
update_button.pack()

window.mainloop()

