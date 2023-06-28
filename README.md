# custom_localization

A Flutter package to generate Localization classes from JSON File

### Note: Your Keys will be converted as per Dart's coding styles.

## Generated Code Sample

```dart
class R {
  static English get string => _getDefaultLocal();

  static String _appLocale;

  static Map<String, English> _supportedLocales = {
    "English": English(),
    "Chinese": Chinese(),
    "French": French(),
    "JAPAN": Japan(),
    "Italian": Italian(),
    "Spanish": Spanish(),
    "Germany": Germany(),
  };

  static English _getDefaultLocal() {
    //return default strings if locale is not set

    if (_appLocale == null) return English();

    //throw exception to notify given local is not found or not generated by the generator

    if (!_supportedLocales.containsKey(_appLocale))
      throw Exception(
          "$_appLocale is not found.\n Make sure you have added this locale in JSON file\n Try running flutter pub run build_runner");

    //return locale from map

    return _supportedLocales[_appLocale];
  }

  static void changeLocale(String newLocale) {
    _appLocale = newLocale;
  }
}

class English {
  AuthStrings authStrings = AuthStrings();
  CommonString commonString = CommonString();
  ErrorString errorString = ErrorString();
  NoDataStrings noDataStrings = NoDataStrings();
  ScreenTitle screenTitle = ScreenTitle();

  static String get languageCode => "English";

  static String get languageName => "English";
}

class AuthStrings {
  String editCompanyInformation = "Edit Company Information";

  String selectNatureOfOrganization = "Select Nature Of Organization";

  String setNewPassword = "Set your new password and sign in again.";

}
```

## Getting Started

1. Add following dependencies to `pubspec.yaml`.

```yaml
dependencies:
    custom_localization:
        git: https://gitlab.diamnow.com/flutter-public/flutter-localisation.git

dev_dependencies:
    build_runner: any
    custom_localization_generator:
        git:
          url: https://gitlab.diamnow.com/flutter-public/flutter-localisation.git
          path: custom_localization_generator
```

3. Create a json file in following format or export from the App Localization sheet

- Root elements must be language code
- ``language_code``,``script_code``  are required.
- set ``is_default`` to ``true`` if the locale is default locale otherwise not required.
- You can create any number of objects inside locale object ex. inside ```"en_us"```. 

```json
{
  "en_us": {
    "language_code": "en",
    "script_code": "us",
    "is_default": true,
    "lbl": {
      "app_name": "Test Localization",
      "user_name": "UserName"
    }
  },
  "iw": {
    "language_code": "iw",
    "lbl": {
      "user_name": "יציאה"
    }
  }
}
```

4. Create a class with ``@CustomLocalization("")`` and pass path of the JSON file in this annotation.

```dart
import 'package:custom_localization/custom_localization.dart';

part 'app_localization.g.dart';

@CustomLocalization("assets/strings.json")
class AppLocalization {}

```

5. Run ``build_runner`` to generate classes.

```shell script
flutter pub run build_runner build 
```