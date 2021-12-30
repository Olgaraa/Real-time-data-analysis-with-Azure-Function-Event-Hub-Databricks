import datetime
import logging
import requests
import azure.functions as func
import json


def main(mytimer: func.TimerRequest, outputEventhub:func.Out[str])->str:
    date = datetime.datetime.now().strftime("%d.%b %Y %H:%M:%S")
    logging.info('The trigger processed a request at %s', date)

    try:
        api= requests.get('https://ckan2.multimediagdansk.pl/gpsPositions').json()
        requests.get('https://ckan2.multimediagdansk.pl/gpsPositions').raise_for_status()

    except requests.exceptions.RequestException as err:
        print ("An error has occured",err)

    else:
        data=json.dumps(api)
        outputEventhub.set(data)
        logging.info('The request has been processed successfully.')
