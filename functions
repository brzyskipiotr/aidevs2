import requests


AI_DEVS_API_KEY = ""
URL = "https://zadania.aidevs.pl"

def print_request(url, method, headers=None, data=None):
    print(f"\nREQUEST to {url} with METHOD {method}")
    if headers:
        print(f"HEADERS: {headers}")
    if data:
        print(f"BODY: {data}")

def print_response(response):
    print(f"RESPONSE STATUS: {response.status_code}")
    print(f"BODY: {response.json()}")

def get_token(task):
    print_request(f"{URL}/token/{task}", "POST", None, {"apikey": AI_DEVS_API_KEY})
    response = requests.post(f"{URL}/token/{task}", json={"apikey": AI_DEVS_API_KEY})
    response.raise_for_status()
    print_response(response)
    return response.json()["token"]

def submit(token, answer):
    print_request(f"{URL}/answer/{token}", "POST", None, {"answer": answer})
    payload = {
        "name": "addUser",
        "description": "Adds a user with given name, surname, and year of birth to the system.",
        "parameters": {
            "type": "object",
            "properties": {
                "name": {
                    "type": "string",
                    "description": "provide the first name of the user"
                },
                "surname": {
                    "type": "string",
                    "description": "provide the surname of the user"
                },
                "year": {
                    "type": "integer",
                    "description": "provide the year of birth of the user"
                }
            }
        }
    }
    
    response = requests.post(f"{URL}/answer/{token}", json={"answer": payload})
    response.raise_for_status()
    print_response(response)
    return response.json()


def main():
    try:
        token = get_token("functions")
                
        answer = {
            "name": "addUser",
            "description": "Adds a user with given name, surname, and year of birth to the system.",
            "parameters": {
                "type": "object",
                "properties": {
                    "name": {
                        "type": "string",
                        "description": "provide the first name of the user"
                    },
                    "surname": {
                        "type": "string",
                        "description": "provide the surname of the user"
                    },
                    "year": {
                        "type": "integer",
                        "description": "provide the year of birth of the user"
                    }
                }
            }
        }
        
        
        result = submit(token, answer)
        print(result)
    except Exception as e:
        print(f"Error occurs: {e}")

if __name__ == "__main__":
    main()
