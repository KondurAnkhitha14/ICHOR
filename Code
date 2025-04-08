import sqlite3
from datetime import datetime, timedelta
from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.button import Button
from kivy.uix.label import Label
from kivy.uix.screenmanager import Screen, ScreenManager
from kivy.uix.textinput import TextInput
class WelcomeScreen(Screen):
def init (self, **kwargs):
super(). init (**kwargs)
self.next_button = Button(
text="Next", size_hint=(0.3, 0.1), pos_hint={"center_x": 0.5},
on_release=self.switch_to_register_page
)
layout = BoxLayout(orientation="vertical")
layout.add_widget(Label(text="Welcome to the App"))
layout.add_widget(self.next_button)
self.add_widget(layout)
def switch_to_register_page(self, instance):
self.manager.current = "register_screen"
class RegisterScreen(Screen):
def init (self, **kwargs):
super(). init (**kwargs)
self.register_button = Button(
text="Register", size_hint=(0.3, 0.1), pos_hint={"center_x": 0.5}, on_release=self.register
)
self.back_button = Button(
text="Back", size_hint=(0.3, 0.1), pos_hint={"center_x": 0.5},
on_release=self.switch_to_home_page
)
self.name_input = TextInput(hint_text="Enter your name", size_hint=(0.5, None), height=30)
self.age_input = TextInput(hint_text="Enter your age", size_hint=(0.5, None), height=30)
self.blood_group_input = TextInput(hint_text="Enter your blood group", size_hint=(0.5, None),
height=30)
self.phone_number_input = TextInput(hint_text="Enter your phone number", size_hint=(0.5,
None), height=30)
layout = BoxLayout(orientation="vertical")
layout.add_widget(Label(text="Registration"))
layout.add_widget(Label(text="Name:"))
layout.add_widget(self.name_input)
layout.add_widget(Label(text="Age:"))
layout.add_widget(self.age_input)
layout.add_widget(Label(text="Blood Group:"))
layout.add_widget(self.blood_group_input)
layout.add_widget(Label(text="Phone Number:"))
layout.add_widget(self.phone_number_input)
button_layout = BoxLayout(orientation="horizontal")
button_layout.add_widget(self.register_button)
button_layout.add_widget(self.back_button)
layout.add_widget(button_layout)
self.add_widget(layout)
def register(self, instance):
name = self.name_input.text
age = self.age_input.text
blood_group = self.blood_group_input.text
phone_number = self.phone_number_input.text
if name and age and blood_group and phone_number:
# Store registration date
registration_date = datetime.now().strftime("%Y-%m-%d")
# Insert registration data into the database
connection = sqlite3.connect("blood_donation.db")
cursor = connection.cursor()
insert_query = """
INSERT INTO registrations (name, age, blood_group, phone_number, registration_date)
VALUES (?, ?, ?, ?, ?)
"""
cursor.execute(insert_query, (name, age, blood_group, phone_number, registration_date))
connection.commit()
connection.close()
print("Registered Successfully")
else:
print("Please fill in all fields")
def switch_to_home_page(self, instance):
self.manager.current = "home_screen"
class HomeScreen(Screen):
def init (self, **kwargs):
super(). init (**kwargs)
self.view_donor_button = Button(
text="View Donors",
size_hint=(0.3, 0.1),
pos_hint={"center_x": 0.5},
on_release=self.switch_to_donor_page,
)
self.view_available_donors_button = Button(
text="View Available Donors",
size_hint=(0.3, 0.1),
pos_hint={"center_x": 0.5},
on_release=self.switch_to_available_donors_page,
)
self.send_blood_request_button = Button(
text="Send Blood Request",
size_hint=(0.3, 0.1),
pos_hint={"center_x": 0.5},
on_release=self.send_blood_request,
)
self.view_notifications_button = Button(
text="View Notifications",
size_hint=(0.3, 0.1),
pos_hint={"center_x": 0.5},
on_release=self.switch_to_notifications_page,
)
self.back_button = Button(
text="Back", size_hint=(0.3, 0.1), pos_hint={"center_x": 0.5},
on_release=self.switch_to_welcome_page
)
layout = BoxLayout(orientation="vertical")
layout.add_widget(Label(text="Home Page"))
layout.add_widget(self.view_donor_button)
layout.add_widget(self.view_available_donors_button)
layout.add_widget(self.send_blood_request_button)
layout.add_widget(self.view_notifications_button)
layout.add_widget(self.back_button)
self.add_widget(layout)
def switch_to_donor_page(self, instance):
self.manager.current = "donor_screen"
def switch_to_available_donors_page(self, instance):
self.manager.current = "available_donors_screen"
def send_blood_request(self, instance):
print("Sent blood request successfully")
def switch_to_notifications_page(self, instance):
self.manager.current = "notifications_screen"
def switch_to_welcome_page(self, instance):
self.manager.current = "welcome_screen"
class DonorScreen(Screen):
def init (self, **kwargs):
super(). init (**kwargs)
layout = BoxLayout(orientation="vertical")
layout.add_widget(Label(text="Donor Information"))
self.back_button = Button(
text="Back", size_hint=(0.3, 0.1), pos_hint={"center_x": 0.5},
on_release=self.switch_to_home_page
)
layout.add_widget(self.back_button)
self.add_widget(layout)
def switch_to_home_page(self, instance):
self.manager.current = "home_screen"
class AvailableDonorsScreen(Screen):
def init (self, **kwargs):
super(). init (**kwargs)
layout = BoxLayout(orientation="vertical")
layout.add_widget(Label(text="Available Donors"))
self.back_button = Button(
text="Back", size_hint=(0.3, 0.1), pos_hint={"center_x": 0.5},
on_release=self.switch_to_home_page
)
layout.add_widget(self.back_button)
self.add_widget(layout)
def switch_to_home_page(self, instance):
self.manager.current = "home_screen"
class NotificationsScreen(Screen):
def init (self, **kwargs):
super(). init (**kwargs)
layout = BoxLayout(orientation="vertical")
layout.add_widget(Label(text="Notifications"))
self.back_button = Button(
text="Back", size_hint=(0.3, 0.1), pos_hint={"center_x": 0.5},
on_release=self.switch_to_home_page
)
layout.add_widget(self.back_button)
self.add_widget(layout)
def switch_to_home_page(self, instance):
self.manager.current = "home_screen"
class BloodDonationApp(App):
def build(self):
self.create_database()
sm = ScreenManager()
sm.add_widget(WelcomeScreen(name="welcome_screen"))
sm.add_widget(RegisterScreen(name="register_screen"))
sm.add_widget(HomeScreen(name="home_screen"))
sm.add_widget(DonorScreen(name="donor_screen"))
sm.add_widget(AvailableDonorsScreen(name="available_donors_screen"))
sm.add_widget(NotificationsScreen(name="notifications_screen"))
return sm
def create_database(self):
connection = sqlite3.connect("blood_donation.db")
cursor = connection.cursor()
create_table_query = """
CREATE TABLE IF NOT EXISTS registrations (
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT NOT NULL,
age INTEGER NOT NULL,
blood_group TEXT NOT NULL,
phone_number TEXT NOT NULL,
registration_date DATE NOT NULL
)
"""
cursor.execute(create_table_query)
connection.commit()
connection.close()
if name == " main ":
BloodDonationApp().run()
