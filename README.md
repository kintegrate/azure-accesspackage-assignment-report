Overview
This PowerShell script is designed to interact with Microsoft Graph API for managing access packages and assignment requests within Azure Entitlement Management. It retrieves access package details and assignment requests, processes them, and generates a CSV report that includes merged data from assignment requests and assignments.

Prerequisites

Microsoft Graph PowerShell SDK: Install the Microsoft Graph PowerShell SDK by running the following command:
Install-Module Microsoft.Graph -Scope CurrentUser

Environment Variables: Set up the following environment variables:

CLIENT_ID: Service Principal Client ID.
CLIENT_SECRET: Service Principal Client Secret.
TENANT: Service Principal Tenant ID.

Permissions: The Service Principal must have the required permissions to access Microsoft Graph API endpoints for Entitlement Management (e.g., EntitlementManagement.ReadWrite.All).

Script Functions
Get-GraphAccessToken: Retrieves the access token for authentication to Microsoft Graph API using a service principal.
Get-Username: Fetches the username for a given target user ID from Microsoft Graph.
Get-ApName: Fetches the access package name for a given access package ID.

Usage

Run the Script:
Open a PowerShell terminal.
Run the script to initiate the process. You will be prompted to enter the access package catalog name.
pwsh ./your_script_name.ps1
Catalog Selection: If multiple catalogs match your input, the script will list the options, and you will need to select one by providing the appropriate index number.
Access Package Selection: You will be prompted to choose between running the report for all access packages or selecting specific ones. For specific access packages, provide the index numbers as comma-separated values (e.g., 0,1,2).

Features

Retrieves information about access packages and assignment requests from Azure Entitlement Management.
Handles pagination for retrieving large sets of data.
Merges access package assignment requests and assignments based on the requestor name, access package name, and date.
Outputs the merged data into a CSV file named MergedAssignmentData.csv.

Matching Pattern for Merging Data

The common matching pattern for merging assignment requests and assignments is based on the following:
Requestor Name: The name of the person who made the request.
Access Package Name: The name of the access package.
Request Date: The request date should be the same as the assignment start date.

Error Handling

Missing Environment Variables: The script checks if the required environment variables are set and exits with an error message if they are missing.
API Request Failures: If API requests fail, the script logs the error and moves to the next item, allowing processing to continue.

Output

The final output is a CSV file (MergedAssignmentData.csv) containing detailed information about each assignment request and its corresponding assignment. This report can be used for auditing purposes and access review.
CSV Fields Include:

Request ID: ID of the assignment request.
Request Type: Type of the request (e.g., AdminAdd).
Request DateTime: Time when the request was created.
Access Package Name: Name of the access package.
Requestor Name: Name of the person who made the request.
Request Justification: Justification for the request.
Assignment ID: ID of the access package assignment.
Assignment State: Current state of the assignment (e.g., Active).
Assignment Start: Start date of the assignment.
Assignment End: End date of the assignment.

Notes

Permissions: Make sure your service principal has sufficient permissions in Azure AD and Microsoft Graph to execute entitlement management actions.
Graph API Version: This script uses the /beta endpoint of Microsoft Graph. Features in beta might be subject to change.

Troubleshooting

Authentication Failures: Ensure that the service principal credentials are correct and that the required permissions have been assigned.
Data Retrieval Issues: If the script cannot retrieve data, verify that the catalog name and access package details are correct, and ensure that the API permissions are set up properly.

License

This script is provided "as is" without warranty of any kind. You may modify and use it in accordance with your needs.
Feel free to reach out for questions or suggestions regarding improvements to this script.
