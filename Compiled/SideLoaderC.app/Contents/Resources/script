# SideLoaderC

# Import libs.
import os

try:
    from PyQt5.QtWidgets import QApplication, QWidget, QVBoxLayout, QHBoxLayout, QFileDialog, QPushButton
    from PyQt5.QtCore import QUrl
    from PyQt5.QtWebEngineWidgets import QWebEngineView, QWebEngineProfile
    from PyQt5.QtGui import QIcon
except Exception as e:
    os.system("pip install -r Packaged.txt")
    os.system("pip3 install -r Packaged.txt")

# Block the context menu.
class CustomWebEngineView(QWebEngineView):
    def contextMenuEvent(self, event):
        pass

# Create the web client.
class MyWebBrowser:
    def __init__(self):
        self.URL = "https://sideloader7.shelldroid.repl.co/"
        
        self.window = QWidget()
        self.window.setWindowTitle("SideLoaderC")
        self.layout = QVBoxLayout(self.window)
        self.horizontal = QHBoxLayout()
        
        self.browser = QWebEngineView()
        
        self.back_button = QPushButton("⬅️")
        self.back_button.setEnabled(False)
        self.back_button.clicked.connect(self.browser.back)
        
        self.forward_button = QPushButton("➡️")
        self.forward_button.setEnabled(False)
        self.forward_button.clicked.connect(self.browser.forward)
        
        self.layout.addLayout(self.horizontal)
        self.layout.addWidget(self.browser)
        self.horizontal.addWidget(self.back_button)
        self.horizontal.addWidget(self.forward_button)
        
        self.browser.setUrl(QUrl(f"{self.URL}"))
        
        self.profile = QWebEngineProfile.defaultProfile()
        self.profile.downloadRequested.connect(self.onDownloadRequested)
        
        self.browser.urlChanged.connect(self.onUrlChanged)
        
        self.window.show()
        
    # Allow downloads.
    def onDownloadRequested(self, download):
        options = QFileDialog.Options()
        options |= QFileDialog.DontUseNativeDialog
        filePath, _ = QFileDialog.getSaveFileName(
            self.window, "Save File", download.url().toString(), "All Files (*);;Text Files (*.txt)", options=options)
        
        if filePath:
            download.setPath(filePath)
            download.accept()
    
    # Update button states based on navigation history.
    def onUrlChanged(self, url):
        self.back_button.setEnabled(self.browser.history().canGoBack())
        self.forward_button.setEnabled(self.browser.history().canGoForward())

# Startup SideLoaderC!
if __name__ == "__main__":
    app = QApplication([])
    window = MyWebBrowser()
    app.exec_()