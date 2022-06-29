### Introduction 👋

I have created a Magento module for the specific task given. This module is created and works on the latest Magento version 2.4.4.
A module contains two  RESTful services (POST and GET) that store organizations with relations (parent to child relation), from the given JSON example.  

## Usage

To test this module, please install Acty_Test Module 

<b> Setup the module </b>

Run the following magento command: 
```bash
bin/magento setup:upgrade 
```
# API REQUESTS

I have used Postman to test my APIS.  

## Insert API 

Api url for insert statement

```bash
/rest/V1/acty/organizaton/insert 
```

Use given JSON to make insert

```json
{ 

    "org_name": "Paradise Island", 

    "daughters": [ 

        { 

            "org_name": "Banana tree", 

            "daughters": [ 

                { 

                    "org_name": "Yellow Banana", 

                    "daughters": [ 

                        { 

                            "org_name": "Pink Banana" 

                        } 

                    ] 

                }, 

                { 

                    "org_name": "Brown Banana" 

                }, 

                { 

                    "org_name": "Black Banana" 

                } 

            ] 

        }, 

        { 

            "org_name": "Big banana tree", 

            "daughters": [ 

                { 

                    "org_name": "Black Banana", 

                    "daughters": [ 

                        { 

                            "org_name": "Phoneutria Spider" 

                        } 

                    ] 

                }, 

                { 

                    "org_name": "Yellow Banana" 

                }, 

                { 

                    "org_name": "Brown Banana" 

                }, 

                { 

                    "org_name": "Green Banana" 

                } 

            ] 

        } 

    ] 

} 
```
Expected Result 200 response code. 

If you try to add deughter organization to be parent, sql error will be returned

Example to get error
```json
{
    "org_name": "Paradise Island",
    "daughters": [
        {
            "org_name": "Banana tree",
            "daughters": [
                {
                    "org_name": "Yellow Banana",
                    "daughters": [
                        {
                            "org_name": "Yellow Banana"
                        }
                    ]
                },
                {
                    "org_name": "Brown Banana"
                },
                {
                    "org_name": "Black Banana"
                }
            ]
        },
        {
            "org_name": "Big banana tree",
            "daughters": [
                {
                    "org_name": "Black Banana",
                    "daughters": [
                        {
                            "org_name": "Phoneutria Spider"
                        }
                    ]
                },
                {
                    "org_name": "Yellow Banana"
                },
                {
                    "org_name": "Brown Banana"
                },
                {
                    "org_name": "Green Banana"
                }
            ]
        }
    ]
}
```

```bash
SQLSTATE[42000]: Syntax error or access violation: 1172 Result consisted of more than one row
```

## Get List API 

Api url for get statement


```bash
/rest/V1/acty/organizaton/list/$organization/$page
```

Run following APi in Postman 

Example:

```bash
/rest/V1/acty/organizaton/list/Banana%20tree/page/1
```
Expected result:
 
Will get 200 response with json result.
This api will return json result with pagination  (max 100 rows per page).

If you run api with  organization name thaht not exist will get error 

```bash
"There is no results with $oganization organization name"
```

