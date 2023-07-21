import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QWidget, QVBoxLayout, QHBoxLayout, QLabel, QLineEdit, QPushButton


class BMIApp(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Kalkulator Indeks Berat Badan")
        self.setGeometry(300, 300, 300, 200)

        # Membuat widget utama
        self.central_widget = QWidget(self)
        self.setCentralWidget(self.central_widget)

        # Membuat layout utama
        self.layout = QVBoxLayout(self.central_widget)

        # Membuat label dan input berat badan
        weight_layout = QHBoxLayout()
        weight_label = QLabel("Berat (kg):")
        self.weight_input = QLineEdit()
        weight_layout.addWidget(weight_label)
        weight_layout.addWidget(self.weight_input)
        self.layout.addLayout(weight_layout)

        # Membuat label dan input tinggi badan
        height_layout = QHBoxLayout()
        height_label = QLabel("Tinggi (cm):")
        self.height_input = QLineEdit()
        height_layout.addWidget(height_label)
        height_layout.addWidget(self.height_input)
        self.layout.addLayout(height_layout)

        # Membuat tombol hitung
        self.calculate_button = QPushButton("Hitung")
        self.layout.addWidget(self.calculate_button)

        # Menghubungkan tombol dengan metode penanganan
        self.calculate_button.clicked.connect(self.calculate_bmi)

    def calculate_bmi(self):
        weight = float(self.weight_input.text())
        height = float(self.height_input.text()) / 100  # Mengubah tinggi ke meter
        bmi = weight / (height * height)
        message = f"Indeks Berat Badan Anda: {bmi:.2f}"
        self.show_result(message)

    def show_result(self, message):
        result_label = QLabel(message)
        self.layout.addWidget(result_label)


if __name__ == "__main__":
    app = QApplication(sys.argv)
    bmi_calculator = BMIApp()
    bmi_calculator.show()
    sys.exit(app.exec_())
