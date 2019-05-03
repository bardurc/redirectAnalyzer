#!/usr/bin/env python3

import requests
from requests.exceptions import ConnectionError, MissingSchema, InvalidURL
import argparse
import sys


parser = argparse.ArgumentParser()
parser.add_argument('-url', help = 'URL to analyse for redirects', required = True)
args = parser.parse_args()

url = args.url

def get_request(url):
    try:
        r = requests.get(url)
    except ConnectionError as e:
        print('***** Connection Error *****')
        print('Couldn\'t connect to %s' % (url))
        sys.exit(1)
    except MissingSchema as e:
        print('***** Schema Error *****')
        print(e)
        sys.exit(1)
    except InvalidURL as e:
        print('***** Invalid URL *****')
        print(e)
        sys.exit(1)
    return r

def get_path(url):
    r = get_request(url)
    if r.history:
        urllist = []
        for resp in r.history:
            urllist.append(resp.url)
        urllist.append(r.url)
        return urllist
    return [url]

path = get_path(url)
no_of_redirects = len(path) - 1
final_destination = path[-1]
intermediary_links = path[1:-1]
print('Number of redirects:\n\t%d' % (no_of_redirects))
print('Path:')
for l in path:
    print('\t%s' % (l))
