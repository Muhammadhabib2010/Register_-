    from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QLineEdit, QPushButton, QHBoxLayout
    from PyQt5.QtCore import QTimer, QSize
    from PyQt5.QtGui import QFont, QIcon
    import sys
    
    class RegistrationForm(QWidget):  
        def __init__(self) :
            super().__init__()
            self.setWindowTitle("Registration")
            self.setGeometry(200, 200, 500, 250)
    
            self.name_label = QLabel("Fullname : ", self)
            self.setFontStyle(self.name_label, 50, 50)
            self.name_input = QLineEdit(self)
            self.name_input.setPlaceholderText("enter a fullname")
            self.setFontStyle(self.name_input, 200, 50)
    
            self.email_label = QLabel("Email: ", self)
            self.setFontStyle(self.email_label, 50, 100)
            self.email_input = QLineEdit(self)
            self.email_input.setPlaceholderText("enter a email")
            self.setFontStyle(self.email_input, 200, 100)
    
            self.password_label = QLabel("Password : ", self)
            self.setFontStyle(self.password_label, 50, 150)
    
            self.password_container = QWidget(self)
            self.password_layout = QHBoxLayout(self.password_container)
    
            self.password_input = QLineEdit(self.password_container)
            self.password_input.setPlaceholderText("enter a password")
            self.password_input.setEchoMode(QLineEdit.Password)
            self.setFontStyle(self.password_input, 0, 0)
    
            self.toggle_button = QPushButton(self.password_container)
            self.toggle_button.setIcon(QIcon("eye_open.png"))
            self.toggle_button.setCheckable(True)
            self.toggle_button.setStyleSheet("border: none; background-color: transparent;")
            self.toggle_button.setFixedSize(50, 50)
            self.toggle_button.setIconSize(QSize(50, 50))
    
            self.password_layout.addWidget(self.password_input)
            self.password_layout.addWidget(self.toggle_button)
            self.password_layout.setContentsMargins(0, 0, 0, 0)
    
            self.password_container.setGeometry(200, 150, 250, 30)
    
            self.toggle_button.move(self.toggle_button.x(), self.toggle_button.y() - 5)
    
            self.register_button = QPushButton("Registration", self)
            self.setFontStyle(self.register_button, 150, 200)
            self.register_button.clicked.connect(self.handle_registration)
    
            self.toggle_button.clicked.connect(self.toggle_password)
    
        def setFontStyle(self, obj, x, y) :
            obj.setFont(QFont("Comic Sans MS", 15))
            obj.move(x, y)
    
        def toggle_password(self) :
            if self.toggle_button.isChecked():
                self.password_input.setEchoMode(QLineEdit.Normal)
                self.toggle_button.setIcon(QIcon("eye_closed.png"))
            else:
                self.password_input.setEchoMode(QLineEdit.Password)
                self.toggle_button.setIcon(QIcon("eye_open.png"))
    
        def handle_registration(self) :
            QTimer.singleShot(2000, self.submit_data)
    
        def submit_data(self) :
            self.check_fullname(self.name_input.text())
            fullname = self.name_input.text()
            
            self.check_email(self.email_input.text())
            email = self.email_input.text()
            
            self.check_password(self.password_input.text())
            password = self.password_input.text()
        
        def check_fullname(self, new_fullname: str) :
            help_fullname = new_fullname.split()
            check = 0
        
            if len(help_fullname) != 3 and len(help_fullname) != 4 :
                raise Exception("Iltimos ism, familiya va otasining ismini to'g'ri kiriting")
            if len(help_fullname) == 3 :
                if new_fullname.title() != new_fullname :
                    raise Exception("Iltimos ism, familiya va otasining ismini to'g'ri kiriting")
            else :
               check_folkword = ["o'gli", "qizi", "O'gli", "Qizi"]
               for word in help_fullname :
                    if word not in check_folkword and word != word.title() :
                        raise Exception("Iltimos ism, familiya va otasining ismini to'g'ri kiriting")
                    
        def check_email(self, new_email : str) :
            check_youremail = [
                ".com", ".net", ".org", ".info", ".biz",
                ".jp", ".in", ".au", ".ca", ".br", ".kr", 
                ".it", ".es", ".mx", ".se", ".no", ".fi", 
                ".ru", ".us", ".uk", ".de", ".fr", ".cn",
                ".me", ".app", ".co", ".tv", ".ws", ".xyz",
                ".nl", ".pl",".edu", ".gov", ".mil", ".int", 
                ".online", ".site", ".tech", ".store", ".blog"
            ]
            assert "@" in new_email, "Sizning elektron pochtangizda @ yo'q"
            assert len(new_email[:new_email.find("@")]) >= 5, "@ dan oldin 5 ta harfdan kam bo'lishi kerak"
            assert any(new_email.endswith(manzil) for manzil in check_youremail), "Iltimos to'g'ri elektron pochta manzilini kiriting"
            if len(new_email[:new_email.find("@")]) == 5 or len(new_email[:new_email.find("@")]) == 6 :
                entity_check = sum(not char.isdigit() for char in new_email)
                if entity_check >= 2 :
                    raise Exception("Bunday elektron pochta mavjud(band)")
    
        def check_password(self, new_password : str) :
            assert len(new_password) >= 8, "Pasportning minimal uzunligi ettidan ortiq bo'lishi kerak"
            if all(not char.isdigit() for char in new_password) :
                raise Exception("Parolda kamida bitta raqam bo'lishi kerak")
            print("Yaraldi !")
    
    
    app = QApplication(sys.argv)
    window = RegistrationForm()
    window.show()
    sys.exit(app.exec_()) 











It is a photo an eyes
![eye_closed](https://github.com/user-attachments/assets/ed409d0a-fdd1-4b3d-89e6-d0c5b71b6b90)
![eye_open](https://github.com/user-attachments/assets/b94f5295-ff1e-4a24-8ef8-5f470ca77ebb)
