# Assistants
This repository contains information about intelligent assistants available on the internet  that are compliant with Open Voice Interoperability messages.

The current list of assistants is included in the file "assistants.json". Send a pull request if you have an assistant that you'd like added to the list. 

The "assistants.json" file only includes a conversational name and a url for the assistant, so this file does not directly include information about what an assistant does. This is done indirectly by sending a query to the assistant's url.

## Finding out what an assistant does

### manifestRequest event
The standard way to find out what an assistant does is to query it for its manifest, with a "manifestRequest" event like this. 

```json
{
  "ovon": {
    "conversation": {
      "id": "convoID8403984",
      "startTime": "01-09-2025_110115"
    },
    "schema": {
      "version": "0.9.0",
      "url": "not_published_yet"
    },
    "sender": {
      "from": "SomeSender"
    },
    "events": [
      {
        "to": "https://secondAssistant.pythonAnywhere.com",
        "eventType": "requestManifest"
      }
    ]
  }
}
```

### publishManifest event
Open Voice compliant assistants are required to respond to a "manifestRequest" with their manifests in a "publishManifest" event. The manifest format is described in the AssistantManifest spec, https://github.com/open-voice-interoperability/docs/blob/main/specifications/AssistantManifest/0.9.1/AssistantManifestSpec.md

Here's an example:
```json
{
        "eventType": "publishManifest",
        "parameters": {
          "manifest": {
            "identification": {
              "serviceEndpoint": "http://secondAssistant.pythonanywhere.com",
              "organization": "Sandbox_LFAI",
              "conversationalName": "WendyWeather",
              "serviceName": "Python Anywhere",
              "role": "Basic weather assistant",
              "synopsis": "weather information"
            },
            "capabilities": [
              {
                "keyphrases": [
                  "weather",
                  "forecast"
                ],
                "languages": [
                  "en-us"
                ],
                "descriptions": [
                  "accesses weather api to get weather information",
                  "a few cities are supported, including boston and new york"
                ],
                "supportedLayers": [
                  "text"
                ]
              }
            ]
          }
        }
      }
```

### Future possibilities


Eventually there could be software that prefetches the manifests and stores them so that assistants that are looking for specific functionality can just check the stored lists of manifests. 
