# SwiftUI_PreferenceKey

### Basic 

```swift


/**
 Preference Key is powerful tool
 When you need to change something from childview.
 Like Navigation Title
 */


// Define Custom Preferencey Key
struct CustomTitlePreferenceKey: PreferenceKey {

    static var defaultValue: String = ""
    
    static func reduce(value: inout String, nextValue: () -> String) {
        value = nextValue()
    }
    
}

/// Observe Preference Key
 .onPreferenceChange(CustomTitlePreferenceKey.self) { value in
     print("Changed Value: \(value)")
    self.text = value
 }


/// Set Preference Key
 .preference(key: CustomTitlePreferenceKey.self, value: "New haha hohohoho")

/// Define extension
extension View {
    
    func customTitle(text: String) -> some View {
        self.preference(key: CustomTitlePreferenceKey.self, value: text)
    }
    
}

```

### Practical Usage 
