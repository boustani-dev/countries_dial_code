Phone Number Validation Summary
This project includes a robust phone number validation system for Flutter applications. It features:

Country Code Detection: Identifies the country code from the phone number input.
Length Validation: Verifies that the phone number (excluding the country code) matches country-specific length requirements.
Support for Multiple Lengths: Accommodates multiple valid lengths for phone numbers in specific countries.

Example Usage
List<Map<String, dynamic>> countries = [
  {
    'code': 'KP',
    'label': "Korea, Democratic People's Republic of",
    'phone': '850',
    'phoneLength': [4, 6, 7, 13]
  }
];

String phoneInput = "+850123456789";
Map<String, dynamic>? countryCodeData = getCountryCodeData(phoneInput, countries);

if (countryCodeData != null) {
  String phoneNumber = phoneInput.substring(countryCodeData['phone'].length + 1);
  bool isValid = isPhoneNumberValid(phoneNumber, countryCodeData);
  print("Is the phone number valid? $isValid");
}
This validation ensures that phone numbers conform to international standards and country-specific rules.


AI(ChatGPT) Generated Description/
