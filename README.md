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

```swift
extension View {
  func readSize(onChange: @escaping (CGSize) -> Void) -> some View {
    background(
      GeometryReader { geometryProxy in
        Color.clear
          .preference(key: SizePreferenceKey.self, value: geometryProxy.size)
      }
    )
    .onPreferenceChange(SizePreferenceKey.self, perform: onChange)
  }
}

private struct SizePreferenceKey: PreferenceKey {
  static var defaultValue: CGSize = .zero
  static func reduce(value: inout CGSize, nextValue: () -> CGSize) {}
}

struct ContentView: View {
    @State private var commonSize = CGSize()
    var body: some View {
        VStack {
        Text("Hello, world!")
            .padding()
            .border(.yellow, width: 1)
            .readSize { textSize in
                commonSize = textSize
            }
        Rectangle()
                .foregroundColor(.yellow)
            .frame(width: commonSize.width, height: commonSize.height)
        }
    }
}
```
