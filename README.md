# SwiftUI-A-moving-sine-wave
Creating a moving sine wave through SwiftUI.
# The first part
https://github.com/S-way520/SwiftUI-A-moving-sine-wave/assets/95877651/2207746e-d212-49be-85e1-cd8ecc48a6b9
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
struct SineWaveView: View {
    @State private var move: Double = 0.0
    var body: some View {
        GeometryReader { geometry in
            Path { path in
                let width = geometry.size.width
                let height = geometry.size.height
                path.move(to: CGPoint(x: 0, y: (height / 2) + sin(.pi * self.move) * Double(height) / 2))
                for angle in stride(from: 0, through: 2 * .pi, by: 0.05) {
                    let x = angle * Double(width) / (2 * .pi)
                    let y = sin(angle + .pi * self.move) * Double(height) / 2
                    path.addLine(to: CGPoint(x: x, y: y + height / 2))
                }
            }
            .stroke(Color.blue, lineWidth: 2)
            .onAppear {
                Timer.scheduledTimer(withTimeInterval: 0.01, repeats: true) { _ in
                    move -= 0.01
                }
            }
        }
    }
}
struct ContentView: View {
    var body: some View {
        VStack {
            SineWaveView()
                .frame(width: 200, height: 200)
                .padding()
            Text("Sine Wave")
        }
    }
}
```
