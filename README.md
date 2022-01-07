[comment]: # "Auto-generated SOAR connector documentation"
# RiskSense

Publisher: RiskSense  
Connector Version: 1\.0\.2  
Product Vendor: RiskSense  
Product Name: RiskSense Platform  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 4\.8\.24304  

This app integrates with the RiskSense platform to perform investigative and generic actions to detect and monitor vulnerabilities across the entire attack surface, hosts and applications, using RiskSense's inherent intelligence\-driven risk analytics to manage and control an organization's cyber risk

[comment]: # " File: readme.md"
[comment]: # ""
[comment]: # "    Copyright (c) RiskSense, 2020"
[comment]: # ""
[comment]: # "    This unpublished material is proprietary to RiskSense."
[comment]: # "    All rights reserved. The methods and"
[comment]: # "    techniques described herein are considered trade secrets"
[comment]: # "    and/or confidential. Reproduction or distribution, in whole"
[comment]: # "    or in part, is forbidden except by express written permission"
[comment]: # "    of RiskSense."
[comment]: # ""
[comment]: # "    Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
[comment]: # ""
## Explanation of the Asset Configuration Parameters

The asset configuration parameters affect \[test connectivity\] and all the other actions of the
application. Below are the explanation and usage of all these parameters.

-   **Base URL:** The URL used to connect with the RiskSense server. It represents the RiskSense
    platform's API base URL where /api/v1 represents the API version. Example:
    https://platform.risksense.com/api/v1
-   **Client Name:** Name of the client. All the actions will be executed for this client.
-   **API Token:** It is the API token of the user.
-   **Verify Server Certificate:** Validate server certificate
-   **Number of Retries:** The value of this parameter defines the number of attempts for which the
    action will keep on retrying if the RiskSense API continuously returns the “500 Internal Server
    Error” or "429 Too Many Requests". If the intermittent error gets eliminated before the number
    of retries gets exhausted, then, the action execution will continue along its workflow and if
    the intermittent error is still persistent and all the number of retries is exhausted, then, the
    action will fail with the latest error message being displayed. The parameter expects a positive
    integer value as input. If the parameter is not provided, then 2 (default value) will be
    considered as the value for the parameter.
-   **Backoff Factor:** A backoff factor to apply between attempts after the second try (most errors
    are resolved immediately by a second try without a delay). The parameter expects a valid float
    value as input. If the parameter is not provided, then 0.3 (default value) will be considered as
    the value for the parameter.
    -   Sleep time calculation: {backoff factor} \* (2 \*\* ({number of total retries} - 1))
        seconds.

## Steps to generate the API token

-   Go to the RiskSense platform and open 'User Settings'.
-   Navigate to the 'API TOKENS' section and click on the 'Generate' button.
-   Enter the name of the new token.

## Explanation of the RiskSense Actions' Parameters

-   ### Test Connectivity (Action Workflow Details)

    -   This action will test the connectivity of the Phantom server to the RiskSense instance by
        making an initial API call to the Client API using the provided asset configuration
        parameters.
    -   The action validates the provided asset configuration parameters. Based on the API call
        response, the appropriate success and failure message will be displayed when the action gets
        executed.

-   ### List Users

    -   **<u>Action Parameter:</u> Max Results**

          

        -   This parameter allows the user to limit the number of results. If the parameter is not
            provided, it will fetch by default 1000 results. The internal pagination logic is
            applied for fetching a large number of results.

    -   **Example:**
        -   List 600 users
            -   Max Results = 600

-   ### List Tags

    -   **<u>Action Parameter:</u> Max Results**

          

        -   This parameter allows the user to limit the number of results. If the parameter is not
            provided, it will fetch by default 1000 results. The internal pagination logic is
            applied for fetching a large number of results.

    -   **Example:**
        -   List 600 tags
            -   Max Results = 600

-   ### List Hosts

    -   **<u>Action Parameter:</u> Field Name**

          

        -   This parameter allows the user to filter the result data set based on the host
            attributes provided as input. It allows the comma-separated values of the host
            attributes. The user can get the list of valid host attributes by executing the List
            Filter Attributes action. The uid of the filter attribute must be provided here.  
            Here are a few examples of host attributes: hostName, ipAddress, criticality, rs3,
            assessment_labels.

    -   **<u>Action Parameter:</u> Operator**

          

        -   This parameter allows the user to provide the operator which will be applied to the
            value(s) provided in the Fieldname parameter. It allows the comma-separated values of
            valid operators. The user can get the list of valid operators by executing the List
            Filter Attributes action.  
            Here are a few examples of the operators:  
            -   **EXACT -** Filter records exactly matching the criteria.
            -   **IN -** Filter records matching any of the comma-separated values.
            -   **LIKE -** Filter the records with fieldname’s value having the string provided by
                the user.
            -   **RANGE -** Filter the records with fieldname’s value falling in the numerical/date
                range provided.

    -   **<u>Action Parameter:</u> Value**

          

        -   This parameter allows the user to provide the value of the host attributes, which is
            mentioned in the Fieldname parameter, to be considered for filter criteria. It expects a
            JSON formatted list of values.

    -   **<u>Action Parameter:</u> Exclusivity**

          

        -   This parameter allows the user to determine whether to fetch the results that are
            matching the filter criteria (defined by the Fieldname, Operator, and Value parameter)
            or to fetch the results that are not matching the filter criteria. It allows the
            comma-separated boolean values (true/false).

    -   **<u>Action Parameter:</u> Sort By**

          

        -   This parameter allows the user to provide the fieldname by which to sort the records. It
            allows the comma-separated values of valid host attributes. If multiple host attributes
            are provided, then multiple sorting will be applied starting from the left-most host
            attribute.
        -   **Note -** If an incorrect attribute value is provided in this parameter, then the
            sorting of the results by that attribute will be ignored.

    -   **<u>Action Parameter:</u> Sort Direction**

          

        -   This parameter allows the user to provide sorting order to be applied to the host
            attribute provided in the Sort By parameter. It allows the comma-separated values of
            valid Sort Direction(s) (ASC/DESC).

    -   **<u>Action Parameter:</u> Page**

          

        -   This parameter allows the user to provide the index of the page from where the results
            are to be fetched. It expects a numeric value as an input. If not provided, then 0 will
            be considered as the starting index of the page.

    -   **<u>Action Parameter:</u> Max Results**

          

        -   This parameter allows the user to limit the number of results. If the parameter is not
            provided, it will fetch by default 1000 results. The internal pagination logic is
            applied for fetching a large number of results.

    -   **Note:**

          

        -   The Fieldname, Operator, Value, and Exclusivity parameters are used to create a filter.
            So, the length of these four parameters must be the same.
        -   Similarly, a sorting direction is required for a host attribute that is used for
            sorting. So, the length of Sort By and Sort Direction parameters must be the same.

    -   **Examples:**
        -   List the hosts having hostname like a “test”, sorted based on the ID in descending
            order.
            -   Fieldname = hostName
            -   Operator = LIKE
            -   Value = \[“test”\]
            -   Exclusivity = false
            -   Sort By = id
            -   Sort Direction = DESC
        -   List the hosts that are not discovered on 2014-05-01. Results are sorted first by rs3 in
            ascending order and then by ID in ascending order.
            -   Fieldname = discoveredOn
            -   Operator = EXACT
            -   Value = \[“2014-05-01”\]
            -   Exclusivity = true
            -   Sort By = rs3, id
            -   Sort Direction = ASC, ASC
            -   **Note:** The date format is in YYYY-MM-DD. Also while using the EXACT operator,
                note that the expected results will be fetched only if the value provided in the
                Value parameter will be exactly matched. So, make sure that there are no unnecessary
                spaces in the Value parameter.
        -   List the hosts having ID 1 or 2 or 3.
            -   Fieldname = id
            -   Operator = IN
            -   Value = \[“1,2,3”\]
            -   Exclusivity = false
            -   **Note:** While using IN operator, note that the expected results will be fetched
                only if the value provided in the Value parameter will be exactly matched. So, make
                sure that there is no space provided between the comma and the value. Example:
                Incorrect Value = \[“1,\<space>2,3\<space>”\], Correct Value = \[“1,2,3”\]
        -   List the hosts having criticality in the range of 2 to 5. The maximum results to be
            fetched are 200.
            -   Fieldname = criticality
            -   Operator = RANGE
            -   Value = \[“2,5”\]
            -   Exclusivity = false
            -   Max Results = 200
        -   List the hosts having hostname like a test and rs3 value 850.
            -   Fieldname = hostName,rs3
            -   Operator = LIKE, EXACT
            -   Value = \[“test”, “850”\]
            -   Exclusivity = false, false

-   ### List Apps

    -   **<u>Action Parameter:</u> Field Name**

          

        -   This parameter allows the user to filter the result data set based on the application
            attributes provided as input. It allows the comma-separated values of application
            attributes. The user can get the list of valid application attributes by executing the
            List Filter Attributes action. The uid of the filter attribute must be provided here.  
            Here are a few examples of application attributes: name, description, criticality,
            assessment_labels, discovered_on.

    -   **<u>Action Parameter:</u> Operator**

          

        -   This parameter allows the user to provide the operator which will be applied to the
            value(s) provided in the Fieldname parameter. It allows the comma-separated values of
            valid operators. The user can get the list of valid operators by executing the List
            Filter Attributes action.  
            Here are a few examples of the operators:  
            -   **EXACT -** Filter records exactly matching the criteria.
            -   **IN -** Filter records matching any one of the comma-separated values.
            -   **LIKE -** Filter the records with fieldname’s value having the string provided by
                the user.
            -   **RANGE -** Filter the records with fieldname’s value falling in the numerical/date
                range provided.

    -   **<u>Action Parameter:</u> Value**

          

        -   This parameter allows the user to provide the value of the application attributes, which
            are mentioned in the Fieldname parameter, to be considered for filter criteria. It
            expects a JSON formatted list of values.

    -   **<u>Action Parameter:</u> Exclusivity**

          

        -   This parameter allows the user to determine whether to fetch the results that are
            matching the filter criteria (defined by the Fieldname, Operator, and Value parameter)
            or to fetch the results that are not matching the filter criteria. It allows the
            comma-separated boolean values (true/false).

    -   **<u>Action Parameter:</u> Sort By**

          

        -   This parameter allows the user to provide the fieldname by which to sort the records. It
            allows the comma-separated values of valid application attributes. If multiple
            application attributes are provided, then multiple sorting will be applied starting from
            the left-most application attribute.
        -   **Note -** If an incorrect attribute value is provided in this parameter, then the
            sorting of the results by that attribute will be ignored.

    -   **<u>Action Parameter:</u> Sort Direction**

          

        -   This parameter allows the user to provide sorting order to be applied to the application
            attribute provided in the Sort By parameter. It allows the comma-separated values of
            valid Sort Direction(s) (ASC/DESC).

    -   **<u>Action Parameter:</u> Page**

          

        -   This parameter allows the user to provide the index of the page from where the results
            are to be fetched. It expects a numeric value as an input. If not provided, then 0 will
            be considered as the starting index of the page.

    -   **<u>Action Parameter:</u> Max Results**

          

        -   This parameter allows the user to limit the number of results. If the parameter is not
            provided, it will fetch by default 1000 results. The internal pagination logic is
            applied for fetching a large number of results.

    -   **Note:**

          

        -   The Fieldname, Operator, Value, and Exclusivity parameters are used to create a filter.
            So, the length of these four parameters must be the same.
        -   Similarly, a sorting direction is required for a host attribute that is used for
            sorting. So, the length of Sort By and Sort Direction parameters must be the same.

    -   **Examples:**
        -   List the applications having a name like a “test”, sorted based on the ID in descending
            order.
            -   Fieldname = name
            -   Operator = LIKE
            -   Value = \[“test”\]
            -   Exclusivity = false
            -   Sort By = id
            -   Sort Direction = DESC
        -   List the applications having the group name “Default Group”. Results are sorted first by
            name in ascending order and then by ID in descending order.
            -   Fieldname = group_names
            -   Operator = EXACT
            -   Value = \[“Default Group”\]
            -   Exclusivity = false
            -   Sort By = name, id
            -   Sort Direction = ASC, DESC
        -   List the applications having ID 1 or 2 or 3.
            -   Fieldname = id
            -   Operator = IN
            -   Value = \[“1,2,3”\]
            -   Exclusivity = false
        -   List the applications having asset criticality in the range of 2 to 5. The maximum
            results to be fetched are 200.
            -   Fieldname = criticality
            -   Operator = RANGE
            -   Value = \[“2,5”\]
            -   Exclusivity = false
            -   Max Results = 200
        -   List the applications having a name like a test and criticality is one of 4,5,6.
            -   Fieldname = name,criticality
            -   Operator = LIKE, IN
            -   Value = \[“test”, “4,5,6”\]
            -   Exclusivity = false, false

-   ### List Unique Findings

    -   **Note:** RiskSense is rewriting the API which is being used for this action.

    -   **<u>Action Parameter:</u> Field Name**

          

        -   This parameter allows the user to filter the result data set based on the unique host
            finding attributes provided as input. It allows the comma-separated values of unique
            host finding attributes. The uid of the filter attribute must be provided here.  
            Here are a few examples of host attributes: title, group_names, severity,
            assessment_labels.

    -   **<u>Action Parameter:</u> Operator**

          

        -   This parameter allows the user to provide the operator which will be applied to the
            value(s) provided in the Fieldname parameter. It allows the comma-separated values of
            valid operators. The user can get the list of valid operators by executing the List
            Filter Attributes action.  
            Here are a few examples of the operators:  
            -   **EXACT -** Filter records exactly matching the criteria.
            -   **IN -** Filter records matching any one of the comma-separated values.
            -   **LIKE -** Filter the records with fieldname’s value having the string provided by
                the user.
            -   **RANGE -** Filter the records with fieldname’s value falling in the numerical/date
                range provided.

    -   **<u>Action Parameter:</u> Value**

          

        -   This boolean parameter allows the user to provide the value of the unique host finding
            attributes, which is mentioned in the Fieldname parameter, to be considered for filter
            criteria. It expects a JSON formatted list of values.

    -   **<u>Action Parameter:</u> Exclusivity**

          

        -   This parameter allows the user to determine whether to fetch the results that are
            matching the filter criteria (defined by the Fieldname, Operator, and Value parameter)
            or to fetch the results that are not matching the filter criteria. It allows the
            comma-separated boolean values (true/false).

    -   **<u>Action Parameter:</u> Sort By**

          

        -   This parameter allows the user to provide the fieldname by which to sort the records. It
            allows the comma-separated values of valid unique host finding attributes. If multiple
            unique host finding attributes are provided, then multiple sorting will be applied
            starting from the left-most unique host finding attribute.
        -   **Note -** If an incorrect attribute value is provided in this parameter, then the
            sorting of the results by that attribute will be ignored.

    -   **<u>Action Parameter:</u> Sort Direction**

          

        -   This parameter allows the user to provide sorting order to be applied to the unique host
            finding attribute provided in the Sort By parameter. It allows the comma-separated
            values of valid Sort Direction(s) (ASC/DESC).

    -   **<u>Action Parameter:</u> Page**

          

        -   This parameter allows the user to provide the index of the page from where the results
            are to be fetched. It expects a numeric value as an input. If not provided, then 0 will
            be considered as the starting index of the page.

    -   **<u>Action Parameter:</u> Max Results**

          

        -   This parameter allows the user to limit the number of results. If the parameter is not
            provided, it will fetch by default 1000 results. The internal pagination logic is
            applied for fetching a large number of results.

    -   **Note:**

          

        -   The Fieldname, Operator, Value, and Exclusivity parameters are used to create a filter.
            So, the length of these four parameters must be the same.
        -   Similarly, a sorting direction is required for a host attribute that is used for
            sorting. So, the length of Sort By and Sort Direction parameters must be the same.

    -   **Examples:**
        -   List the unique host findings having a title like a “Solaris”, sorted based on the
            severity in descending order.
            -   Fieldname = title
            -   Operator = LIKE
            -   Value = \[“Solaris”\]
            -   Exclusivity = false
            -   Sort By =severity
            -   Sort Direction = DESC
        -   List the unique host findings having the Assessment “First Assessment”. Results are
            sorted first by title in ascending order and then by severity in descending order.
            -   Fieldname = assessment_labels
            -   Operator = EXACT
            -   Value = \[“First Assessment”\]
            -   Exclusivity = false
            -   Sort By = title, severity
            -   Sort Direction = ASC, DESC
        -   List the unique host findings having group ID 1 or 2 or 3.
            -   Fieldname = group_ids
            -   Operator = IN
            -   Value = \[“1,2,3”\]
            -   Exclusivity = false
        -   List the unique host findings having severity in the range of 2.0 to 5.0, maximum
            results to be fetched are 200.
            -   Fieldname = severity
            -   Operator = RANGE
            -   Value = \[“2.0,5.0”\]
            -   Exclusivity = false
            -   Max Results = 200
        -   List the unique host findings having a title like a “Solaris” and severity is one of
            4.0,5.0,6.0.
            -   Fieldname = title,severity
            -   Operator = LIKE, IN
            -   Value = \[“Solaris”, “4.0,5.0,6.0”\]
            -   Exclusivity = false, false

-   ### List Host Findings

    -   **<u>Action Parameter:</u> Field Name**

          

        -   This parameter allows the user to filter the result data set based on the host finding
            attributes provided as input. It allows the comma-separated values of host finding
            attributes. The user can get the list of valid host finding attributes by executing the
            List Filter Attributes action. The uid of the filter attribute must be provided here.  
            Here are a few examples of host finding attributes: state, id, criticality, riskRating,
            assessment_labels.

    -   **<u>Action Parameter:</u> Operator**

          

        -   This parameter allows the user to provide the operator which will be applied to the
            value(s) provided in the Fieldname parameter. It allows the comma-separated values of
            valid operators. The user can get the list of valid operators by executing the List
            Filter Attributes action.  
            Here are a few examples of the operators:  
            -   **EXACT -** Filter records exactly matching the criteria.
            -   **IN -** Filter records matching any one of the comma-separated values.
            -   **LIKE -** Filter the records with fieldname’s value having the string provided by
                the user.
            -   **RANGE -** Filter the records with fieldname’s value falling in the numerical/date
                range provided.

    -   **<u>Action Parameter:</u> Value**

          

        -   This parameter allows the user to provide the value of the host finding attributes,
            which is mentioned in the Fieldname parameter, to be considered for filter criteria. It
            expects a JSON formatted list of values.

    -   **<u>Action Parameter:</u> Exclusivity**

          

        -   This parameter allows the user to determine whether to fetch the results that are
            matching the filter criteria (defined by the Fieldname, Operator, and Value parameter)
            or to fetch the results that are not matching the filter criteria. It allows the
            comma-separated boolean values (true/false).

    -   **<u>Action Parameter:</u> Status**

          

        -   This parameter allows the user to determine whether to fetch the open host findings or
            the closed host findings. It expects a string value (Valid values: Open/Closed).

    -   **<u>Action Parameter:</u> Sort By**

          

        -   This parameter allows the user to provide the fieldname by which to sort the records. It
            allows the comma-separated values of valid host finding attributes. If multiple host
            finding attributes are provided, then multiple sorting will be applied starting from the
            left-most host attribute.
        -   **Note -** If an incorrect attribute value is provided in this parameter, then the
            sorting of the results by that attribute will be ignored.

    -   **<u>Action Parameter:</u> Sort Direction**

          

        -   This parameter allows the user to provide sorting order to be applied to the host
            finding attribute provided in the Sort By parameter. It allows the comma-separated
            values of valid Sort Direction(s) (ASC/DESC).

    -   **<u>Action Parameter:</u> Page**

          

        -   This parameter allows the user to provide the index of the page from where the results
            are to be fetched. It expects a numeric value as an input. If not provided, then 0 will
            be considered as the starting index of the page.

    -   **<u>Action Parameter:</u> Max Results**

          

        -   This parameter allows the user to limit the number of results. If the parameter is not
            provided, it will fetch by default 1000 results. The internal pagination logic is
            applied for fetching a large number of results.

    -   **Note:**

          

        -   The Fieldname, Operator, Value, and Exclusivity parameters are used to create a filter.
            So, the length of these four parameters must be the same.
        -   Similarly, a sorting direction is required for a host attribute that is used for
            sorting. So, the length of Sort By and Sort Direction parameters must be the same.

    -   **Examples:**
        -   List the host findings having a title like a “test”, sorted based on the ID in
            descending order.
            -   Fieldname = title
            -   Operator = LIKE
            -   Value = \[“test”\]
            -   Exclusivity = false
            -   Sort By = id
            -   Sort Direction = DESC
        -   List the host findings having the state “assigned”. Results are sorted first by
            riskRating in descending order and then by ID in ascending order.
            -   Fieldname = state
            -   Operator = EXACT
            -   Value = \[“assigned”\]
            -   Exclusivity = false
            -   Sort By = riskRating, id
            -   Sort Direction = DESC, ASC
        -   List the host findings having ID 1 or 2 or 3.
            -   Fieldname = id
            -   Operator = IN
            -   Value = \[“1,2,3”\]
            -   Exclusivity = false
        -   List the host findings having asset criticality in the range of 2 to 5. The maximum
            results to be fetched are 200.
            -   Fieldname = criticality
            -   Operator = RANGE
            -   Value = \[“2,5”\]
            -   Exclusivity = false
            -   Max Results = 200
        -   List the host findings having status “Closed” and criticality is NOT in the range of 4
            to 8.
            -   Fieldname = criticality
            -   Operator = RANGE
            -   Value = \[“4,8”\]
            -   Exclusivity = true
            -   Status = Closed

-   ### List Filter Attributes

    -   **<u>Action Parameter:</u> Asset Type**

          

        -   Type of the asset of which the filter attributes will be fetched. Example: host,
            hostFinding, application, applicationFinding, tag, user.

    -   **Examples:**
        -   List filter attributes of host asset type.
            -   Asset Type = host
        -   List filter attributes of host finding asset type.
            -   Asset Type = hostFinding
        -   List filter attributes of application asset type.
            -   Asset Type = application

-   ### Get Hosts

    -   **<u>Action Parameter:</u> Host ID**

          

        -   The unique host ID of the host. The Host ID is either known by RiskSense users or it can
            be fetched from the output of List Hosts action.

    -   **<u>Action Parameter:</u> Host Name**

          

        -   The hostname of the host. Host Name is either known by RiskSense users or it can be
            fetched from the output of List Hosts action.

    -   **Note:**

          

        -   If both the parameters (Host Name and Host ID) are provided, then the action will be
            executed based on the host ID.

    -   **Examples:**
        -   Get the host(s) having hostname “image1”
            -   Host Name= image1
        -   Get the host(s) having ID “7”
            -   Host ID = 7
        -   Hostname = “image1” and ID = “7”
            -   Host Name = image1
            -   Host ID = 7

-   ### Get Host Finding

    -   **<u>Action Parameter:</u> Host Finding ID**

          

        -   The unique host finding ID of the host finding. Host finding ID is either known by
            RiskSense users or it can be fetched from the output of List Host Findings action.

    -   **Examples:**
        -   Get the host finding having ID “6”
            -   Host Finding ID = 6

-   ### Get App

    -   **<u>Action Parameter:</u> App ID**

          

        -   The unique application ID of the application. The Application ID is either known by
            RiskSense users or it can be fetched from the output of List Apps action.

    -   **Examples:**
        -   Get the application having ID “5”
            -   Application ID = 5

-   ### List Vulnerabilities

    -   **<u>Action Parameter:</u> Host Finding ID**

          

        -   The host finding ID for which the vulnerabilities are to be fetched. Host finding ID is
            either known by RiskSense users or it can be fetched from the output of List Hosts
            action.

    -   **Examples:**
        -   List the vulnerabilities of the host finding having ID “6”
            -   Host Finding ID = 6

-   ### Tag Asset

    -   **Note:** This app supports the below tag types.

          

        -   CUSTOM
        -   LOCATION
        -   COMPLIANCE
        -   REMEDIATION
        -   PEOPLE
        -   SCANNER
        -   CMDB

    -   **<u>Action Parameter:</u> Tag Name**

          

        -   This parameter allows the user to provide the name of an existing tag or to provide the
            name of a new tag, which will get associated with the assets. Users can get the list of
            all the available tags using the List Tags action.

    -   **<u>Action Parameter:</u> Asset Type**

          

        -   Type of the asset to which the tag will be applied. Example: host, hostFinding,
            application, applicationFinding.

    -   **<u>Action Parameter:</u> Field Name**

          

        -   This parameter allows the user to filter the result data set based on the asset type’s
            attributes provided as input. It allows the comma-separated values of the attributes.
            The user can get the list of valid asset types’ attributes by executing the List Filter
            Attributes action. The uid of the filter attribute must be provided here.  
            Here are a few examples: name, title, severity, rs3, riskRating, group_names,
            description, criticality, assessment_labels, discovered_on.

    -   **<u>Action Parameter:</u> Operator**

          

        -   This parameter allows the user to provide the operator which will be applied to the
            value(s) provided in the Fieldname parameter. It allows the comma-separated values of
            valid operators. The user can get the list of valid operators by executing the List
            Filter Attributes action.  
            Here are a few examples of the operators:  
            -   **EXACT -** Filter records exactly matching the criteria.
            -   **IN -** Filter records matching any one of the comma-separated values.
            -   **LIKE -** Filter the records with fieldname’s value having the string provided by
                the user.
            -   **RANGE -** Filter the records with fieldname’s value falling in the numerical/date
                range provided.

    -   **<u>Action Parameter:</u> Value**

          

        -   This parameter allows the user to provide the value of the asset type’s attributes,
            which are mentioned in the Fieldname parameter, to be considered for filter criteria. It
            expects a JSON formatted list of values.

    -   **<u>Action Parameter:</u> Exclusivity**

          

        -   This parameter allows the user to determine whether to fetch the results that are
            matching the filter criteria (defined by the Fieldname, Operator, and Value parameter)
            or to fetch the results that are not matching the filter criteria. It allows the
            comma-separated boolean values (true/false).

    -   **<u>Action Parameter:</u> Create New Tag**

          

        -   This parameter allows the user to create a new tag if the provided tag name in the Tag
            Name parameter is not available on the RiskSense platform.
        -   **Note -** This parameter will only come into picture when the provided tag name is not
            available.

    -   **<u>Action Parameter:</u> Tag Type**

          

        -   Type of the new tag. This parameter is used to create a new tag.
        -   **Note -** This parameter is required when the provided tag name is not available and
            the Create New Tag parameter is enabled.

    -   **<u>Action Parameter:</u> Tag Description**

          

        -   Description of the new tag. This parameter is used to create a new tag.
        -   **Note -** This parameter is required when the provided tag name is not available and
            the Create New Tag parameter is enabled.

    -   **<u>Action Parameter:</u> Tag Owner ID**

          

        -   Owner of the new tag. This parameter is used to create a new tag. Users can get the list
            of all the available owner IDs using the List Users action.
        -   **Note -** This parameter is required when the provided tag name is not available and
            the Create New Tag parameter is enabled.

    -   **<u>Action Parameter:</u> Tag Color**

          

        -   Color of the new tag. This parameter is used to create a new tag.
        -   **Note -** This parameter is required when the provided tag name is not available and
            the Create New Tag parameter is enabled.

    -   **<u>Action Parameter:</u> Propagate To All Findings**

          

        -   It denotes if an asset tag should be applied to all its findings. This parameter is used
            to create a new tag.
        -   Propagate to all findings is a special boolean. If a tag is created at asset level
            (example: host/app level) and if the use case is to propagate those tags to associated
            findings also, then this parameter should be enabled. If not, it should be disabled.
        -   **Note -** This parameter is required when the provided tag name is not available and
            the Create New Tag parameter is enabled.

    -   **Note:**

          

        -   The Fieldname, Operator, Value, and Exclusivity parameters are used to create a filter.
            So, the length of these four parameters must be the same.

    -   **Examples:**
        -   Tag all the host findings that are in the assigned state. Tag Name = “ state assigned”.
            **Note-** Assuming that the “state assigned” tag is already available and the tag ID is
            1234.
            -   Tag Name = state assigned
            -   Asset Type = hostFinding
            -   Fieldname = state
            -   Operator = EXACT
            -   Value = \[“assigned”\]
            -   Exclusivity = false
            -   Create New Tag = false
        -   Tag all the hosts having rs3 value in the range of 300-400 with a tag named “high risk”.
            If tag is not available, create new tag with Description = “high risk alert”, Tag Type=
            “CUSTOM”, Tag Color= “#648d9f”, Tag Owner ID = “321”. Also, this tag should get
            associated with all the findings of the hosts as well. **Note** - Assuming that the
            “high risk” tag is not available
            -   Tag Name = high risk
            -   Asset Type = host
            -   Fieldname = rs3
            -   Operator = RANGE
            -   Value = \[“300,400”\]
            -   Exclusivity = false
            -   Create New Tag = true
            -   Tag Type = CUSTOM
            -   Tag Description = high risk alert
            -   Tag Owner ID = 321
            -   Tag Color = “#648d9f”
            -   Propagate To All Findings = True
        -   Tag all the applications with the tag name “test tag”. **Note-** Assuming that the “test
            tag” tag is already available and the tag ID is 1233.
            -   Tag Name = test tag
            -   Asset Type = application
            -   Create New Tag = false

            **Note-** This will associate the tag named “test tag” to all the applications of the
            client (provided in the configuration parameter). Please make sure that you filter the
            assets correctly using the filter parameters (Fieldname, Operator, Value, Exclusivity).
        -   Tag all the applicationFindings with a tag named “tag application finding” **Note-**
            Assuming that the “tag application finding” tag is not available
            -   Tag Name = tag application finding
            -   Asset Type = applicationFinding
            -   Create New Tag = false

            **Note-** As the tag is not available and the user is not requesting for a new tag
            creation, the action will fail with a proper error message.
        -   Tag all the hosts having rs3 value in the range of 650-850 with a tag named “low risk”.
            If tag is not available, create new tag with Description = “low risk alert”, Tag Type=
            “CUSTOM”, Tag Color= “#648d9f”, Tag Owner ID = “321”. Also, this tag should get
            associated with all the findings of the hosts as well. **Note-** Assuming that the “low
            risk” tag is already available
            -   Tag Name = low risk
            -   Asset Type = host
            -   Fieldname = rs3
            -   Operator = RANGE
            -   Value = \[“650,850”\]
            -   Exclusivity = false
            -   Create New Tag = true
            -   Tag Type = CUSTOM
            -   Tag Description = low risk alert
            -   Tag Owner ID = 321
            -   Tag Color = “#648d9f”
            -   Propagate To All Findings = True

            **Note-** As the user is trying to create a tag which is already created, the tag will
            not get updated and the already existing tag will get associated with the filtered
            assets.
        -   Tag all the hosts having rs3 value in the range of 650-850 with a tag named “low risk”.
            If tag is not available, create new tag with Description = “low risk alert”, Tag Type=
            “CUSTOM”, Tag Color= “#648d9f”, Tag Owner ID = “321”. Also, this tag should get
            associated with all the findings of the hosts as well. **Note-** Assuming that the “low
            risk” tag does not exist and there is no asset available for the provided filter related
            input parameter (Fieldname, Operator, Exclusivity, Value).
            -   Tag Name = low risk
            -   Asset Type = host
            -   Fieldname = rs3
            -   Operator = RANGE
            -   Value = \[“650,850”\]
            -   Exclusivity = false
            -   Create New Tag = true
            -   Tag Type = CUSTOM
            -   Tag Description = low risk alert
            -   Tag Owner ID = 321
            -   Tag Color = “#648d9f”
            -   Propagate To All Findings = True

            **Note-** The new tag will not be created and won't be associated as no data is
            available for the provided filter inputs. The action will return an appropriate error
            message.


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a RiskSense Platform asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base\_url** |  required  | string | Base URL \(Example\: https\://platform\.risksense\.com/api/v1\)
**verify\_server\_cert** |  optional  | boolean | Verify server certificate
**client\_name** |  required  | string | Client name
**api\_key** |  required  | password | API token
**number\_of\_retries** |  optional  | numeric | Maximum number of retries to attempt
**backoff\_factor** |  optional  | string | Backoff factor \(type\: float\)

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[list users](#action-list-users) - List all the users  
[list tags](#action-list-tags) - List all the tags  
[list hosts](#action-list-hosts) - List all the hosts  
[list apps](#action-list-apps) - List all the applications  
[list unique findings](#action-list-unique-findings) - List all the unique findings  
[list host findings](#action-list-host-findings) - List all the host findings  
[list filter attributes](#action-list-filter-attributes) - List all the filter attributes of a given asset type  
[get hosts](#action-get-hosts) - Fetch the details for the host\(s\) for the given host name or host ID  
[get host finding](#action-get-host-finding) - Fetch the details for the single host finding for the given host finding ID  
[get app](#action-get-app) - Fetch the details for the single app for the given app ID  
[list vulnerabilities](#action-list-vulnerabilities) - List all the vulnerabilities  
[tag asset](#action-tag-asset) - Tag the assets that are fetched using the filter  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'list users'
List all the users

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**max\_results** |  optional  | Maximum number of users to return \(Default\: 1000\) | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.max\_results | numeric | 
action\_result\.data\.\*\.error\_users\.\*\.cause | string | 
action\_result\.data\.\*\.error\_users\.\*\.code | numeric | 
action\_result\.data\.\*\.error\_users\.\*\.errorRefId | string | 
action\_result\.data\.\*\.error\_users\.\*\.id | string |  `risksense owner id` 
action\_result\.data\.\*\.users\.\*\.attribute1value | string | 
action\_result\.data\.\*\.users\.\*\.attribute2value | string | 
action\_result\.data\.\*\.users\.\*\.authority | string | 
action\_result\.data\.\*\.users\.\*\.clientId | numeric | 
action\_result\.data\.\*\.users\.\*\.clientRoles\.\*\.clientId | numeric | 
action\_result\.data\.\*\.users\.\*\.clientRoles\.\*\.expiresOn | string | 
action\_result\.data\.\*\.users\.\*\.clientRoles\.\*\.label | string | 
action\_result\.data\.\*\.users\.\*\.clientRoles\.\*\.roleId | string | 
action\_result\.data\.\*\.users\.\*\.email | string |  `email` 
action\_result\.data\.\*\.users\.\*\.expirationDate | string | 
action\_result\.data\.\*\.users\.\*\.firstName | string | 
action\_result\.data\.\*\.users\.\*\.id | numeric |  `risksense owner id` 
action\_result\.data\.\*\.users\.\*\.lastLogin | string | 
action\_result\.data\.\*\.users\.\*\.lastLoginIp | string |  `ip` 
action\_result\.data\.\*\.users\.\*\.lastName | string | 
action\_result\.data\.\*\.users\.\*\.multiClientUser | boolean | 
action\_result\.data\.\*\.users\.\*\.phoneNumber | string | 
action\_result\.data\.\*\.users\.\*\.readOnly | boolean | 
action\_result\.data\.\*\.users\.\*\.samlEnabled | boolean | 
action\_result\.data\.\*\.users\.\*\.username | string |  `user name` 
action\_result\.data\.\*\.users\.\*\.uuid | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_error\_users | numeric | 
action\_result\.summary\.number\_of\_users | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list tags'
List all the tags

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**max\_results** |  optional  | Maximum number of tags to return \(Default\: 1000\) | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.max\_results | numeric | 
action\_result\.data\.\*\.error\_tags\.\*\.cause | string | 
action\_result\.data\.\*\.error\_tags\.\*\.code | numeric | 
action\_result\.data\.\*\.error\_tags\.\*\.errorRefId | string | 
action\_result\.data\.\*\.error\_tags\.\*\.id | string | 
action\_result\.data\.\*\.tags\.\*\.color | string |  `risksense tag color` 
action\_result\.data\.\*\.tags\.\*\.created | string | 
action\_result\.data\.\*\.tags\.\*\.daysRemaining | numeric | 
action\_result\.data\.\*\.tags\.\*\.description | string | 
action\_result\.data\.\*\.tags\.\*\.dueDate | string | 
action\_result\.data\.\*\.tags\.\*\.id | numeric | 
action\_result\.data\.\*\.tags\.\*\.locked | boolean | 
action\_result\.data\.\*\.tags\.\*\.name | string |  `risksense tag name` 
action\_result\.data\.\*\.tags\.\*\.openFindingCount | numeric | 
action\_result\.data\.\*\.tags\.\*\.owner | string | 
action\_result\.data\.\*\.tags\.\*\.percentageComplete | numeric | 
action\_result\.data\.\*\.tags\.\*\.priority | numeric | 
action\_result\.data\.\*\.tags\.\*\.readOnly | boolean | 
action\_result\.data\.\*\.tags\.\*\.startDate | string | 
action\_result\.data\.\*\.tags\.\*\.totalFindingCount | numeric | 
action\_result\.data\.\*\.tags\.\*\.type | string | 
action\_result\.data\.\*\.tags\.\*\.updated | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_error\_tags | numeric | 
action\_result\.summary\.number\_of\_tags | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list hosts'
List all the hosts

Type: **investigate**  
Read only: **True**

<ul><li>The <b>fieldname</b>, <b>operator</b>, <b>value</b>, and <b>exclusivity</b> parameters are used to create a filter\. So, the length of these four parameters must be the same\.</li><li>Similarly, a sorting direction is required for a host attribute that is used for sorting\. So, the length of <b>sort\_by</b> and <b>sort\_direction</b> parameters must be the same\.</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**fieldname** |  optional  | Host attributes to filter the results \(allows comma\-separated\) | string | 
**operator** |  optional  | Operators to be applied on the provided fieldnames \(allows comma\-separated\) | string | 
**value** |  optional  | Values for the respective fieldnames \(allows JSON formatted list\) | string | 
**exclusivity** |  optional  | This parameter allows the user to determine whether to fetch the results that are matching the filter criteria \(defined by the Fieldname, Operator, and Value parameter\) or to fetch the results that are not matching the filter criteria | string | 
**sort\_by** |  optional  | Host attributes to sort the results \(allows comma\-separated\) | string | 
**sort\_direction** |  optional  | Sort direction values for the respective host attributes in sort by parameter \(allows comma\-separated\) | string | 
**page** |  optional  | Index of the starting page to fetch the results \(Default\: 0\) | numeric | 
**max\_results** |  optional  | Maximum number of hosts to return \(Default\: 1000\) | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.exclusivity | string | 
action\_result\.parameter\.fieldname | string | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.parameter\.operator | string | 
action\_result\.parameter\.page | numeric | 
action\_result\.parameter\.sort\_by | string | 
action\_result\.parameter\.sort\_direction | string | 
action\_result\.parameter\.value | string | 
action\_result\.data\.\*\.error\_hosts\.\*\.cause | string | 
action\_result\.data\.\*\.error\_hosts\.\*\.code | numeric | 
action\_result\.data\.\*\.error\_hosts\.\*\.errorRefId | string | 
action\_result\.data\.\*\.error\_hosts\.\*\.id | string |  `risksense host id` 
action\_result\.data\.\*\.hosts\.\*\.clientId | numeric | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.key | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.label | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.key | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.label | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.nestedFields\.\*\.key | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.nestedFields\.\*\.label | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.nestedFields\.\*\.order | numeric | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.nestedFields\.\*\.value | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.order | numeric | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.value | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.order | numeric | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.value | string | 
action\_result\.data\.\*\.hosts\.\*\.criticality | numeric | 
action\_result\.data\.\*\.hosts\.\*\.discoveredByRS | boolean | 
action\_result\.data\.\*\.hosts\.\*\.discoveredOn | string | 
action\_result\.data\.\*\.hosts\.\*\.external | boolean | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.critical\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.critical\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.critical\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.high\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.high\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.high\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.info\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.info\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.info\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.low\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.low\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.low\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.medium\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.medium\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.medium\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.total\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.total\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.total\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.critical\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.critical\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.critical\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.high\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.high\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.high\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.info\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.info\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.info\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.low\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.low\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.low\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.medium\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.medium\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.medium\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.total\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.total\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.total\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.group\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.hosts\.\*\.group\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.group\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.groups\.\*\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.hosts\.\*\.groups\.\*\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.groups\.\*\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.hostName | string |  `risksense host name`  `host name` 
action\_result\.data\.\*\.hosts\.\*\.id | numeric |  `risksense host id` 
action\_result\.data\.\*\.hosts\.\*\.ipAddress | string |  `ip` 
action\_result\.data\.\*\.hosts\.\*\.isp | string | 
action\_result\.data\.\*\.hosts\.\*\.lastFoundOn | string | 
action\_result\.data\.\*\.hosts\.\*\.lastScanTime | string | 
action\_result\.data\.\*\.hosts\.\*\.lastThreatTrendingOn | string | 
action\_result\.data\.\*\.hosts\.\*\.lastVulnTrendingOn | string | 
action\_result\.data\.\*\.hosts\.\*\.network\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.network\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.network\.type | string | 
action\_result\.data\.\*\.hosts\.\*\.notes\.\*\.date | string | 
action\_result\.data\.\*\.hosts\.\*\.notes\.\*\.note | string | 
action\_result\.data\.\*\.hosts\.\*\.notes\.\*\.user\.id | numeric |  `risksense owner id` 
action\_result\.data\.\*\.hosts\.\*\.notes\.\*\.user\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.oldestOpenFindingWithThreatDiscoveredOn | string | 
action\_result\.data\.\*\.hosts\.\*\.openCveCount | numeric | 
action\_result\.data\.\*\.hosts\.\*\.openRansomwareCount | numeric | 
action\_result\.data\.\*\.hosts\.\*\.openRceAndPeCount | numeric | 
action\_result\.data\.\*\.hosts\.\*\.openThreatCount | numeric | 
action\_result\.data\.\*\.hosts\.\*\.operatingSystemScanner\.class | string | 
action\_result\.data\.\*\.hosts\.\*\.operatingSystemScanner\.family | string | 
action\_result\.data\.\*\.hosts\.\*\.operatingSystemScanner\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.operatingSystemScanner\.vendor | string | 
action\_result\.data\.\*\.hosts\.\*\.ports\.\*\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.ports\.\*\.number | numeric | 
action\_result\.data\.\*\.hosts\.\*\.rs3 | numeric | 
action\_result\.data\.\*\.hosts\.\*\.sources\.\*\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.sources\.\*\.scannerType | string | 
action\_result\.data\.\*\.hosts\.\*\.sources\.\*\.uuid | string | 
action\_result\.data\.\*\.hosts\.\*\.srsLastScanTime | string | 
action\_result\.data\.\*\.hosts\.\*\.tagIds | numeric | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.category | string | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.color | string |  `risksense tag color` 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.created | string | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.description | string | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.name | string |  `risksense tag name` 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.updated | string | 
action\_result\.data\.\*\.hosts\.\*\.tickets\.\*\.connectorName | string | 
action\_result\.data\.\*\.hosts\.\*\.tickets\.\*\.deepLink | string | 
action\_result\.data\.\*\.hosts\.\*\.tickets\.\*\.detailedStatus | string | 
action\_result\.data\.\*\.hosts\.\*\.tickets\.\*\.ticketNumber | string | 
action\_result\.data\.\*\.hosts\.\*\.tickets\.\*\.ticketStatus | string | 
action\_result\.data\.\*\.hosts\.\*\.tickets\.\*\.type | string | 
action\_result\.data\.\*\.hosts\.\*\.trending | boolean | 
action\_result\.data\.\*\.hosts\.\*\.xRS3 | string | 
action\_result\.data\.\*\.hosts\.\*\.xRS3date | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_error\_hosts | numeric | 
action\_result\.summary\.number\_of\_hosts | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list apps'
List all the applications

Type: **investigate**  
Read only: **True**

<ul><li>The <b>fieldname</b>, <b>operator</b>, <b>value</b>, and <b>exclusivity</b> parameters are used to create a filter\. So, the length of these four parameters must be the same\.</li><li>Similarly, a sorting direction is required for an application attribute which is used for sorting\. So, the length of <b>sort\_by</b> and <b>sort\_direction</b> parameters must be the same\.</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**fieldname** |  optional  | App attributes to filter the results \(allows comma\-separated\) | string | 
**operator** |  optional  | Operators to be applied on the provided fieldnames \(allows comma\-separated\) | string | 
**value** |  optional  | Values for the respective fieldnames \(allows JSON formatted list\) | string | 
**exclusivity** |  optional  | This parameter allows the user to determine whether to fetch the results that are matching the filter criteria \(defined by the Fieldname, Operator, and Value parameter\) or to fetch the results that are not matching the filter criteria | string | 
**sort\_by** |  optional  | App attributes to sort the results \(allows comma\-separated\) | string | 
**sort\_direction** |  optional  | Sort direction values for the respective app attributes in sort by parameter \(allows comma\-separated\) | string | 
**page** |  optional  | Index of the starting page to fetch the results \(Default\: 0\) | numeric | 
**max\_results** |  optional  | Maximum number of apps to return \(Default\: 1000\) | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.exclusivity | string | 
action\_result\.parameter\.fieldname | string | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.parameter\.operator | string | 
action\_result\.parameter\.page | numeric | 
action\_result\.parameter\.sort\_by | string | 
action\_result\.parameter\.sort\_direction | string | 
action\_result\.parameter\.value | string | 
action\_result\.data\.\*\.applications\.\*\.clientId | numeric | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.ferpaComplianceAsset | boolean | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.hipaaComplianceAsset | boolean | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.lastScanDate | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.location | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.macAddress | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.managedBy | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.manufacturedBy | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.model | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.operatingSystem | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.ownedBy | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.pciComplianceAsset | boolean | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.supportGroup | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.supportedBy | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.sysId | string | 
action\_result\.data\.\*\.applications\.\*\.description | string | 
action\_result\.data\.\*\.applications\.\*\.discoveredOn | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.critical\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.critical\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.critical\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.high\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.high\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.high\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.info\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.info\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.info\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.low\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.low\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.low\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.medium\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.medium\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.medium\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.total\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.total\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.total\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.critical\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.critical\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.critical\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.high\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.high\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.high\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.info\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.info\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.info\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.low\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.low\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.low\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.medium\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.medium\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.medium\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.total\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.total\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.total\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.group\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.applications\.\*\.group\.id | numeric | 
action\_result\.data\.\*\.applications\.\*\.group\.name | string | 
action\_result\.data\.\*\.applications\.\*\.groups\.\*\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.applications\.\*\.groups\.\*\.id | numeric | 
action\_result\.data\.\*\.applications\.\*\.groups\.\*\.name | string | 
action\_result\.data\.\*\.applications\.\*\.hostId | string | 
action\_result\.data\.\*\.applications\.\*\.icons\.\*\.overlayText | string | 
action\_result\.data\.\*\.applications\.\*\.icons\.\*\.type | string | 
action\_result\.data\.\*\.applications\.\*\.id | numeric |  `risksense app id` 
action\_result\.data\.\*\.applications\.\*\.lastFoundOn | string | 
action\_result\.data\.\*\.applications\.\*\.name | string | 
action\_result\.data\.\*\.applications\.\*\.network\.id | numeric | 
action\_result\.data\.\*\.applications\.\*\.network\.name | string | 
action\_result\.data\.\*\.applications\.\*\.network\.type | string | 
action\_result\.data\.\*\.applications\.\*\.notes\.\*\.date | string | 
action\_result\.data\.\*\.applications\.\*\.notes\.\*\.note | string | 
action\_result\.data\.\*\.applications\.\*\.notes\.\*\.user\.id | numeric |  `risksense owner id` 
action\_result\.data\.\*\.applications\.\*\.notes\.\*\.user\.name | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.acronym | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.businessRisk | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.customLabel | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.cwe | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.dateAdded | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.description | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.filterUrl | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.findingCount | numeric | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.label | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.remediation | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.solution | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.title | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.urlCount | numeric | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.volume | numeric | 
action\_result\.data\.\*\.applications\.\*\.sources\.\*\.name | string | 
action\_result\.data\.\*\.applications\.\*\.sources\.\*\.scannerType | string | 
action\_result\.data\.\*\.applications\.\*\.sources\.\*\.uuid | string | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.category | string | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.color | string |  `risksense tag color` 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.created | string | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.description | string | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.id | numeric | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.name | string |  `risksense tag name` 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.updated | string | 
action\_result\.data\.\*\.applications\.\*\.uri | string |  `url` 
action\_result\.data\.\*\.applications\.\*\.urlCount | numeric | 
action\_result\.data\.\*\.applications\.\*\.wascs\.\*\.dateAdded | string | 
action\_result\.data\.\*\.applications\.\*\.wascs\.\*\.id | string | 
action\_result\.data\.\*\.applications\.\*\.wascs\.\*\.title | string | 
action\_result\.data\.\*\.error\_applications\.\*\.cause | string | 
action\_result\.data\.\*\.error\_applications\.\*\.code | numeric | 
action\_result\.data\.\*\.error\_applications\.\*\.errorRefId | string | 
action\_result\.data\.\*\.error\_applications\.\*\.id | string |  `risksense app id` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_applications | numeric | 
action\_result\.summary\.number\_of\_error\_applications | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list unique findings'
List all the unique findings

Type: **investigate**  
Read only: **True**

<ul><li>The <b>fieldname</b>, <b>operator</b>, <b>value</b>, and <b>exclusivity</b> parameters are used to create a filter\. So, the length of these four parameters must be the same\.</li><li>Similarly, a sorting direction is required for an unique host finding attribute which is used for sorting\. So, the length of <b>sort\_by</b> and <b>sort\_direction</b> parameters must be the same\.</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**fieldname** |  optional  | Unique host finding attributes to filter the results \(allows comma\-separated\) | string | 
**operator** |  optional  | Operators to be applied on the provided fieldnames \(allows comma\-separated\) | string | 
**value** |  optional  | Values for the respective fieldnames \(allows JSON formatted list\) | string | 
**exclusivity** |  optional  | This parameter allows the user to determine whether to fetch the results that are matching the filter criteria \(defined by the Fieldname, Operator, and Value parameter\) or to fetch the results that are not matching the filter criteria | string | 
**sort\_by** |  optional  | Unique host finding attributes to sort the results \(allows comma\-separated\) | string | 
**sort\_direction** |  optional  | Sort direction values for the respective unique host finding attributes in sort by parameter \(allows comma\-separated\) | string | 
**page** |  optional  | Index of the starting page to fetch the results \(Default\: 0\) | numeric | 
**max\_results** |  optional  | Maximum number of unique findings to return \(Default\: 1000\) | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.exclusivity | string | 
action\_result\.parameter\.fieldname | string | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.parameter\.operator | string | 
action\_result\.parameter\.page | numeric | 
action\_result\.parameter\.sort\_by | string | 
action\_result\.parameter\.sort\_direction | string | 
action\_result\.parameter\.value | string | 
action\_result\.data\.\*\.unique\_host\_findings\.\*\.hostCount | numeric | 
action\_result\.data\.\*\.unique\_host\_findings\.\*\.severity | numeric | 
action\_result\.data\.\*\.unique\_host\_findings\.\*\.source | string | 
action\_result\.data\.\*\.unique\_host\_findings\.\*\.sourceId | string | 
action\_result\.data\.\*\.unique\_host\_findings\.\*\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_error\_unique\_host\_findings | numeric | 
action\_result\.summary\.number\_of\_unique\_host\_findings | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list host findings'
List all the host findings

Type: **investigate**  
Read only: **True**

<ul><li>The <b>fieldname</b>, <b>operator</b>, <b>value</b>, and <b>exclusivity</b> parameters are used to create a filter\. So, the length of these four parameters must be the same\.</li><li>Similarly, a sorting direction is required for a host finding attribute which is used for sorting\. So, the length of <b>sort\_by</b> and <b>sort\_direction</b> parameters must be the same\.</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**fieldname** |  optional  | Host finding attributes to filter the results \(allows comma\-separated\) | string | 
**operator** |  optional  | Operators to be applied on the provided fieldnames \(allows comma\-separated\) | string | 
**value** |  optional  | Values for the respective fieldnames \(allows JSON formatted list\) | string | 
**exclusivity** |  optional  | This parameter allows the user to determine whether to fetch the results that are matching the filter criteria \(defined by the Fieldname, Operator, and Value parameter\) or to fetch the results that are not matching the filter criteria | string | 
**sort\_by** |  optional  | Host finding attributes to sort the results \(allows comma\-separated\) | string | 
**sort\_direction** |  optional  | Sort direction values for the respective host finding attributes in sort by parameter \(allows comma\-separated\) | string | 
**status** |  optional  | Status of the host findings\. Valid values\: Open/Closed | string | 
**page** |  optional  | Index of the starting page to fetch the results \(Default\: 0\) | numeric | 
**max\_results** |  optional  | Maximum number of host findings to return \(Default\: 1000\) | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.exclusivity | string | 
action\_result\.parameter\.fieldname | string | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.parameter\.operator | string | 
action\_result\.parameter\.page | numeric | 
action\_result\.parameter\.sort\_by | string | 
action\_result\.parameter\.sort\_direction | string | 
action\_result\.parameter\.status | string | 
action\_result\.parameter\.value | string | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.cause | string | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.code | numeric | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.errorRefId | string | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.id | string |  `risksense host finding id` 
action\_result\.data\.\*\.host\_findings\.\*\.additionalInfo | string | 
action\_result\.data\.\*\.host\_findings\.\*\.additionalInfo\.additional\_info | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assessments\.\*\.date | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assessments\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.assessments\.\*\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.email | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.firstName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.lastName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.receiveEmails | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.username | string | 
action\_result\.data\.\*\.host\_findings\.\*\.authScanDetail | string | 
action\_result\.data\.\*\.host\_findings\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.detailedDescription | string | 
action\_result\.data\.\*\.host\_findings\.\*\.detailedSolution | string | 
action\_result\.data\.\*\.host\_findings\.\*\.discoveredOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.dns | string | 
action\_result\.data\.\*\.host\_findings\.\*\.findingType | string | 
action\_result\.data\.\*\.host\_findings\.\*\.group\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.group\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.group\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.groups\.\*\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.groups\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.groups\.\*\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.criticality | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.external | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.hostId | numeric |  `risksense host id` 
action\_result\.data\.\*\.host\_findings\.\*\.host\.hostName | string |  `risksense host name`  `host name` 
action\_result\.data\.\*\.host\_findings\.\*\.host\.ipAddress | string |  `ip` 
action\_result\.data\.\*\.host\_findings\.\*\.host\.lastScannedTime | string | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.ports\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.ports\.\*\.number | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.rs3 | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.id | numeric |  `risksense host finding id` 
action\_result\.data\.\*\.host\_findings\.\*\.lastFoundOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.machineId | string | 
action\_result\.data\.\*\.host\_findings\.\*\.manualFindingReports\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.manualFindingReports\.\*\.easeOfExploit | string | 
action\_result\.data\.\*\.host\_findings\.\*\.manualFindingReports\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.manualFindingReports\.\*\.isManualExploit | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.manualFindingReports\.\*\.label | string | 
action\_result\.data\.\*\.host\_findings\.\*\.manualFindingReports\.\*\.pii | string | 
action\_result\.data\.\*\.host\_findings\.\*\.manualFindingReports\.\*\.source | string | 
action\_result\.data\.\*\.host\_findings\.\*\.manualFindingReports\.\*\.title | string | 
action\_result\.data\.\*\.host\_findings\.\*\.netbios | string | 
action\_result\.data\.\*\.host\_findings\.\*\.network\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.network\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.network\.type | string | 
action\_result\.data\.\*\.host\_findings\.\*\.notes\.\*\.date | string | 
action\_result\.data\.\*\.host\_findings\.\*\.notes\.\*\.note | string | 
action\_result\.data\.\*\.host\_findings\.\*\.notes\.\*\.user\.id | numeric |  `risksense owner id` 
action\_result\.data\.\*\.host\_findings\.\*\.notes\.\*\.user\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.output | string | 
action\_result\.data\.\*\.host\_findings\.\*\.patches\.\*\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.patches\.\*\.url | string |  `url` 
action\_result\.data\.\*\.host\_findings\.\*\.port | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.resolvedOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.riskRating | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerPluginStatus | string | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerReferences\.\*\.refType | string | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerReferences\.\*\.referencesInfo\.\*\.referenceId | string | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerReferences\.\*\.referencesInfo\.\*\.url | string |  `url` 
action\_result\.data\.\*\.host\_findings\.\*\.severity | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.aggregated | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.combined | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.cvssV2 | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.cvssV3 | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.expirationDate | string | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.overridden | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.scanner | string | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.state | string | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.stateName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.solution | string | 
action\_result\.data\.\*\.host\_findings\.\*\.source | string | 
action\_result\.data\.\*\.host\_findings\.\*\.sourceId | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.dueDate | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.durationInDays | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.expirationDate | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.state | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.stateDescription | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.stateName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.status | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.category | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.color | string |  `risksense tag color` 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.created | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.name | string |  `risksense tag name` 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.updated | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.category | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.color | string |  `risksense tag color` 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.created | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.name | string |  `risksense tag name` 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.updated | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.manualExploits\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.manualExploits\.\*\.easeOfExploit | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.manualExploits\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.manualExploits\.\*\.isManualExploit | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.manualExploits\.\*\.label | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.manualExploits\.\*\.pii | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.manualExploits\.\*\.source | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.manualExploits\.\*\.title | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threatLastTrendingOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.category | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.cves | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.details | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.link | string |  `url` 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.published | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.severity | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.source | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.threatLastTrendingOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.title | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.trending | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.updated | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.trending | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.tickets\.\*\.connectorName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tickets\.\*\.deepLink | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tickets\.\*\.detailedStatus | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tickets\.\*\.ticketNumber | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tickets\.\*\.ticketStatus | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tickets\.\*\.type | string | 
action\_result\.data\.\*\.host\_findings\.\*\.title | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.trending | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.accessComplexity | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.attackVector | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.authentication | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.availabilityImpact | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.baseScore | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.confidentialityImpact | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.cve | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.integrity | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.summary | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.threatCount | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.trending | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.vulnLastTrendingOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnLastTrendingOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.attackComplexity | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.attackVector | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.availabilityImpact | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.baseScore | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.confidentialityImpact | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.cve | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.integrityImpact | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.nvdVersion | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.privilegesRequired | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.scope | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.summary | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.threatCount | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilitiesWithV3\.\*\.userInteraction | string | 
action\_result\.data\.\*\.host\_findings\.\*\.xrs3Impact | string | 
action\_result\.data\.\*\.host\_findings\.\*\.xrs3ImpactOnCategory | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_error\_host\_findings | numeric | 
action\_result\.summary\.number\_of\_host\_findings | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list filter attributes'
List all the filter attributes of a given asset type

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**asset\_type** |  required  | Type of the asset of which the filter attributes will be fetched\. Example\: host, hostFinding, application, applicationFinding | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.asset\_type | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.legacyUid | string | 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.operators | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.uid | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.asset\_filter\_attributes | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get hosts'
Fetch the details for the host\(s\) for the given host name or host ID

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**host\_id** |  optional  | The host ID of the host to be fetched | numeric |  `risksense host id` 
**host\_name** |  optional  | The host name of the host to be fetched | string |  `risksense host name` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.host\_id | numeric |  `risksense host id` 
action\_result\.parameter\.host\_name | string |  `risksense host name` 
action\_result\.data\.\*\.error\_hosts\.\*\.cause | string | 
action\_result\.data\.\*\.error\_hosts\.\*\.code | numeric | 
action\_result\.data\.\*\.error\_hosts\.\*\.errorRefId | string | 
action\_result\.data\.\*\.error\_hosts\.\*\.id | string |  `risksense host id` 
action\_result\.data\.\*\.hosts\.\*\.clientId | numeric | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.key | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.label | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.key | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.label | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.nestedFields\.\*\.key | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.nestedFields\.\*\.label | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.nestedFields\.\*\.order | numeric | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.nestedFields\.\*\.value | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.order | numeric | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.nestedFields\.\*\.value | string | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.order | numeric | 
action\_result\.data\.\*\.hosts\.\*\.configurationManagementDB\.\*\.value | string | 
action\_result\.data\.\*\.hosts\.\*\.criticality | numeric | 
action\_result\.data\.\*\.hosts\.\*\.discoveredByRS | boolean | 
action\_result\.data\.\*\.hosts\.\*\.discoveredOn | string | 
action\_result\.data\.\*\.hosts\.\*\.external | boolean | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.critical\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.critical\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.critical\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.high\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.high\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.high\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.info\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.info\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.info\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.low\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.low\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.low\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.medium\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.medium\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.medium\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.total\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.total\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsByVrrDistribution\.total\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.critical\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.critical\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.critical\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.high\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.high\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.high\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.info\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.info\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.info\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.low\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.low\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.low\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.medium\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.medium\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.medium\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.total\.filter | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.total\.subject | string | 
action\_result\.data\.\*\.hosts\.\*\.findingsDistribution\.total\.value | numeric | 
action\_result\.data\.\*\.hosts\.\*\.group\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.hosts\.\*\.group\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.group\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.groups\.\*\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.hosts\.\*\.groups\.\*\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.groups\.\*\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.hostName | string |  `risksense host name`  `host name` 
action\_result\.data\.\*\.hosts\.\*\.id | numeric |  `risksense host id` 
action\_result\.data\.\*\.hosts\.\*\.ipAddress | string |  `ip` 
action\_result\.data\.\*\.hosts\.\*\.isp | string | 
action\_result\.data\.\*\.hosts\.\*\.lastFoundOn | string | 
action\_result\.data\.\*\.hosts\.\*\.lastScanTime | string | 
action\_result\.data\.\*\.hosts\.\*\.lastThreatTrendingOn | string | 
action\_result\.data\.\*\.hosts\.\*\.lastVulnTrendingOn | string | 
action\_result\.data\.\*\.hosts\.\*\.network\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.network\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.network\.type | string | 
action\_result\.data\.\*\.hosts\.\*\.oldestOpenFindingWithThreatDiscoveredOn | string | 
action\_result\.data\.\*\.hosts\.\*\.openCveCount | numeric | 
action\_result\.data\.\*\.hosts\.\*\.openRansomwareCount | numeric | 
action\_result\.data\.\*\.hosts\.\*\.openRceAndPeCount | numeric | 
action\_result\.data\.\*\.hosts\.\*\.openThreatCount | numeric | 
action\_result\.data\.\*\.hosts\.\*\.operatingSystemScanner\.class | string | 
action\_result\.data\.\*\.hosts\.\*\.operatingSystemScanner\.family | string | 
action\_result\.data\.\*\.hosts\.\*\.operatingSystemScanner\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.operatingSystemScanner\.vendor | string | 
action\_result\.data\.\*\.hosts\.\*\.ports\.\*\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.ports\.\*\.number | numeric | 
action\_result\.data\.\*\.hosts\.\*\.rs3 | numeric | 
action\_result\.data\.\*\.hosts\.\*\.services | string | 
action\_result\.data\.\*\.hosts\.\*\.sources\.\*\.name | string | 
action\_result\.data\.\*\.hosts\.\*\.sources\.\*\.scannerType | string | 
action\_result\.data\.\*\.hosts\.\*\.sources\.\*\.uuid | string | 
action\_result\.data\.\*\.hosts\.\*\.srsLastScanTime | string | 
action\_result\.data\.\*\.hosts\.\*\.tagIds | numeric | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.category | string | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.color | string |  `risksense tag color` 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.created | string | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.description | string | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.id | numeric | 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.name | string |  `risksense tag name` 
action\_result\.data\.\*\.hosts\.\*\.tags\.\*\.updated | string | 
action\_result\.data\.\*\.hosts\.\*\.trending | boolean | 
action\_result\.data\.\*\.hosts\.\*\.xRS3 | string | 
action\_result\.data\.\*\.hosts\.\*\.xRS3date | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_error\_hosts | numeric | 
action\_result\.summary\.number\_of\_hosts | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get host finding'
Fetch the details for the single host finding for the given host finding ID

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**host\_finding\_id** |  required  | The host finding ID of the host finding to be fetched | numeric |  `risksense host finding id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.host\_finding\_id | numeric |  `risksense host finding id` 
action\_result\.data\.\*\.error\_host\_findings\.\*\.cause | string | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.code | numeric | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.errorRefId | string | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.id | string |  `risksense host finding id` 
action\_result\.data\.\*\.host\_findings\.\*\.additionalInfo | string | 
action\_result\.data\.\*\.host\_findings\.\*\.additionalInfo\.additional\_info | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assessments\.\*\.date | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assessments\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.assessments\.\*\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.email | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.firstName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.lastName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.receiveEmails | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.assignments\.\*\.username | string | 
action\_result\.data\.\*\.host\_findings\.\*\.authScanDetail | string | 
action\_result\.data\.\*\.host\_findings\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.detailedDescription | string | 
action\_result\.data\.\*\.host\_findings\.\*\.detailedSolution | string | 
action\_result\.data\.\*\.host\_findings\.\*\.discoveredOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.dns | string | 
action\_result\.data\.\*\.host\_findings\.\*\.findingType | string | 
action\_result\.data\.\*\.host\_findings\.\*\.group\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.group\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.group\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.groups\.\*\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.groups\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.groups\.\*\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.criticality | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.external | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.hostId | numeric |  `risksense host id` 
action\_result\.data\.\*\.host\_findings\.\*\.host\.hostName | string |  `risksense host name`  `host name` 
action\_result\.data\.\*\.host\_findings\.\*\.host\.ipAddress | string |  `ip` 
action\_result\.data\.\*\.host\_findings\.\*\.host\.lastScannedTime | string | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.ports\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.ports\.\*\.number | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.host\.rs3 | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.id | numeric |  `risksense host finding id` 
action\_result\.data\.\*\.host\_findings\.\*\.lastFoundOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.machineId | string | 
action\_result\.data\.\*\.host\_findings\.\*\.netbios | string | 
action\_result\.data\.\*\.host\_findings\.\*\.network\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.network\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.network\.type | string | 
action\_result\.data\.\*\.host\_findings\.\*\.output | string | 
action\_result\.data\.\*\.host\_findings\.\*\.patches\.\*\.name | string | 
action\_result\.data\.\*\.host\_findings\.\*\.patches\.\*\.url | string |  `url` 
action\_result\.data\.\*\.host\_findings\.\*\.port | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.resolvedOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.riskRating | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerPluginStatus | string | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerReferences\.\*\.refType | string | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerReferences\.\*\.referencesInfo\.\*\.referenceId | string | 
action\_result\.data\.\*\.host\_findings\.\*\.scannerReferences\.\*\.referencesInfo\.\*\.url | string |  `url` 
action\_result\.data\.\*\.host\_findings\.\*\.severity | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.aggregated | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.combined | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.cvssV2 | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.cvssV3 | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.expirationDate | string | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.overridden | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.scanner | string | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.state | string | 
action\_result\.data\.\*\.host\_findings\.\*\.severityEmbedded\.stateName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.solution | string | 
action\_result\.data\.\*\.host\_findings\.\*\.source | string | 
action\_result\.data\.\*\.host\_findings\.\*\.sourceId | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.dueDate | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.durationInDays | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.expirationDate | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.state | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.stateDescription | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.stateName | string | 
action\_result\.data\.\*\.host\_findings\.\*\.statusEmbedded\.status | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.category | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.color | string |  `risksense tag color` 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.created | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.name | string |  `risksense tag name` 
action\_result\.data\.\*\.host\_findings\.\*\.tags\.\*\.updated | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.category | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.color | string |  `risksense tag color` 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.created | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.id | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.name | string |  `risksense tag name` 
action\_result\.data\.\*\.host\_findings\.\*\.tagsAsset\.\*\.updated | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threatLastTrendingOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.category | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.cves | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.description | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.details | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.link | string |  `url` 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.published | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.severity | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.source | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.threatLastTrendingOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.title | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.trending | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.threats\.\*\.updated | string | 
action\_result\.data\.\*\.host\_findings\.\*\.threats\.trending | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.title | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.trending | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.accessComplexity | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.attackVector | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.authentication | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.availabilityImpact | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.baseScore | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.confidentialityImpact | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.cve | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.integrity | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.summary | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.threatCount | numeric | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.trending | boolean | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnInfoList\.\*\.vulnLastTrendingOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.vulnerabilities\.vulnLastTrendingOn | string | 
action\_result\.data\.\*\.host\_findings\.\*\.xrs3Impact | string | 
action\_result\.data\.\*\.host\_findings\.\*\.xrs3ImpactOnCategory | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_error\_host\_findings | numeric | 
action\_result\.summary\.number\_of\_host\_findings | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get app'
Fetch the details for the single app for the given app ID

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**app\_id** |  required  | The app ID of the application to be fetched | numeric |  `risksense app id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.app\_id | numeric |  `risksense app id` 
action\_result\.data\.\*\.applications\.\*\.clientId | numeric | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.ferpaComplianceAsset | boolean | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.hipaaComplianceAsset | boolean | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.lastScanDate | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.location | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.macAddress | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.managedBy | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.manufacturedBy | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.model | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.operatingSystem | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.ownedBy | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.pciComplianceAsset | boolean | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.supportGroup | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.supportedBy | string | 
action\_result\.data\.\*\.applications\.\*\.configurationManagementDB\.sysId | string | 
action\_result\.data\.\*\.applications\.\*\.description | string | 
action\_result\.data\.\*\.applications\.\*\.discoveredOn | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.critical\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.critical\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.critical\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.high\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.high\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.high\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.info\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.info\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.info\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.low\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.low\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.low\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.medium\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.medium\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.medium\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.total\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.total\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsByVrrDistribution\.total\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.critical\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.critical\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.critical\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.high\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.high\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.high\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.info\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.info\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.info\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.low\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.low\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.low\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.medium\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.medium\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.medium\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.total\.filter | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.total\.subject | string | 
action\_result\.data\.\*\.applications\.\*\.findingsDistribution\.total\.value | numeric | 
action\_result\.data\.\*\.applications\.\*\.group\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.applications\.\*\.group\.id | numeric | 
action\_result\.data\.\*\.applications\.\*\.group\.name | string | 
action\_result\.data\.\*\.applications\.\*\.groups\.\*\.hasGroupPermission | boolean | 
action\_result\.data\.\*\.applications\.\*\.groups\.\*\.id | numeric | 
action\_result\.data\.\*\.applications\.\*\.groups\.\*\.name | string | 
action\_result\.data\.\*\.applications\.\*\.hostId | string | 
action\_result\.data\.\*\.applications\.\*\.icons\.\*\.overlayText | string | 
action\_result\.data\.\*\.applications\.\*\.icons\.\*\.type | string | 
action\_result\.data\.\*\.applications\.\*\.id | numeric |  `risksense app id` 
action\_result\.data\.\*\.applications\.\*\.lastFoundOn | string | 
action\_result\.data\.\*\.applications\.\*\.name | string | 
action\_result\.data\.\*\.applications\.\*\.network\.id | numeric | 
action\_result\.data\.\*\.applications\.\*\.network\.name | string | 
action\_result\.data\.\*\.applications\.\*\.network\.type | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.acronym | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.businessRisk | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.customLabel | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.cwe | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.dateAdded | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.description | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.filterUrl | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.findingCount | numeric | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.label | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.remediation | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.solution | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.title | string | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.urlCount | numeric | 
action\_result\.data\.\*\.applications\.\*\.owasps\.\*\.volume | numeric | 
action\_result\.data\.\*\.applications\.\*\.sources\.\*\.name | string | 
action\_result\.data\.\*\.applications\.\*\.sources\.\*\.scannerType | string | 
action\_result\.data\.\*\.applications\.\*\.sources\.\*\.uuid | string | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.category | string | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.color | string |  `risksense tag color` 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.created | string | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.description | string | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.id | numeric | 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.name | string |  `risksense tag name` 
action\_result\.data\.\*\.applications\.\*\.tags\.\*\.updated | string | 
action\_result\.data\.\*\.applications\.\*\.uri | string |  `url` 
action\_result\.data\.\*\.applications\.\*\.urlCount | numeric | 
action\_result\.data\.\*\.applications\.\*\.wascs\.\*\.dateAdded | string | 
action\_result\.data\.\*\.applications\.\*\.wascs\.\*\.id | string | 
action\_result\.data\.\*\.applications\.\*\.wascs\.\*\.title | string | 
action\_result\.data\.\*\.error\_applications\.\*\.code | numeric | 
action\_result\.data\.\*\.error\_applications\.\*\.errorRefId | string | 
action\_result\.data\.\*\.error\_applications\.\*\.id | string |  `risksense app id` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_applications | numeric | 
action\_result\.summary\.number\_of\_error\_applications | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list vulnerabilities'
List all the vulnerabilities

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**host\_finding\_id** |  required  | The host finding ID for which the vulnerabilities is to be fetched | numeric |  `risksense host finding id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.host\_finding\_id | numeric |  `risksense host finding id` 
action\_result\.data\.\*\.error\_host\_findings\.\*\.cause | string | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.code | numeric | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.errorRefId | string | 
action\_result\.data\.\*\.error\_host\_findings\.\*\.id | string |  `risksense host finding id` 
action\_result\.data\.\*\.vulnerability\_list\.\*\.accessComplexity | string | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.attackVector | string | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.authentication | string | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.availabilityImpact | string | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.baseScore | numeric | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.confidentialityImpact | string | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.cve | string | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.integrity | string | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.summary | string | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.threatCount | numeric | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.trending | boolean | 
action\_result\.data\.\*\.vulnerability\_list\.\*\.vulnLastTrendingOn | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.attackComplexity | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.attackVector | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.availabilityImpact | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.baseScore | numeric | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.confidentialityImpact | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.cve | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.integrityImpact | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.nvdVersion | numeric | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.privilegesRequired | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.scope | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.summary | string | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.threatCount | numeric | 
action\_result\.data\.\*\.vulnerability\_with\_v3\_list\.\*\.userInteraction | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.number\_of\_error\_host\_findings | numeric | 
action\_result\.summary\.number\_of\_v2\_vulnerabilities | numeric | 
action\_result\.summary\.number\_of\_v3\_vulnerabilities | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'tag asset'
Tag the assets that are fetched using the filter

Type: **generic**  
Read only: **False**

<ul><li>The <b>fieldname</b>, <b>operator</b>, <b>value</b>, and <b>exclusivity</b> parameters are used to create a filter\. So, the length of these four parameters must be the same\.</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**tag\_name** |  required  | Name of the tag to be associated | string |  `risksense tag name` 
**entity\_type** |  required  | Type of the asset/entity to which the tag will be applied | string | 
**fieldname** |  optional  | Attributes of the asset type to filter the results \(allows comma\-separated\) | string | 
**operator** |  optional  | Operators to be applied on the provided fieldnames \(allows comma\-separated\) | string | 
**value** |  optional  | Values for the respective fieldnames \(allows JSON formatted list\) | string | 
**exclusivity** |  optional  | This parameter allows the user to determine whether to fetch the results that are matching the filter criteria \(defined by the Fieldname, Operator, and Value parameter\) or to fetch the results that are not matching the filter criteria | string | 
**create\_new\_tag** |  optional  | Create a new tag or not if the tag does not exist | boolean | 
**tag\_type** |  optional  | Type of the new tag \(required field when Create New Tag is enabled\) | string | 
**tag\_description** |  optional  | Description of the new tag \(required field when Create New Tag is enabled\) | string | 
**tag\_owner\_id** |  optional  | Owner of the new tag \(required field when Create New Tag is enabled\) | numeric |  `risksense owner id` 
**tag\_color** |  optional  | Color of the new tag \(required field when Create New Tag is enabled\) | string |  `risksense tag color` 
**propagate\_to\_all\_findings** |  optional  | Detonates if an asset tag should be applied to all its findings \(required field when Create New Tag is enabled\) | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.entity\_type | string | 
action\_result\.parameter\.create\_new\_tag | boolean | 
action\_result\.parameter\.exclusivity | string | 
action\_result\.parameter\.fieldname | string | 
action\_result\.parameter\.operator | string | 
action\_result\.parameter\.propagate\_to\_all\_findings | boolean | 
action\_result\.parameter\.tag\_color | string |  `risksense tag color` 
action\_result\.parameter\.tag\_description | string | 
action\_result\.parameter\.tag\_name | string |  `risksense tag name` 
action\_result\.parameter\.tag\_owner\_id | numeric |  `risksense owner id` 
action\_result\.parameter\.tag\_type | string | 
action\_result\.parameter\.value | string | 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.id | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.tag\_id | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 