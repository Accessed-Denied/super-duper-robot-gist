# super-duper-robot-gist

## 1. To change the keyboard language programmatically
#### NOTE: - Keyboard must be added in the device
```swift
// To change the keyboard language programmatically
class CustomTextField: UITextField {
    private func getKeyboardLanguage() -> String? {
        return "ur" // here you can choose keyboard any way you need
    }
    override var textInputMode: UITextInputMode? {
        if let language = getKeyboardLanguage() {
            for tim in UITextInputMode.activeInputModes {
                if tim.primaryLanguage!.contains(language) {
                    return tim
                }
            }
        }
        return super.textInputMode
    }
}
```
