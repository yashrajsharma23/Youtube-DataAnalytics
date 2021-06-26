# Youtube-DataAnalytics

##Abstract
Analytics is the way to find the trends & information from data. Data analytics is a discipline focused on extracting insights from data. It comprises the processes, tools and techniques of data analysis and management, including the collection, organization, and storage of data. Here we will extract the detailed information of all the Youtube video Ids and did furthermore analysis.

##1.0 Data Collection
	
	- At first collected csv dataset having 3 features/columns & 25,623 observations. 3 columns include “youtubeId, movieId, and title”. So, using the youtubeId I extracted the detailed data of all the videos i.e: title, description, 100 comments, like count, dislike count, view count, comment count, duration, and favourite count. To extract all these details I used Google Cloud console by enabling Youtube Data API v3, created service account & OAuth 2.0 Client IDs. After creating service account used .json credential file which is authentication procedure to use Youtube Data v3 API in project.
	- Used Jupyter local Python notebook, installed libraries; pandas, apiclient.discovery, oauth2client.service to extract all the detail data of each videos.
	- Used Google Cloud API Keys to fetch the youtube comments & used .json credentials service to extract; title, description, like count, dislike count, view count, duration, favourite count & comment count.
	- After completing all the initialization of services, I used async IO method to fetch all the record in background thread. Created 3 custom functions; 

1.RemoveExtractedData()
- This function remove the already extracted data using drop function & passes the filtered dataframe that are still remaining to extract the data.

2.getYoutubeData()
- This function create small task of 50 batch size as Youtube API only limits 50 Ids at once to fetch the data. As our fetchingData() is async function so batch task will be stored in list &  call “await asyncio.wait(tasks)” this will execute all the list of stored task each with 50 batch size to parse it to Youtube API & extract the expected data & it will store all the extracted data to csv file & save or append it as per needed.

3.fetchingData()
- This function will take all the 50 batch size task sequentially and parse the required data from the Youtube API response & save it to dataframe.

![image](https://user-images.githubusercontent.com/39268487/123518010-ba720980-d6c1-11eb-87fd-219a798b5745.png)
Fig: Extracted Youtube dataset

##2.0     Data Cleansing

	- Using pandas “read_csv” method fetched the saved extracted data and did below basic data cleansing steps;
###1.Drop unwanted columns
- Dropped “Unnamed 0” column as it was created at the time of extraction and it is of no use.

###2.Drop duplicates
- There may be chances of same Youtube Ids got fetched multiple times, so it is important to drop those observations

###3.Converting datatype
- Like, dislike, comment, view, and faviourite count was stored in Object datatype so converted these features in Integer datatype so we can do further statistical analysis on these columns.

![image](https://user-images.githubusercontent.com/39268487/123518027-ca89e900-d6c1-11eb-9570-ef4dda0a17f6.png)
Fig: Converting datatype

##3.0     Visualization


##3.1 Top & Bottom Viewed Videos
	###A) Top 10 viewed videos:
	1.John Legend - All of Me (Official Video)
	2. Fresh Guacamole by PES | Oscar Nominated Short
	3. Unfaithful (2002) - The Other Woman Scene (1/3) | Movieclips
	4. Britney Spears - Ooh La La (From The Smurfs 2)
	5. Beastie Boys - Sabotage
	6. ILO ILO ??????????????? Official Trailer
	7. Growth Trailer
	8. Transformers 3 Dark of the Moon Teaser Trailer - Official (HD)
	9. Disney's Frozen Fever Trailer
	10 .Don {HD} - Amitabh Bachchan - Zeenat Aman - Superhit Old Hindi Movie - (With Eng Subtitles)
![image](https://user-images.githubusercontent.com/39268487/123518038-d9709b80-d6c1-11eb-98dd-4d0119874e6b.png)
Fig: Top 10 viewed videos


###B)Bottom 10 viewed videos:
1.Spring Fever
2.Black Fury
3.Okie Noodling
4.Ballad of Cable Hogue - Trailer
5.Who's the Caboose
6.The Ballad Of Nessie
7.Behold A Pale Horse
8.The End Of The Affair (1955)
9.Houseguest
10.Born Reckless

![image](https://user-images.githubusercontent.com/39268487/123518047-e097a980-d6c1-11eb-8fd0-52524b8090a0.png)
Fig: Bottom 10 Viewed Videos



##3.2 Most & Least Liked Videos

###A)Top 10 liked videos
1.John Legend - All of Me (Official Video)
2.Fresh Guacamole by PES | Oscar Nominated Short
3.Britney Spears - Ooh La La (From The Smurfs 2)
4.The Fault In Our Stars | Official Trailer [HD] | 20th Century FOX
5.Beastie Boys - Sabotage
6.Kiwi!
7.The Horribly Slow Murderer with the Extremely Inefficient Weapon by Richard Gale
8.POWER/RANGERS UNAUTHORIZED  [BOOTLEG UNIVERSE]
9.Too Many Cooks | Adult Swim
10.THE PUNISHER: DIRTY LAUNDRY [BOOTLEG UNIVERSE]

![image](https://user-images.githubusercontent.com/39268487/123518052-e8efe480-d6c1-11eb-97ac-ec03e9040c27.png)
Fig: Top 10 liked videos

###B)Bottom 5 liked videos
1.48 Hrs. - Trailer
2.Happiness - Trailer
3.Virginia City - Trailer
4.A Piece of the Action - Trailer
5.Unhook the Stars - Trailer
![image](https://user-images.githubusercontent.com/39268487/123518069-f4431000-d6c1-11eb-8113-a1cc0932697b.png)
Fig: Bottom 5 liked videos


##2.3 Highest Duration Video

###Top 5 highest duration videos are;
1.Trailer for "Getting to Know You”
2.The Century of the Self (Full Documentary)
3.The best of youth (trailer)
4.Peter Brook - Mahabharata 1
5.Kevin Smith: Too Fat for 40

##2.4 Highest Positive Sentiment Scored Videos
		Top 5 highest duration videos are;
1.How to Pickup Using the Theory of Relativity!
2.Passengers Trailer
3.Scaramouche (1952) Official Trailer - Stewart Granger, Janet Leigh Swashbuckler Movie HD
4.“NEVER ON SUNDAY" TRAILER
5.Man's favorite sport
6.Wild Child Trailer
7.Revolutionary Road, Leonardo DiCaprio and Kate Winslet together again!
8.Constantine's Sword Trailer
9.WAR OF THE WORLDS 2: THE NEXT WAVE
10.5 Centimeters Per Second Trailer

![image](https://user-images.githubusercontent.com/39268487/123518082-fc9b4b00-d6c1-11eb-867b-f2078499ec91.png)

![image](https://user-images.githubusercontent.com/39268487/123518085-fefda500-d6c1-11eb-9de0-72f9ced6768c.png)
Fig: Top 10 Highest Sentiment Scored Videos

