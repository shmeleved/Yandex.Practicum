<h1>Table of Contents<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#Data-Overview" data-toc-modified-id="Data-Overview-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>Data Overview</a></span></li><li><span><a href="#Data-preprocessing" data-toc-modified-id="Data-preprocessing-2"><span class="toc-item-num">2&nbsp;&nbsp;</span>Data preprocessing</a></span><ul class="toc-item"><li><span><a href="#Header-style" data-toc-modified-id="Header-style-2.1"><span class="toc-item-num">2.1&nbsp;&nbsp;</span>Header style</a></span></li><li><span><a href="#Missing-values" data-toc-modified-id="Missing-values-2.2"><span class="toc-item-num">2.2&nbsp;&nbsp;</span>Missing values</a></span></li><li><span><a href="#Duplicates" data-toc-modified-id="Duplicates-2.3"><span class="toc-item-num">2.3&nbsp;&nbsp;</span>Duplicates</a></span></li></ul></li><li><span><a href="#Hypothesis-testing" data-toc-modified-id="Hypothesis-testing-3"><span class="toc-item-num">3&nbsp;&nbsp;</span>Hypothesis testing</a></span><ul class="toc-item"><li><span><a href="#Comparison-of-user-behavior-of-two-capitals" data-toc-modified-id="Comparison-of-user-behavior-of-two-capitals-3.1"><span class="toc-item-num">3.1&nbsp;&nbsp;</span>Comparison of user behavior of two capitals</a></span></li><li><span><a href="#Music-at-the-beginning-and-end-of-the-week" data-toc-modified-id="Music-at-the-beginning-and-end-of-the-week-3.2"><span class="toc-item-num">3.2&nbsp;&nbsp;</span>Music at the beginning and end of the week</a></span></li><li><span><a href="#Genre-preferences-in-Moscow-and-St.-Petersburg" data-toc-modified-id="Genre-preferences-in-Moscow-and-St.-Petersburg-3.3"><span class="toc-item-num">3.3&nbsp;&nbsp;</span>Genre preferences in Moscow and St. Petersburg</a></span></li></ul></li><li><span><a href="#Results-of-the-research" data-toc-modified-id="Results-of-the-research-4"><span class="toc-item-num">4&nbsp;&nbsp;</span>Results of the research</a></span></li></ul></div>

# Yandex.Music

The comparison of Moscow and St. Petersburg is surrounded by myths. For example:
 * Moscow is a megapolis subject to the rigid rhythm of the working week;
 * St. Petersburg is a cultural capital, with its own tastes.

Using Yandex.Music data, we will compare the behavior of users of the two capitals.

**Research objective** — test three hypotheses:
1. User activity depends on the day of the week. Moreover, in Moscow and St. Petersburg, this manifests itself in different ways.
2. On Monday morning, some genres prevail in Moscow, and others in St. Petersburg. Similarly, on Friday evening, different genres prevail — depending on the city.
3. Moscow and St. Petersburg prefer different genres of music. In Moscow, pop music is more often listened to, in St. Petersburg - Russian rap.

**Research progress**

We will get data about user behavior from the file `yandex_music_project.csv`. Nothing is known about the quality of the data. Therefore, a review of the data will be needed before testing hypotheses.

We will check the data for errors and evaluate their impact on the study. Then, at the preprocessing stage, we will look for an opportunity to correct the most critical data errors.

Thus, the study will take place in three stages:
1. Data overview.
2. Data preprocessing.
3. Hypothesis testing.



## Data Overview


```python
import pandas as pd
```


```python
df=pd.read_csv('datasets/yandex_music_project.csv')
```


```python
# getting the first 10 rows of the df table
df.head(10)
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
      <th>userID</th>
      <th>Track</th>
      <th>artist</th>
      <th>genre</th>
      <th>City</th>
      <th>time</th>
      <th>Day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>FFB692EC</td>
      <td>Kamigata To Boots</td>
      <td>The Mass Missile</td>
      <td>rock</td>
      <td>Saint-Petersburg</td>
      <td>20:28:33</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55204538</td>
      <td>Delayed Because of Accident</td>
      <td>Andreas Rönnberg</td>
      <td>rock</td>
      <td>Moscow</td>
      <td>14:07:09</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20EC38</td>
      <td>Funiculì funiculà</td>
      <td>Mario Lanza</td>
      <td>pop</td>
      <td>Saint-Petersburg</td>
      <td>20:58:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3DD03C9</td>
      <td>Dragons in the Sunset</td>
      <td>Fire + Ice</td>
      <td>folk</td>
      <td>Saint-Petersburg</td>
      <td>08:37:09</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E2DC1FAE</td>
      <td>Soul People</td>
      <td>Space Echo</td>
      <td>dance</td>
      <td>Moscow</td>
      <td>08:34:34</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>5</th>
      <td>842029A1</td>
      <td>Преданная</td>
      <td>IMPERVTOR</td>
      <td>rusrap</td>
      <td>Saint-Petersburg</td>
      <td>13:09:41</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4CB90AA5</td>
      <td>True</td>
      <td>Roman Messer</td>
      <td>dance</td>
      <td>Moscow</td>
      <td>13:00:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>7</th>
      <td>F03E1C1F</td>
      <td>Feeling This Way</td>
      <td>Polina Griffith</td>
      <td>dance</td>
      <td>Moscow</td>
      <td>20:47:49</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8FA1D3BE</td>
      <td>И вновь продолжается бой</td>
      <td>NaN</td>
      <td>ruspop</td>
      <td>Moscow</td>
      <td>09:17:40</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>9</th>
      <td>E772D5C0</td>
      <td>Pessimist</td>
      <td>NaN</td>
      <td>dance</td>
      <td>Saint-Petersburg</td>
      <td>21:20:49</td>
      <td>Wednesday</td>
    </tr>
  </tbody>
</table>
</div>




```python
# getting general information about the data in the df table
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 65079 entries, 0 to 65078
    Data columns (total 7 columns):
     #   Column    Non-Null Count  Dtype 
    ---  ------    --------------  ----- 
     0     userID  65079 non-null  object
     1   Track     63848 non-null  object
     2   artist    57876 non-null  object
     3   genre     63881 non-null  object
     4     City    65079 non-null  object
     5   time      65079 non-null  object
     6   Day       65079 non-null  object
    dtypes: object(7)
    memory usage: 3.5+ MB
    

So, there are seven columns in the table. The data type in all columns is `object`.

According to the data documentation:
* `userID` is the user ID;
* `Track` — the name of the track;
* `artist` — artist's name;
* `genre` — the name of the genre;
* `City` — the user's city;
* `time` — the start time of listening;
* `Day` — the day of the week.

Three style violations are visible in the column names:
1. Lowercase letters are combined with uppercase.
2. There are gaps.
3. It is necessary to use the "snake" style, for example, in the case of 'userID' it would be better to write 'user_id'


**Conclusions**

Each row of the table contains data about the listened track. Part of the columns describes the composition itself: name, artist and genre. The rest of the data tells about the user: what city he is from, when he listened to music.

Previously, it can be argued that there is enough data to test hypotheses. But there are gaps in the data, and in the column names there are discrepancies with good style.

To move forward, we need to fix the data problems.

## Data preprocessing
Let's fix the style in the column headers, eliminate omissions. Then we will check the data for duplicates.

### Header style


```python
# list of column names of the df table
df.columns
```




    Index(['  userID', 'Track', 'artist', 'genre', '  City  ', 'time', 'Day'], dtype='object')



Rename columns:
* `'  userID'` → `'user_id'`;
* `'Track'` → `'track'`;
* `'  City  '` → `'city'`;
* `'Day'` → `'day'`.


```python
df  =df.rename(columns = {'  userID' : 'user_id','Track' : 'track','  City  ' : 'city','Day' : 'day'})
```


```python
df.columns
```




    Index(['user_id', 'track', 'artist', 'genre', 'city', 'time', 'day'], dtype='object')



### Missing values
First, let's calculate how many missing values are in the table. Two `pandas` methods are enough for this:


```python
df.isna().sum()
```




    user_id       0
    track      1231
    artist     7203
    genre      1198
    city          0
    time          0
    day           0
    dtype: int64



Not all missing values affect the research. So in `track` and `artist` omissions are not important for our work. It is enough to replace them with explicit designations.

But missing values in `genre` may interfere with the comparison of musical tastes in Moscow and St. Petersburg. In practice, it would be correct to establish the reason for the missing values and restore the data. There is no such possibility in this project, so we will have to:
* fill in these gaps with explicit notation,
* assess how much they will distort the calculations.

Replace the missing values in the columns `track`, `artist` and `genre` with the string 'unknown':


```python
columns_to_replace=['track','artist','genre']
for col in columns_to_replace:
    df[col]=df[col].fillna('unknown')
```


```python
# missing values counting
df.isna().sum()
```




    user_id    0
    track      0
    artist     0
    genre      0
    city       0
    time       0
    day        0
    dtype: int64



### Duplicates


```python
# counting obvious duplicates
df.duplicated().sum()
```




    3826




```python
# removing obvious duplicates (with the elimination of old indexes and the formation of new ones)
df=df.drop_duplicates().reset_index(drop=True)
```


```python
# checking for the absence of duplicates
df.duplicated().sum()
```




    0



Now let's get rid of other duplicates in the `genre` column. For example, the name of the same genre may be written a little differently. Such errors will also affect the result of the research.


```python
# Unique genre titles
all_genres=df['genre'].sort_values().unique()
all_genres
```




    array(['acid', 'acoustic', 'action', 'adult', 'africa', 'afrikaans',
           'alternative', 'alternativepunk', 'ambient', 'americana',
           'animated', 'anime', 'arabesk', 'arabic', 'arena',
           'argentinetango', 'art', 'audiobook', 'author', 'avantgarde',
           'axé', 'baile', 'balkan', 'beats', 'bigroom', 'black', 'bluegrass',
           'blues', 'bollywood', 'bossa', 'brazilian', 'breakbeat', 'breaks',
           'broadway', 'cantautori', 'cantopop', 'canzone', 'caribbean',
           'caucasian', 'celtic', 'chamber', 'chanson', 'children', 'chill',
           'chinese', 'choral', 'christian', 'christmas', 'classical',
           'classicmetal', 'club', 'colombian', 'comedy', 'conjazz',
           'contemporary', 'country', 'cuban', 'dance', 'dancehall',
           'dancepop', 'dark', 'death', 'deep', 'deutschrock', 'deutschspr',
           'dirty', 'disco', 'dnb', 'documentary', 'downbeat', 'downtempo',
           'drum', 'dub', 'dubstep', 'eastern', 'easy', 'electronic',
           'electropop', 'emo', 'entehno', 'epicmetal', 'estrada', 'ethnic',
           'eurofolk', 'european', 'experimental', 'extrememetal', 'fado',
           'fairytail', 'film', 'fitness', 'flamenco', 'folk', 'folklore',
           'folkmetal', 'folkrock', 'folktronica', 'forró', 'frankreich',
           'französisch', 'french', 'funk', 'future', 'gangsta', 'garage',
           'german', 'ghazal', 'gitarre', 'glitch', 'gospel', 'gothic',
           'grime', 'grunge', 'gypsy', 'handsup', "hard'n'heavy", 'hardcore',
           'hardstyle', 'hardtechno', 'hip', 'hip-hop', 'hiphop',
           'historisch', 'holiday', 'hop', 'horror', 'house', 'hymn', 'idm',
           'independent', 'indian', 'indie', 'indipop', 'industrial',
           'inspirational', 'instrumental', 'international', 'irish', 'jam',
           'japanese', 'jazz', 'jewish', 'jpop', 'jungle', 'k-pop',
           'karadeniz', 'karaoke', 'kayokyoku', 'korean', 'laiko', 'latin',
           'latino', 'leftfield', 'local', 'lounge', 'loungeelectronic',
           'lovers', 'malaysian', 'mandopop', 'marschmusik', 'meditative',
           'mediterranean', 'melodic', 'metal', 'metalcore', 'mexican',
           'middle', 'minimal', 'miscellaneous', 'modern', 'mood', 'mpb',
           'muslim', 'native', 'neoklassik', 'neue', 'new', 'newage',
           'newwave', 'nu', 'nujazz', 'numetal', 'oceania', 'old', 'opera',
           'orchestral', 'other', 'piano', 'podcasts', 'pop', 'popdance',
           'popelectronic', 'popeurodance', 'poprussian', 'post',
           'posthardcore', 'postrock', 'power', 'progmetal', 'progressive',
           'psychedelic', 'punjabi', 'punk', 'quebecois', 'ragga', 'ram',
           'rancheras', 'rap', 'rave', 'reggae', 'reggaeton', 'regional',
           'relax', 'religious', 'retro', 'rhythm', 'rnb', 'rnr', 'rock',
           'rockabilly', 'rockalternative', 'rockindie', 'rockother',
           'romance', 'roots', 'ruspop', 'rusrap', 'rusrock', 'russian',
           'salsa', 'samba', 'scenic', 'schlager', 'self', 'sertanejo',
           'shanson', 'shoegazing', 'showtunes', 'singer', 'ska', 'skarock',
           'slow', 'smooth', 'soft', 'soul', 'soulful', 'sound', 'soundtrack',
           'southern', 'specialty', 'speech', 'spiritual', 'sport',
           'stonerrock', 'surf', 'swing', 'synthpop', 'synthrock',
           'sängerportrait', 'tango', 'tanzorchester', 'taraftar', 'tatar',
           'tech', 'techno', 'teen', 'thrash', 'top', 'traditional',
           'tradjazz', 'trance', 'tribal', 'trip', 'triphop', 'tropical',
           'türk', 'türkçe', 'ukrrock', 'unknown', 'urban', 'uzbek',
           'variété', 'vi', 'videogame', 'vocal', 'western', 'world',
           'worldbeat', 'ïîï', 'электроника'], dtype=object)



The following other duplicates:
* *hip*,
* *hop*,
* *hip-hop*,


* *електроника*,
* *electronic*.

Let's write the function `replace_wrong_genres()` with two parameters:
* `wrong_genres` — list of duplicates,
* `correct_genre` is a string with the correct value.


```python
# Function for replacing duplicates
def replace_wrong_genres(wrong_genres,correct_genre):
    df['genre'] = df['genre'].replace(wrong_genres, correct_genre)
    return df['genre']
```


```python
# Eliminate duplicates
wrong_genres_1 = ['hip','hop','hip-hop']
correct_genre_1 = 'hiphop'

wrong_genres_2 = 'электроника'
correct_genre_2 = 'electronic'

replace_wrong_genres(wrong_genres_1,correct_genre_2)
replace_wrong_genres(wrong_genres_2,correct_genre_2)
```




    0              rock
    1              rock
    2               pop
    3              folk
    4             dance
                ...    
    61248           rnb
    61249    electronic
    61250    industrial
    61251          rock
    61252       country
    Name: genre, Length: 61253, dtype: object




```python
# Checking for duplicates
all_genres=df['genre'].sort_values().unique()
all_genres
```




    array(['acid', 'acoustic', 'action', 'adult', 'africa', 'afrikaans',
           'alternative', 'alternativepunk', 'ambient', 'americana',
           'animated', 'anime', 'arabesk', 'arabic', 'arena',
           'argentinetango', 'art', 'audiobook', 'author', 'avantgarde',
           'axé', 'baile', 'balkan', 'beats', 'bigroom', 'black', 'bluegrass',
           'blues', 'bollywood', 'bossa', 'brazilian', 'breakbeat', 'breaks',
           'broadway', 'cantautori', 'cantopop', 'canzone', 'caribbean',
           'caucasian', 'celtic', 'chamber', 'chanson', 'children', 'chill',
           'chinese', 'choral', 'christian', 'christmas', 'classical',
           'classicmetal', 'club', 'colombian', 'comedy', 'conjazz',
           'contemporary', 'country', 'cuban', 'dance', 'dancehall',
           'dancepop', 'dark', 'death', 'deep', 'deutschrock', 'deutschspr',
           'dirty', 'disco', 'dnb', 'documentary', 'downbeat', 'downtempo',
           'drum', 'dub', 'dubstep', 'eastern', 'easy', 'electronic',
           'electropop', 'emo', 'entehno', 'epicmetal', 'estrada', 'ethnic',
           'eurofolk', 'european', 'experimental', 'extrememetal', 'fado',
           'fairytail', 'film', 'fitness', 'flamenco', 'folk', 'folklore',
           'folkmetal', 'folkrock', 'folktronica', 'forró', 'frankreich',
           'französisch', 'french', 'funk', 'future', 'gangsta', 'garage',
           'german', 'ghazal', 'gitarre', 'glitch', 'gospel', 'gothic',
           'grime', 'grunge', 'gypsy', 'handsup', "hard'n'heavy", 'hardcore',
           'hardstyle', 'hardtechno', 'hiphop', 'historisch', 'holiday',
           'horror', 'house', 'hymn', 'idm', 'independent', 'indian', 'indie',
           'indipop', 'industrial', 'inspirational', 'instrumental',
           'international', 'irish', 'jam', 'japanese', 'jazz', 'jewish',
           'jpop', 'jungle', 'k-pop', 'karadeniz', 'karaoke', 'kayokyoku',
           'korean', 'laiko', 'latin', 'latino', 'leftfield', 'local',
           'lounge', 'loungeelectronic', 'lovers', 'malaysian', 'mandopop',
           'marschmusik', 'meditative', 'mediterranean', 'melodic', 'metal',
           'metalcore', 'mexican', 'middle', 'minimal', 'miscellaneous',
           'modern', 'mood', 'mpb', 'muslim', 'native', 'neoklassik', 'neue',
           'new', 'newage', 'newwave', 'nu', 'nujazz', 'numetal', 'oceania',
           'old', 'opera', 'orchestral', 'other', 'piano', 'podcasts', 'pop',
           'popdance', 'popelectronic', 'popeurodance', 'poprussian', 'post',
           'posthardcore', 'postrock', 'power', 'progmetal', 'progressive',
           'psychedelic', 'punjabi', 'punk', 'quebecois', 'ragga', 'ram',
           'rancheras', 'rap', 'rave', 'reggae', 'reggaeton', 'regional',
           'relax', 'religious', 'retro', 'rhythm', 'rnb', 'rnr', 'rock',
           'rockabilly', 'rockalternative', 'rockindie', 'rockother',
           'romance', 'roots', 'ruspop', 'rusrap', 'rusrock', 'russian',
           'salsa', 'samba', 'scenic', 'schlager', 'self', 'sertanejo',
           'shanson', 'shoegazing', 'showtunes', 'singer', 'ska', 'skarock',
           'slow', 'smooth', 'soft', 'soul', 'soulful', 'sound', 'soundtrack',
           'southern', 'specialty', 'speech', 'spiritual', 'sport',
           'stonerrock', 'surf', 'swing', 'synthpop', 'synthrock',
           'sängerportrait', 'tango', 'tanzorchester', 'taraftar', 'tatar',
           'tech', 'techno', 'teen', 'thrash', 'top', 'traditional',
           'tradjazz', 'trance', 'tribal', 'trip', 'triphop', 'tropical',
           'türk', 'türkçe', 'ukrrock', 'unknown', 'urban', 'uzbek',
           'variété', 'vi', 'videogame', 'vocal', 'western', 'world',
           'worldbeat', 'ïîï'], dtype=object)



**Conclusions**

Preprocessing found three problems in the data:

- violations in the style of headlines,
- missing values,
- duplicates — obvious and other.

We have corrected the headers to simplify working with the table. Without duplicates, the study will become more accurate.

We replaced the missing values with `'unknown'`. It remains to be seen whether omissions in the `genre` column will damage the research.

Now we can proceed to hypothesis testing.

## Hypothesis testing

### Comparison of user behavior of two capitals

The first hypothesis states that users listen to music differently in Moscow and St. Petersburg. Let's check this assumption based on data on three days of the week — Monday, Wednesday and Friday. For this:

* We will divide the users of Moscow and St. Petersburg
* Compare how many tracks each user group listened to on Monday, Wednesday and Friday.


```python
# Counting auditions in each city
df.groupby('city')['city'].count()
```




    city
    Moscow              42741
    Saint-Petersburg    18512
    Name: city, dtype: int64



There are more auditions in Moscow than in St. Petersburg. This does not mean that Moscow users listen to music more often. It's just that there are more users in Moscow.

Now let's group the data by day of the week and count the auditions on Monday, Wednesday and Friday. Please note that the data contains information only about the auditions for these days only.


```python
# Counting auditions on each of the three days
df.groupby('day')['day'].count()
```




    day
    Friday       21840
    Monday       21354
    Wednesday    18059
    Name: day, dtype: int64



On average, users from two cities are less active on Wednesdays. But the picture may change if we consider each city separately.

Let's create a function `number_tracks()`, which will count auditions for a given day and city. We will need two parameters:
* day of the week,
* name of the city.


```python
def number_tracks(day,city):
    track_list=df[df['day']==day]
    track_list=track_list[track_list['city']==city]
    track_list_count=track_list['user_id'].count()
    return track_list_count
```


```python
# number of auditions in Moscow on Mondays
number_tracks('Monday','Moscow')
```




    15740




```python
# number of auditions in St. Petersburg on Mondays
number_tracks('Monday','Saint-Petersburg')
```




    5614




```python
# number of auditions in Moscow on Wednesdays
number_tracks('Wednesday','Moscow')
```




    11056




```python
# number of auditions in St. Petersburg on Wednesdays
number_tracks('Wednesday','Saint-Petersburg')
```




    7003




```python
# number of auditions in Moscow on Fridays
number_tracks('Friday','Moscow')
```




    15945




```python
# number of auditions in St. Petersburg on Fridays
number_tracks('Friday','Saint-Petersburg')
```




    5895




```python
# Таблица с результатами
columns_names = ['city', 'monday', 'wednesday', 'friday']
counts = [
    ['Moscow', 15740, 11056, 15945],
    ['Saint-Petersburg', 5614, 7003, 5895]
]

table = pd.DataFrame(data = counts, columns = columns_names)
table
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
      <th>city</th>
      <th>monday</th>
      <th>wednesday</th>
      <th>friday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Moscow</td>
      <td>15740</td>
      <td>11056</td>
      <td>15945</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Saint-Petersburg</td>
      <td>5614</td>
      <td>7003</td>
      <td>5895</td>
    </tr>
  </tbody>
</table>
</div>



**Conclusions**

The data shows the difference in user behavior:

- In Moscow, the peak of auditions falls on Monday and Friday, and on Wednesday there is a noticeable decline.
- In St. Petersburg, on the contrary, they listen to music more on Wednesdays. Activity on Monday and Friday here is almost equally inferior to Wednesday.

So, the data indicate theсvalidity of the first hypothesis.

### Music at the beginning and end of the week

According to the second hypothesis, some genres prevail in Moscow on Monday morning, and others in St. Petersburg. Similarly, on Friday evening, different genres prevail — depending on the city.


```python
# getting the moscow_general table from the rows of the df table
moscow_general = df[df['city'] == 'Moscow']
```


```python
# getting the spb_general table from the rows of the df table
spb_general = df[df['city'] == 'Saint-Petersburg']
```

Let's create the `genre_weekday()` function with four parameters:
* table (dataframe) with data,
* day of the week,
* initial timestamp in the format 'hh:mm',
* the last timestamp in the format 'hh:mm'.

The function will return information about the top 10 genres of those tracks that were listened to on the specified day, in the interval between two timestamps.


```python
def genre_weekday(table, day, time1, time2):
    genre_df = table[table['day'] == day]
    genre_df = genre_df[genre_df['time'] > time1]
    genre_df = genre_df[genre_df['time'] < time2]
    genre_df_count = genre_df.groupby('genre')['genre'].count()
    genre_df_sorted = genre_df_count.sort_values(ascending=False)
    return genre_df_sorted.head(10)
```

Let's compare the results of the `genre_weekday()` function for Moscow and St. Petersburg on Monday morning (from 7:00 to 11:00) and Friday evening (from 17:00 to 23:00):


```python
genre_weekday(moscow_general, 'Monday', '07:00', '11:00')
```




    genre
    pop            781
    electronic     762
    dance          549
    rock           474
    ruspop         186
    world          181
    rusrap         175
    alternative    164
    unknown        161
    classical      157
    Name: genre, dtype: int64




```python
genre_weekday(spb_general, 'Monday', '07:00', '11:00')
```




    genre
    electronic     226
    pop            218
    dance          182
    rock           162
    ruspop          64
    alternative     58
    rusrap          55
    jazz            44
    classical       40
    world           36
    Name: genre, dtype: int64




```python
genre_weekday(moscow_general, 'Friday', '17:00', '23:00')
```




    genre
    electronic     749
    pop            713
    rock           517
    dance          495
    world          208
    ruspop         170
    alternative    163
    classical      163
    rusrap         142
    jazz           111
    Name: genre, dtype: int64




```python
genre_weekday(spb_general, 'Friday', '17:00', '23:00')
```




    genre
    electronic     310
    pop            256
    rock           216
    dance          210
    alternative     63
    jazz            61
    classical       60
    rusrap          59
    world           54
    unknown         47
    Name: genre, dtype: int64



**Conclusions**

If we compare the top 10 genres on Monday morning, we can make the following conclusions:

1. In Moscow and St. Petersburg, people listen to similar music. The only difference is that the jazz entered the St. Petersburg rating.


2. In Moscow, there were so many missing values that the value `'unknown'` took the ninth place among the most popular genres. This means that the missing values take up a significant part of the data and threaten the validity of the research.

Friday night doesn't change that picture. Some genres rise a little higher, others go down, but overall the top 10 remains the same.

Thus, the second hypothesis was only partially confirmed:
* Users listen to similar music at the beginning of the week and at the end.
* The difference between Moscow and St. Petersburg is not too obvious.

However, omissions in the data cast doubt on this result. There are so many of them in Moscow that the top-10 rating could look different if not for the lost data on genres.

### Genre preferences in Moscow and St. Petersburg

Hypothesis: St. Petersburg is the capital of rap, music of this genre is listened to more often than in Moscow. And Moscow is a city of contrasts, in which, nevertheless, pop music prevails.


```python
moscow_genres = moscow_general.groupby('genre')['genre'].count().sort_values(ascending=False)
```


```python
# first 10 lines of moscow_genres
moscow_genres.head(10)
```




    genre
    pop            5892
    electronic     5829
    dance          4435
    rock           3965
    classical      1616
    world          1432
    alternative    1379
    ruspop         1372
    rusrap         1161
    jazz            980
    Name: genre, dtype: int64




```python
spb_genres = spb_general.groupby('genre')['genre'].count().sort_values(ascending=False)
```


```python
# first 10 lines of spb_genres
spb_genres.head(10)
```




    genre
    electronic     2671
    pop            2431
    dance          1932
    rock           1879
    alternative     649
    classical       646
    rusrap          564
    ruspop          538
    world           515
    jazz            486
    Name: genre, dtype: int64



**Conclusions**

The hypothesis was partially confirmed:
* Pop music is the most popular genre in Moscow, as the hypothesis suggested. Moreover, in the top 10 genres there is a similar genre - Russian popular music.
* Contrary to expectations, rap is about equally popular in Moscow and St. Petersburg.

## Results of the research

We tested three hypotheses and established:

1. The day of the week has different effects on user activity in Moscow and St. Petersburg.

The first hypothesis was fully confirmed.

2. Musical preferences do not change much during the week — be it Moscow or St. Petersburg. Small differences are noticeable at the beginning of the week, on Mondays.

Thus, the second hypothesis was only partially confirmed. This result could have been different if not for the omissions in the data.

3. There are more similarities than differences in the tastes of users in Moscow and St. Petersburg. Contrary to expectations, genre preferences in St. Petersburg resemble those in Moscow.

The third hypothesis was not confirmed. If there are differences in preferences, they are invisible to the majority of users.
