# Settings-UI

A Kotlin library for building user settings interfaces in Android applications.

**Note :**  This library is in development, which means it is prone to some errors and views may not look as clean. It may also provide methods that are not documented, so it is recommended not to use these methods as they may be changed in the future.


## Why use this library

- **Easy to use:** The library provides a simple and flexible way to create a settings screen for your Android app,
    with a variety of built-in preference items that can be easily added to the screen.
- **Customizable:** You can customize the appearance and behavior of the SettingsFragment and its preference items by 
    overriding the appropriate styles and attributes in your app's theme.
- **Clean UI:** The library provides a clean and intuitive user interface for the settings screen, 
    with a consistent look and feel across different preference items.
- **Supports multiple preference types:** The library supports various types of preferences, including switches, text input fields,
    dropdown lists, and more.
- **Saves preferences automatically:** The library automatically saves user preferences to Shared Preferences,
    so you don't have to worry about manually storing and retrieving them.
- **Provides functions to handle preferences:** The library provides function to change and get values from Preferences of different types
    
 ## Contribution
  Any contributions, large or small, major features, bug fixes, additional language translations,recommendations,
  unit/integration tests are welcomed and appreciated but will be thoroughly reviewed and discussed.

## Installation

To use the library, add the following dependency to your app's `build.gradle` file:

```kotlin
  repositories {
     google()
     mavenCentral()
     maven { url 'https://jitpack.io'}          
  }
```

```kotlin
  implementation 'com.github.Deaths-Door:settings-ui:latest-version'
```


## Usage

TODO

## Extra Functions 

### Preference Extensions

These extensions provide several extension functions that make it easier to work with `SharedPreferences` in Android.

To get a `SharedPreferences` instance, you can use the `Context.getPreference(name: String)` function. This function takes a name as a parameter and a mode *(default is Context.MODE_PRIVATE)* ,returns a `SharedPreferences` object.

```kotlin
    Context.getPreference(name,mode) 
```

Provides several `getPreferenceValue` functions that allow you to retrieve a value from the `SharedPreferences` object for a given key. These functions accept a default value that will be returned if the key does not exist in the `SharedPreferences`. The functions are overloaded for different data types, including `String`, `Boolean`, `Int`, `Float`, `Long`, `Set<String>` and `Any` (when type is unknown). There is also a version that can be used to retrieve a `List<Any>` of objects.

```kotlin
    SharedPreferences.getPreferenceValue(key)
```

Also provides several `changePreference` functions that allow you to change a value in the `SharedPreferences` object for a given key. These functions are also overloaded for different data types, including `String`, `Boolean`, `Int`, `Float`, `Long`, and `Set<String>`. There is also a version that can be used to change a `List<Any>` of objects. All of these functions return `void` and make the changes to the `SharedPreferences` immediately.

```kotlin
    SharedPreferences.changePreference(key,defaultValue)
```


## Customization

You can customize the appearance and behavior of the SettingsFragment and its preference items by overriding the
appropriate styles and attributes in your app's theme. Refer to the library's documentation for a full list of available 
styles and attributes which stated is below.
Some commons attributes include *( where this == custom view )*


Namespace for xml
```kotlin
    xmlns:setting="http://schemas.android.com/apk/res-auto"
```

| Attribute | XML Syntax | Kotlin Code | Description |
| --- | --- | --- | --- |
| `preferenceName` | `app:preferenceName="choices"` | `singleChoice.preferenceName = getSharedPreferences("choices", Context.MODE_PRIVATE)` | Specifies the name of the shared preferences file where the selected choice will be stored. |
| `key` | `app:key="selected_choice"` | `singleChoice.key = "selected_choice"` | Specifies the key used to store the selected choice in the shared preferences file. |

### Switch 

The `SwitchSetting` view is a custom view that allows the user to toggle a setting on or off using a switch.


#### In XML Layout
```kotlin
<com.deathsdoor.ui_core.widgets.Switch
        android:layout_width="match_parent"
        android:layout_height="100dp"
        setting:title="Enable Dark Mode"
        setting:shortDescription="This setting changes theme of app"
        setting:detailedDescription="Setting changes theme of app between Light and Dark mode"
        setting:switchChecked="false"
        setting:switchOffColor="@color/purple_500"
        setting:switchOnColor="@color/teal_200"
        setting:key="switch"
        setting:preferenceName="pref" />

```

#### Attributes

| Attribute | XML Syntax | Kotlin Code | Description |
| --- | --- | --- | --- |
| `title` | `app:title="Turn on notifications"` | `switchSetting.title = "Turn on notifications"` | Specifies the title displayed at the top of the view. |
| `shortDescription` | `app:shortDescription="Receive notifications"` | `switchSetting.shortDescription = "Receive notifications"` | Specifies a short summary of the setting's description. |
| `detailedDescription` | `app:detailedDescription="Enabling notifications allows you to receive updates and alerts from the app."` | `switchSetting.detailedDescription = "Enabling notifications allows you to receive updates and alerts from the app."` | Specifies a more detailed description of the setting. If not provided, the value of `shortDescription` will be used. |
| `useShortDescription` | `app:useShortDescription="true"` | `switchSetting.useShortDescription = true` | Forces the use of the `shortDescription` instead of the `detailedDescription` when displaying the setting's description. |
| `switchChecked` | `app:switchChecked="true"` | `switchSetting.switchChecked = true` | Specifies whether the switch should be checked or not. |
| `switchOnColor` | `app:switchOnColor="#00FF00"` | `switchSetting.switchOnColor = Color.GREEN` | Specifies the color of the switch when it is checked|
| `switchOffColor` | `app:switchOnColor="#0ADHAS"` | `switchSetting.switchOffColor = Color.RED` | Specifies the color of the switch when it is not checked|
| `showWarnWhenSwitchToggledOn` | `app:showWarnWhenSwitchToggledOn="false"` | `switchSetting.showWarnWhenSwitchToggledOn = false` | Determines whether a warning message should be displayed when the switch is turned on. |
| `showWarnWhenSwitchToggledOff` | `app:showWarnWhenSwitchToggledOff="false"` | `switchSetting.showWarnWhenSwitchToggledOff = false` | Determines whether a warning message should be displayed when the switch is turned off.|
| `showWarnWhenSwitchToggledOnMsg` | `app:showWarnWhenSwitchToggledOnMsg="Message"` | `switchSetting.showWarnWhenSwitchToggledOnMsg = "Message"` | contains the message to be displayed when the switch is turned on and `showWarnWhenSwitchToggledOn` is set to true.|
| `showWarnWhenSwitchToggledOffMsg` | `app:showWarnWhenSwitchToggledOffMsg="Message"` | `switchSetting.showWarnWhenSwitchToggledOffMsg = "Message"` | contains the message to be displayed when the switch is turned off and `showWarnWhenSwitchToggledOff` is set to true.|

The SwitchCustomView also has a `toggleListener` variable, which is an instance of the `OnSwitchToggleListener` interface. This listener is called when the switch is turned on or off and can be used to perform actions such as displaying a warning message.

```kotlin
val switchCustomView = SwitchCustomView(context)
switchCustomView.toggleListener = object : OnSwitchToggleListener {
    override fun onSwitchToggleOn(switchView: SwitchMaterial) {
        Toast.makeText(context, "Switch turned on", Toast.LENGTH_SHORT).show()
    }
    override fun onSwitchToggleOff(switchView: SwitchMaterial) {
        Toast.makeText(context, "Switch turned off", Toast.LENGTH_SHORT).show()
    }
}
```

### TextInput

The `TextInput` view is a custom view that displays a title, a description, and an edit button. When the edit button is clicked, a pop-up window appears with an EditText field where the user can enter a new value. The new value is then saved and the pop-up window is dismissed.

#### In XML Layout
```kotlin
    <com.deathsdoor.ui_core.widgets.TextInput
        android:layout_width="match_parent"
        android:layout_height="100dp"
        setting:description="Description"
        setting:inputType="InputType.ClASS_TEXT"
        setting:key="singleChoice"
        setting:preferenceName="smth"
        setting:title="Title" />
```

| Attribute | XML Syntax | Kotlin Code | Description |
| --- | --- | --- | --- |
| `title` | `app:title="Select a choice"` | `singleChoice.title = "Select a choice"` | Specifies the title displayed at the top of the view. |
| `description` | `app:description="Enter username"` | `singleChoice.description = "Enter username"` | Specifies the description displayed below the title. |
| `inputType` | `app:inputType="1"` | `singleChoice.inputType = InputType.CLASS_MAKE_TEXT` | Specifies the input type for the edit text. Accepted values are constants from the InputType class, such as TYPE_CLASS_TEXT or TYPE_CLASS_PHONE. |
| `hint` | `app:hint="Hint"` | `singleChoice.hint = "Hint"` | Specifies the hint text to be displayed in the edit text when it is empty. |

The TypeInput also has a `onConfirmListener` variable, which is an instance of the `OnConfirmListener` interface. This interface is used to define a listener for events related to the confirmation of input in a TextInput view.

- **`onConfirm(input: String, window: PopupWindow): Boolean` :** This method is called when the user confirms the input by clicking the "OK" button in the input dialog. The method should return a boolean value indicating whether the input is valid. If the input is valid, the value will be saved. If the input is invalid, `onDeny` is called.

- **`onCancel(input: String, window: PopupWindow) :`** This method is called when the user cancels the input by clicking the "Cancel" button in the input dialog. The method should close the input dialog by calling the `dismiss method of the window object`.

- **`onDeny(_binding: PopupEdittextBinding, window: PopupWindow) :`** This method is called when the user denies the input by clicking the "Deny" button in the input dialog. The method should display a toast message or perform some other action to indicate that the input has been denied.


**Note :** Below is the default implementation of the `onConfirmListener` variable

```kotlin
var onConfirmListener = object : OnConfirmListener{
        override fun onConfirm(input: String, window: PopupWindow): Boolean = true
        override fun onCancel(input: String, window: PopupWindow) = window.dismiss()
       override fun onDeny(_binding: PopupEdittextBinding, window: PopupWindow) {
            
            val currentBackground = (_binding.inputField.background as ColorDrawable).color
            _binding.inputField.setBackgroundColor(Color.RED)

            Toast.makeText(context,"DENIED",Toast.LENGTH_SHORT).show()

            // Vibrate the edit text view
            val vibrator =  context.getSystemService(Context.VIBRATOR_SERVICE) as Vibrator
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) vibrator.vibrate(VibrationEffect.createOneShot(50, VibrationEffect.DEFAULT_AMPLITUDE))
            else @Suppress("DEPRECATION") vibrator.vibrate(50)

            _binding.inputField.setBackgroundColor(currentBackground)
        }
    }
```

### SingleChoice

@Decpreated
The `SingleChoice` view is a custom view that allows the user to select a single choice from a list of options.

#### In XML Layout
```kotlin
<com.deathsdoor.ui_core.widgets.SingleChoice
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    setting:key="switch"
    setting:preferenceName="pref"
    setting:title="Choide Favourties"
    setting:shortDescription="This setting changes your favourite..."/>
```
#### Attributes

| Attribute | XML Syntax | Kotlin Code | Description |
| --- | --- | --- | --- |
| `title` | `app:title="Select a choice"` | `singleChoice.title = "Select a choice"` | Specifies the title displayed at the top of the view. |
| `description` | `app:description="Choose one of the following options"` | `singleChoice.description = "Choose one of the following options"` | Specifies the description displayed below the title. |

The SwitchCustomView also has a `whenLimitExceed` variable, which is an instance of the `OnRadioButtonLimitExceededListener` interface. This listener is called when the limit (which is 1) has exceeded.

```kotlin
val singleChoice = SingleChoice(context)
singleChoice.whenLimitExceed = object:OnLimitExceededListener {
        override fun onLimitExceeded(radioGroup: RadioGroup, id: Int) {
            Toast.makeText(context,"LIMIT EXCEEDED",Toast.LENGTH_SHORT).show()
        }
    }
```
## License

```
Copyright 2022 Aarav Shah

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
