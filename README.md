# super-duper-robot-gist


```
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
