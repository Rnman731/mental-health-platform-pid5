# Mental Health Assessment Platform - Deployment Guide

This guide provides instructions for deploying and using the Mental Health Assessment Platform, a bilingual (English/Hindi) web application for administering mental health assessments.

## Overview

The Mental Health Assessment Platform includes:

1. Multiple validated assessment scales:
   - CES-D (Center for Epidemiologic Studies Depression Scale) - 20-item version
   - PHQ-9 (Patient Health Questionnaire-9)

2. Key features:
   - Bilingual support (English/Hindi) throughout the platform
   - Provider setup for administering assessments
   - Automatic scoring and clinical interpretation
   - Results display with severity indicators
   - Downloadable reports for patients
   - Email functionality for healthcare providers
   - QR code access for easy sharing
   - Resource links and clinical guidance

## Recent Fixes

The platform has been updated to fix two key issues:

1. **Method Not Allowed Error**: Fixed the HTTP method handling in the administrator flow to ensure proper navigation between provider setup and assessment selection.

2. **QR Code Internal Server Error**: Implemented a robust QR code generation system using the Python `qrcode` library to replace the simplified SVG pattern approach.

## Deployment Instructions

### Local Deployment (Development)

1. Clone or download the project repository
2. Navigate to the project directory
3. Create a virtual environment (optional but recommended):
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
4. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
5. Run the application:
   ```
   python run.py
   ```
6. Access the application at http://localhost:5001

### Production Deployment

For a permanent deployment, we recommend:

1. Set up a proper hosting environment (e.g., AWS, Google Cloud, DigitalOcean)
2. Configure a production WSGI server (e.g., Gunicorn, uWSGI)
3. Set up a reverse proxy (e.g., Nginx, Apache)
4. Configure SSL for secure connections
5. Update the mail settings in `main.py` with your actual SMTP server details
6. Deploy using the provided `requirements.txt`

## Configuration

### Email Configuration

To enable email functionality, update the following settings in `src/main.py`:

```python
app.config['MAIL_SERVER'] = 'your-smtp-server.com'
app.config['MAIL_PORT'] = 587
app.config['MAIL_USE_TLS'] = True
app.config['MAIL_USERNAME'] = 'your-email@example.com'
app.config['MAIL_PASSWORD'] = 'your-password'
app.config['MAIL_DEFAULT_SENDER'] = 'Mental Health Platform <your-email@example.com>'
```

## Usage Instructions

1. **Provider Setup**:
   - Enter healthcare provider information
   - Enter basic patient information
   - Submit to proceed to assessment selection

2. **Assessment Selection**:
   - Choose between CES-D or PHQ-9 assessment
   - Click "Start Assessment" to begin

3. **Assessment Administration**:
   - Guide the patient through each question
   - Select the appropriate response for each item
   - Submit the assessment when complete

4. **Results**:
   - View the assessment results with severity interpretation
   - Download the report as HTML
   - Results are automatically emailed to the provider (if configured)

5. **QR Code Access**:
   - Click "Get QR Code" on the homepage
   - Share the QR code with colleagues for easy access to the platform

## Customization

To add additional assessment scales:

1. Add the scale information to the `assessments` dictionary in `src/main.py`
2. Add the scale items to a new list (similar to `cesd_items` or `phq9_items`)
3. Update the scoring and interpretation logic in the `interpret_score` function
4. Create appropriate templates or modify existing ones as needed

## Troubleshooting

If you encounter any issues:

1. Check the application logs for error messages
2. Verify that all dependencies are installed correctly
3. Ensure the server has proper permissions to access all files
4. For email issues, verify your SMTP server settings

## Support

For additional support or feature requests, please contact the development team.
