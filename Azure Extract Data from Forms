#Environment variable
DOC_INTELLIGENCE_ENDPOINT=
DOC_INTELLIGENCE_KEY=
MODEL_ID=

#Code
from azure.core.credentials import AzureKeyCredential
from azure.ai.formrecognizer import DocumentAnalysisClient
from dotenv import load_dotenv
import os

# Get configuration settings
load_dotenv()
endpoint = os.getenv("DOC_INTELLIGENCE_ENDPOINT")
key = os.getenv("DOC_INTELLIGENCE_KEY")
model_id = os.getenv("MODEL_ID")

formUrl = "https://github.com/MicrosoftLearning/mslearn-ai-document-intelligence/blob/main/Labfiles/02-custom-document-intelligence/test1.jpg?raw=true"

# Create a Document Analysis Client
document_analysis_client = DocumentAnalysisClient(
    endpoint=endpoint,
    credential=AzureKeyCredential(key)
)

# Make sure your document's type is included in the list of document types the custom model can analyze
response = document_analysis_client.begin_analyze_document_from_url(model_id, formUrl)
result = response.result()

# Analyze the results
for idx, document in enumerate(result.documents):
    print("-------- Analyzing document #{} --------".format(idx + 1))
    print("Document has type: {}".format(document.doc_type))
    print("Document confidence: {}".format(document.confidence))
    print("Analyzed by model with ID: {}".format(result.model_id))
    
    for name, field in document.fields.items():
        field_value = field.value if field.value else field.content
        print("Found field '{}' with value '{}' and confidence: {}".format(name, field_value, field.confidence))

print("-----------------------------------")



'''OUTPUT
python test-model.py
--------Analyzing document #1--------
Document has type mitsuri_obonai:mitsuri_obonai
Document has confidence 0.818
Document was analyzed by model with ID mitsuri_obonai
Found field 'CompanyAddress' with value '343 E Winter Road Seattle, WA 93849 Phone:' and with confidence 0.486
Found field 'Tax' with value '$600.00' and with confidence 0.993
Found field 'CompanyPhoneNumber' with value '234-986-6454' and with confidence 0.995
Found field 'VendorName' with value 'Seth Stanley' and with confidence 0.99
Found field 'DatedAs' with value '04/04/2020' and with confidence 0.994
Found field 'Quantity' with value '50.0' and with confidence 0.99
Found field 'Website' with value 'www.herolimited.com' and with confidence 0.99
Found field 'Subtotal' with value '$6750.00' and with confidence 0.994
Found field 'CompanyName' with value 'Yoga for You' and with confidence 0.991
Found field 'PhoneNumber' with value '555-348-6512' and with confidence 0.99
Found field 'Merchant' with value 'Hero Limited' and with confidence 0.99
Found field 'PurchaseOrderNumber' with value '3929423' and with confidence 0.994
Found field 'Email' with value 'accounts@herolimited.com' and with confidence 0.949
Found field 'Signature' with value 'Josh Granger' and with confidence 0.452
Found field 'Total' with value '$7350.00' and with confidence 0.994
-----------------------------------
'''
