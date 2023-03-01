### Register, Verify and Test

#### Register edge device with a `node policy`
```
hzn register --policy node-policy.json
```

#### Verify running service
```
docker ps
CONTAINER ID   IMAGE                                                            COMMAND                  CREATED       STATUS       PORTS                    NAMES
c973ce04d319   us.icr.io/ieam-dev/sg.edge.watson.stt.watson-stt-runtime_amd64   "/usr/local/bin/tini…"   7 hours ago   Up 7 hours   0.0.0.0:1080->1080/tcp   cf6e980a19d1602a7e6dd32c7beefdbcf9d9a1be129943a82296636538aaf6dd-sg.edge.watson.stt.watson-stt-runtime
```

#### Test
The Speech-To-Text (STT) runtime service container exposes an endpoint at port 1080. The service is preloaded with `english` and `french` STT models. Test by querying with sample a `.wav` file. Default is `english`.
For other languages, for example french, provide an additional parameter in the query as shown below.

- English
```
curl "http://localhost:1080/speech-to-text/api/v1/recognize" --header "Content-Type: audio/wav" --data-binary @single-container-stt_sample_dataset_en-quote-1.wav
```
Expected output:
```
curl "http://localhost:1080/speech-to-text/api/v1/recognize"   --header "Content-Type: audio/wav"   --data-binary @single-container-stt_sample_dataset_en-quote-1.wav
{
   "result_index": 0,
   "results": [
      {
         "final": true,
         "alternatives": [
            {
               "transcript": "the day will come when there will be no battlefields but markets opening to commerce and minds opening to ideas ",
               "confidence": 0.94
            }
         ]
      }
   ]
}
```

- French
```
curl "http://localhost:1080/speech-to-text/api/v1/recognize?model=fr-FR_Multimedia" --header "Content-Type: audio/wav" --data-binary @single-container-stt_sample_dataset_fr-quote-1.wav
```

Expected output:
```
curl "http://localhost:1080/speech-to-text/api/v1/recognize?model=fr-FR_Multimedia" --header "Content-Type: audio/wav" --data-binary @single-container-stt_sample_dataset_fr-quote-1.wav
{
   "result_index": 0,
   "results": [
      {
         "final": true,
         "alternatives": [
            {
               "transcript": "un jour viendra où il n'y aura plus d'autres champs de bataille que les marchés s'ouvrant au commerce et les esprits s'ouvrant aux idées ",
               "confidence": 0.98
            }
         ]
      }
   ]
}
```
