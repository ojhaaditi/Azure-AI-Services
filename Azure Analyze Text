#Enviroment
AI_SERVICE_ENDPOINT=YOUR_AI_SERVICES_ENDPOINT
AI_SERVICE_KEY=YOUR_AI_SERVICES_KEY

#CODE
from dotenv import load_dotenv
import os

# Import namespaces
from azure.core.credentials import AzureKeyCredential
from azure.ai.textanalytics import TextAnalyticsClient

def main():
    try:
        # Get Configuration Settings
        load_dotenv()
        ai_endpoint = os.getenv('AI_SERVICE_ENDPOINT')
        ai_key = os.getenv('AI_SERVICE_KEY')

        # Create client using endpoint and key
        credential = AzureKeyCredential(ai_key)
        ai_client = TextAnalyticsClient(endpoint=ai_endpoint, credential=credential)

        # Analyze each text file in the reviews folder
        reviews_folder = 'reviews'
        for file_name in os.listdir(reviews_folder):
            # Read the file contents
            print('\n-------------\n' + file_name)
            text = open(os.path.join(reviews_folder, file_name), encoding='utf8').read()
            print('\n' + text)

            # Get language
            detected_language = ai_client.detect_language(documents=[text])[0]
            print('\nLanguage: {}'.format(detected_language.primary_language.name))

            # Get sentiment
            sentiment_analysis = ai_client.analyze_sentiment(documents=[text])[0]
            print("\nSentiment: {}".format(sentiment_analysis.sentiment))

            # Get key phrases
            phrases = ai_client.extract_key_phrases(documents=[text])[0].key_phrases
            if len(phrases) > 0:
                print("\nKey Phrases:")
                for phrase in phrases:
                    print('\t{}'.format(phrase))

            # Get entities
            entities = ai_client.recognize_entities(documents=[text])[0].entities
            if len(entities) > 0:
                print("\nEntities:")
                for entity in entities:
                    print('\t{} ({})'.format(entity.text, entity.category))

            # Get linked entities
            linked_entities = ai_client.recognize_linked_entities(documents=[text])[0].entities
            if len(linked_entities) > 0:
                print("\nLinks:")
                for linked_entity in linked_entities:
                    print('\t{} ({})'.format(linked_entity.name, linked_entity.url))

    except Exception as ex:
        print(ex)

if __name__ == "__main__":
    main()


#OUTPUT
'''
review1.txt

Good Hotel and staff
The Royal Hotel, London, UK
3/2/2018
Clean rooms, good service, great location near Buckingham Palace and Westminster Abbey, and so on. We thoroughly enjoyed our stay. The courtyard is very peaceful and we went to a restaurant which is part of the same group and is Indian ( West coast so plenty of fish) with a Michelin Star. We had the taster menu which was fabulous. The rooms were very well appointed with a kitchen, lounge, bedroom and enormous bathroom. Thoroughly recommended.

Language: English

Sentiment: positive

Key Phrases:
        The Royal Hotel
        Good Hotel
        good service
        great location
        Buckingham Palace
        Westminster Abbey
        same group
        West coast
        Michelin Star
        taster menu
        enormous bathroom
        Clean rooms
        staff
        London
        UK
        stay
        courtyard
        restaurant
        part
        plenty
        fish
        kitchen
        lounge
        bedroom

Entities
        staff (PersonType)
        Royal Hotel (Location)
        London (Location)
        UK (Location)
        3/2/2018 (DateTime)
        rooms (Location)
        Buckingham Palace (Location)
        Westminster Abbey (Location)
        stay (Event)
        courtyard (Location)
        restaurant (Location)
        Indian (Skill)
        West coast (Location)
        fish (Product)
        rooms (Location)
        kitchen (Location)
        lounge (Location)
        bedroom (Location)
        bathroom (Location)

Links
        GOOD Music (https://en.wikipedia.org/wiki/GOOD_Music)
        Hotel (https://en.wikipedia.org/wiki/Hotel)
        The Royal Hotel (https://en.wikipedia.org/wiki/The_Royal_Hotel)
        London (https://en.wikipedia.org/wiki/London)
        Buckingham Palace (https://en.wikipedia.org/wiki/Buckingham_Palace)
        Westminster Abbey (https://en.wikipedia.org/wiki/Westminster_Abbey)
        India (https://en.wikipedia.org/wiki/India)
        West Coast Main Line (https://en.wikipedia.org/wiki/West_Coast_Main_Line)
        Michelin Guide (https://en.wikipedia.org/wiki/Michelin_Guide)

-------------
review2.txt

Tired hotel with poor service
The Royal Hotel, London, United Kingdom
5/6/2018
This is a old hotel (has been around since 1950's) and the room furnishings are average - becoming a bit old now and require changing. The internet didn't work and had to come to one of their office rooms to check in for my flight home. The website says it's close to the British Museum, but it's too far to walk.

Language: English

Sentiment: negative

Key Phrases:
        The Royal Hotel
        Tired hotel
        old hotel
        poor service
        United Kingdom
        room furnishings
        office rooms
        flight home
        British Museum
        London
        changing
        internet
        website
        1950

Entities
        hotel (Location)
        Hotel (Location)
        London (Location)
        United Kingdom (Location)
        5/6/2018 (DateTime)
        hotel (Location)
        since 1950 (DateTime)
        room (Location)
        now (DateTime)
        internet (Skill)
        one (Quantity)
        office rooms (Location)
        flight (Event)
        home (Location)
        British Museum (Location)

Links
        The Royal Hotel (https://en.wikipedia.org/wiki/The_Royal_Hotel)
        London (https://en.wikipedia.org/wiki/London)
        British Museum (https://en.wikipedia.org/wiki/British_Museum)
'''
'''
review5.txt

Un hôtel agréable
L'Hotel Buckingham, Londres, UK
J’adore cet hôtel. Le personnel est très amical et les chambres sont confortables.

Language: French

Sentiment: positive

Key Phrases:
        hôtel agréable
        L'Hotel Buckingham
        Londres
        UK
        personnel
        chambres

Entities
        hôtel (Location)
        Hotel Buckingham (Location)
        Londres (Location)
        UK (Location)
        hôtel (Location)
        personnel (PersonType)
        amical (Skill)
        chambres (Location)

Links
        United Nations (https://en.wikipedia.org/wiki/United_Nations)
        L'Hôtel (https://en.wikipedia.org/wiki/L'Hôtel)
        Buckingham (https://en.wikipedia.org/wiki/Buckingham)
        London (https://en.wikipedia.org/wiki/London)
        United Kingdom (https://en.wikipedia.org/wiki/United_Kingdom)
'''
