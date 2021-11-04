![image](https://user-images.githubusercontent.com/66803124/120327249-66c8f780-c29e-11eb-9a43-026227ff6877.png)

# Fermi Paradox

The idea that we are not alone in the universe has excited and frightened sceintist and earthly other inhabitants for centuries. Yes, the chances of life occuring on Earth are slim, in fact two well known scientists calculated the odds of life forming by natural processes. They estimated that there is less than 1 chance in 10 to the 40,000power that life could have originated by random trials. 10 to the 40,000power is a 1 with 40,000 zeros after it!

```
- "...life cannot have had a random beginning...The trouble is that there are about two thousand enzymes, and the 
chance of obtaining them all in a random trial is only one part in 10 to the 40,000power, an outrageously small 
probability that could not be faced even if the whole universe consisted of organic soup. If one is not prejudiced 
either by social beliefs or by a scientific training into the conviction that life originated on the Earth, this 
simple calculation wipes the idea entirely out of court....The enormous information content of even the simplest 
living systems...cannot in our view be generated by what are often called "natural" processes...For life to have 
originated on the Earth it would be necessary that quite explicit instruction should have been provided for its 
assembly...There is no way in which we can expect to avoid the need for information, no way in which we can simply 
get by with a bigger and better organic soup, as we ourselves hoped might be possible a year or two ago."

Fred Hoyle and N. Chandra Wickramasinghe,

Evolution from Space [Aldine House, 33 Welbeck Street, London W1M 8LX:J.M. Dent & Sons, 1981), p. 148, 24,150,30,31).
```
Though this may seem impossible to replicate, the universe's size is nearly beyond comprehension. Not only is our galaxy immense, but so are the perhaps infinite others that make up our universe. When looked at on this scale, the chances of life are much more probable. 

![image](https://user-images.githubusercontent.com/66803124/120330082-51090180-c2a1-11eb-9921-16f466cbbf21.png)

Drake's Equation is a probabilistic argument used to estimate the number of active, communicative extraterrestrial civilizations in the Milky Way galaxy. The equation looks at the  galaxy currently producing electromagnetic emissions, such as radio waves. 

The equation has been updated to account for the 2017 exoplanet discoveries made by NASA's Kepler satelite.

![image](https://user-images.githubusercontent.com/66803124/120327170-51ec6400-c29e-11eb-8529-2407bd20afbe.png)

This is where it gets interesting. 

For humanity to be the first and only technologically advanced species, the probability of an advanced civilization developing on a habitable alien planet would have to be less than 1 in 10 billion trillion! And yet, as Nobel Prize–winning physicist Enrico Fermi famously observed,  “Where is everybody?”

That is the problem we are looking at today. We are going to simulate this theory in the Milky Way Galaxy using Drake's Equation and Fermi's Paradox as an underlying current pushing us towards discovery. 

![image](https://user-images.githubusercontent.com/66803124/120471546-b02a4d00-c359-11eb-9c7f-b6e18622ddbd.png)

# THE STRATEGY
Here are the steps needed to complete this project:
1. Estimate the number of transmitting civilizations using the Drake equation.
2. Choose a size range for their radio bubbles.
3. Generate a formula for estimating the probability of one civilization detecting another.
4. Build a graphical model of the galaxy and post Earth’s radio emissions bubble.
In order to keep the description close to the code, each of these tasks will be described in
detail in its own section. Note that the first two steps don’t require the use of Python.

![image](https://user-images.githubusercontent.com/66803124/120471280-5fb2ef80-c359-11eb-9adc-a22342abb5f5.png)

First, we will model the Milky Way Galaxy in 2D so we can have perspective for the rest of the project. 

![image](https://user-images.githubusercontent.com/66803124/120471229-532e9700-c359-11eb-8ab1-3fbb931f436d.png)

You can find the full code in  Jupyter Notebook within the files but here is how I got started:

VOLUMES = 1000 
number of locations in which to place civilizations (Cubes)

MAX_CIVS = 5000 
maximum number of advanced civilizations 
(We aren't going to start off looking at 5,000, starting at 2 civilizations and randomly assign them to one of the locations)

TRIALS = 1000 
# number of times to model a given number of civilizations
# (In order to come up with a probability that makes sense)
CIV_STEP_SIZE = 100 
# civilizations count step size
# (Since we start at 2, we step up by 100 each time to try and limit the amount of time/memory usage.) 
# Step 1: 2 and run 1,000 times, Step 2: 102 etc.
In [29]:
x = [] 
# x values for polynomial fit 
# Civilizations per volume (Step 1: x = 2 / 1000) .002 which makes it very unlikely that they will be sharing the same cube (detectable). 
y = [] 
# y values for polynomial fit
# After we randomly assigning the civilization to locations 1,000 times, 
# we will know the probability of the civilizations being able to detect one another.
In [30]:
for num_civs in range(2, MAX_CIVS + 2, CIV_STEP_SIZE):
# Need to start at 2 because if there was 1, there would be ZERO probability of detection. 
    number_of_single_civs = 0
    civs_per_volume = num_civs / VOLUMES
    for trial in range(TRIALS):
        locations = []
        while len(locations) < num_civs:
            # Keep adding to locations until it is equal to the num_civs we have. 
            # If we are testing 102 civilizations, we only want there to be 102 possible locations.
            location = randint(1, VOLUMES)
            locations.append(location)
            # Append the location to the locations list, keep adding so long as the # is less than num_civs. 
        overlap_count = Counter(locations)
        count_of_values = Counter(overlap_count.values())
        number_of_single_civs = number_of_single_civs + count_of_values[1]
#         if num_civs == 102:
#             print("trial " + str(trial) + ": " + str(locations) + "\n" + str(overlap_count))
#             print("Occurences: " + str(count_of_values))
#             print("Number of Single Civilizations: " + str(count_of_values[1]))
#             print("Probability of Single: " + str(count_of_values[1]/num_civs))
#             single_prob = count_of_values[1]/num_civs
#             detect_prob = 1 - single_prob 
#             print("Probability of Detection: " + str(detect_prob))
#             print()
    detection_prob = 1 - (number_of_single_civs/(num_civs * TRIALS))
#     print("Civilizations per Volume: " + str(civs_per_volume))
#     print("Probability of Detection/Probability of 2 or more civilizations in one location: " + str(detection_prob))
#     print(num_civs)
#     print()
    x.append(civs_per_volume)
    y.append(detection_prob)
# for x, y in zip(x, y):
#     print(x, y)
