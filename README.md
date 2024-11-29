# AWS PPE (Personal Protective Equipment) Detection

A Python implementation that uses AWS Rekognition to detect personal protective equipment (PPE) in images stored in S3 buckets. The script provides detailed analysis of face covers, hand covers, and head covers for each person detected in the image.

## Prerequisites

- Python 3.8.8
- AWS Account with Rekognition access
- AWS Access Key and Secret Key
- S3 bucket containing images
- boto3 library

## Installation

```bash
pip install boto3
```

## Required Libraries
```python
import boto3
```

## Configuration

```python
aws_accesskey = "Your Access Key"
aws_secretaccess = "Your Secret Access Key"
myregion = "your-region"
```

## Features

### Main PPE Detection Function
```python
def Detect_PPE(aws_access, aws_secret, aws_region, Image, Bucket_Name):
    """
    Detects PPE equipment in images stored in S3.
    
    Args:
        aws_access: AWS access key
        aws_secret: AWS secret key
        aws_region: AWS region name
        Image: Name of image file in S3
        Bucket_Name: S3 bucket name
    
    Returns:
        int: Number of persons detected in the image
    """
```

### Analysis Parameters

Default configuration:
- Minimum confidence threshold: 80%
- Required equipment types:
  - FACE_COVER
  - HAND_COVER
  - HEAD_COVER

## Usage Example

```python
person_count = Detect_PPE(
    aws_accesskey,
    aws_secretaccess,
    "us-west-2",
    "image.jpg",
    "my-bucket"
)
```

## Output Information

The analysis provides detailed information about:

1. Person Detection:
   - Unique person IDs
   - Body parts detected
   - Confidence scores

2. PPE Details:
   - Type of equipment detected
   - Coverage assessment
   - Confidence scores
   - Bounding box coordinates

3. Summary Statistics:
   - Persons with required equipment
   - Persons without required equipment
   - Indeterminate cases

### Example Output Format
```
Detected PPE for people in image [image_name]

Detected people
---------------
Person ID: 0
Body Parts
----------
    FACE
        Confidence: 99.69
        Detected PPE
        ------------
        FACE_COVER
            Confidence: 99.70
            Covers body part: True
            Confidence: 99.49
```

## Features Detected

1. Body Parts:
   - FACE
   - HEAD
   - LEFT_HAND
   - RIGHT_HAND

2. PPE Types:
   - FACE_COVER (masks, respirators)
   - HAND_COVER (gloves)
   - HEAD_COVER (helmets, hard hats)

## Best Practices

1. Image Quality:
   - Use clear, well-lit images
   - Ensure subjects are clearly visible
   - Consider image resolution requirements

2. Performance:
   - Batch process multiple images when possible
   - Consider S3 transfer times
   - Monitor API usage limits

3. Security:
   - Secure credential storage
   - Use appropriate S3 bucket permissions
   - Implement access controls

## Error Handling

The implementation handles:
- S3 access errors
- Image processing failures
- Invalid parameters
- Service limits

## Limitations

- Works only with images stored in S3
- Requires minimum confidence threshold
- Subject to AWS Rekognition service limits
- May have reduced accuracy in poor lighting conditions

## AWS Requirements

1. IAM Permissions:
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "rekognition:DetectProtectiveEquipment",
                   "s3:GetObject"
               ],
               "Resource": "*"
           }
       ]
   }
   ```

2. S3 Bucket Requirements:
   - Appropriate bucket permissions
   - Supported image formats
   - Size limits

## Support

For AWS specific issues, refer to:
- [AWS Rekognition PPE Documentation](https://docs.aws.amazon.com/rekognition/latest/dg/ppe-detection.html)
- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/)
