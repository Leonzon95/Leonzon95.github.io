---
layout: post
title:      "CLI Project"
date:       2020-05-31 22:39:24 +0000
permalink:  cli_project
---


For my first project I made a CLI application that can tell you different facts about  characters, episodes and locations of the TV show: Rick and Morty. It calls on an API abuot Rick and Morty and sets different objects for each character, episode and location. To do this I had to make different classes for each one, and design the relationship between the objects. I first called on the episodes and locations information to later be able to initialize characters with locations and episodes.
In the character class I made a custom setter `episode =(argument)` and a `origin =(argument)`, these methods take in a url, get the id of the instance, searches for the that particular instance in the episode or location class, and finally, adds it to an instance variable in that character instance.

```
def episode=(url_array)
        episode_array = url_array.collect do |episode_url|
            array = episode_url.split("/")
            last_peice = array[-1].to_i
            episode_obj = Episode.all.detect {|episode| episode.id == last_peice}
            episode_obj
        end
        @episode = episode_array
    end

    def origin=(url)
            array = url.split("/")
            last_peice = array[-1].to_i
            location_obj = Location.all.detect {|episode| episode.id == last_peice}
            @origin = location_obj
    end
```

In the location and episode classes I made a  `characters`  method in the episode class and `residents` method in the location class . These are very similar. This method looks through all of the characters, checks thorugh the characters episodes or origin, and if instance the method is being called on matches with on of the characters attributes instances, they get displayed. 

```
def characters
        character_array = []
        Character.all.each do |character|
            character.episode.each do |episode_char|
                if episode_char == self
                    character_array << character
                end
            end
        end
        character_array
    end
		
		def residents
        resident_array = Character.all.select{|resident| resident.origin == self}
        resident_array
    end
```

This way only the character class keeps track of the relationship and the rest just check to see if they match with a certain character. It keeps it simpler and less likely to get realationship related bugs.
