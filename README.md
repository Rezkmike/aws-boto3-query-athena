# Athena Query Executor

This Python script enables querying Amazon Athena from a Kubernetes pod running on AWS EKS. The script assumes a specific IAM role (`ROLE-X`) to access Athena and outputs the results to an S3 bucket. This is particularly useful in environments where the default service account's permissions are insufficient for the required Athena queries.

## Requirements

- AWS CLI installed and configured (only for local testing)
- Python 3.x
- `boto3` library
- AWS Account and appropriate permissions to assume `ROLE-X` and query Athena
- Kubernetes cluster with AWS EKS configured to use IAM Roles for Service Accounts (IRSA)

## Setup

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Rezkmike/aws-boto3-query-athena.git
   cd aws-boto3-query-athena
   ```

2. **Install Dependencies:**
   ```bash
   pip install boto3
   ```

3. **Configure Kubernetes and AWS:**
   - Ensure that your Kubernetes service account is linked to an IAM role with permissions to assume `ROLE-X`.
   - Configure `ROLE-X` in AWS IAM with the necessary permissions to execute queries in Athena and to write to the specified S3 bucket.

## Configuration

Edit the `config.py` file (you should create this file to manage configurations) to specify the Athena database, query, and the S3 output path:

```python
DATABASE = 'your_database'
QUERY = 'SELECT * FROM your_table LIMIT 10;'
S3_OUTPUT = 's3://your-output-bucket/path/'
ROLE_ARN = "arn:aws:iam::ACCOUNT_ID:role/ROLE-X"
```

## Usage

Run the script directly from the command line or as part of a Kubernetes job:

```bash
python query-athena.py
```

## Security

Ensure that all AWS and Kubernetes configurations adhere to the principle of least privilege. Do not hardcode sensitive information such as AWS access keys or secrets within the scripts or configuration files.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please ensure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)