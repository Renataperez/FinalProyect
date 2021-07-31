```python
import tweepy as tw
import config_twitter
auth = tw.OAuthHandler(config_twitter.consumer_key, config_twitter.consumer_secret)
auth.set_access_token(config_twitter.access_token, config_twitter.access_token_secret)
api = tw.API(auth, wait_on_rate_limit=True)
user = api.verify_credentials()
user
```




    User(_api=<tweepy.api.API object at 0x10fb8d9d0>, _json={'id': 1414953849639612420, 'id_str': '1414953849639612420', 'name': 'Renata Perez', 'screen_name': 'RenataP56794649', 'location': '', 'description': '', 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 0, 'friends_count': 0, 'listed_count': 0, 'created_at': 'Tue Jul 13 14:24:36 +0000 2021', 'favourites_count': 0, 'utc_offset': None, 'time_zone': None, 'geo_enabled': False, 'verified': False, 'statuses_count': 0, 'lang': None, 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'F5F8FA', 'profile_background_image_url': None, 'profile_background_image_url_https': None, 'profile_background_tile': False, 'profile_image_url': 'http://abs.twimg.com/sticky/default_profile_images/default_profile_normal.png', 'profile_image_url_https': 'https://abs.twimg.com/sticky/default_profile_images/default_profile_normal.png', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': True, 'default_profile_image': True, 'following': False, 'follow_request_sent': False, 'notifications': False, 'translator_type': 'none', 'withheld_in_countries': [], 'suspended': False, 'needs_phone_verification': False}, id=1414953849639612420, id_str='1414953849639612420', name='Renata Perez', screen_name='RenataP56794649', location='', description='', url=None, entities={'description': {'urls': []}}, protected=False, followers_count=0, friends_count=0, listed_count=0, created_at=datetime.datetime(2021, 7, 13, 14, 24, 36), favourites_count=0, utc_offset=None, time_zone=None, geo_enabled=False, verified=False, statuses_count=0, lang=None, contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='F5F8FA', profile_background_image_url=None, profile_background_image_url_https=None, profile_background_tile=False, profile_image_url='http://abs.twimg.com/sticky/default_profile_images/default_profile_normal.png', profile_image_url_https='https://abs.twimg.com/sticky/default_profile_images/default_profile_normal.png', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=True, default_profile=True, default_profile_image=True, following=False, follow_request_sent=False, notifications=False, translator_type='none', withheld_in_countries=[], suspended=False, needs_phone_verification=False)




```python
import json
import tweepy as tw
import config_twitter
def connect_api_client():
    auth = tw.OAuthHandler(config_twitter.consumer_key, config_twitter.consumer_secret)
    auth.set_access_token(config_twitter.access_token, config_twitter.access_token_secret)
    api = tw.API(auth, wait_on_rate_limit=True)
    try:
        api.verify_credentials()
        user = api.verify_credentials()
        if not user:
            raise("Credentials could not be verified: Please check config.py")
        print(f"Connected to Twitter API as {user.name}")
    except Exception as e:
        raise e
    return api
api = connect_api_client()
```

    Connected to Twitter API as Renata Perez



```python
query = 'mach-e -filter:retweets'
ntweets = 1000
tweets = [tweet._json for tweet in tw.Cursor(api.search, q=query, lang="en", tweet_mode='extended').items(ntweets)]
len(tweets)
```




    904




```python
tweets[0]
```




    {'created_at': 'Fri Jul 30 21:54:54 +0000 2021',
     'id': 1421227832009691141,
     'id_str': '1421227832009691141',
     'full_text': "@MachE_VLOG @mrlevine @mashable That power guage display on the left side of the driver's panel is *exactly* what I've been craving in my Mach-E!  OTA me, baby!",
     'truncated': False,
     'display_text_range': [32, 160],
     'entities': {'hashtags': [],
      'symbols': [],
      'user_mentions': [{'screen_name': 'MachE_VLOG',
        'name': 'Mustang Mach-E VLOG',
        'id': 1284964301527085056,
        'id_str': '1284964301527085056',
        'indices': [0, 11]},
       {'screen_name': 'mrlevine',
        'name': 'Mike Levine',
        'id': 23326965,
        'id_str': '23326965',
        'indices': [12, 21]},
       {'screen_name': 'mashable',
        'name': 'Mashable',
        'id': 972651,
        'id_str': '972651',
        'indices': [22, 31]}],
      'urls': []},
     'metadata': {'iso_language_code': 'en', 'result_type': 'recent'},
     'source': '<a href="http://twitter.com/download/android" rel="nofollow">Twitter for Android</a>',
     'in_reply_to_status_id': 1421226681331765248,
     'in_reply_to_status_id_str': '1421226681331765248',
     'in_reply_to_user_id': 1279173682997362693,
     'in_reply_to_user_id_str': '1279173682997362693',
     'in_reply_to_screen_name': 'eStang14',
     'user': {'id': 1279173682997362693,
      'id_str': '1279173682997362693',
      'name': 'eStang',
      'screen_name': 'eStang14',
      'location': '',
      'description': 'Nothing but metal, plastic, rubber, glass and electrons.',
      'url': None,
      'entities': {'description': {'urls': []}},
      'protected': False,
      'followers_count': 63,
      'friends_count': 110,
      'listed_count': 0,
      'created_at': 'Fri Jul 03 22:02:54 +0000 2020',
      'favourites_count': 3617,
      'utc_offset': None,
      'time_zone': None,
      'geo_enabled': False,
      'verified': False,
      'statuses_count': 562,
      'lang': None,
      'contributors_enabled': False,
      'is_translator': False,
      'is_translation_enabled': False,
      'profile_background_color': 'F5F8FA',
      'profile_background_image_url': None,
      'profile_background_image_url_https': None,
      'profile_background_tile': False,
      'profile_image_url': 'http://pbs.twimg.com/profile_images/1375918031763869703/g6S8S8Kd_normal.jpg',
      'profile_image_url_https': 'https://pbs.twimg.com/profile_images/1375918031763869703/g6S8S8Kd_normal.jpg',
      'profile_banner_url': 'https://pbs.twimg.com/profile_banners/1279173682997362693/1593815233',
      'profile_link_color': '1DA1F2',
      'profile_sidebar_border_color': 'C0DEED',
      'profile_sidebar_fill_color': 'DDEEF6',
      'profile_text_color': '333333',
      'profile_use_background_image': True,
      'has_extended_profile': True,
      'default_profile': True,
      'default_profile_image': False,
      'following': False,
      'follow_request_sent': False,
      'notifications': False,
      'translator_type': 'none',
      'withheld_in_countries': []},
     'geo': None,
     'coordinates': None,
     'place': None,
     'contributors': None,
     'is_quote_status': False,
     'retweet_count': 0,
     'favorite_count': 1,
     'favorited': False,
     'retweeted': False,
     'lang': 'en'}




```python
file_out = f"mach_e_data_{ntweets}.json"
with open(file_out, mode='w') as f:
    f.write(json.dumps(tweets, indent=2))
```


```python
import html
import json
import string
import re
from nltk import word_tokenize
from nltk.corpus import stopwords
from textblob import TextBlob
from wordcloud import WordCloud
import pandas as pd
import matplotlib.pyplot as plt
```


```python
mache_json = 'mach_e_data_1000.json'
with open(mache_json) as file:
    data = json.load(file)
len(data)
```




    904




```python
mache_tweets = pd.DataFrame([t['full_text'] for t in data], columns=['text'])
mache_tweets['retweets'] = [t['retweet_count'] for t in data]
mache_tweets['favorites'] = [t['favorite_count'] for t in data]
mache_tweets['user'] = [t['user']['screen_name'] for t in data]
mache_tweets
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>text</th>
      <th>retweets</th>
      <th>favorites</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>@MachE_VLOG @mrlevine @mashable That power gua...</td>
      <td>0</td>
      <td>1</td>
      <td>eStang14</td>
    </tr>
    <tr>
      <th>1</th>
      <td>@Joseph_Cote @TheSmokingTire Because Americans...</td>
      <td>0</td>
      <td>0</td>
      <td>JustinMBecker</td>
    </tr>
    <tr>
      <th>2</th>
      <td>@mrlevine @mashable Can we get some of those o...</td>
      <td>0</td>
      <td>11</td>
      <td>MachE_VLOG</td>
    </tr>
    <tr>
      <th>3</th>
      <td>@jec79 @KenBoessenkool @maxfawcett I will neve...</td>
      <td>0</td>
      <td>1</td>
      <td>Stu_parnell</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Built on all the passion for its iconic herita...</td>
      <td>0</td>
      <td>0</td>
      <td>empireflny</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>899</th>
      <td>@iamjeremyjoh @Ford To each their own, dude. I...</td>
      <td>0</td>
      <td>0</td>
      <td>MrSockpuppet</td>
    </tr>
    <tr>
      <th>900</th>
      <td>The stunning exterior design of the 2021 Ford ...</td>
      <td>0</td>
      <td>0</td>
      <td>billyhowellford</td>
    </tr>
    <tr>
      <th>901</th>
      <td>Car furries.\nYour stance on the Mach-E and th...</td>
      <td>1</td>
      <td>2</td>
      <td>DLRShaw</td>
    </tr>
    <tr>
      <th>902</th>
      <td>Ford has revealed its first all-electric car, ...</td>
      <td>0</td>
      <td>1</td>
      <td>BroditUK</td>
    </tr>
    <tr>
      <th>903</th>
      <td>Porsche Taycan, Ford Mustang Mach-E, Volkswage...</td>
      <td>0</td>
      <td>0</td>
      <td>thenewsglobal</td>
    </tr>
  </tbody>
</table>
<p>904 rows × 4 columns</p>
</div>




```python
stop_words = set(stopwords.words('english'))
def text_cleanup(s):
    s_unesc = html.unescape(re.sub(r"http\S+", "", re.sub('\n+', ' ', s)))
    s_noemoji = s_unesc.encode('ascii', 'ignore').decode('ascii')
    # normalize to lowercase and tokenize
    wt = word_tokenize(s_noemoji.lower())
    wt_filt = [w for w in wt if (w not in stop_words) and (w not in string.punctuation) and (w.isalnum())]
    return ' '.join(wt_filt)

mache_tweets['clean_text'] = mache_tweets['text'].apply(text_cleanup)
mache_tweets
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>text</th>
      <th>retweets</th>
      <th>favorites</th>
      <th>user</th>
      <th>clean_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>@MachE_VLOG @mrlevine @mashable That power gua...</td>
      <td>0</td>
      <td>1</td>
      <td>eStang14</td>
      <td>mrlevine mashable power guage display left sid...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>@Joseph_Cote @TheSmokingTire Because Americans...</td>
      <td>0</td>
      <td>0</td>
      <td>JustinMBecker</td>
      <td>thesmokingtire americans buy insignificant mar...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>@mrlevine @mashable Can we get some of those o...</td>
      <td>0</td>
      <td>11</td>
      <td>MachE_VLOG</td>
      <td>mrlevine mashable get really like see power me...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>@jec79 @KenBoessenkool @maxfawcett I will neve...</td>
      <td>0</td>
      <td>1</td>
      <td>Stu_parnell</td>
      <td>jec79 kenboessenkool maxfawcett never drive pr...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Built on all the passion for its iconic herita...</td>
      <td>0</td>
      <td>0</td>
      <td>empireflny</td>
      <td>built passion iconic heritage mustang new form...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>899</th>
      <td>@iamjeremyjoh @Ford To each their own, dude. I...</td>
      <td>0</td>
      <td>0</td>
      <td>MrSockpuppet</td>
      <td>iamjeremyjoh ford dude id never considered for...</td>
    </tr>
    <tr>
      <th>900</th>
      <td>The stunning exterior design of the 2021 Ford ...</td>
      <td>0</td>
      <td>0</td>
      <td>billyhowellford</td>
      <td>stunning exterior design 2021 ford mustang tur...</td>
    </tr>
    <tr>
      <th>901</th>
      <td>Car furries.\nYour stance on the Mach-E and th...</td>
      <td>1</td>
      <td>2</td>
      <td>DLRShaw</td>
      <td>car furries stance f150l</td>
    </tr>
    <tr>
      <th>902</th>
      <td>Ford has revealed its first all-electric car, ...</td>
      <td>0</td>
      <td>1</td>
      <td>BroditUK</td>
      <td>ford revealed first car ford mustang brodit cu...</td>
    </tr>
    <tr>
      <th>903</th>
      <td>Porsche Taycan, Ford Mustang Mach-E, Volkswage...</td>
      <td>0</td>
      <td>0</td>
      <td>thenewsglobal</td>
      <td>porsche taycan ford mustang volkswagen could r...</td>
    </tr>
  </tbody>
</table>
<p>904 rows × 5 columns</p>
</div>




```python
def tweet_pol(s):
    return TextBlob(s).sentiment.polarity

def tweet_sub(s):
    return TextBlob(s).sentiment.subjectivity

mache_tweets['polarity'] = mache_tweets['clean_text'].apply(tweet_pol)
mache_tweets['subjectivity'] = mache_tweets['clean_text'].apply(tweet_sub)
mache_tweets
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>text</th>
      <th>retweets</th>
      <th>favorites</th>
      <th>user</th>
      <th>clean_text</th>
      <th>polarity</th>
      <th>subjectivity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>@MachE_VLOG @mrlevine @mashable That power gua...</td>
      <td>0</td>
      <td>1</td>
      <td>eStang14</td>
      <td>mrlevine mashable power guage display left sid...</td>
      <td>0.125000</td>
      <td>0.125000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>@Joseph_Cote @TheSmokingTire Because Americans...</td>
      <td>0</td>
      <td>0</td>
      <td>JustinMBecker</td>
      <td>thesmokingtire americans buy insignificant mar...</td>
      <td>0.031250</td>
      <td>0.250000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>@mrlevine @mashable Can we get some of those o...</td>
      <td>0</td>
      <td>11</td>
      <td>MachE_VLOG</td>
      <td>mrlevine mashable get really like see power me...</td>
      <td>0.200000</td>
      <td>0.200000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>@jec79 @KenBoessenkool @maxfawcett I will neve...</td>
      <td>0</td>
      <td>1</td>
      <td>Stu_parnell</td>
      <td>jec79 kenboessenkool maxfawcett never drive pr...</td>
      <td>0.300000</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Built on all the passion for its iconic herita...</td>
      <td>0</td>
      <td>0</td>
      <td>empireflny</td>
      <td>built passion iconic heritage mustang new form...</td>
      <td>0.318182</td>
      <td>0.477273</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>899</th>
      <td>@iamjeremyjoh @Ford To each their own, dude. I...</td>
      <td>0</td>
      <td>0</td>
      <td>MrSockpuppet</td>
      <td>iamjeremyjoh ford dude id never considered for...</td>
      <td>-0.166667</td>
      <td>0.066667</td>
    </tr>
    <tr>
      <th>900</th>
      <td>The stunning exterior design of the 2021 Ford ...</td>
      <td>0</td>
      <td>0</td>
      <td>billyhowellford</td>
      <td>stunning exterior design 2021 ford mustang tur...</td>
      <td>0.500000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>901</th>
      <td>Car furries.\nYour stance on the Mach-E and th...</td>
      <td>1</td>
      <td>2</td>
      <td>DLRShaw</td>
      <td>car furries stance f150l</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>902</th>
      <td>Ford has revealed its first all-electric car, ...</td>
      <td>0</td>
      <td>1</td>
      <td>BroditUK</td>
      <td>ford revealed first car ford mustang brodit cu...</td>
      <td>0.250000</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>903</th>
      <td>Porsche Taycan, Ford Mustang Mach-E, Volkswage...</td>
      <td>0</td>
      <td>0</td>
      <td>thenewsglobal</td>
      <td>porsche taycan ford mustang volkswagen could r...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>904 rows × 7 columns</p>
</div>




```python
all_text = ''.join(mache_tweets['clean_text'])
wc = WordCloud(width=1200, height=800, max_font_size=110, background_color = 'white', collocations=False).generate(all_text)
plt.axis("off")
plt.imshow(wc, interpolation="bilinear")
plt.show()
```


    
![png](output_10_0.png)
    



```python
me_kw = WordCloud().process_text(all_text)
df_me_kw = pd.DataFrame(list(me_kw.items()), columns = ['Key words', 'Count'])
df_me_kw
df_me_kw.sort_values(by='Count', ascending=False).head(20)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Key words</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>59</th>
      <td>ford</td>
      <td>313</td>
    </tr>
    <tr>
      <th>20</th>
      <td>mustang</td>
      <td>169</td>
    </tr>
    <tr>
      <th>151</th>
      <td>tesla</td>
      <td>136</td>
    </tr>
    <tr>
      <th>3787</th>
      <td>ford mustang</td>
      <td>109</td>
    </tr>
    <tr>
      <th>413</th>
      <td>ev</td>
      <td>105</td>
    </tr>
    <tr>
      <th>278</th>
      <td>car</td>
      <td>95</td>
    </tr>
    <tr>
      <th>55</th>
      <td>new</td>
      <td>90</td>
    </tr>
    <tr>
      <th>3799</th>
      <td>women airforce</td>
      <td>57</td>
    </tr>
    <tr>
      <th>3800</th>
      <td>airforce service</td>
      <td>56</td>
    </tr>
    <tr>
      <th>166</th>
      <td>model</td>
      <td>48</td>
    </tr>
    <tr>
      <th>64</th>
      <td>one</td>
      <td>47</td>
    </tr>
    <tr>
      <th>3801</th>
      <td>service pilots</td>
      <td>46</td>
    </tr>
    <tr>
      <th>227</th>
      <td>electric</td>
      <td>44</td>
    </tr>
    <tr>
      <th>149</th>
      <td>better</td>
      <td>42</td>
    </tr>
    <tr>
      <th>184</th>
      <td>vehicle</td>
      <td>41</td>
    </tr>
    <tr>
      <th>179</th>
      <td>look</td>
      <td>36</td>
    </tr>
    <tr>
      <th>77</th>
      <td>make</td>
      <td>35</td>
    </tr>
    <tr>
      <th>123</th>
      <td>charge</td>
      <td>35</td>
    </tr>
    <tr>
      <th>28</th>
      <td>see</td>
      <td>35</td>
    </tr>
    <tr>
      <th>225</th>
      <td>year</td>
      <td>34</td>
    </tr>
  </tbody>
</table>
</div>




```python
avg_pol = mache_tweets['polarity'].mean()
avg_pol
```




    0.1359903214008974




```python
avg_sub = mache_tweets['subjectivity'].mean()
avg_sub
```




    0.3625010753208845




```python
mache_tweets.sort_values(by='polarity', ascending=False).head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>text</th>
      <th>retweets</th>
      <th>favorites</th>
      <th>user</th>
      <th>clean_text</th>
      <th>polarity</th>
      <th>subjectivity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>196</th>
      <td>@jimcramer Ford has best EV's 😂\n@garyblack00\...</td>
      <td>0</td>
      <td>3</td>
      <td>gafj42</td>
      <td>jimcramer ford best ev garyblack00 watched f t...</td>
      <td>1.0</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>232</th>
      <td>Awesome design\n"Ford salutes WWII Women Airfo...</td>
      <td>0</td>
      <td>0</td>
      <td>Exposed_Comic</td>
      <td>awesome design ford salutes wwii women airforc...</td>
      <td>1.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>106</th>
      <td>@jimcramer Best EVs!? \n\nUmm... they manufact...</td>
      <td>0</td>
      <td>7</td>
      <td>ChrisDungeon</td>
      <td>jimcramer best evs umm manufacture 1 ev model ...</td>
      <td>1.0</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>883</th>
      <td>@ElonardoM @EV_Stevee @jaminwestby @TeslaOwls ...</td>
      <td>0</td>
      <td>3</td>
      <td>DylanMilota</td>
      <td>elonardom jaminwestby teslaowls elonmusk jrosi...</td>
      <td>1.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>403</th>
      <td>Ford Mustang Mach-E Sets Impressive World Reco...</td>
      <td>0</td>
      <td>0</td>
      <td>GwinnettPlace</td>
      <td>ford mustang sets impressive world record</td>
      <td>1.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>140</th>
      <td>This Ford Mustang Mach-E honors wonderful Girl...</td>
      <td>0</td>
      <td>0</td>
      <td>newsx24channel</td>
      <td>ford mustang honors wonderful girls airforce s...</td>
      <td>1.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>104</th>
      <td>One-off Ford Mustang Mach-E is a brilliant tri...</td>
      <td>0</td>
      <td>0</td>
      <td>SponEndCov</td>
      <td>ford mustang brilliant tribute ww2 women pilots</td>
      <td>0.9</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>800</th>
      <td>@Leerzeit I drive the Mach-E. My brother has t...</td>
      <td>0</td>
      <td>0</td>
      <td>ericson_kris</td>
      <td>leerzeit drive brother ipace great cars</td>
      <td>0.8</td>
      <td>0.75</td>
    </tr>
    <tr>
      <th>649</th>
      <td>@Buddyboybudbud The Ford Mustang Mach-E is a g...</td>
      <td>0</td>
      <td>3</td>
      <td>PaulHartNYC</td>
      <td>buddyboybudbud ford mustang great electric car...</td>
      <td>0.8</td>
      <td>0.75</td>
    </tr>
    <tr>
      <th>49</th>
      <td>@wendishen99 @TeslaProTips1 @28delayslater @wh...</td>
      <td>0</td>
      <td>1</td>
      <td>MachE_VLOG</td>
      <td>wendishen99 teslaprotips1 28delayslater whatca...</td>
      <td>0.8</td>
      <td>0.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
mache_tweets['text'][780]
```




    'Ford dealership adds $10,000 in document fees to Mach-E order \n\nIf you like getting fucked, head on over to your nearest Ford dealership https://t.co/Lk5yagVlBB'




```python
mache_tweets.sort_values(by='polarity', ascending=True).head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>text</th>
      <th>retweets</th>
      <th>favorites</th>
      <th>user</th>
      <th>clean_text</th>
      <th>polarity</th>
      <th>subjectivity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>694</th>
      <td>I think you're insane to spend $47k on one of ...</td>
      <td>0</td>
      <td>2</td>
      <td>YSSMAN</td>
      <td>think insane spend 47k one versus</td>
      <td>-1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>890</th>
      <td>The Mach-E Buying Experience Is AWFUL! https:/...</td>
      <td>0</td>
      <td>0</td>
      <td>soryparra</td>
      <td>buying experience awful via youtube fordcredit</td>
      <td>-1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>770</th>
      <td>The Mach-E Buying Experience Is AWFUL! https:/...</td>
      <td>0</td>
      <td>0</td>
      <td>wiley695</td>
      <td>buying experience awful via youtube</td>
      <td>-1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>764</th>
      <td>Is it just me or does the design of the Mach-E...</td>
      <td>0</td>
      <td>1</td>
      <td>d4t4wr4ngl3r</td>
      <td>design battery pack look like insanely labor i...</td>
      <td>-1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>368</th>
      <td>@crypto_almanac @KateFantom I-PACE has the wor...</td>
      <td>0</td>
      <td>0</td>
      <td>ForRossiya</td>
      <td>katefantom worst charging car price bracket ch...</td>
      <td>-1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>733</th>
      <td>The Mach-E Buying Experience Is AWFUL! https:/...</td>
      <td>0</td>
      <td>1</td>
      <td>skynetazul</td>
      <td>buying experience awful via youtube</td>
      <td>-1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>219</th>
      <td>@8muerte @1478397vw @DriveTeslaca Mach-e def t...</td>
      <td>0</td>
      <td>1</td>
      <td>1stMarsColonist</td>
      <td>8muerte 1478397vw driveteslaca def ugly dude</td>
      <td>-0.7</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>812</th>
      <td>@Is_that_the_top @GordonJohnson19 @TroyTeslike...</td>
      <td>0</td>
      <td>0</td>
      <td>mindsoul</td>
      <td>gordonjohnson19 troyteslike anyway usa law bad...</td>
      <td>-0.7</td>
      <td>0.666667</td>
    </tr>
    <tr>
      <th>682</th>
      <td>Let me re-emphasize how badly @Cadillac is han...</td>
      <td>0</td>
      <td>29</td>
      <td>bgluckman</td>
      <td>let badly cadillac handling marketing lyriq fo...</td>
      <td>-0.7</td>
      <td>0.666667</td>
    </tr>
    <tr>
      <th>706</th>
      <td>Too bad he doesn’t care about the horrors some...</td>
      <td>0</td>
      <td>6</td>
      <td>JohnnaCrider1</td>
      <td>bad doesnt care horrors ford customers go thru...</td>
      <td>-0.7</td>
      <td>0.666667</td>
    </tr>
  </tbody>
</table>
</div>




```python
mache_tweets['text'][694]
```




    "I think you're insane to spend $47k on one of these versus an ID.4 or Mach-E"




```python
mache_tweets.sort_values(by='retweets', ascending=False).head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>text</th>
      <th>retweets</th>
      <th>favorites</th>
      <th>user</th>
      <th>clean_text</th>
      <th>polarity</th>
      <th>subjectivity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>780</th>
      <td>Ford dealership adds $10,000 in document fees ...</td>
      <td>164</td>
      <td>1128</td>
      <td>WholeMarsBlog</td>
      <td>ford dealership adds document fees order like ...</td>
      <td>-0.600000</td>
      <td>0.700000</td>
    </tr>
    <tr>
      <th>265</th>
      <td>Mustang Mach-E is both bottom line profitable ...</td>
      <td>46</td>
      <td>453</td>
      <td>mrlevine</td>
      <td>mustang bottom line profitable contribution ma...</td>
      <td>0.227273</td>
      <td>0.545455</td>
    </tr>
    <tr>
      <th>455</th>
      <td>Ford salutes WWII Women Airforce Service Pilot...</td>
      <td>30</td>
      <td>139</td>
      <td>FoxNews</td>
      <td>ford salutes wwii women airforce service pilot...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>64</th>
      <td>This is your sign to go test-drive a Mustang M...</td>
      <td>26</td>
      <td>278</td>
      <td>FordMustang</td>
      <td>sign go mustang ford fordmustang mustangmache</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>471</th>
      <td>Ford Honors WWII Women Airforce Service Pilots...</td>
      <td>21</td>
      <td>164</td>
      <td>mrlevine</td>
      <td>ford honors wwii women airforce service pilots...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>662</th>
      <td>Ford charged a Mustang Mach-E owner $10,000 in...</td>
      <td>16</td>
      <td>272</td>
      <td>Teslarati</td>
      <td>ford charged mustang owner documentation fees ...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>736</th>
      <td>Ford charges Mustang Mach-E customer $10k in d...</td>
      <td>12</td>
      <td>181</td>
      <td>Teslarati</td>
      <td>ford charges mustang customer 10k doc fees big...</td>
      <td>0.000000</td>
      <td>0.100000</td>
    </tr>
    <tr>
      <th>298</th>
      <td>Ford Mustang Mach-E commemorates WWII Women Ai...</td>
      <td>10</td>
      <td>29</td>
      <td>therealautoblog</td>
      <td>ford mustang commemorates wwii women airforce ...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>267</th>
      <td>Ford CFO John Lawler says Mustang Mach-E is al...</td>
      <td>9</td>
      <td>25</td>
      <td>sokane1</td>
      <td>ford cfo john lawler says mustang already prof...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>745</th>
      <td>"Take a look at Twitter, a digital hunting gro...</td>
      <td>9</td>
      <td>58</td>
      <td>WPipperger</td>
      <td>take look twitter digital hunting ground suppo...</td>
      <td>-0.350000</td>
      <td>0.500000</td>
    </tr>
  </tbody>
</table>
</div>




```python
mache_tweets['text'][662]
```




    'Ford charged a Mustang Mach-E owner $10,000 in documentation fees.\n\nIt was a mistake.\n\nhttps://t.co/ept1iQyjbl https://t.co/PISOt4B6PH'




```python
mache_tesla = mache_tweets[mache_tweets['text'].str.contains('tesla')]
mache_tesla
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>text</th>
      <th>retweets</th>
      <th>favorites</th>
      <th>user</th>
      <th>clean_text</th>
      <th>polarity</th>
      <th>subjectivity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>@jec79 @KenBoessenkool @maxfawcett I will neve...</td>
      <td>0</td>
      <td>1</td>
      <td>Stu_parnell</td>
      <td>jec79 kenboessenkool maxfawcett never drive pr...</td>
      <td>0.300000</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>227</th>
      <td>@teslaownersSV @sscamerica @elonmusk Mach-E bl...</td>
      <td>0</td>
      <td>3</td>
      <td>teslatidbits</td>
      <td>teslaownerssv sscamerica elonmusk blue teasing...</td>
      <td>0.000000</td>
      <td>0.100000</td>
    </tr>
    <tr>
      <th>318</th>
      <td>@AmazingChevVolt @elonmusk @DimaZeniuk @truth_...</td>
      <td>2</td>
      <td>2</td>
      <td>RustyRoad</td>
      <td>amazingchevvolt elonmusk dimazeniuk vwgroup vw...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>357</th>
      <td>@teslamaniacs @raffaeru @fordaustria It’s main...</td>
      <td>0</td>
      <td>0</td>
      <td>CaptainVoni</td>
      <td>teslamaniacs raffaeru fordaustria mainly wife ...</td>
      <td>0.183333</td>
      <td>0.216667</td>
    </tr>
    <tr>
      <th>394</th>
      <td>@enscand @elonmusk @DimaZeniuk @truth_tesla Is...</td>
      <td>1</td>
      <td>1</td>
      <td>RustyRoad</td>
      <td>enscand elonmusk dimazeniuk also true fast maj...</td>
      <td>0.161310</td>
      <td>0.431548</td>
    </tr>
    <tr>
      <th>408</th>
      <td>@elonmusk @DimaZeniuk @truth_tesla Not sure wh...</td>
      <td>0</td>
      <td>1</td>
      <td>Choppnuts</td>
      <td>elonmusk dimazeniuk sure know however vwgroup ...</td>
      <td>0.375000</td>
      <td>0.569444</td>
    </tr>
    <tr>
      <th>440</th>
      <td>@wolfoftesla @squawksquare @dayyanl @jimcramer...</td>
      <td>0</td>
      <td>0</td>
      <td>MachE_VLOG</td>
      <td>wolfoftesla squawksquare dayyanl jimcramer dri...</td>
      <td>0.333333</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>506</th>
      <td>@xIronman777 @mazenaljabowbi and they even sai...</td>
      <td>0</td>
      <td>0</td>
      <td>ACE_Trader8</td>
      <td>xironman777 mazenaljabowbi even said drive nev...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>552</th>
      <td>News from Auto Industry: Mach-E, Buick refresh...</td>
      <td>0</td>
      <td>0</td>
      <td>CRSAutomotive</td>
      <td>news auto industry buick refresh kia nissan te...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>578</th>
      <td>@teslabros I can’t get past the front clown fa...</td>
      <td>0</td>
      <td>2</td>
      <td>fromVeganning</td>
      <td>teslabros cant get past front clown face im al...</td>
      <td>0.125000</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>620</th>
      <td>@MichelBruns_ @ray4tesla @elonmusk No, you can...</td>
      <td>0</td>
      <td>0</td>
      <td>GoudzAlex</td>
      <td>ray4tesla elonmusk cant taycan ms p90d taycan ...</td>
      <td>0.000000</td>
      <td>0.150000</td>
    </tr>
    <tr>
      <th>737</th>
      <td>@funnygamedev im sure it feels a lot better to...</td>
      <td>0</td>
      <td>2</td>
      <td>spiketickett</td>
      <td>funnygamedev im sure feels lot better drive te...</td>
      <td>0.500000</td>
      <td>0.694444</td>
    </tr>
    <tr>
      <th>743</th>
      <td>@elonmusk @Teslarati Was wondering if the rubb...</td>
      <td>0</td>
      <td>0</td>
      <td>pascalguertin</td>
      <td>elonmusk teslarati wondering rubber compound u...</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>810</th>
      <td>@LyftGyft Speaking only for me as a tesla owne...</td>
      <td>0</td>
      <td>1</td>
      <td>JohnMaddox1990</td>
      <td>lyftgyft speaking tesla owner deep breath awes...</td>
      <td>0.200000</td>
      <td>0.581250</td>
    </tr>
  </tbody>
</table>
</div>




```python
compar_text = ''.join(mache_tesla['clean_text'])
wc = WordCloud(width=1200, height=800, max_font_size=110, background_color = 'white', collocations=False).generate(compar_text)
plt.axis("off")
plt.imshow(wc, interpolation="bilinear")
plt.show()
```


    
![png](output_21_0.png)
    



```python
comp_kw = WordCloud().process_text(compar_text)
df_comp_kw = pd.DataFrame(list(comp_kw.items()), columns = ['Key words', 'Count'])
df_comp_kw
df_comp_kw.sort_values(by='Count', ascending=False).head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Key words</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <td>tesla</td>
      <td>10</td>
    </tr>
    <tr>
      <th>61</th>
      <td>even</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>drive</td>
      <td>5</td>
    </tr>
    <tr>
      <th>56</th>
      <td>still</td>
      <td>4</td>
    </tr>
    <tr>
      <th>23</th>
      <td>elonmusk</td>
      <td>4</td>
    </tr>
    <tr>
      <th>80</th>
      <td>update</td>
      <td>4</td>
    </tr>
    <tr>
      <th>96</th>
      <td>better</td>
      <td>4</td>
    </tr>
    <tr>
      <th>123</th>
      <td>cant</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>im</td>
      <td>3</td>
    </tr>
    <tr>
      <th>65</th>
      <td>software</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
