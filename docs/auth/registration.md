### User Registration API

#### Description
This endpoint allows new users to register on the platform. During registration, users must provide personal information such as phone number, first and last name, date of birth (DOB), and national ID number. Upon successful registration, a user number is generated and sent via WhatsApp to the user to complete the registration process.

#### Route
- **Method:** POST
- **URL:** `/v1/auth/register`

#### Headers
- **Content-Type:** application/json

#### Parameters
- **first_name** (required): String. The user's first name.
- **last_name** (required): String. The user's last name.
- **dob** (required): Date in the format `d/m/Y`. The user's date of birth.
- **phone** (required): String. The user's phone number. Must be valid and unique across profiles.
- **id_number** (required): String. The user's national identification number.

#### Response Status Codes
- **200 OK**: Registration successful. The response includes a success message and indicates that an SMS with the user number has been sent to the provided phone number.
- **500 Internal Server Error**: An error occurred while sending the user number via SMS. This might be due to an issue with the phone number or the SMS service. The response includes an error message advising the user to verify their phone number and try again.

#### Example Response
```json
{
  "success": true,
  "message": "Registration successful! Check your SMS for a user number to finish registration"
}
```