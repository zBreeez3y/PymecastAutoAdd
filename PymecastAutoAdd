#!/usr/env/python3

import requests
import getpass
import re

accessToken = ""

def getAccessToken():
    global accessToken  
    clientID = getpass.getpass("[+] Please enter the Mimecast API 2.0 Client ID: ")
    clientSecret = getpass.getpass("[+] Please enter the Mimecast API 2.0 Client Secret: ")
    url = "https://api.services.mimecast.com/oauth/token"
    payload=f'client_id={clientID}&client_secret={clientSecret}&grant_type=client_credentials'
    headers = {
        'Content-Type': 'application/x-www-form-urlencoded'
    }
    response = requests.post(url, headers=headers, data=payload)
    if response.status_code == 200:
        regex = re.search('[a-zA-Z0-9]{28}', response.text)
        accessToken = regex.group()
        print("Access Token successfully received.")
    else:
        print(f"Error receiving Access Token: {accessToken.status_code}") 
        print("Check HTTP response codes here: https://developer.services.mimecast.com/api-overview#api-call-restrictions") 
        exit()

def AddAddress():
    while True:
        try:
            global accessToken
            groupID = ""
            if groupID == "":
                print("Provide your Mimecast Group ID on line 32...")
                exit()
            email = input("[+] Please enter the email to add (Press CTRL+C to quit): ")
            note = input("[+] Please add a note to detail the member addtion (Press CTRL+C to quit): ")
            addUrl = "https://api.services.mimecast.com/api/directory/add-group-member"
            headers = {
                "Authorization":f"Bearer {accessToken}",
                "Accept":"application/json",
                "Content-Type":"application/json"
            }
            body = {
                "data": [
                    {
                        "id":f"{groupID}",
                        "emailAddress":f"{email}",
                        "notes":f"{note}"
                    }
                ]
            }
            response = requests.post(addUrl, headers=headers, json=body)
            if response.status_code == 200:
                print("Email successfully added to profile group.")
                continue
            elif response.status_code == 401:
                renew = input("Access token has expired, would you like to renew? [Y/N]: ")
                while renew not in ["y","Y","n","N"]:
                    renew = input('Incorrect response received, please select "Y" or "N": ')
                if renew in ["y","Y"]:
                    print("Renewing Access Token...")
                    getAccessToken()
                    continue
                elif renew in ["n","N"]:
                    print("Not renewing Access Token. Exiting...")
                    exit()
            else:
                print(f"HTTP Error: {response.status_code}")
                print("Check error codes here: https://developer.services.mimecast.com/docs/userandgroupmanagement/1/routes/api/directory/add-group-member/post")
                continue
        except KeyboardInterrupt:
            print('\n' + "Exiting...")
            exit()

if __name__ == "__main__":
    if not accessToken:
        print("No Access Token found. Obtaining Access Token...")
        getAccessToken()
    AddAddress()
