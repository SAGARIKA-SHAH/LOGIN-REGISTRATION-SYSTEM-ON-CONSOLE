# LOGIN-REGISTRATION-SYSTEM-ON-CONSOLE
Login and Registration code using file handling on console language python.










def Signup():
    users = open(r"C:\Users\shah4\OneDrive\Desktop\users.txt", 'a+')
    users = open(r"C:\Users\shah4\OneDrive\Desktop\users.txt", "r")
    users_list = []
    passwords_list = []
    for i in users:
        a, b = i.split(" ")
        users_list.append(a.strip())
        passwords_list.append(b.strip())
    user_dict = dict(zip(users_list, passwords_list))

    username = input("enter username/EmailId: ")
    if username in user_dict:
        print("Username already exists,Login with Existing username or choose another username")

        home_screen()
    elif not username[0].isalpha() or "@" not in username or "." not in username or "@." in username:
        print("invalid username")
        Signup()

    #VALIDATE PASSWORD
    def set_password():

        password = input("enter password: ")
        reenter_password = input("re-enter password: ")
        if password != reenter_password:
            print("Password not matching")
            set_password()
        else:
            import re
            flag = 0
            while True:
                if (len(password)) < 5 or len(password) > 16:
                    flag = -1
                    break
                elif not re.search("[a-z]", password) or not re.search("[A-Z]", password):
                    flag = -1
                    break
                elif not re.search("[0-9]", password):
                    flag = -1
                    break
                elif not re.search("[!@#$%^&*()_+]", password):
                    flag = -1
                    break
                else:
                    flag = 0
                    users = open(r"C:\Users\shah4\OneDrive\Desktop\users.txt", "a+")
                    users.write(username + " " + password + "\n")
                    print("Registration Successful")
                    break
            if flag == -1:
                print("password not valid")
                set_password()

    set_password()



def forgot_password():
  users = open(r"C:\Users\shah4\OneDrive\Desktop\users.txt", "r")
  users_indb = []
  passwords_list = []
  for i in users:
        a, b = i.split(" ")
        users_indb.append(a.strip())
        passwords_list.append(b.strip())
  user_dict = dict(zip(users_indb, passwords_list))
  input_name = input("Enter your username/EmailId:")
  if input_name in user_dict:
        print(user_dict[input_name])
  else:
        print("user name does not exists, check with another username")
        forgot_password()


#LOGIN
def login():
    user_n = input("enter username/EmailId:")
    user_password = input("Enter password:")
    users = open(r"C:\Users\shah4\OneDrive\Desktop\users.txt", "r")
    users_indb = []
    passwords_list = []
    for i in users:
        a, b = i.split(" ")
        users_indb.append(a.strip())
        passwords_list.append(b.strip())
    user_dict = dict(zip(users_indb, passwords_list))
    if user_n in user_dict:
        if user_password == user_dict[user_n]:
            print("Login successful")
        else:
            print("Password Incorrect")
            print("Forgot Password ?")
            fp = input("Choose Y/N :")
            if fp == "Y":
                forgot_password()
                login()
            elif fp == "N":
                login()
            else:
                print('Invalid Choice')
                login()


    else:
        print("username not found")
        home_screen()


#HOME SCREEN DISPLAY
def home_screen():
    print("1. Resister\n2. Login\n")
    n = input("choose 1 or 2: ")
    if int(n) == 1:
        Signup()
    elif int(n) == 2:
        login()

    else:
        print("please choose either 1 or 2")
        home_screen()


default_screen = home_screen()
