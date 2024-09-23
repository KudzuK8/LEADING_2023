## This is the code for the latest iteration of the LEADING fellowship work. It takes the ORCID ID from one person (Jack Brookshire), gets the related works from the work in OpenAlex, and puts them in a list.

import json
import requests
import pandas as pd
import numpy as np


# input ORCID ID for Jack Brookshire
orcid = 'https://orcid.org/0000-0002-0412-7696'

# build API URL for one author works
def build_author_works_url(orcid):
    # specify endpoint
    endpoint = 'works'

# build the 'filter' parameter
    filters = (
      f'author.orcid:{orcid}',
      'is_paratext:false'
    )

# put the URL together
    return f'https://api.openalex.org/{endpoint}?filter={",".join(filters)}'

author_works_url = build_author_works_url(orcid)

# get JSON data from API URL and put it in the variable "response_data"
r = requests.get(author_works_url)
response_data = r.json()

related_results = [result['related_works'] for result in response_data['results']]

related_strip_to_W = np.char.strip(related_results, chars ='https://openalex.org/')

related_flat = related_strip_to_W.flat
related_flat.copy()

for x in related_flat:
    print(x)
