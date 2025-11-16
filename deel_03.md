## Part 3: Creating a PMTiles Extract of Dundee

For this workshop, we want to host the map data ourselves. A PMTiles file with map data of the entire world is approximately 120GB. That's too much to deploy with GitHub, and we're not interested in the entire world, only the area around Dundee.

In this part, we're therefore going to create an extract of the PMTiles file that Protomaps makes available.

---

The PMTiles CLI (command line interface) is already installed in your development environment.

- [ ] Look up the documentation for the PMTiles CLI, read the documentation for [`pmtiles extract`](https://docs.protomaps.com/pmtiles/cli#extract).

As you can see, you need the bbox of Dundee.

---

- [ ] Find out what the bbox of Dundee is.

There are many roads that lead to Rome (or Dundee).

You can, for example, look up the [OSM relation](https://www.openstreetmap.org/relation/418758) and use the following [Overpass query](https://overpass-ultra.trailsta.sh/):
```
[out:json];
rel(334228);
out bb;
```

You can also use the website http://bboxfinder.com/ (there is no https), zoom to Dundee, set the EPSG code to 4326 (instead of 3857), click the square icon, draw a bbox and copy it in the "lon,lat,lon,lat" order.

---

- [ ] Find out what the latest URL is from Protomaps. Go to https://maps.protomaps.com/builds/ for this

<img width="464" alt="image" src="https://github.com/user-attachments/assets/a05b37e8-7740-4de1-a177-ed84b467be55" />


---

- [ ] In the terminal: create a directory 'assets' and go into it. Then create the file `Dundee.pmtiles` there:

```
mkdir assets
cd assets
pmtiles extract <latest PMTiles URL> Dundee.pmtiles --minzoom=10 --maxzoom=16 --bbox=<answer from step 1>

pmtiles extract https://build.protomaps.com/20250629.pmtiles Dundee.pmtiles --minzoom=10 --maxzoom=16 --bbox=5.6058239,51.9364055,5.7243627,52.0007083
```

---

- [ ] Download `Dundee.pmtiles` and inspect the file.

Drag and drop your PMTiles file into the [PMTiles Viewer](https://pmtiles.io/) to check if the extraction was successful. To do this, you need to download the file (a few MB) to your computer: right-click on the file, then `Download...`.

<img width="1483" alt="image" src="https://github.com/user-attachments/assets/47b1667a-bb28-48bf-8b01-e99a9c2cc1d8#gh-light-mode-only" />

<img width="1483" alt="image" src="https://github.com/user-attachments/assets/a6e697c7-038f-4840-98f2-936c27f7faad#gh-dark-mode-only" />

---

- [ ] Make a commit with `Dundee.pmtiles` and push the file to your fork.

Use the UI or the command line (always faster!):

```
# Return to your 'home' directory from assets
cd ..

# 'Stage' the file
git add assets/Dundee.pmtiles

# 'Commit' the file with a message (-m)
git commit -m "Add Dundee.pmtiles"

# 'Push' the file
git push
```

Once the file is pushed, it should be online, because you published your GitHub repository as a website in part 2. This can sometimes take a while.

---

- [ ] Check if you can access the PMTiles file you created via your browser.

Go to https://maps.protomaps.com/ and load the following URL:

```
https://<your github username>.github.io/makers-gonna-make-dundee/assets/Dundee.pmtiles
```

Click on 'fit bounds'. If everything is correct, you should now see the following:

<img width="1378" alt="image" src="https://github.com/user-attachments/assets/a6b10049-f4af-4eb3-9626-7408222d8257" />

---

- [ ] Save the Protomaps basemap style in your repo.

Now click on "Get style JSON", copy the MapLibre style from Protomaps Light and save it as `assets/style.json`. We're going to use this in Part 5. Don't forget to make a commit!

