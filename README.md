# MDXDeviceNotch

MDXDeviceNotch is a lightweight Objective-C utility designed to help iOS developers determine whether the current device has a **notch** (e.g., on iPhone X models and later) or a **physical Home Button** (e.g., on iPhone 8 and earlier). The project includes two convenience functions that allow you to easily detect these characteristics in your app, ensuring proper UI layout adjustments depending on the device.

## Features

- **Detect device notch**: Determine if the current iOS device has a notch.
- **Detect Home Button**: Check if the current iOS device has a physical Home Button.
- **Simple API**: Easily check for either a notch or a Home Button with two functions.
- **Lightweight**: The utility is minimal and focused, designed to integrate seamlessly into any iOS project.

## Installation

1. **Clone the repository:**

    ```bash
    git clone https://github.com/yourusername/MDXDeviceNotch.git
    ```

2. **Add the files to your project:**

   Copy the `MDXDeviceNotch.h` and `MDXDeviceNotch.m` files into your Xcode project.

3. **Import the header:**

   In any file where you need to detect the device notch or Home Button, simply import the header:

    ```objc
    #import "MDXDeviceNotch.h"
    ```

## Usage

### Detect if a device has a notch

Use the `MDXHasDeviceNotch()` function to determine if the current device has a notch.

#### Example:

```objc
if (MDXHasDeviceNotch()) {
    NSLog(@"This device has a notch.");
} else {
    NSLog(@"This device does not have a notch.");
}
```

### Detect if a device has a Home Button

Use the `MDXHasHomeButton()` function to check if the device has a physical Home Button.

#### Example:

```objc
if (MDXHasHomeButton()) {
    NSLog(@"This device has a Home Button.");
} else {
    NSLog(@"This device does not have a Home Button.");
}
```

## Important Notes

Both `MDXHasDeviceNotch()` and `MDXHasHomeButton()` rely on the application's **key window** being available to inspect its safe area insets. Therefore, **these functions should not be called too early in the app's lifecycle** (e.g., before the root view controller's view has been laid out). If called too early, they will log a warning and may not return meaningful results.

### Initialization Recommendation

To ensure the functions are called at the appropriate time, it is recommended to initialize them in your root view controller’s `viewWillLayoutSubviews` method:

```objc
- (void)viewWillLayoutSubviews
{
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        MDXHasDeviceNotch();
    });
}
```

This guarantees that the functions are only initialized once after the key window has been mounted, and their results will always be correct thereafter.

## License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.

## Contributions

Contributions are welcome! Please feel free to submit pull requests or open issues on GitHub.
