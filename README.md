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

## 2. UISearchBar Customizations
````swift
//MARK: - UISearchBarDelegate
extension SearchVC: UISearchBarDelegate {
    // SearchBar Properties
    func SearchBarCustomization(){
        searchBar.scopeBarBackgroundImage = UIImage()
        searchBar.backgroundImage = UIImage()
        var searchTextField : UITextField?
        if #available(iOS 13.0, *) {
            searchTextField = searchBar.searchTextField
        } else {
            // Fallback on earlier versions
            if let matchingTextField = searchBar.subviews[0].subviews.compactMap ({ $0 as? UITextField }).first {
                searchTextField = matchingTextField
            }
        }
        guard let validTextField = searchTextField else { return }
        let image:UIImage = UIImage(named: "ic_iconSearch")!
        let imageView:UIImageView = UIImageView.init(image: image)
        imageView.contentMode = .scaleAspectFit
        validTextField.leftView = imageView
        validTextField.layer.cornerRadius = 6
        validTextField.layer.borderWidth = 1.0
        validTextField.layer.borderColor = #colorLiteral(red: 0.9058823529, green: 0.9058823529, blue: 0.9058823529, alpha: 1)
        validTextField.backgroundColor = .white
        validTextField.font = UIFont(name: APP_FONT.buenosAiresBook.rawValue, size: 14)
//        var bounds: CGRect
//        bounds = validTextField.frame
//        bounds.size.height = 60 //(set height whatever you want)
//        validTextField.bounds = bounds
        let cancelButtonAttributes = [NSAttributedString.Key.foregroundColor: UIColor.black]
        UIBarButtonItem.appearance().setTitleTextAttributes(cancelButtonAttributes , for: .normal)
        searchBar.becomeFirstResponder()
    }
    
    // searchBarCancelButtonClicked
    func searchBarCancelButtonClicked(_ searchBar: UISearchBar) {
        self.navigationController?.popViewController(animated: false)
    }
    
    // textDidChange
    func searchBar(_ searchBar: UISearchBar, textDidChange searchText: String) {
        let text = searchBar.text ?? ""
        // todo
    }
    
    // searchBarSearchButtonClicked
    func searchBarSearchButtonClicked(_ searchBar: UISearchBar) {
        searchBar.resignFirstResponder()
    }
}
