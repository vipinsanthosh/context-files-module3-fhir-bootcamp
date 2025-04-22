# SMART on FHIR Provider Application Implementation

A SvelteKit-based SMART on FHIR provider application that launches from the Cerner EHR system, focusing on retrieving and recording patient vital signs. This app will be opened after the user launches the app from the EHR, and it will handle the OAuth 2.0 authorization flow, including token exchange and secure storage of access tokens.
The application will also implement a user-friendly interface for managing patient vitals, including retrieval, entry, and visualization of vital sign data.
DO NOT hardcode any patient data in the application. All patient data should be retrieved from the FHIR API using the access token obtained during the authorization process.

LAUNCH URL = eg: http://localhost:5173/?launch=(launch_id)&iss=(BASE_URL)
Redirect URI: http://localhost:5173

## Completed Tasks

- [x] Project setup with SvelteKit, TypeScript, and TailwindCSS

## In Progress Tasks

- [ ] Implement SMART on FHIR EHR Launch workflow
  - [ ] Capture the launch id and iss from the launch URL
  - [ ] Make sure to save iss in local storage
  - [ ] Set up authorization request handling with PKCE
  - [ ] Implement token exchange
  - [ ] Store and manage access tokens

## Future Tasks

- [ ] FHIR Data Access Implementation

  - [ ] Retrieve patient context from access token response
  - [ ] Implement FHIR API client for data access
  - [ ] Set up error handling for API requests
  - [ ] Create type definitions for FHIR resources

- [ ] Retrieve Patient Information

  - [ ] Capture patient ID from the access token
  - [ ] Check if patient banner is needed by looking at need_patient_banner in the access token
  - [ ] Fetch patient demographics using FHIR API
  - [ ] Display patient name, age, and other relevant details
  - [ ] Implement error handling for patient data retrieval
  - [ ] Create a loading state for patient data fetching

- [ ] Patient Vitals Management

  - [ ] Retrieve and display vital signs
  - [ ] Implement chronological ordering of vitals
  - [ ] Add visual indicators for abnormal values
  - [ ] Create filtering by date range and vital type
  - [ ] Implement search functionality
  - [ ] Create form for documenting new vital signs
  - [ ] Implement validation for vital sign entries
  - [ ] Set up submission of new vitals via FHIR API
  - [ ] Add confirmation for successful documentation
  - [ ] Support correction of recently documented vitals

- [ ] User Interface Development

  - [ ] Design responsive UI optimized for clinical workflow
  - [ ] Create consistent patient context display
  - [ ] Implement efficient forms for vital sign entry
  - [ ] Add appropriate units of measurement
  - [ ] Create visualizations for vital sign trends

- [ ] Security and Compliance
  - [ ] Implement proper OAuth 2.0 flow
  - [ ] Ensure secure token storage
  - [ ] Set up session timeout with warnings
  - [ ] Configure appropriate FHIR resource scopes
  - [ ] Add LOINC codes for vital sign measurements
  - [ ] Adhere to FHIR Observation resource profiles

## Implementation Plan

1. Set up SMART on FHIR launch flow

   - Implement the launch endpoint to receive parameters from EHR
   - Set up authorization request with proper scopes
   - Create token exchange mechanism
   - Implement secure token storage

2. Develop FHIR data access layer

   - Create utility functions for API requests
   - Implement specific endpoints for Patient and Observation resources
   - Set up proper error handling

3. Build patient vitals UI components

   - Create vitals list component with filtering options
   - Implement vitals entry form with validation
   - Build visualizations for trends

4. Implement security features
   - Token refresh mechanism
   - Session management
   - Proper scope handling

## Relevant Files

- `src/routes/+page.svelte` - Main application entry point
- `src/routes/launch/+page.svelte` - SMART launch endpoint
- `src/routes/auth/+page.svelte` - Authorization callback handler
- `src/lib/fhir/client.ts` - FHIR API client utilities
- `src/lib/components/VitalsList.svelte` - Component for displaying patient vitals
- `src/lib/components/VitalsEntry.svelte` - Form for entering new vitals
- `src/lib/utils/auth.ts` - Authentication utilities
- `src/lib/types/fhir.ts` - TypeScript definitions for FHIR resources

## Configuration

- Client ID: [[YOUR_APP_CLIENT_ID]]
- Redirect URI: http://localhost:5173
- Scopes: fhirUser openid user/Patient.rs user/Observation.cruds launch
