---
title: Maps
layout: default
nav_order: 2
---
# Maps

Player create maps using [Azgaar's Fantasy Map Generator](https://azgaar.github.io/Fantasy-Map-Generator/). These are then downloaded as a JSON file and imported into the games map folder. The game will then read the JSON file and create a map object. The game world is then created from the map object.

## Azgaar's Fantasy Map Generator

Azgaar's Fantasy Map Generator is a free open source tool for generating fantasy maps. It's a web based tool to create a map and then downloaded as a JSON file using the full setting. The player then adds json to the maps folder so it can be available for starting a new game.

## Map Object

The map object is then analyzed and procedurally generated components are then added before saving the map for game play.

### Locations

The following rules are for determining locations:

#### Burgs

1. Determine population for all burgs.
   1. get largest and smallest population.
   2. Subtract the smallest from every city.
   3. Multiply max population by 3.
   4. Divide the smallest by 3.
   5. subtract the adjusted min from the adjusted max.
   6. spin through all burgs and adjust population based on the adjusted min and max.
2. Identify City of Light:
   1. Find the largest capitol city.
   2. Increase the size of the city 3x.
   3. Mark the city as the City of Light.
3. Determine burg size for all burgs.
   - hamlet = 0 > 100
   - village = 100 > 1000
   - town = 1000 > 5000
   - city = 5000 > 25000
   - metropolis = 25000 > 100000
   - megalopolis = 100000+  
4. Based on size determine number of quality slots using fibonacci sequence.
   - hamlet
     - 1 common
   - village
     - 2 common
     - 1 uncommon
   - town = 3
     - 3 common
     - 2 uncommon
     - 1 rare
   - city = 4
     - 5 common
     - 3 uncommon
     - 2 rare
     - 1 epic
   - metropolis = 5
     - 8 common
     - 5 uncommon
     - 3 rare
     - 2 epic
     - 1 legendary
   - megalopolis = 6
     - 13 common
     - 8 uncommon
     - 5 rare
     - 3 epic
     - 2 legendary
5. Based on burg properties determine common locations that need added first in priority order. Property specific locations will have priority over other common locations.
    - Port, if port property is true then add port location. The port will be a different size based on the burg size.
      - hamlet = pier
      - village = dock
      - town = harbor
      - city = port
      - metropolis = port
    - Temple, if temple property is true then add temple location. The temple will be a different size based on the burg size.
      - hamlet = shrine
      - village = shrine
      - town = temple
      - city = temple
      - metropolis = temple
    - Always required in order
      1. tavern
      2. inn
      3. general store

6. After slots and required locations done then randomly add remaining locations for each remaining slot. Rules determine if selection is valid for the given slot. If a valid location is not found then try again. Rules to consider:
   1. Some locations do not allow multiples
   2. Some locations require a specific property
   3. Some locations require a specific burg size
   4. If a location with a lower base quality gets selected for a higher quality slot then add location with a higher quality equal to the difference. The difference mist be no more than 2 levels lower than the slot otherwise reject the selection.
