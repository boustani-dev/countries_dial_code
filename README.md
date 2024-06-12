**Phone Number Validation Summary**


This project includes a robust phone number validation system for Flutter applications. It features:


- Country Code Detection: Identifies the country code from the phone number input.
- Length Validation: Verifies that the phone number (excluding the country code) matches country-specific length requirements.
- Support for Multiple Lengths: Accommodates multiple valid lengths for phone numbers in specific countries.


**Example Usage**


**> models:**

```javascript
class CountryDialCode {
  final String label;
  final String phone;
  final String code;
  final List<int> phoneLength;

  CountryDialCode({
    required this.label,
    required this.phone,
    required this.code,
    required this.phoneLength,
  });
}

class PhoneNumberResult {
  final CountryDialCode? countryDialCode;
  final String strippedNumber;

  PhoneNumberResult(
      {required this.countryDialCode, required this.strippedNumber});
}

```

**> Functions:**

```javascript

  PhoneNumberResult identifyCountryCode(
      String phoneNumber, List<CountryDialCode> countryData) {
    // Normalize the phone number
    phoneNumber = phoneNumber.trim().replaceAll(' ', '').replaceAll('-', '');

    // Check if the phone number starts with a '+'
    if (!phoneNumber.startsWith('+')) {
      // throw FormatException('Phone number must start with "+" sign');
    }

    // Try to match the phone number with country codes
    for (var country in countryData) {
      if (phoneNumber.startsWith('+' + country.phone)) {
        // Strip the country code from the phone number
        String strippedNumber =
            phoneNumber.substring(('+' + country.phone).length);
        return PhoneNumberResult(
            countryDialCode: country, strippedNumber: strippedNumber);
      }
    }

    // If no match is found, return null
    return PhoneNumberResult(
        countryDialCode: null, strippedNumber: phoneNumber);
  }

  bool checkPhoneNumberLength(String strippedNumber, CountryDialCode? country) {
    if (country == null) {
      return false;
    }
    int length = strippedNumber.length;
    return country.phoneLength.contains(length);
  }
```
**>Example of Usage in a textField validator**

```python
List<CountryDialCode> countries = [
  CountryDialCode(code: 'IR', label: 'Iran, Islamic Republic of',phone: '98', phoneLength: [6, 10]),
 CountryDialCode(code: 'IS', label: 'Iceland', phone: '354', phoneLength: [7, 9]),
 CountryDialCode(code: 'IT', label: 'Italy', phone: '39', phoneLength: [10]),
 CountryDialCode(code: 'JE', label: 'Jersey', phone: '44', phoneLength: [10]),
];

String phoneInput = "+850123456789";

//checks if the value is phone number
              if (phoneNumberValidation.hasMatch(value)) {
                //checks if the phone number is valid
                PhoneNumberResult result =identifyCountryCode(value, countryData);
                if (result.countryDialCode != null) {
                  // print('The phone number $phoneNumber belongs to ${result.countryDialCode!.label}.');
                  bool isValidLength =checkPhoneNumberLength(
                          result.strippedNumber, result.countryDialCode);
                  if (!isValidLength) {
                    print('The phone number length is not valid.');
                    return ();
                  }
                } else {
                      print("Phone number is not valid ");
                  return ();
                }
              }
```
This validation ensures that phone numbers conform to international standards and country-specific rules.


AI(ChatGPT) Generated Description/
