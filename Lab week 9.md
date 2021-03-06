Lab Week 9

> 19/20

## Problem Set 1

1)	Is North America currently (i.e., in the present) to the West or East of its position in the Cretaceous?
#North America is currently west of its Cretaceous position.

2) Look at the following line of code that you used before.

````R
plot(ModernMap,col=rgb(1,0,0,0.33),lty=0,add=TRUE)
Describe what this code is doing. A good answer will describe what each of the plot( ) function arguments is doing - i.e., what is the meaning of col=, lty= and add=. As well, what does the rgb( ) function do? What does it mean? Use google or the R help( ) function.
#This code plots a map of modern continents. “col=” designates the color of the map, and the rgb() function specifies the intensity of red, green, and blue so in this case, the map is completely red and the fourth value corresponds to transparency. “lty=” designates the line type for the shape outlines. “add=TRUE” makes this plot superimposed on the Cretaceous map.
````

2)	Download a map of the middle Cretaceous (Albian Epochs ~110 mys ago). Name it AlbianMap. 

```R
> AlbianMap<-downloadPaleogeography(Age=110)
````

4) Add AlbianMap to the plot you made earlier. The added continents should be colored green, and use the same level of opacity (translucence) as your CretaceousMap and ModernMap. Show your code!

````R
> plot(AlbianMap,col=rgb(0,1,0,0.33),lty=0,add=TRUE
````

5) Has there been more movement north and south or east and west in the Eastern Hemisphere since the Albian?

#There has been southward movement in the Eastern Hemisphere since the Albian.

> Really? Most people (me included) said north? India and Australia both move North, for example.

6) Has there been more movement north and south or east and west in the Western hemisphere since the Albian?

#There has been westward movement in the Western Hemisphere since the Albian


## Problem Set 2

1)	Download and plot a new map of the Paleocene/Eocene boundary (Use google to find the age of this boundary, remember the downloadMap( ) function only takes whole numbers). You may use any color and level of opacity. Show your code.

````R
> PaleoceneMap<-downloadPaleogeography(Age=56)
>plot(PaleoceneMap,col=rgb(0.5,0,0.5,0.33),lty=0,add=TRUE)
````

2) Download a dataset of Anthozoan occurrences from the paleobiology database ranging from the Paleocene through Eocene. Consult with previous labs if you do not remember how to do this. Show your code.

````R
>DataPBDB<-downloadPBDB(Taxa=c("Anthozoa"), StartInterval="Paleocene", StopInterval="Eocene")
````

3) How many occurences did you download?

````R
> nrow(DataPBDB)
[1] 2847
````

4) What are the names of columns of the PBDB data matrix you just downloaded. What does each column mean? If you do not know, consult with the API documentation. 

````R
> colnames(DataPBDB)
+ occurrence_no: number associated with the occurrence
+ record_type: 
+ reid_no: unique identifier for an occurrence that has been reidentified
+ flags: will have an R in this field if the occurrence has a more recent identification    
+ collection_no: identifier for the collection an occurrence is from
+ identified_name: taxonomic name for the occurrence
+ identified_rank: taxonomic rank of identified occurrence
+ identified_no: unique identifier for the taxonomic name
+ difference: gives reason for discrepancies in identified and accepted name
+ accepted_name: accepted taxonomic name for the identified name
+ accepted_rank: taxonomic rank of accepted name
+ accepted_no: unique identifier of taxonomic name 
+early_interval: geologic time range for earliest time for the occurrence (not necessarily the early interval specified)
+ late_interval: geologic time range for earliest time for the occurrence (not necessarily the early interval specified)
+ max_ma: early bound of geologic time in Ma
+ min_ma: late bound of geologic time in Ma
+ reference_no: identifier for reference that the occurrence was entered
+ paleomodel: model specified by “pgm”
+ paleolng: longitude occurrence was collected 
+ paleolat: latitude occurrence was collected
+ geoplate: geological plate identifier
+ phylum: phylum occurrence belongs to 
+ class: class occurrence belongs to
+ order: order occurrence belongs to
+ family: family occurrence belongs to        
+ genus: genus occurrence belongs to
````

5) Use the points( ) function to plot each occurrence on the map you made previously (make sure to use the paleolatitude and paleolongitude coordinates). Show your code. If you do not know how to use the points( ) function, consult the help file or use Google.

````R
> plot(PaleoceneMap,col=rgb(0.5,0,0.5,0.33),lty=0)
> EoceneMap<-downloadPaleogeography(Age=34)
> plot(EoceneMap,col=rgb(0,0.5,0,0.33),lty=0, add=TRUE)
> points(DataPBDB[,"paleolng"], DataPBDB[,"paleolat"]) 
````

6) Where are most of the Anthozoan occurrences in the Eastern Hemisphere (i.e., what region of the world)? Are Anthozoans primarily marine or freshwater organisms? What can you infer must have existed in this region of the world during this time?

The most occurrences are in south and southeastern Europe. Anthozoans are marine organisms so there must have been reef and salt water conditions in this area.

> An epicontinental sea!

## Problem Set 3
1)	Download a dataset of Perissodactyla occurrences from the PBDB that span the Paleogene. Show your code.

````R
> DataPBDB<-downloadPBDB(Taxa=c("Perissodactyla"), StartInterval="Paleogene", StopInterval="Paleogene")
````

2)	What is the defining attribute of Perissodactyla? What are some prominent examples (e.g., lions, tigers, bears, oh my!)? [Hint: Neither lions, nor tigers, nor bears are members of Perissodactyla.]

Perissodactyla are odd-toed ungulates. Examples are zebras, rhinoceroses, and horses.

3)	Find collection number 112723 in the dataset you just downloaded in Question 1. Show your code.

````R
> subset(DataPBDB, collection_no==112723)
````

4)	What "geoplate" id (tectonic plate) is associated with this collection? What modern day region of the world does this geoplate id correspond to? The remaining questions will refer to this geoplate/region as region-X.

The geoplate is number 501 which corresponds to the Ghazij Formation in Pakistan.

> Not exactly. Geoplates are tectonic plates, not geological formations. So 501 just means Pakistan, not specifically the Ghazij Formation. Talk to me about this if you don't understand. It's kind of an important point.

5)	Subset your dataset of Perissodactyla occurrences to only include occurrences that occur in region-X. How many occurrences are there? Show your code.

````R
> Geoplate<- subset(DataPBDB, geoplate=501)
````

6)	Using the maps we have created previously, making your own new maps, or using the Paleobiology Database Navigator tool, what is the general history of region-X from the Albian through to the present day?

````R
> plot(AlbianMap,col=rgb(0,1,0,0.33),lty=0)
> plot(ModernMap,col=rgb(1,0,0,0.33),lty=0,add=TRUE)
#Region-X has moved southwest from the Albian to modern day.
````

> It has definitely moved North! India has slammed into Eurasia and created the Himalayas! -1 Points

7) There are also many Paleogene occurrences of Perissodactyla in present day China. Using the maps we have created previously, making your own new maps, or using the Paleobiology Navigator tool, evaluate the plausibility of each of the following scenarios? Thoroughly explain your reasoning and how you tested your ideas.

+ Species of Perissodactyla migrated from region-X to China during the Paleogene?
+ Species of Perissodactyla migrated from China to region-X during the Paleogene?
+ The species of Perissodactyla in China and region-X are unrelated and probably both came from a third region? 

````R
> PaleogeneMap<-downloadPaleogeography(Age=23)
> plot(PaleogeneMap,col=rgb(0,0,1,0.33),lty=0,add=TRUE)
````

During the Paleogene, Region-X (Pakistan, India, Afghanistan) separated from the main continent of modern-day Asia compared to the Albian map. Since Perissodactyla cannot swim for long distances it is unlikely that they were able to migrate to modern-day China from the separated landmass they existed on during the Albian. There is a strip of land on the east that connects the separated part with the mainland, but it is far enough away that is is unlikely any Perissodactyla migrated through. So the species in China and Region-X are probably from a different region and are unrelated. 
