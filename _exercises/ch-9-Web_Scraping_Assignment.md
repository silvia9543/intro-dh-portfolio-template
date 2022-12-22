---
layout: page
title: Week 8, Web-Scraping Assignment
description: Web Scraping a Text from Project Gutenberg
---

# 11/2
Select a text from Project Gutenberg. Using what you learned in class, scrap the text (and *only* the text). Divide into smallest structural units in the text (i.e. chapters, or paragraphs etc). Then parse your results into a DataFrame with headings "chapter/paragraph #", text. Finally, save as .csv. When you're finished upload your notebook to your DH portfolio under "Exercises."


```python
import requests
```


```python
response = requests.get('https://www.gutenberg.org/cache/epub/69357/pg69357-images.html')
type(response)
```




    requests.models.Response




```python
response_text = response.text
type(response_text)
response_text[:500]
```




    '<!DOCTYPE html>\r\n<html lang="en">\r\n<head>\r\n<meta charset="utf-8"><style>.xhtml_center {justify-content: center; display: flex;}</style><title>\r\n      The Project Gutenberg eBook of Forgotten World, by Edmond Hamilton.\r\n    </title>\r\n<link href="images/cover.jpg" rel="icon" type="image/x-cover" id="id-7544375868710705494">\r\n<style>body {\r\n    margin-left: 10%;\r\n    margin-right: 10%\r\n    }\r\nh1, h2 {\r\n    text-align: center;\r\n    clear: both\r\n    }\r\np {\r\n    margin-top: 0.51em;\r\n    text-align: ju'




```python
from bs4 import BeautifulSoup 
soup = BeautifulSoup(response_text) 
print(type(soup))
```

    <class 'bs4.BeautifulSoup'>



```python
soup
```




    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="utf-8"/><style>.xhtml_center {justify-content: center; display: flex;}</style><title>
          The Project Gutenberg eBook of Forgotten World, by Edmond Hamilton.
        </title>
    <link href="images/cover.jpg" id="id-7544375868710705494" rel="icon" type="image/x-cover"/>
    <style>body {
        margin-left: 10%;
        margin-right: 10%
        }
    h1, h2 {
        text-align: center;
        clear: both
        }
    p {
        margin-top: 0.51em;
        text-align: justify;
        margin-bottom: 0.49em
        }
    hr {
        width: 33%;
        margin-top: 2em;
        margin-bottom: 2em;
        margin-left: 33.5%;
        margin-right: 33.5%;
        clear: both
        }
    hr.chap {
        width: 65%;
        margin-left: 17.5%;
        margin-right: 17.5%
        }
    hr.tb {
        width: 45%;
        margin-left: 27.5%;
        margin-right: 27.5%
        }
    .center {
        text-align: center
        }
    .right {
        text-align: right
        }
    .poetry .stanza {
        margin: 1em auto
        }
    .poetry .verse {
        padding-left: 3em
        }
    .figcenter {
        margin: auto;
        text-align: center
        }
    .caption p {
        text-align: center;
        text-indent: 0;
        margin: 0.25em 0;
        font-weight: bold
        }
    x-ebookmaker-drop {
        display: none
        }
    div.titlepage {
        text-align: center;
        page-break-before: always;
        page-break-after: always
        }
    div.titlepage p {
        text-align: center;
        text-indent: 0;
        font-weight: bold;
        line-height: 1.5;
        margin-top: 3em
        }
    .ph1 {
        text-align: center;
        text-indent: 0
        }
    .ph1 {
        font-size: medium;
        margin: 0.83em auto
        }</style>
    <link href="http://purl.org/dc/elements/1.1/" rel="schema.dc"/>
    <link href="http://purl.org/dc/terms/" rel="schema.dcterms"/>
    <meta content="Forgotten world" name="dc.title"/>
    <meta content="en" name="dc.language"/>
    <meta content="https://www.gutenberg.org/files/69357/69357-h/69357-h.htm" name="dcterms.source"/>
    <meta content="2022-11-15T17:00:10.768737+00:00" name="dcterms.modified"/>
    <meta content="Public domain in the USA." name="dc.rights"/>
    <link href="http://www.gutenberg.org/ebooks/69357" rel="dcterms.isFormatOf"/>
    <meta content="Hamilton, Edmond, 1904-1977" name="dc.creator"/>
    <meta content="2022-11-15" name="dcterms.created"/>
    <meta content="Ebookmaker 0.12.21 by Project Gutenberg" name="generator"/>
    <meta content="Forgotten world" property="og:title"/>
    <meta content="Text" property="og:type"/>
    <meta content="https://www.gutenberg.org/ebooks/69357/pg69357-images.html.utf8" property="og:url"/>
    <meta content="https://www.gutenberg.org/ebooks/69357/pg69357.cover.medium.jpg" property="og:image"/>
    </head>
    <body><section class="pg-boilerplate pgheader" id="pg-header" lang="en">
    <h2 style="text-align:center; font-size:1.2em; font-weight:bold">The Project Gutenberg eBook of <span lang="en">Forgotten world</span>, by Edmond Hamilton</h2>
    <div style="display:block; margin:1em 0">
    This ebook is for the use of anyone anywhere in the United States and most other parts of the world at no cost and with almost no restrictions whatsoever. You may copy it, give it away or re-use it under the terms of the Project Gutenberg License included with this ebook or online at <a class="reference external" href="https://www.gutenberg.org">www.gutenberg.org</a>. If you are not located in the United States, you’ll have to check the laws of the country where you are located before using this eBook.</div>
    <div class="container" id="pg-machine-header">
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Title</strong>: Forgotten world</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Author</strong>: Edmond Hamilton</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Release Date</strong>: November 15, 2022 [EBook #69357]</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Language</strong>: English</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Original Publication</strong>: US: , United States: Standard Magazines, Inc.,1945.</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Credits</strong>: Greg Weeks, Mary Meehan and the Online Distributed Proofreading Team at http://www.pgdp.net</p>
    </div>
    <div class="vspace" style="height: 2em"><br/></div>
    <div style="text-align:center">
    <span>*** START OF THE PROJECT GUTENBERG EBOOK FORGOTTEN WORLD ***</span>
    </div>
    </section><div style="margin-top:2em; margin-bottom:4em"></div>
    <div class="titlepage">
    <div class="figcenter x-ebookmaker-drop">
    <img alt="" id="id-1769455700647303836" src="images/illusc.jpg"/>
    </div>
    <hr class="chap"/>
    <h1>FORGOTTEN WORLD</h1>
    <h2>By EDMOND HAMILTON</h2>
    <p>[Transcriber's Note: This etext was produced from<br/>
    Thrilling Wonder Stories Winter 1946.<br/>
    Extensive research did not uncover any evidence that<br/>
    the U.S. copyright on this publication was renewed.]</p>
    </div>
    <hr class="chap"/>
    <p class="ph1">CHAPTER I</p>
    <p class="ph1"><i>Stranger from the Stars</i></p>
    <p>Carlin was the only one of the four hundred passengers on the "Larkoom"
    who hated the star-ship and everything about it.</p>
    <p>He was bored with the vessel and everyone aboard. A pack of chattering
    idiots! For the hundredth time since leaving Canopus, he told himself
    that he was a monumental fool to let that psychotherapist talk him into
    this crazy trip.</p>
    <p>A blond girl from Altair Four came tripping along the deck and favored
    Laird Carlin with the bright smile that all the younger feminine
    tourists had practised on the tall, dark, dour-looking young man.</p>
    <hr class="chap"/>
    <div class="figcenter">
    <img alt="" id="id-4434892378565761655" src="images/illus1.jpg"/>
    <div class="caption">
    <p>The blonde from Altair Four favored the tall dour-looking young man with a bright smile.</p>
    </div>
    </div>
    <hr class="chap"/>
    <p>"Oh, Mr, Carlin, the annunciators just said that we're only eight
    hours from Sol. By night, we'll be on Earth! Isn't it thrilling?"</p>
    <p>"Just what is thrilling about it?" Carlin asked sourly.</p>
    <p>The girl was a little dumfounded. "Why, I mean, Earth! All the ancient
    history we study in schools, about how men first came from there two
    thousand years ago. Or was it twenty-one hundred?"</p>
    <p>She prattled on, voicing all the appropriate clichés.</p>
    <p>"Just think, all of us in this ship came from different stats and
    worlds, yet long ago all our ancestors lived on that one little world
    Earth. And they say it's still much the same as it was then. Isn't it
    wonderful?"</p>
    <p>Carlin could not see anything wonderful about it, and a little wearily
    he said so.</p>
    <p>The girl flushed in exasperation. "Then why are you going to Earth at
    all?"</p>
    <p>Why indeed, Carlin wondered savagely? Why the devil wasn't he back
    on the other side of the galaxy where he belonged, supervising
    establishment of the new star-ship line to Algol Six, spending his
    leaves in Sun City with Nila?</p>
    <p>Nila—he yearned for her, for her gay, mocking humor, her cool beauty,
    her quick, clever mind. What was he doing here with a bunch of
    bird-brained tourists who were conscientiously tripping for local color
    to an old, forgotten world?</p>
    <p>This whole part of the galaxy was a stagnant, half-dead area. This side
    of Vega there weren't a score of suns with worlds of any importance.
    And the old "Larkoom," a second-rate star-ship that couldn't make more
    than eighty light-speeds, was plodding determinedly and monotonously on
    into it.</p>
    <hr class="tb"/>
    <p>Curse that psychotherapist anyway! Why had he been crazy enough to
    listen to the fellow? That smug, pink, blinking Arcturian had smiled as
    gently as a well-bred pussy-cat as he told Carlin what his trouble was.</p>
    <p>"Star-sick?" Carlin had flared. "What do you mean, star-sick? I've made
    the trip to Algol ten times in the last three months."</p>
    <p>The psychotherapist had nodded. "Yes. And that was nine times too many.
    You've been overdoing it for a long time, Mr. Carlin."</p>
    <p>Before Carlin could protest, the other man had referred to the dossier
    on his desk.</p>
    <p>"I have your record here. Born at Aldebaran four thirty years ago.
    Graduated at twenty-two from Canopus University with the degree
    of Cosmic Engineer. Worked since then establishing spaceports for
    star-ship lines between Rigel, Sharak, Tibor, Algol and other stars."</p>
    <p>The psychotherapist looked up gravely. "The point is that you've spent
    fifty per cent of your time in the last eight years in star-ships. The
    average has been seventy per cent since you took charge of establishing
    the new Algol line. And that's too much time in space for any man. No
    wonder you're star-sick."</p>
    <p>"Blast it, I'm not star-sick!" Carlin exploded. "What kind of therapist
    are you? I come here to have you treat a perfectly simple syndrome of
    reflex-fatigue, and you tell me all this!"</p>
    <p>The Arcturian shook his head wisely. "Your case was only simple on the
    surface, Mr. Carlin. The hypnosis showed up your trouble unmistakably.
    Want to hear the record?"</p>
    <p>Carlin heard it. And it wasn't pretty. Not pretty, to hear his
    hypnosis-freed subconscious yelling out a frantic hatred of space and
    star-ships and everything connected with them.</p>
    <p>"You see?" said the Arcturian gently. "This has been building up in you
    for a long time."</p>
    <p>Carlin was stunned. He had known of other men who had got star-sick and
    had had to drop their work and quit traveling space for a while. Other
    men—but he'd always laughed contemptuously at them for it.</p>
    <p>The psychos might declare that it was perfectly natural for a man to
    develop a subconscious aversion to space if he crowded his work, but
    the hard-bitten engineers of Carlin's set believed that a star-sick man
    was nine times in ten a shirker. And now he himself was told he was
    star-sick.</p>
    <p>"You've got to quit work and stay out of space for a while," the
    Arcturian therapist told him.</p>
    <p>Carlin felt sick at heart. "Then all my work in building up the Algol
    line will go into young Brewer's hands."</p>
    <p>Still, he thought after a moment, it might not be so bad. Working in
    his line's main offices here on Canopus Two, he could keep in touch.
    And he would have more time here with Nila.</p>
    <p>But the psychotherapist shook his head quite decisively at that.</p>
    <p>"No, Mr. Carlin. Your case is too dangerous for that. Your subconscious
    is twisted into a knot that is going to be hard to untie." He hesitated
    a moment as though he knew what reaction his next words would provoke.
    "In fact, there's only one way in which you can be normalized. That's
    the Earth-treatment."</p>
    <p>"Earth-treatment?" Carlin didn't even know what it meant. "You mean,
    some treatment that has reference to the old planet over on the other
    side of the galaxy?"</p>
    <p>The Arcturian nodded. "Yes, our ancestral planet Earth. Where all our
    race came from, two thousand years ago. Where you're going back to, for
    perhaps a year."</p>
    <p>Carlin was knocked breathless by that calm statement.</p>
    <p>"Me going to Earth for a year? Are you crazy? Why should I go there?"</p>
    <p>"Because," the therapist said soberly, "if you don't I'm afraid you
    won't last another six months as a star-line man."</p>
    <p>"But why can't I take a rest right here on Canopus Two?" Carlin
    demanded heatedly. "Why send me to that moldering, forgotten old planet
    where there's nothing now but a few historical monuments?"</p>
    <p>"You've never been to Earth, I take it?" the psychotherapist asked
    thoughtfully.</p>
    <p>Carlin made an impatient gesture. "I'm not interested in ancient
    history. That part of the galaxy is all a backwater."</p>
    <p>"Yes," the expert said. "I know all that. But old and small and
    forgotten as it is these days, Earth is still important."</p>
    <p>"To historians," Carlin snapped. "To people who like to poke in the
    dusty past."</p>
    <hr class="tb"/>
    <p>The Arcturian nodded, and shrugged.</p>
    <p>"And to psychologists," he said quietly. "Most people these days don't
    realize something. They don't realize that we, all of us, are still
    really Earthmen in a way." He held up a protesting hand. "Oh, I know
    we don't think of ourselves like that! Since those first Earthmen
    pioneered to their neighbor planets and then to the stars, since our
    civilization spread out over most of the galaxy, a hundred generations
    of us have been born on different star-worlds from Rigel to Fomalhaut.
    But except for local modifications, the type of humanity has persisted
    since our ancestors left Earth and Sol long ago.</p>
    <p>"That's because we've altered star-world conditions to fit ourselves,
    instead of adapting ourselves to those conditions. We've cunningly
    changed atmospheres, gravities, everything, wherever we went. We've
    kept ourselves one race, one type, that way. But it's a type that is
    still indexed to that old plane Earth as its norm."</p>
    <p>"Does that explain why I have to give up my work and go live on the old
    relic for a year?" Carlin demanded furiously.</p>
    <p>"Yes, it does," the Arcturian replied. "We're a star-traveling race
    now. But the mind can take only so much of the strain of star-travel.
    Overdo that strain and you get a revulsion, you get star-sickness. Then
    the only cure is rest for the mind in completely normal conditions. And
    complete normality, for us descendants of Earthmen, is—Earth."</p>
    <p>Carlin had stormed. He carried his wrathful resistance to the last
    pitch.</p>
    <p>And then the psychotherapist had crushed him.</p>
    <p>"I've turned in your psycho-record to your star-ship line. You'll not
    be allowed to work there until you're cured."</p>
    <p>And that, Laird Carlin thought bitterly, was why he was sprawled in a
    deck-chair here on the "Larkoom" as the old tub creaked and labored and
    plodded through space toward the yellow spark of Sol.</p>
    <p>"A year!" he thought in impotent rage. "A year in that hole! I might as
    well be dead."</p>
    <p>The psychotherapist had held out the hope that it might not take a
    year. Some cases of star-sickness responded quickly to Earth-treatment.
    But even a few months seemed an eternity to Carlin.</p>
    <p>The passengers of the "Larkoom" were crowding toward the transparent
    wall of the deck. Earth was coming into sight. And these people—men
    and women bronzed by the glare of Canopus, reddened by the desert winds
    of Rigel's worlds, paled by the mists of Altair's planets—all were
    watching with an intense and eager expectation.</p>
    <p>Carlin walked wearily over to the deck wall and watched with them.
    Sol, ahead, was a small and undistinguished yellow sun. Its orb was
    unimpressive to eyes that had looked on Antares and Altair.</p>
    <p>And the planets that circled it were so little that Carlin could
    hardly make them out. He remembered half-forgotten names from ancient
    history—Saturn, Jupiter, Mars. And that little gray-green dot beyond
    must be Earth.</p>
    <p>"Isn't it tiny?" babbled a rapturous, overweight woman beside Carlin.
    "I think it's cute!"</p>
    <p>A very young man from Mizar Seven proudly aired his knowledge.</p>
    <p>"That satellite beyond it is Luna, its moon."</p>
    <p>"The moon is almost as big as the little planet!" exclaimed someone,
    laughing.</p>
    <p>Carlin found their chatter getting on his nerves, and edged further
    along the deck. In gloomy silence, he looked down as the "Larkoom"
    swept in swift, almost soundless rush toward the little planet.</p>
    <p>A gray-green, cloud-screened ball spinning around a second-rate sun—it
    looked like the end of the universe to Carlin. And he might have to
    spend a year here! His spirits sank still lower.</p>
    <p>"They say you can get the most wonderful souvenirs here," one of the
    tourists' voices reached him.</p>
    <p>Carlin writhed. He would be glad to get out even at Earth, to get away
    from this bunch of babbling fools.</p>
    <p>He realized his irritability was extreme, unreasonable. It was the
    result of his star-sickness, he supposed. But that didn't make it any
    more endurable.</p>
    <p>"Landing in ten minutes," spoke the annunciators throughout the ship.
    "Stasis going on."</p>
    <p>The dim glow of the force-stasis that cushioned everything in the ship
    against pressure of deceleration came on like a tangible medium around
    them. The big propulsion-wave generators droned in lower key.</p>
    <p>Swaddled in the cushioning force, they felt no discomfort as the
    "Larkoom" quickly dropped toward the little planet. Atmosphere screamed
    briefly outside the ship. They came down through a belt of clouds.</p>
    <p>"That's the city New York!" cried an eager voice. "The oldest human
    city in the galaxy!"</p>
    <hr class="chap"/>
    <p class="ph1">CHAPTER II</p>
    <p class="ph1"><i>Ancient Town</i></p>
    <p>Carlin looked with a jaundiced eye on the scene widening out below
    them. There was a blue ocean stretching eastward, a long green coast,
    and an island that was covered by the grotesquely lofty buildings of an
    extremely antiquated type of city.</p>
    <p>This ancient town called New York was like a memento of the primitive
    past. Not for a thousand years had men crowded their structures so
    crazily together, or built them to such insane heights.</p>
    <p>"It's like one of the bird-people's lofts on Polaris One!" exclaimed a
    girl, laughing. "And how old it looks!"</p>
    <p>Old? Yes. Pitifully old, like a withered beldame who endeavors still
    to maintain stiff dignity. The city looked only half-occupied, vines
    growing on some of the grotesque towers, parks ragged around the edges.</p>
    <p>The spaceport, some distance northward amid low rolling hills, was so
    small as to be inadequate for any decent world. Carlin's practised eyes
    condemned the cracked, blackened tarmac, the ill-placed rows of docks,
    the insufficient hangar and repair buildings.</p>
    <p>The "Larkoom" landed softly. Carlin waited wearily until the squealing
    rush of tourists was over, and then walked out into the soft yellow
    sunshine. He looked around without interest. Landing on a new world was
    no novelty to him.</p>
    <p>But for a moment, he was startled by the air he breathed. It was so
    sweet, so buoyant, so right. It was subtly stimulating, exhilarating
    to the lungs. Then he realized the cause. All over the galaxy, the
    descendants of Earthmen had conditioned planetary atmospheres with this
    atmosphere of Earth as the desired norm.</p>
    <p>He looked around uncertainly. The tourists were already being
    shepherded by their tour-conductors toward some old monuments at the
    far end of the spaceport. But he had no desire to follow them.</p>
    <p>The psychotherapist had told him, "Live as nearly an ordinary Earth
    life as you can. Your cure will be quicker if you do. Best thing would
    be to lodge in some typical Earth home, if you can."</p>
    <p>Carlin wondered where he could find such a lodging. There were a few
    Earthmen about, spacemen, port officials and the like. He could ask one
    of them.</p>
    <p>He had met Earthmen before throughout the galaxy, for many of them
    followed space as a trade. And he didn't much like them. A proud,
    taciturn, half-sulky lot, they had always seemed to him.</p>
    <p>"Can you tell me where I could find lodgings around here?" He asked a
    lanky, lantern-jawed man in faded clothes.</p>
    <p>The Earthman contemplated Laird Carlin with unfriendly eyes, taking in
    his sun-darkened face, his pearl-colored synthesilk slacks and jacket,
    every detail of his appearance that was alien here.</p>
    <p>"Well, no," the fellow drawled coolly. "Don't know where a stranger
    could get lodgin's round here."</p>
    <p>He slouched on. Carlin flushed with anger at the scarcely veiled
    hostility in the fellow's manner.</p>
    <p>These blasted yokels of Earth! Living here on an old, outworn,
    fifth-rate planet, resenting the progress and prosperity of the great
    star-worlds, talking of everybody but themselves as "strangers"!</p>
    <p>"And I'm supposed to live among them for a year!" he thought bitterly.</p>
    <p>He started across the spaceport. He had noted a spick-and-span
    chromaloy building with a half-dozen trim Control cruisers parked
    nearby, and with the Control Council emblem on its wall. He could find
    out something there.</p>
    <p>The spaceport was a somnolent, slovenly place to Carlin's eyes. A
    few star-ships, all of them freighters except the tubby "Larkoom," a
    scattering of little inter-planet craft, a few workers lounging about.
    Even the smallest world of the great stars would be ashamed of such a
    port.</p>
    <p>That soft yellow sun, he found, had a deceptive warmth. And walking was
    tiring after days of the ship's artificial gravity. Then Carlin stopped
    as he came abreast of a rickety little planet-ship.</p>
    <p>Two Earthmen were inspecting its stern drive-plates—one of them a
    stocky, red-faced young man, the other a lame younger fellow with a
    crutch. Carlin asked them his question.</p>
    <p>The red-faced individual answered with the same hostility of manner.</p>
    <p>"You'll find no lodgings around here. Better go with the rest of your
    crowd. There's a big tourist hotel down in the city."</p>
    <p>Carlin swore. "Blast it, I'm not a tourist. I'm an engineer sent here
    by a crazy psycho to spend a year on Earth—heaven knows why!"</p>
    <hr class="tb"/>
    <p>The lame young Earthman looked at Carlin more closely. He had a thin,
    pleasant brown face with intelligent blue eyes.</p>
    <p>"Oh, an Earth-treatment man?" he said. "A few come in all the time." He
    asked interestedly, "You're a Cosmic Engineer? Do you mind telling me
    what field?"</p>
    <p>"Star-ship line chief surveyor," Carlin said wearily. "That means I lay
    out spaceport and beacon routes between star-worlds."</p>
    <p>"I know what it means." The lame youngster nodded quietly. He
    hesitated, frowning slightly as though weighing something. Then, as if
    deciding, he spoke. "I'm Jonny Land. I think we could fix you up with
    lodgings if you don't mind putting up with a little discomfort."</p>
    <p>"You mean, in your own home?" Carlin asked doubtfully. "Where is it?"</p>
    <p>Jonny Land pointed to one of the low green ridges west of the spaceport.</p>
    <p>"Just up on the ridge there. There's only my grandfather, my brother
    and sister, and myself. And we have an extra room."</p>
    <p>The red-faced young Earthman made a sharp protest. "Jonny, what the
    blazes are you thinking of? You don't want this fellow in with you!"</p>
    <p>The violence of his protest seemed uncalled-for to Carlin, even
    granting the general Earthman hostility to strangers.</p>
    <p>Jonny Land quietly quelled the outburst. "I'm doing this, Loesser." He
    looked at Carlin. "Well, what about it? I warn you that you won't find
    the comforts of a big star-world apartment."</p>
    <p>"I don't expect anything like that here," Carlin answered tiredly. He
    felt worn out by the voyage, the discouragingly primitive aspect of
    this place where he must live, the open unfriendliness. He nodded.
    "I'll try it. The name is Laird Carlin."</p>
    <p>"If you'll get your luggage, I'll take you up," Jonny Land suggested.
    "I have a truck. I'll meet you over at the terminal."</p>
    <p>Carlin came out of the shabby terminal a little later with his two
    kitbags and found the lame youngster waiting at the wheel of a
    disreputable-looking old ato-truck.</p>
    <p>Loesser, the red-faced young man, was standing beside it voicing
    emphatic protest about something. Carlin overheard a few words.</p>
    <p>"—ruin everything by taking this fellow in!" he was saying violently.
    "How do you know he isn't a Control spy?"</p>
    <p>"I know what I'm doing, Loesser," Jonny Land repeated firmly.</p>
    <p>They broke off as they saw Carlin coming. But Loesser gave him a hot,
    angry glare as he climbed into the machine.</p>
    <p>The old truck ran westward across the bumpy tarmac and started climbing
    an ancient, cracked concrete road toward the green ridge.</p>
    <p>Carlin wondered wearily what these Earthmen were up to that made them
    afraid of Control? Smuggling, maybe? He didn't much care. He was hot,
    tired, grimy with dust, and unutterably disgusted with Earth.</p>
    <p>The concrete road that climbed the ridge looked as though it was
    centuries old. And its engineering had been timid, for it wound around
    hills instead of cutting through them, bridged small streams instead of
    trampling over them. But the battered truck had difficulty negotiating
    even these easy grades. Its ato-motor drumming noisily as it climbed.</p>
    <p>Carlin looked out gloomily at the sunset-lit landscape. He could not
    get used to the vivid, dominating green of all vegetation here. And
    he was shocked by the unkempt, ragged look of everything. Untended
    fields of weeds and clumps of woods grew right up to the road. It was
    dismayingly different from the groomed, parklike planets of Canopus.</p>
    <p>The houses Carlin glimpsed along the road added to his dislike. They
    were mostly old ferroconcrete dwellings half-hidden by trees and
    bright flowers, with behind them the big tanks used in hydroponic
    farming. Hydroponic farming was so old-fashioned he had thought it had
    disappeared from the galaxy. What was the matter with these people that
    they didn't directly synthesize their food as others did?</p>
    <p>Young Jonny Land was speaking to him.</p>
    <p>"You've never been here before? You must find Earth a little odd."</p>
    <p>Carlin shrugged. "It's all right, I suppose. But I just can't
    understand how you people could let your planet get into this kind of
    shape. Why haven't you spread out more, instead of huddling around a
    few archaic centralized cities like that one back yonder?"</p>
    <p>The lame young Earthman answered slowly, his thin, brown face turned to
    the road ahead.</p>
    <p>"The answer to that is simple. One word, in fact. And that word is
    'power.' We just don't have power enough here on Earth to smooth it out
    into a garden-planet like your star-worlds, to come and go around it
    any distance at will."</p>
    <p>"Atomic power is about the easiest thing to produce there is," Carlin
    commented skeptically.</p>
    <p>"Yes, if you have copper fuel," Jonny Land replied. "If we had enough
    copper we could make a garden of this world too, could spread all
    around its loveliest spots and come and go by fast flier, could give
    up the old hydroponic farming and synthesize our food, and produce the
    luxuries you people have on the star-worlds.</p>
    <p>"But we have little copper. Earth, and its sister-planets here, are all
    starved for it. Once, we had a lot. But not now. And it's economically
    impossible to haul copper in sufficient quantities from other stars.
    That's why we're power-starved, unable to progress."</p>
    <hr class="tb"/>
    <p>Carlin made no further comment. He was not much interested. He was
    only wondering sickly how long he would have to stay on this unkempt,
    stagnant planet.</p>
    <p>The sun was burning his neck, for the old truck was topless. He was
    jolted by holes in the ancient road. The sweetness of the air had lost
    its magic for him, for now with the twilight had appeared swarms of
    evil little gnats and midges.</p>
    <p>"This is the house," said Jonny Land, pulling up the truck in front of
    a square dwelling.</p>
    <p>Laird Carlin's heart sank. It was like the other houses he had seen,
    a ferroconcrete structure festooned with climbing flower-vines,
    surrounded by tall, untrimmed trees except on the side that looked down
    into the twilit valley. Primitive hydroponic tanks gleamed dully beyond
    the trees.</p>
    <p>He followed the lame youngster into a dim, cool living room. It looked
    like an antique stage set to Carlin, with its ridiculous cloth curtains
    at the windows, its obsolete krypton light bulbs in the ceiling, its
    massive furniture that was actually made of wood.</p>
    <p>Jonny Land had been making explanations in lowered tones to the two
    people at the other end of the room. They came forward, a spry old man
    and a girl.</p>
    <p>"This is Gramp Land, my grandfather," Jonny introduced. "And my sister
    Marn."</p>
    <p>The old man looked at Laird Carlin with inquisitive, bright eyes, and
    his gnarled hand reached for an old-fashioned handshake.</p>
    <p>"Come from Canopus, do you?" he chirped. "Well, that's a long way off.
    I was there once years ago when I followed space. And my grandson Harb
    has been there lots of times when he was a star-ship man."</p>
    <p>The girl, Marn, looked doubtful and troubled as she murmured a word of
    greeting to Carlin. He sensed that his coming had disturbed her.</p>
    <p>She was a rather small girl, with a thick mop of ash-colored hair
    carelessly combed back. Her eyes were grave blue. She wore a faded old
    slack-suit that he thought the most barbaric feminine garment he had
    seen.</p>
    <p>"I hope we can make you comfortable here, Mr. Carlin," she said,
    troubled. "We've never had any lodger before. I can't understand why
    Jonny made the suggestion."</p>
    <p>A heavy step at the door cut her short. Her look of distress and worry
    deepened.</p>
    <p>"There's my brother Harb, now."</p>
    <p>Harb Land was a gangling young giant with a craggy face and
    slate-colored eyes that looked at Carlin with instant hostility. Jonny
    had limped forward and was quickly explaining Carlin's presence.</p>
    <p>"He's going to live here with us for a while, Harb."</p>
    <p>Harb Land's reaction was violent. "Have you gone out of your mind,
    Jonny?" he flared. "We can't have him here."</p>
    <p>Disgusted, Carlin started to turn away. But Jonny Land stopped him with
    a gesture. There was a quiet, unsuspected strength in his thin brown
    face as he spoke to his lowering brother.</p>
    <p>"He's going to stay, Harb. We'll talk about it later."</p>
    <p>Harb Land made no reply, but glared at Carlin. And Carlin felt an
    unutterable weariness and dislike.</p>
    <p>These primitive, backward, suspicious Earth yokels, quarreling over the
    privilege of staying in their grotesque old house. As though he would
    stay on their cursed planet one minute if he didn't have to!</p>
    <p>"I'm very tired," he said heavily. "If you could show me where the room
    is, I should like to rest."</p>
    <p>Marn uttered an apologetic exclamation. "Oh, I'm sorry! Of course
    you're tired. Come with me, Mr. Carlin."</p>
    <p>She led upstairs. There was no grav-lift, just old-fashioned steps
    going up a dark hall. And the bedroom on the upper floor to which she
    took him was as bad as he had expected.</p>
    <p>It was clean, of course, spotlessly so. But it was more like a museum
    exhibit than a sleeping chamber, to Carlin. There were no aerators,
    just open windows with crude screens across them. No somnigrav pad,
    just a high, old-style bed. There wasn't even a video.</p>
    <p>Yet the girl made no apologies for it, seemed not to think any
    necessary.</p>
    <p>"We'll bring your bags up after dinner," she said. "It will be soon."</p>
    <hr class="chap"/>
    <p class="ph1">CHAPTER III</p>
    <p class="ph1"><i>Old Planet</i></p>
    <p>When Marn had gone, Carlin lay down wearily on the lumpy, sagging bed.
    He closed his eyes. The reaction to the long, slow voyage had set in.
    No doubt about it, he was star-sick all right. Time was when no voyage
    could have made him feel like this.</p>
    <p>But it wasn't the voyage so much as this world to which he had been
    condemned. How was he going to live here for months, for a whole year
    maybe?</p>
    <p>The sound of an angry voice came up dimly through the twilight, from
    the lower floor of the house. He recognized Harb Land's angry tones.</p>
    <p>"—if Control Operations finds out what we're doing!"</p>
    <p>There was a murmur of lower voices, and then the argument seemed to
    stop. Carlin remembered what he had overheard the red-faced Loesser
    saying at the spaceport.</p>
    <p>What were these Earthmen doing that they were so secretive about? It
    must be something against the laws by which Control Council governed
    the galaxy, or they would not fear discovery by Control Operations.</p>
    <p>When Carlin went down to dinner, he expected open hostility from the
    gangling older brother. But Harb Land muttered a curt greeting, his
    half-civil manner indicating his angry protests had been overridden.</p>
    <p>Carlin stared dismayedly at the food set before them. Instead of the
    clear, colored synthetic jellies and liquids he was used to, the food
    was served in what seemed barbarically primitive state. Cooked whole
    vegetables, natural eggs, natural milk—everything rawly natural.</p>
    <p>He ate what he could, which was little. His weariness was drugging him,
    and Harb Land's smothered hostility gave a sense of strain.</p>
    <p>Gramp Land carried on most of the conversation, questioning Carlin
    about the far-away star-worlds. Carlin answered wearily.</p>
    <p>"Saw a lot of them worlds myself once," the old man said. He added
    proudly, "Following space runs in my family. My mother was a direct
    descendant of Gorham Johnson himself."</p>
    <p>"Gorham Johnson?" Carlin asked. "Who was he?"</p>
    <p>The question was unfortunate.</p>
    <p>"What do they teach out in your star-world schools?" Gramp exploded.
    "Don't you know that Gorham Johnson was the first man ever to travel
    space? That he was an Earthman, who took off from down in the valley
    here two thousand years ago?"</p>
    <p>Gramp's pride was outraged. Carlin remembered the old galaxy
    proverb—"Proud as an Earthman." They were all like that, inordinately
    vain of the fact that their world's people had first conquered space.</p>
    <p>"Sorry," he said tiredly. "I remember the name now. Anyway, I had too
    much cosmic physics to study to spend much time on ancient history."</p>
    <p>Gramp still spluttered, but Jonny intervened, questioning Carlin on his
    work.</p>
    <p>"Did you study sub-atomics or just straight dynamics?"</p>
    <p>"Sub-atomics," Carlin answered. And, to another question, "Yes, I had
    electronic mechanics too."</p>
    <p>He caught the swift, triumphant glance that Jonny Land shot at his
    brother. It puzzled him.</p>
    <p>"Jonny knows all that stuff," boasted Gramp, his good humor restored.
    "He's a Cosmic Engineer graduate from Canopus University, too."</p>
    <p>Laird Carlin was genuinely surprised. He looked at the quiet,
    thin-faced youngster.</p>
    <p>"You're a Canopus graduate? Why the devil is a man of your training
    wasting your time here on Earth?"</p>
    <p>"I just like Earth," Jonny answered evenly, "and wanted to come back
    here when my education was finished."</p>
    <p>"Oh, sure." Carlin nodded. "But if this world is as outworn as it
    looks, there's no field here for a CE. You ought to be out at Algol."</p>
    <p>"You star-world people are all the same—always advising us to leave
    Earth!" Harb Land interrupted with suppressed passion. "That's what
    Control Council keeps harping on as a solution to all our poverty and
    problems. They keep asking, 'Why don't you emigrate to other stars?'"</p>
    <p>Gramp Land shook his head. "We don't leave our planet as lightly as
    some folks do. No matter how far an Earthman goes, he always comes
    home."</p>
    <p>"Still, you can hardly blame Control Council for giving you good
    advice," Carlin said, exasperated. "After all, it's your own fault if
    you foolishly squandered the copper resources of your planet and now
    lack power."</p>
    <p>Harb Land's craggy face darkened. "Yes, we squandered our copper
    foolishly. We did it twenty centuries ago, when Earth was opening
    up the whole galaxy to travel. We spent our copper establishing the
    galactic civilization that's forgotten all about our power-starved
    world."</p>
    <p>"Harb, please!" said Marn in a low voice, distress in her face.</p>
    <p>A silence fell, and they finished the dinner without further
    conversation. But Jonny Land spoke to Carlin before he went upstairs.</p>
    <p>"Don't take Harb too seriously. A lot of people here on Earth are so
    embittered about our lack of power that they're unreasonable."</p>
    <hr class="tb"/>
    <p>Carlin found his bedroom dark. No automatic lights came on when he
    entered, and he could not find the switch. He gave it up, and got into
    bed and lay looking heavily out into the night.</p>
    <p>Soft wind was stirring the trees around the house. Heavy scent of
    flowers drifted on it, stirring the window curtains. Down in the valley
    gleamed the spaceport beacons, and beyond lay a thin rim of glimmering
    sea over which the quarter-phase shield of Luna was rising.</p>
    <p>He felt utterly miserable, homesick, wretched. If he were back at
    Canopus right now, he would be dancing with Nila in Sun City ballroom,
    or wandering in Yellow Gardens.</p>
    <p>He drifted off to sleep despite himself, in his lumpy bed....</p>
    <p>Carlin awoke with bright sunrise splashing his face. He reached
    sleepily for the aerator and refreshment buttons—then remembered.</p>
    <p>To his surprise, he was feeling much better. He had slept well in the
    primitive bed, and fatigue had drained out of him.</p>
    <p>Queer, musical notes that he guessed were calls of birds came to his
    ears. The air that snapped the curtains was chill now, but pure and
    sweet, subtly intoxicating.</p>
    <p>"They do have finer air on this old world than any aerator can
    furnish," he thought.</p>
    <p>He put on a zipper-suit that was dark brown and rough in weave.</p>
    <p>"Going native," he thought with a sour grin, and went downstairs.</p>
    <p>Marn Land was the only person he found in the sunny rooms. She still
    wore those barbaric faded old slacks, but had a red flower in her ashen
    hair. A little frown of worry in her forehead disappeared as she looked
    at him.</p>
    <p>"You're feeling better, aren't you?" she asked.</p>
    <p>"A lot," Carlin admitted. "I'm afraid I was rather rude last night, you
    know."</p>
    <p>"You were tired," she said gravely. "Just sit down. I'll get your
    breakfast."</p>
    <p>It was a new experience to Carlin to sit chatting in a sunny old
    kitchen while a girl in faded slacks prepared his breakfast on an
    electrode stove. Instead of punching the refreshment-button for it.</p>
    <p>"Jonny and Harb have gone down to the spaceport," she said over her
    shoulder. "They and a few friends have an old planet-ship there that
    they're fixing up for a trip to Mercury."</p>
    <p>"Mercury?" he said. "Oh, that's the innermost of these planets, isn't
    it?"</p>
    <p>"Yes. Men here on Earth are always going prospecting for copper on its
    Hot Side. Jonny got up this prospecting expedition."</p>
    <p>The breakfast she put before Carlin was of coarse wheaten bread, more
    of the natural eggs and milk, and a curious brown beverage made from
    stewing certain dried berries. She informed him its name was coffee.
    Carlin tried it, found it bitter and unpalatable.</p>
    <p>A little surprised by his own action, he ate nearly everything else.
    The food was coarse, but satisfying enough, and he would have to get
    used to it if he were to stay here.</p>
    <p>"I'll try not to be any trouble to you," he told Marn. "I'm just
    supposed to take it easy, do anything I want to."</p>
    <p>She nodded. "I know. Some of our neighbors had Earth-treatment visitors
    as lodgers. They all got to like Earth a lot before they left."</p>
    <p>Carlin did not voice his pessimism on that point. He went to the door
    and stood looking out into the sun-bright, flowery yard.</p>
    <p>He felt at a loss. It was baffling to find himself without anything
    to do, no work crowding up that must be hurried through, no crews of
    ato-men to supervise in blasting spaceports out of untamed planets.</p>
    <p>Marn looked at him understandingly. "You've always been busy, haven't
    you? Earth must seem slow and dull to you."</p>
    <p>Carlin shrugged. "I might as well get used to it. I think I'll take a
    look around."</p>
    <p>"You'll find Gramp fishing up at the north brook if you go that far,"
    Marn called after him as he walked across the yard.</p>
    <p>Carlin sauntered past a big, locked ferroconcrete workshop of some
    kind, and some tall storage sheds, then on past the flat, wide
    hydroponic tanks that were now loaded with their masses of green growth.</p>
    <p>He found a road beyond them that he did not recognize as a road, at
    first. It was a mere wide track gouged northward along the wooded
    ridge, the first dirt road that he had ever seen on a civilized world.</p>
    <p>"A poor planet, all right," Carlin thought. "Can't even build decent
    roads."</p>
    <p>There were hardly even any ato-fliers in the sky, only an occasional
    one flitting across the blue vault.</p>
    <p>"No wonder these poverty-stricken devils resent the rest of the
    galaxy," he thought. "I suppose I would too, if it had been my bad luck
    to be born here."</p>
    <hr class="tb"/>
    <p>The road was crazily illogical, winding westward along the woods-clad
    ridge in serpentine fashion. It twisted accomodatingly to avoid big
    boulders, a spring, a small gully.</p>
    <p>The woods on either side was deplorably unkempt to Carlin's eyes. Big
    and small trees jumbled together, saplings choking each other out, dead
    brush and thorns and vines everywhere. There was even wild life in the
    woods, furry rodents scuttling away, hosts of birds.</p>
    <p>This sort of thing was what you expected on some unpeopled planet that
    hadn't yet been pioneered and civilized. But Earth was the oldest
    human-peopled world in the whole galaxy.</p>
    <p>Yet Carlin had to admit that there were certain compensations here.
    That winelike air was still an experience to him. And walking now came
    more easily to his muscles here than on any world. It seemed odd to be
    walking with such perfect ease, without wearing a de-grav.</p>
    <p>He could not find the brook Marn had mentioned. He sat down on a log by
    the roadside, musing on the drowsy, dull quiet of this place. There was
    not a sound of human activity. Didn't these Earth people ever get bored
    with the sleepiness of the place?</p>
    <p>Carlin found he was still tired. He watched a small, brilliant insect
    fluttering over a flower near by. Soft wind breathed through the ragged
    woods, stirring the green leaves and making a dappled, dancing pattern
    of sunlight on the ground. A distant bird called rustily.</p>
    <p>"An old, outworn planet, dreaming," he thought. "These people, all of
    them, living in its past."</p>
    <p>Carlin finally got up stiffly, and lounged back along the road. He was
    surprised to find that time had passed quickly, that the sun was now at
    the zenith. And that, somehow, his taut nerves had relaxed.</p>
    <p>The big workshop behind the house had its doors open now. He glanced
    through them and was surprised to see that the cavernous room in there
    was a fairly well-equipped atomic-engineering laboratory.</p>
    <p>Interested, Carlin started toward it. In the center of the big room
    he had glimpsed a towering, massive machine whose inner mechanism was
    concealed by a cylindrical metal cover.</p>
    <p>"Looks like it might be a big field-generator of some kind," he
    muttered. "I wonder what it really is?"</p>
    <p>There was a violent exclamation as an Earthman came running out from
    behind the machine to block his entrance.</p>
    <p>Carlin recognized the broad red face, angry eyes and stocky figure of
    Loesser, the man who had argued with Jonny at the spaceport.</p>
    <p>"What are you doing here?" Loesser demanded harshly.</p>
    <p>Carlin was bewildered by his vehemence. "Why, I just wanted to take a
    look at this machine."</p>
    <p>"I thought so!" blazed Loesser, his eyes raging. "I told Jonny that was
    why you came here!"</p>
    <p>He snatched an object from his jacket pocket. To Carlin's thunderstruck
    amazement, the object was a stubby atom-pistol that Loesser was
    furiously leveling at him.</p>
    <hr class="chap"/>
    <p class="ph1">CHAPTER IV</p>
    <p class="ph1"><i>Mystery Machine</i></p>
    <p>Laird Carlin was child of a galactic civilization in which violence
    between men was rare. There was plenty of danger yet, in pioneering new
    star-worlds, but over the civilized worlds themselves the unchallenged
    law of the Control Council maintained unbroken order. A man could go a
    lifetime without ever seeing violence.</p>
    <p>The atom-pistol in Loesser's hand and the obvious murderous intention
    in the man's face stupefied Carlin. He was simply unable to adjust his
    thinking to the possibility that the enraged Earthman before him meant
    to blast him down.</p>
    <p>"Why, what's the matter?" he began, puzzled and stunned.</p>
    <p>He knew later how near he had been to death. At the moment, he so
    little recognized it that he felt no relief at the interruption that
    came now. Harb and Jonny Land came running forward from the cavernous
    interior of the workshop.</p>
    <p>"Loesser, put that gun down!" snapped Jonny.</p>
    <p>Loesser turned violently. "This fellow was spying on us! I saw him at
    the door!"</p>
    <p>Harb Land's craggy face darkened ominously.</p>
    <p>"I warned you what might happen," he said harshly to his brother.</p>
    <p>"Is this man crazy?" Laird Carlin demanded bewilderedly of Jonny.</p>
    <p>The lame youngster limped quickly forward. "Get back to work," he told
    the other two briefly. "Carlin, I'm sorry about this. I'll explain."</p>
    <p>He walked beside Carlin toward the house. It was not until later that
    Carlin realized how deftly and unobtrusively he had been steered away
    from the workshop.</p>
    <p>"Harb and Loesser and I, and a few others, are planning an expedition
    to Mercury to prospect for copper," Jonny was explaining. "In that ship
    you saw down at the spaceport. We've devised a new metal-finder of the
    radiolocator type, with which we hope to be able to locate new copper
    deposits. That's the machine in the workshop.</p>
    <p>"We've maintained a certain secrecy about it," he went on, "because
    naturally we don't want other prospectors stealing the idea of our new
    finder and beating us to it. And I'm afraid Loesser thought you were
    spying on us. People here are always a little suspicious of strangers."</p>
    <p>"So I've noticed," Carlin answered dryly. "This is the first world in
    the galaxy where I've ever felt completely unwelcome."</p>
    <p>"Oh, I wouldn't say that," replied the other. "But put yourself in our
    place, Carlin. Figure how you would feel if you were an Earthman, your
    world starved for power because its copper was spent to establish a
    galactic civilization that now neglects it."</p>
    <p>Jonny's thin brown face was earnest, his blue eyes watching Carlin as
    though eager to convince him. Carlin shook his head.</p>
    <p>"I can see your problem in lacking copper," he said. "But the remedy
    for it is so simple. Nine-tenths of you should emigrate to other,
    better worlds as the Control Council advised."</p>
    <p>Jonny smiled. "There you come up against the obstinacy of my people.
    We've an older planetary tradition, a deeper, more ancient love for our
    world, than any other people in the galaxy."</p>
    <p>"I think you people live too much in the past," Carlin answered
    frankly. "But it's none of my business. Anyway, I hope your expedition
    brings home copper."</p>
    <p>"Thanks," Jonny said softly. "I think we have a good chance."</p>
    <p>Carlin went back to the veranda of the old house and sat there
    pondering. Something about Jonny's explanation had been vaguely
    unsatisfying.</p>
    <p>To his trained eyes, the glimpse he had had of that towering machine
    had not suggested any metal-finding device. There had somehow been a
    suggestion in its half-glimpsed bulk of something quite different;
    something vaguely disturbing, almost menacing.</p>
    <p>"The devil, I must have knots in my subconscious to start getting
    premonitions like that," Carlin swore. "The poor devils are just
    secretive about their plans because everyone else here is that way."</p>
    <p>He lounged boredly around the house during the hot, sleepy afternoon.
    There was no one to talk to, for the brothers stayed out in their
    workshop and Marn was out tending the big hydroponic tanks.</p>
    <p>He tinkered with the old video set in the living room but the
    only stations he could get were local Earth ones, and lectures on
    hydroponics and gossip about unknown people didn't interest him.</p>
    <p>He finally gave up and stretched out on the veranda, staring sleepily
    down into the green cup of the valley and cursing the psychotherapist
    whose insane idea had sent him here to die of boredom. He dozed until
    he was awakened by the sputter of an arriving ato-truck.</p>
    <hr class="tb"/>
    <p>It contained three lanky young men, tall Earthmen who went back to
    the workshop without stopping at the house. The other partners in the
    prospecting expedition, Carlin supposed sleepily.</p>
    <p>Again he felt that queer sense of something threatening, that vague
    premonition that had clung to him ever since he glanced into the
    workshop. If only he could remember what that machine reminded him of.</p>
    <p>Days passed and Carlin still could not remember that, though his
    disturbing doubt persisted. There was no chance of another look into
    the workshop for it was always locked except when Jonny and Harb and
    their half-dozen partners worked in it.</p>
    <p>"The trouble with me," Carlin told himself ironically, "is that I
    haven't anything else to occupy my mind on this blamed world."</p>
    <p>Yet Carlin's first repelled dislike of Earth had faded much by now.
    The crudities of existence, the lack of civilized conveniences, no
    longer bothered him so much. He had to admit that whether or not
    Earth-treatment was benefiting his twisted subconscious, this sleepy
    old planet was a fine place for a rest.</p>
    <p>He spent his mornings idly rambling the twisting roads, his afternoons
    lounging on the cool, shady veranda of the old house, or helping Marn
    tend the hydroponic tanks. Or fishing with Gramp in the foaming brook
    below the ridge, while that oldster told interminable tales of the old
    days when he had followed space.</p>
    <p>Neighbors, hydroponic farmers up and down the valley, dropped in at
    the Land house in the evenings. Carlin did not intrude, and gradually
    their first stiff suspicion of him abated and they talked freely before
    him. The talk always swung to the paramount consideration on this
    power-starved planet—the need for copper. It made Carlin feel a little
    guilty to remember how much of it was wasted on other worlds.</p>
    <p>"I have to drive down to the spaceport for Jonny, to get some
    instruments he left in the ship," Marn said to him after dinner one
    evening. "Do you want to go along?"</p>
    <p>Carlin grinned. "I've legged it so much lately that riding anywhere
    would be a change."</p>
    <p>The old ato-truck swung down the twisting road in the blaring sunset.
    The heavens behind them were a glory of fusing colors as the red ball
    of Sol dipped majestically toward the horizon.</p>
    <p>Despite his appreciation of that wild splendor, Carlin felt a vague
    uneasiness. Why should the loveliness of the evening bring disturbing
    recollection of Jonny Land's puzzling machine into his mind?</p>
    <p>"You're getting to like it better here, aren't you?" asked Marn.</p>
    <p>She was usually so silent with him that Carlin glanced quickly at
    her profile as she drove. It struck him with surprise that she had a
    certain beauty. Her thick mop of ashen hair, and firm-chinned face,
    and small, competent hands grasping the wheel, were oddly attractive.
    It wasn't the fine-edged, shimmering beauty that Nila had, but it had
    appeal.</p>
    <p>"Yes, I must be getting more accustomed to it," he answered her
    question. "And it's not as provincial as I thought. Nearly every man
    you meet here has been to space some time or other."</p>
    <p>"Every Earth boy runs away to space sooner or later," she said, and
    smiled. "Following space is in our blood. And our planet's so poor now
    that it's the only way most of our men can make a living." She added,
    "Some of our men never come back. My father didn't. And my mother died,
    when he was lost."</p>
    <p>It was dusk when they reached the spaceport. As he walked with the girl
    along its edge toward her brothers' ship, she drew him aside toward a
    tall shaft that loomed up spectrally in the twilight.</p>
    <p>"This is where the first Earthman went away to space," she told him.</p>
    <p>He looked at the deeply engraved legend on the pedestal of the soaring
    column. It was the Monument to the Space-Pioneers.</p>
    <p>"Gorham Johnson took off in his first flight from this very spot," Marn
    said.</p>
    <p>Carlin strained his eyes in the dusk to read the roll of names and
    dates engraved on the pedestal.</p>
    <p class="ph1">Gorham Johnson, 1991<br/>
    Mark Carew, 1998<br/>
    Jan Wenzi, 2006<br/>
    John North, 2012</p>
    <p>Names of the men who long ago had first dared space, the men who had
    first followed a dream to the nearby planets that then had seemed so
    far, the men who had first hurtled starward and opened up the galaxy.</p>
    <p>"Lord, more than two thousand years ago," Carlin murmured. "Queer
    little ships they must have had."</p>
    <p>His imagination was touched. This simple roll of names of men long dead
    somehow brought it all close to him for the first time.</p>
    <hr class="tb"/>
    <p>Those old, pathetically flimsy ships, the enormous courage of those men
    to whom space was all one unknown abyss. He began to understand why
    tourists came from all the galaxy to see these mementoes.</p>
    <p>"They and their little ships started it all, the whole galactic
    civilization, the vast human empire," he said musingly.</p>
    <p>Marn was looking up at the spire towering in the dusk.</p>
    <p>"People criticize us Earthmen for our pride. But this is why we're
    proud. We're the people who opened up the frontiers of the Universe."</p>
    <p>Carlin nodded thoughtfully. "You've a great heritage. But perhaps you
    remember it too well. This is the present, not the past."</p>
    <p>"You're like all the others, you think Earth's history is over," Marn
    said defiantly. "You'll find out differently. Earthmen will open up the
    last frontier of all—" She checked herself suddenly, and then said,
    crestfallen, "I'm sorry. I didn't mean to quarrel."</p>
    <p>Carlin wanted to ask what she had meant, but Marn started on again
    through the deepening darkness toward her brother's ship.</p>
    <p>He walked with her into the battered planet-cruiser and looked around
    curiously. It was a medium craft designed for a minimum crew, with
    oversize cyclotrons and propulsion-wave equipment, drive-plates fore
    and aft, and an unusually heavy set of heat-screen generators.</p>
    <p>"The Hot Side of Mercury is terrible," Marn said when she saw him
    glancing at the generators. "You need the heaviest heat-screens you can
    get to prospect there."</p>
    <p>Amidships, Carlin noticed a big, empty round room or hold. There was
    nothing in it but a skeleton of girders designed to hold something over
    a sliding plate in the floor.</p>
    <p>He remembered Jonny's big machine in the workshop. It would fit into
    this frame. He would have liked to make further inspection but Marn had
    found the instruments she had come after.</p>
    <p>As they emerged from the ship, a lean, uniformed figure in the dusk
    greeted them in a pleasant voice.</p>
    <p>"Hello, Marn. I saw you walking across the tarmac. How is Jonny coming
    with his plans?"</p>
    <p>It was a young man in the gray uniform of Control Operations, the
    agency of law and order throughout the galaxy. He bowed to Carlin.</p>
    <p>"I'm Ross Floring, Control Operations commander here. You're the
    Earth-treatment chap staying with the Lands? Glad to meet you."</p>
    <p>Floring was not more than thirty, an alert, clean-cut, likable young
    man. He turned back to Marn.</p>
    <p>"How soon are Jonny and his friends planning to take off for Mercury?"</p>
    <p>Marn looked uncomfortable. "I don't know, Ross. They have some more
    preparations to make, they say."</p>
    <p>Carlin somehow sensed a strain in the atmosphere. There was an
    earnestness in Floring's manner that was not accounted for by his words.</p>
    <p>"I like Jonny a lot, Marn," he said seriously. "You know that. I'd
    hate to see him have trouble on this expedition."</p>
    <p>Marn seemed to evade his meaning. "Jonny won't have any trouble. A trip
    to Mercury is nothing for Harb and him."</p>
    <p>"I sincerely hope he won't," Floring said quietly. "Copper isn't worth
    risking too much for. Tell him I said so, will you? And tell him I'm
    coming up some day to talk with him."</p>
    <p>Marn was obviously eager to get away. Carlin, puzzled, followed her.</p>
    <p>"I'll see you again, Mr. Carlin," Floring called after him pleasantly.
    "We can have a talk about home. Yes, I come from Canopus too."</p>
    <p>It wasn't until they were in the ato-truck driving homeward that Carlin
    realized he hadn't told Floring his name or origin. Why would Control
    Operations have taken the trouble to check up on that?</p>
    <p>"Floring seemed like a nice chap," he told Marn. The girl nodded,
    troubled.</p>
    <p>"He is—one of the best," she said. "And he likes Jonny. But he'd
    forget everything else for his duty."</p>
    <p>She was, obviously, thinking aloud rather than answering Carlin. He
    wondered again about that queer feeling of strain. It had sounded
    almost as though Floring were warning her.</p>
    <hr class="chap"/>
    <p class="ph1">CHAPTER V</p>
    <p class="ph1"><i>Desperate Play</i></p>
    <p>The truck wheezed and groaned up the dark old road to the ridge. In the
    velvet black skies, the stars were chains of glittering light. Vega,
    Arcturus, Altair—they looked far away.</p>
    <p>The house was dark when Marn stopped the truck behind it, though there
    were still lights out in the workshop. There was a solemn, buzzing hush
    about the starlit summer night.</p>
    <p>"I have to take these things back to Jonny," said the girl.</p>
    <p>"Marn, what are your brothers really planning?" Carlin asked her. "Does
    Floring know?"</p>
    <p>She twisted uncomfortably. "Jonny told you all about their plans
    himself, didn't he?"</p>
    <p>She was such a poor liar, she was so oddly appealing a figure in the
    starlight as she looked up at him with troubled white face, that
    sudden impulse made Carlin bend and kiss her.</p>
    <p>Her small body was firm and warm in his hands and there was a
    breathlessness about her cool lips. But she did not move.</p>
    <p>He looked down at her. "You don't mind, do you?" he asked.</p>
    <p>"No, I don't mind," Marn said, her voice toneless, "It's all right for
    a star-world visitor to have a little flirtation with an Earth girl
    before he goes away, isn't it?"</p>
    <p>"But it isn't that!" Carlin started to protest, and then stopped.</p>
    <p>After all, what was it but that? What could it be but that?</p>
    <p>"It's all right, but please don't again," Marn said quietly. "Good
    night, Laird."</p>
    <p>He went into the house feeling depressed and thoughtful. He wished now
    that he hadn't had that impulse. Marn wasn't the sophisticated sort.</p>
    <p>Lying in his bed and looking out the window at the distant spaceport
    beacons down in the valley, Carlin heard her come in and retire.
    Apparently Jonny and Harb were still working.</p>
    <p>What were they working at really? Why had Floring been so grave in his
    veiled warning?</p>
    <p>"Oh, the devil, it's none of my business," Carlin yawned. "There isn't
    much in this little system for them to get into trouble about. Nothing
    but eight or nine small planets and one medium sun."</p>
    <p>Carlin suddenly sat bolt upright in bed as his mind dwelt on that last
    thought.</p>
    <p>"The Sun? Good glory, that's what they're up to! It must be!
    Sun-mining!"</p>
    <p>He was dismayed, horrified by the sudden flash of revelation. The
    disquieting mystery that had puzzled him since his first coming here
    suddenly shaped clearly as pieces fell together in his mind.</p>
    <p>"They wouldn't be so crazy as to try it, surely! Yet it all fits
    together—the heat-screens on their ship, the secrecy about it all. And
    that machine I saw could be a big magnetic dredge!"</p>
    <p>Sun-mining! Most strictly forbidden of enterprises, banned by the
    Control Council for years since the first disastrous attempts at it had
    almost wrecked certain planetary systems.</p>
    <p>Visions of frightening possibilities crowded Carlin's mind, of a
    desperately reckless attempt unchaining catastrophe on the inner
    planets of this little system.</p>
    <p>"But Jonny Land wouldn't try it! He's a CE, he knows what would happen."</p>
    <p>Carlin could not convince himself. He remembered only too clearly
    Jonny's intense obsession with Earth's copper shortage, his quiet
    determination.</p>
    <p>And Floring must suspect something of the truth! That was what had made
    the Control Officer give his grave hinted warning.</p>
    <p>Carlin got up and feverishly dressed. He had to find out the truth,
    now, at once. If the Land brothers and their friends were really bent
    on such a mad enterprise, it would have to be stopped even if it meant
    his informing Control Operations.</p>
    <p>"If I could get one good look at the inside of that machine of theirs,
    I could soon tell whether it's really a magnetic dredge," he thought.</p>
    <p>He went quietly down through the dark house and out into the starlight.
    Light and sounds of activity still came from the workshop.</p>
    <p>Carlin crept toward it. He hated this spying. But he had to know. He
    couldn't permit a crazy attempt to unloose disaster here.</p>
    <p>The workshop was closed, and there were no windows. But as he stood
    irresolute, the big front doors opened and Loesser and two other young
    Earthmen came out, wearily mopping their brows.</p>
    <p>"We'll be back tomorrow, Jonny," Loesser called back into the building.
    "Ought to finish her up in a few days now."</p>
    <p>The three strode wearily toward their ato-truck and drove away. The
    doors remained open for the moment.</p>
    <hr class="tb"/>
    <p>Carlin stepped forward and from his vantage in the dark peered into the
    big lighted room. Jonny and Harb Land were putting back the metal cover
    on the central mechanism, before they too quit work.</p>
    <p>One glance at the interior of that machine was enough for Carlin's
    trained eyes. Those big magnetic-current coils, that massive beam-head,
    that battery of Markheim filters—he had been right, they spelled
    disaster.</p>
    <p>A small, hard object prodded Carlin's back and a voice throbbing with
    anger spoke in his ear.</p>
    <p>"This is an atom-pistol. Raise your hands. I don't want to harm you."</p>
    <p>"Marn!" he exclaimed, stunned.</p>
    <p>"Don't turn!" warned the girl. Her voice was choked with wrath. "I
    heard you get up and I followed you out here. You are a spy!"</p>
    <hr class="chap"/>
    <div class="figcenter">
    <img alt="" id="id-519352862673982940" src="images/illus2.jpg"/>
    <div class="caption">
    <p>"Don't turn!" warned the girl. "I followed you here. You are a spy!"</p>
    </div>
    </div>
    <hr class="chap"/>
    <p>Carlin was so stunned with horror by his discovery of the brothers'
    catastrophic plans, that he reacted by sheer, desperate impulse to the
    weapon in his back. He swung around and grabbed for the atom-pistol.</p>
    <p>It would have been suicidal, had another than Marn been holding the
    weapon. But Marn, as much a stranger as he to deadly violence, let her
    finger hesitate on the trigger too long. Perhaps she would not have
    fired in any case. Pondering it later, he was not sure.</p>
    <p>What happened was that he got his hand on the slim pistol and snatched
    it out of her grasp before her hesitation ended. Marn, her face white,
    called frantically:</p>
    <p>"Harb! Jonny!"</p>
    <p>The two brothers came running out from the rear of the lighted
    workshop, Harb's craggy face dark and deadly as he saw them.</p>
    <p>Carlin jumped back, leveled the weapon he had just taken from the girl.</p>
    <p>"Get back!" he ordered hoarsely. And as Harb Land, blindly raging, came
    on: "I don't want to kill anybody!"</p>
    <p>Jonny's voice rang command. The lame youngster's thin brown face was
    set, but he had not lost calm.</p>
    <p>"Harb, stop!"</p>
    <p>The thing froze into a queer sort of tableau as Harb Land pulled up
    and stood there, his giant figure quivering with wrath, his big fists
    clenched as he glared at Carlin.</p>
    <p>"I told you," Harb said thickly over his shoulder to his brother. "I
    told you what would happen if we took him in."</p>
    <p>Marn had run toward them, her face pale and stricken.</p>
    <p>"It's my fault, Jonny," she said despairingly. "I heard him come out
    and followed him, but let him take my gun instead of shooting."</p>
    <p>"Quiet, Marn," soothed Jonny. "It's going to be all right. Carlin just
    doesn't understand."</p>
    <p>The lame youngster, in this taut moment of strain, was suddenly the
    biggest of them, the dominating personality here.</p>
    <p>"I understand, all right," Carlin said hotly. "I guessed it tonight,
    and one look at that magnetic dredge confirmed my guess." His voice
    crackled with the rising wrath he felt. "Going to Mercury prospecting,
    were you? You never had any such plan. You and your partners have been
    getting ready to attempt sun-mining."</p>
    <p>Jonny's eyes and voice were calm as he said:</p>
    <p>"Carlin, Earth's starved for power. You've seen for yourself. To get
    the power that will revive our world, we've got to have copper. And
    the copper in our planets was exhausted long ago. But there's still
    billions of tons of copper in our System, in one place. The Sun. It's
    there in hot gases, more copper than Earth and our sister-planets will
    need for millenniums to come. It's our only possible source of copper
    and we intend to tap it."</p>
    <p>"You and the others have brooded so long over your need for copper that
    you've gone crazy!" Carlin said, his voice whipped with anger.</p>
    <p>"What's crazy about our using the copper of the Sun for our planet?"
    Jonny asked evenly.</p>
    <p>"You, a CE, ask me that?" cried Carlin. "You know as well as I do that
    sun-mining brings catastrophe! Oh, you can get close enough to the Sun
    in your ship, I know. You can suck up all the gaseous copper you want
    from it, with that magnetic dredge. But what happens on your Sun when
    you do it?</p>
    <p>"You know as well as I what would happen, what has always happened
    when it was tried. The suction creates a whirl in the solar surface,
    a tiny Sun-spot that grows and grows until it's grown into a terrific
    solar typhoon that pours disastrous increased heat and electric force
    onto its planets. You know it's happened every time Sun-mining was ever
    tried, and that that's why Control Council forbids Sun-mining."</p>
    <p>Jonny Land nodded calmly. "I know all that. But suppose I've found a
    way to do Sun-mining without starting Sun-spots?"</p>
    <hr class="tb"/>
    <p>Disbelief hardened Carlin's voice. "You haven't. Nobody ever has. There
    just isn't any way—suck out gases from any point on the Sun and you
    lower pressure at that point, and lowered pressure automatically starts
    a whirl."</p>
    <p>"Carlin, I <i>have</i> found such a way! I tell you, with it we can suck
    unlimited copper from the Sun without creating one tiny Sun-spot!"</p>
    <p>Laird Carlin stared. "You're telling me that, because you know I'm
    going to report your plans to Control Operations."</p>
    <p>"You wouldn't do that!" cried Marn, incredulously.</p>
    <p>Carlin nodded firmly. "I don't want to but I've got to. I can't let a
    bunch of crazy men bring on a disaster that might scorch life itself
    off your inner planets."</p>
    <p>Jonny Land's thin face flared irritable emotion as he limped forward
    unheeding of the gun in Carlin's hand.</p>
    <p>"Carlin, man, be reasonable! Why do you suppose I had you come here and
    live with us? It was because you're a CE and I'll need another trained
    engineer's help in operating this thing. And do you suppose I ever
    thought I could get your help unless I could convince you I've found
    the way to safe Sun-mining? I can convince you, Carlin!"</p>
    <p>Carlin felt the conviction in Jonny's voice. What the crippled young
    man said did logically explain something otherwise puzzling—why they
    had taken him into their home when their work was so secret.</p>
    <p>He remembered now that it was not until Jonny Land had learned he was
    a CE, on his first arrival on Earth, that the young Earthman had shown
    interest and offered him lodgings.</p>
    <p>"All I ask," Jonny was saying earnestly, "is that you give me a chance
    to explain our plans to you. I know I can convince you that we can mine
    the Sun without the slightest danger of disaster."</p>
    <p>"If that's so," Carlin demanded skeptically, "why didn't you convince
    the Control Council of that, and get permission for Sun-mining instead
    of trying to do all this in secret?"</p>
    <p>"Carlin, I did try to convince the Council," Jonny Land declared. "I
    made one petition to them after another, giving them full details of
    my plan. But Council isn't composed of engineers. And the popular
    prejudice against Sun-mining, due to those past disasters, is so strong
    that Council refused us permission to make the attempt."</p>
    <p>"That's why Ross Floring and the others down at Control Operations
    watch my brothers so closely, Laird," Marn added quickly. "They know
    about our petitions, and Floring suspects that Jonny is going to try
    this thing anyway."</p>
    <p>It all fitted together logically, Carlin had to admit. Yet he still
    stood irresolute, the atom-gun in his hand.</p>
    <p>"Here's a proposition, Carlin," said Jonny. "I'll explain every detail
    of our plan to you in the morning. If you don't admit then that the
    plan's completely without danger of disaster, I'll let you go and tell
    everything to Floring. I give you my word on it."</p>
    <p>Carlin looked at him doubtfully. "Jonny, you'd break your word as
    cheerfully as your neck to carry out your purpose for Earth."</p>
    <p>Jonny Land grinned crookedly. "That's true. But on the other hand,
    I'm still hoping for your help in this project. That's why I want to
    convince you, and that's the best guarantee I can give you."</p>
    <p>Carlin shrugged, but he slowly lowered the weapon.</p>
    <p>"I can tell you right now that I'll have no part in any such illegal
    venture," he said flatly. "But I'm willing to hear your explanation."</p>
    <p>"Well," Jonny said, with a tired sigh, "we've had enough dramatics
    for one evening. Harb, lock up the workshop and we'll all turn in for
    tonight."</p>
    <p>Carlin looked a little awkwardly at Marn as he handed her back the
    atom-pistol.</p>
    <p>"I'm sorry if I appear ungrateful for your hospitality," he told her.
    "It's just that I can't stand by and do nothing if a crazy attempt
    threatens to bring on catastrophe."</p>
    <p>"I know," Marn said soberly, and there was no hostility in her face.
    "But you'll find out that Jonny knows what he's doing."</p>
    <p>Out of the darkness behind them spoke a shrill voice that made Laird
    Carlin swing around in astonishment.</p>
    <p>"Well, I'm blamed glad you people quit arguin' for tonight, anyway.
    It's time all decent folks was in bed."</p>
    <p>Gramp Land stood back there in the dark where he had apparently been
    standing for some time. There was a grin on his withered face as he
    lowered the heavy atom-gun he had been holding.</p>
    <p>"Sure got tired holdin' this thing aimed at your back, Mr. Carlin," he
    chuckled.</p>
    <hr class="chap"/>
    <p class="ph1">CHAPTER VI</p>
    <p class="ph1">"<i>You Owe a Chance to Earth!</i>"</p>
    <p>Doubts assailed Carlin almost as soon as he retired. He could not
    sleep, the rest of that night.</p>
    <p>Had he been childish to let Jonny persuade him into giving the plan a
    hearing? Jonny was sincere enough, but he was a fanatic on this one
    subject of securing power for Earth.</p>
    <p>The recklessness of Earthmen was proverbial. These men, made desperate
    by long brooding over the poverty of their world, might think little of
    the danger of provoking solar catastrophe in their obsessed desire to
    secure copper.</p>
    <p>Carlin chilled. He remembered what had happened years ago at the star
    Mizar when Sun-mining had been attempted. The suck of magnetic dredges
    swiftly creating a whirl in the star's surface gases, a Sun-spot
    maelstrom that had expanded with disastrous swiftness. And then the
    engulfing of the mining ships in the sudden outpour of increased heat,
    the scorching of inner planets that wreaked ruin before the spots
    subsided.</p>
    <p>It had been the same later at Polaris, and at Delta Gemini. No wonder
    that such a popular wrath against Sun-mining had arisen that Control
    Council had strictly forbidden further attempts! Man's science, great
    as it was, was not yet great enough to dare tampering with stars.</p>
    <p>Yet he could see, too, how these Earthmen would inevitably turn their
    thoughts to Sun-mining. There was not any copper left in their System
    except in one body—their Sun. And that had limitless amounts of the
    power-metal, in vaporized form. No wonder they had been led into the
    plan to tap the metal of their Sun.</p>
    <p>Carlin dozed before daybreak, but woke with the sunrise and went down,
    to find the others already at breakfast. They greeted him with a word,
    all but Harb Land who maintained a stony, dangerous silence.</p>
    <p>"We'll go out and show you our work, as soon as you have breakfast,"
    Jonny said quietly.</p>
    <p>Gramp Land was the only one in good spirits. The old man twitted Carlin.</p>
    <p>"It's sure a good thing you got reasonable last night. I would have
    hated to blast you."</p>
    <p>Marn smiled slightly. "You wouldn't have done it. You're too
    chicken-hearted even to kill a fly."</p>
    <p>"Ho, what are you talking about?" exclaimed Gramp indignantly. "When I
    was young, they called me the toughest Earthman in space."</p>
    <p>Carlin walked silently out to the workshop with Harb and Jonny. The
    lame youngster opened the building, and then gestured toward the tall,
    cylindrical machine.</p>
    <p>"Take a look for yourself, first," he invited.</p>
    <p>Carlin scanned the mechanism with trained eyes. Magnetic dredges were
    a little out of his line, yet the principle of the mechanism was clear
    enough.</p>
    <p>"You understand the basic idea of Sun-mining?" Jonny was saying.
    "A ship approaches the photosphere or visible surface of the Sun
    as closely as possible, protected by heavy heat-screens from the
    radiation. The magnetic dredge is then turned on. The dredge generates
    a high-powered magnetic field concentrated into a beam. That beam
    drives down into the swirling super-hot gases of the solar surface.</p>
    <p>"Those gases consist of dozens of metals and other elements in
    vaporized form—iron, copper, sodium, calcium and so on, all mixed
    together. The beam sucks a column of those solar gases up to the
    ship. For its magnetic pull powerfully attracts the iron vapor in the
    mixture, and so the whole mixture is rapidly sucked upward."</p>
    <p>He pointed to the massive flared nozzles in the downward projector-face
    of the great machine.</p>
    <p>"The gases are sucked in there, through Markheim filters which can be
    set to screen out the atoms of any desired element. The copper gases
    are screened out, solidified by cooling, and stored. The other gases go
    on through the filters."</p>
    <p>Carlin nodded curtly. "And those unwanted gases are ejected into space,
    and more of the solar mixture continuously drawn up, and so on until
    your ship is filled with copper. Yes, it's the same scheme that was
    used by the Mizar and Polaris Sun-miners. And it will have exactly the
    same result! Sucking gases out of any point in the solar surface will
    lower pressure at that point. And lowered pressure at any point of the
    photosphere instantly and inevitably starts a whirl of gases, a growing
    maelstrom or Sun-spot!"</p>
    <p>Jonny Land shook his head. "Carlin, you're jumping to conclusions. This
    dredge does not simply eject its unwanted gases into space like former
    designs. Take a look at that beam-head more closely."</p>
    <hr class="tb"/>
    <p>Carlin looked. And he was puzzled, after a brief inspection of the
    curious concentric construction of the beam-head.</p>
    <p>"I don't get it. It looks like you have two circular beam-heads, one
    inside the other."</p>
    <p>"That," said Jonny, "is the secret of my scheme. Lowered pressure in
    the solar surface at the point of suction creates a whirl, a Sun-spot.
    But suppose we can suck up gases without lowering pressure?"</p>
    <p>Carlin stared. "How?"</p>
    <p>"The two beam-heads," reminded the lame youngster eagerly. "The inner
    one is the one that beams down a positive magnetic pull to suck up
    solar vapors. The outer one is designed to use a simultaneous negative
    magnetism to shoot the unwanted vapors back down into the Sun."</p>
    <p>The whole meaning of the explanation flashed over Carlin, and the
    possibilities of it dawned across his brain.</p>
    <p>He said nothing, but crawled under the towering dredge and for minutes
    inspected inside and outside of the beam-head, feed-tubes and cut-offs.
    He finally came back out to them.</p>
    <p>"Well?" challenged Jonny Land.</p>
    <p>Carlin bit his lip. "I've got to admit your scheme looks practical
    enough. You should be able to suck up gases without any Sun-spotting
    effect, by using that continuous kickback. But—"</p>
    <p>"But what?" demanded Harb Land, frowning.</p>
    <p>Carlin shook his head. "Blast it, I can't see why the Council would
    turn down your petition if this is as workable as it seems."</p>
    <p>Jonny shrugged. "I told you why. Control Council contains the finest
    statesmen in the galaxy. Statesmen, not engineers. They admitted their
    experts' reports on this showed it theoretically workable. But they
    said it was too dangerous to take a chance on theory when it comes to
    tampering with suns. We don't need copper that badly, they said."</p>
    <p>His fists clenched in sudden passion. "We don't need copper! The galaxy
    as a whole doesn't need it, they meant. And what does it matter if one
    little world called Earth is fading and dying for lack of the copper
    it squandered to open up the galaxy? What does it matter, except to
    Earthmen?"</p>
    <p>It was the first time that Carlin had ever seen Jonny Land give way to
    emotion. The superhuman strain that drove and dominated this lame, thin
    youngster for a moment flared hot and anguished on his face. Then his
    narrow shoulders sagged. He stood looking at the towering dredge with
    brooding eyes, before turning to Carlin.</p>
    <p>"Carlin," he said then, "there's only one way to prove to the Council
    this way of Sun-mining is safe—and that's by doing it! That's what
    we're going to do. We're going to the Sun and come back with a shipload
    of copper. They'll see then that it's wholly safe. They'll have to
    give permission then. And a fleet of ships equipped with dredges can
    suck enough copper from the Sun to give Earth all the power it needs
    hereafter.</p>
    <p>"You've seen the dredge and you know our plans. You've seen enough of
    Earth to know how much our success would mean to this world. Carlin, do
    you still want to tell Floring about this?"</p>
    <p>"You couldn't!" exclaimed Harb Land harshly. "You couldn't destroy all
    the hope that's left for our world's people. You—all you star-world
    people—you owe this chance to Earth!"</p>
    <p>Carlin stood there, torn by conflicting feelings. Strong among them was
    his intense admiration as an engineer for the ingenuity and daring of
    Jonny Land's solution to the problem.</p>
    <p>But there were other things to consider. There was the duty he and
    every citizen had to support the Control Council. That support was what
    kept galactic civilization going. Yet these Earthmen, this little band
    fighting so fiercely for their ancient, worn world would flout it.</p>
    <p>"Jonny!" came Marn's sharp cry from outside. "Jonny!"</p>
    <p>"Something's wrong!" Jonny exclaimed, limping hastily forward.</p>
    <p>They hurried out into the sunlight. Marn was running toward them and at
    the same moment they heard the drumming of an approaching ato-car.</p>
    <p>"It's Ross Floring coming here!" Marn panted. "I recognized his car
    coming up the hill!"</p>
    <p>Harb uttered a fierce exclamation, but Jonny cut in quickly:</p>
    <p>"He's only coming up here to look around. He suspects what we're up to,
    but he can't be sure. Don't show any excitement."</p>
    <p>Harb gestured fiercely toward Carlin. "But if he says anything, Floring
    will know."</p>
    <p>A pleasant voice hailed them. Ross Floring, lean in his gray uniform,
    drove up behind the house and climbed out of his ato-car.</p>
    <p>"Hello, folks," he greeted. "Thought I'd come up and see you. Jonny, I
    haven't seen you for weeks. Every time you come down to the spaceport,
    you spend all your time buried in that ship."</p>
    <p>Jonny smiled. "It's keeping us pretty busy, getting ready."</p>
    <hr class="tb"/>
    <p>Laird Carlin sensed genuine liking between the Control Operations
    officer and the lame young engineer. Yet there was unspoken tension
    too. It showed behind Jonny's cool smile and Floring's pleasant eyes.</p>
    <p>Floring was looking past them, through the open doors of the workshop
    at the towering magnetic dredge.</p>
    <p>"Is that your new metal-finding dingus, Jonny? The thing you're going
    to use to locate copper on Mercury?"</p>
    <p>He stepped toward it. Harb Land made a violent movement forward, but a
    flat look from his brother stopped him.</p>
    <p>"Yes, that's it," Jonny said. "Want to look it over, Ross?"</p>
    <p>Floring stood, cocking his head at the towering machine. He laughed at
    the question.</p>
    <p>"Jonny, you know I'm no engineer. A thing like this is beyond me." He
    turned toward Carlin. "But Mr. Carlin, you're a CE. What do you think
    of this new metal-finding device of Jonny's?"</p>
    <p>Breathless silence held the group for a moment. Floring's face was
    unmoved, pleasant, but his purpose was obvious now. Knowing that Carlin
    had come to Earth merely as an Earth-treatment case, he was counting on
    Carlin's unbiased truthfulness.</p>
    <p>Carlin felt their eyes on him. Now was the time, he knew, to play the
    part of a good galactic citizen and inform Floring just what was going
    on. It was his duty to do it.</p>
    <p>But he couldn't! He couldn't betray the last desperate hope of a
    gallant old planet's people in their struggle against destiny! He had
    known he couldn't, from the time Floring had first appeared. He spoke
    as casually as he could.</p>
    <p>"Yes, I've looked it over. It's one of the most ingenious metal-finders
    I've ever seen."</p>
    <p>Carlin felt a queer relief that was almost happiness, as he spoke. For
    he knew now that he could never have obstructed these people in their
    brave, desperate struggle to revive their planet.</p>
    <p>But Ross Floring looked astounded. A little blank frown of surprise
    came into his face and he stared steadily at Carlin.</p>
    <p>"Then you approve of Jonny's plans?" he said quietly, "But, of course,
    I might have known that he'd convince you."</p>
    <p>There was double meaning to the Control officer's words, clear to all
    of them. Yet they all ignored it.</p>
    <p>Floring was temporarily defeated. He couldn't take action without
    expert opinion that the machine before him was for Sun-mining. He had
    expected such an opinion from Carlin, and had been disappointed.</p>
    <p>But he was not completely frustrated. Carlin found out now how
    thorough and resourceful was this pleasant young officer.</p>
    <p>"It would be a shame, Jonny," Floring remarked casually, "if you should
    run into disaster on this trip and the design of your new apparatus be
    lost. A metal-finder like this is too valuable to lose."</p>
    <p>They were momentarily puzzled by the comment. But in the next moment,
    Floring showed what he had in mind. He drew from his jacket pocket
    a tiny tri-dimen camera, stepped close to the towering dredge, and
    before anyone could prevent it had snapped a half-dozen pictures of its
    interior mechanism.</p>
    <p>Harb Land started forward with a smothered oath. But it was too late.
    Floring was already pocketing the camera.</p>
    <p>"I'll keep these films," he said calmly. "If your machine should ever
    be lost, the design of it will be preserved this way."</p>
    <p>"You can't keep those films!" Harb Land exclaimed angrily. "You've no
    right!"</p>
    <p>"You surely don't think I would steal the design from you?" Floring
    said, with a look of surprise.</p>
    <p>"It isn't that," Harb protested. "But—"</p>
    <p>"But what?" the officer asked calmly.</p>
    <p>Harb was silent, his craggy face a mixture of emotions as he looked
    appealingly at Jonny.</p>
    <p>Carlin understood Floring's cleverness. They could not protest the
    films without giving the real reason for their protest, and that they
    could not do.</p>
    <p>"It's all right for him to keep those pictures, Harb," Jonny said
    quietly.</p>
    <p>Floring turned, bidding a pleasant farewell.</p>
    <p>"I'll be seeing you again soon," he promised.</p>
    <hr class="chap"/>
    <p class="ph1">CHAPTER VII</p>
    <p class="ph1"><i>Last Frontier</i></p>
    <p>As soon as Floring's ato-car had purred away, the little group stood in
    the sunlight outside the workshop, in stricken silence.</p>
    <p>Carlin put into words what was in all their minds.</p>
    <p>"Jonny, you know why he took those pictures! He'll telephoto them to
    Canopus headquarters to be examined by engineer experts, and they'll
    send back word that the machine is a magnetic dredge for Sun-mining!"</p>
    <p>Jonny nodded. "Yes, of course. Floring has suspected our plans all
    along, and now he's going to make sure."</p>
    <p>"And when word comes back from Canopus, he'll seize our dredge and ship
    to stop our expedition!" groaned Harb.</p>
    <p>"I know that," Jonny Land said, as his blue eyes swept them. "But it
    will take fourteen or fifteen hours before he gets that report back.
    Before that time ends, we've got to be on our way to the Sun!"</p>
    <p>Laird Carlin felt a shock of astonishment, but before he could comment,
    Jonny was speaking swiftly on.</p>
    <p>"It's our only chance now—to get away before Floring receives the
    proof that will authorize him to stop us! The dredge here is almost
    finished. If we can install it in the 'Phoenix' and take off tonight,
    we'll have our chance to prove to the galaxy that Sun-mining can be
    safe."</p>
    <p>"Install the dredge tonight?" cried Harb Land. The gangling giant's
    face was sick with anxiety. "Jonny, we can't do it! Not that soon."</p>
    <p>"We've got to!" Jonny's voice cut like a steel rapier. "Harb, you go
    get Loesser and Vito and the other boys. Have them bring the big truck
    with them. If we work hard enough, we should be able to have the dredge
    ready to roll by dark. Once we get it into the 'Phoenix', we can take
    off and complete installation in space."</p>
    <p>"You can't do it," groaned his brother. "You know you figured on taking
    a week yet for that installation."</p>
    <p>Carlin stepped forward. He had long ago reached his decision. He had
    reached it in that moment when he had answered Floring.</p>
    <p>"I'm a CE, you know," he reminded. "I can help a lot in that
    installation."</p>
    <p>Marn stared at him, amazement and dawning gladness in her eyes. And
    Harb Land's tortured face turned haggardly on Carlin.</p>
    <p>"You'd do that? You'd help us? By heaven, if you would, we might make
    it!"</p>
    <p>Jonny's brilliant blue eyes bored Carlin's face.</p>
    <p>"Carlin, I was hoping for this. I knew from the first I'd need another
    engineer's help in installing and operating the dredge. I brought you
    home because I was hoping I could enlist your aid before we started on
    the expedition. But all the same, I've got to warn you. We're directly
    bucking a Control Council order. You can lose your certificate and go
    to Rigel prison, even if our plan succeeds. And if it doesn't succeed,
    it may mean perishing with us. And after all, Earth isn't your world."</p>
    <p>"Who the devil is doing anything for Earth?" Carlin retorted. "This old
    planet of yours means nothing to me either way."</p>
    <p>"Laird, are you so sure of that?" Marn asked him, her eyes very bright.</p>
    <p>"Do we have to get emotional?" Carlin asked roughly. "I'm an engineer,
    and this is the biggest engineering experiment to be tried for
    centuries. Don't you think I want to be in on it?" He added crushingly,
    "And as for my getting mixed up in the blame, I'm already blasted well
    mixed in it. When I denied to Floring that this was a magnetic dredge,
    I implicated myself right there in the whole business. I've got to make
    it succeed, now."</p>
    <p>Harb Land was already running toward his truck. Jonny shot sharp orders
    at his sister.</p>
    <p>"Marn, I want you and Gramp to watch the road this afternoon. Floring
    might come back. Carlin, you and I haven't a moment to lose."</p>
    <p>Carlin strode after the limping youngster into the workshop, and Jonny
    there rapidly explained what remained to be done.</p>
    <p>"The kickback feed-pipes to the beam-head have to be hooked up, the
    cooling coils to solidify the copper are not yet in place, and the
    whole dredge has to be fastened in its frame so it'll be ready to swing
    aboard the truck tonight."</p>
    <p>Carlin was appalled by the amount of work that remained, for two pairs
    of hands. But Jonny added an encouraging qualification.</p>
    <p>"Loesser and Harb and the others can help in the ato-welding and cable
    work if we set it up for them. They're all veteran spacemen and know
    how to handle ordinary tools."</p>
    <p>Carlin plunged into the work with Jonny. But as they toiled to set up
    the coils and feed-pipes of the massive mechanism, an inward aghastness
    at what he was doing oppressed Carlin's mind.</p>
    <hr class="tb"/>
    <p>Why was he doing it, breaking Control law and endangering his
    certificate and even his liberty? Why under heaven should he be sharing
    the risks of these men for a planet he hadn't even seen until a few
    weeks ago?</p>
    <p>"I must still be star-sick, unstable," he thought dismally. "Or I'd
    never have got mixed up in this mad business. Sun-mining!"</p>
    <p>Blind reaction was dominating him. Curse it, he wasn't the type to
    join Quixotic forlorn hopes. He was Laird Carlin, sober, hard-working
    engineer, who ought right now to be far across the galaxy at the job to
    which he belonged.</p>
    <p>And all the time Carlin's mind spun miserably to this whirl of
    self-reproach and foreboding, he was working with Jonny at topmost
    speed, squeezing into the frame of the great dredge where the lame
    youngster could not go, fastening Veer-clamps, hooking self-sealing
    leads to the flat Markheim filters.</p>
    <p>The sound of ato-trucks rocked the noon air, and Harb Land came running
    heavily into the workshop.</p>
    <p>"I got the others—Loesser's bringing in the big truck now," panted
    Harb. "What do you want us to do, Jonny?"</p>
    <p>Loesser, and Vito, and the other four young Earthmen who came hastening
    after Harb were dominated by excitement. Loesser's broad red face was
    shining with emotion as he came up to Carlin.</p>
    <p>"I want to apologize. I never thought any star-world stranger would
    come in with us and help us."</p>
    <p>"Save it, and get the welders on those rear feed-pipes," Carlin
    retorted. "Get in here—I'll show you."</p>
    <p>Through the hot afternoon hours, the hiss of ato-welders and reek of
    fusing metal stifled the workshop.</p>
    <p>Dripping with perspiration, stiff from cramped postures, Carlin worked
    on inside the great dredge.</p>
    <p>And all those hours, in rhythm with the welders' hiss and the clang of
    wrenches, his thoughts beat a mocking tempo through his brain.</p>
    <p>"All this, for no reason! For somebody else's world, a world that ought
    to have been evacuated long ago! Even if it succeeds, you win nothing.
    And if it fails, the Sun licks you all up like midges."</p>
    <p>Yet he labored blindly on. It might be crazy, but what he had started,
    he would finish.</p>
    <p>It was work against an inexorable time limit that rapidly was
    approaching. As the shadows lengthened, as the sun went down, they
    still had not finished.</p>
    <p>Jonny Land limped unsteadily to turn on the workshop lights. His face
    was a gray mask of fatigue and sweat as he turned to the others.</p>
    <p>"Two more hours," he said huskily. "We can't take more, if we're to get
    the dredge into the 'Phoenix' and take off before midnight."</p>
    <p>Those two hours, afterward, seemed weeks in length to Carlin. And the
    mocking devil in his brain kept taunting, "It's no business of yours,
    you know!"</p>
    <hr class="tb"/>
    <p>"That's near enough!" Jonny's hoarse voice finally declared. "We can
    hook up those last cables on the way. All the work that require heavy
    tools is done—and we daren't take more time."</p>
    <p>They were, all of them, drunk with fatigue, staggering with the furious
    drive of twelve hours of unbroken toil. Blackened by welder flare,
    glistening with sweat, they looked to Carlin like a crew of devils.</p>
    <p>Jonny's driving energy remained unconquerable.</p>
    <p>"Marn," he ordered, "back the big truck in here. Harb, you and Carlin
    rig the hoist."</p>
    <p>The big, flat-bodied ato-truck backed ponderously into the workshop
    and they swung the massive magnetic dredge carefully aboard. Loesser
    and the others then hastily chained it to the bed of the truck.</p>
    <p>Jonny limped toward the cab. "All right, we're starting. Harb, you
    drive. No, Marn—you're not going to the spaceport with us."</p>
    <p>Marn, face white and eyes big with fear, saw the gleam of the
    atom-pistol that Harb was thrusting into his pocket.</p>
    <hr class="tb"/>
    <p>"Oh, Jonny, not that, no matter what happens!"</p>
    <p>Jonny's blue eyes flashed arctic light. "That, or anything, now," he
    rasped. "You know what this means to our people, Marn."</p>
    <p>Then his face softened, and he patted her arm.</p>
    <p>Tears streaked her cheeks as she kissed and clung to him, and then to
    Harb.</p>
    <p>Carlin was climbing heavily onto the truck when he felt her touch on
    his arm.</p>
    <p>"You too, Laird," she whispered, quivering lips blindly pressing his
    cheek. "All of you must come back."</p>
    <p>"Get on!" cried Harb Land, and then the truck went into gear.</p>
    <p>Carlin jumped for the cab, and under the starry night they were rolling
    at increasing speed down the twisting road toward the valley.</p>
    <p>And suddenly all the nightmare mocking in Carlin's brain was gone and
    there was only the rush of sweet air against his face, and the splash
    of the lamps ahead, and the jolt and rumble of the big machine as they
    raced down toward the spaceport's distant beacons.</p>
    <hr class="tb"/>
    <p>Earth air and Earth smells in Carlin's nostrils, sleepy Earth sounds
    in his ears; the shine of the old spaceport's beacons, and the soaring
    loom of the distant tower that marked the spot where a man of long ago
    had first dared space. This world, this little Earth, was worth risking
    death for, even for a stranger from far stars!</p>
    <p>He knew he was a little crazy, he still had a corner of his mind that
    told him all this was mere intoxication of emotion which was sweeping
    away reason. But the mocking devil in Carlin's mind was gone, and he
    was one in mind and purpose with his companions, now.</p>
    <p>The others too were feeling that wild reaction, for Loesser clapped
    Carlin's shoulder, crying:</p>
    <p>"It's like getting out of prison to get started!"</p>
    <p>"We're not off Earth yet!" warned Jonny. "Cut the lights and drive
    around to the north end of the spaceport, Harb. Ease the truck to the
    'Phoenix' as quietly as you can." A little later he warned, "Slower,
    slower. Keep to the edge of the tarmac."</p>
    <p>Lightless, its motors a mere low rumble, the big truck crept around the
    dark edge of the spaceport toward the "Phoenix." The little planet-ship
    took black shape in the darkness, a low, torpedo bulk brooding beneath
    the stars. Harb backed the truck toward its side, as they jumped out of
    the cab.</p>
    <p>Light flashed on them from a hand-krypton in the door of the "Phoenix!"
    A lean, uniformed figure stood there, gun in hand, looking at them.</p>
    <p>"I thought you would be coming," said Ross Floring quietly. "Jonny, I'm
    sorry about this."</p>
    <p>Carlin was as frozen as his companions, by the disastrous overturn of
    their attempt at secrecy. Floring stepped out of the ship.</p>
    <p>"I've been looking through your ship while I waited," he said. "You
    have triple as much heat-screen coverage as you'd need for the Hot Side
    of Mercury. You were going to the Sun."</p>
    <p>"You can't prove it, Ross," Jonny said levelly. "You've no proof."</p>
    <p>"I've enough to prohibit this ship from clearing Earth until
    investigation," Floring replied. "A certain report will reach me from
    Canopus by morning. Then we'll see."</p>
    <p>Carlin saw it then, saw the dark giant figure of Harb Land stealing
    around the truck and looming up behind Floring. He glimpsed the gleam
    of Harb's raised atom-pistol.</p>
    <p>Then Harb struck. The butt of the weapon came down on Floring's head
    and the officer crumpled limply to the tarmac.</p>
    <p>"See if anyone else is in the ship!" Jonny said swiftly. "Loesser,
    watch the Control station!"</p>
    <p>Then he bent with Carlin over the unconscious man.</p>
    <p>"We'll have to take him with us," Jonny said. "If we leave him here
    he'd soon be found, then the Control cruisers would be after us."</p>
    <p>A few weeks before, Laird Carlin would have been aghast at seeing
    a semi-sacred officer of Control Operations struck down. With what
    spirit of reckless defiance of law had his companions infected him? He
    marveled at himself as he coolly picked up the limp figure.</p>
    <p>"Tie him into one of the chairs in the pilot room," Jonny was saying.</p>
    <p>Harb came plunging out of the ship. "Nobody else aboard. He came over
    here alone."</p>
    <p>By the time Carlin had the unconscious man secured in the pilot room,
    Harb and the others had slid open the big hatch in the side of the
    "Phoenix." Hastily, fumbling in darkness, they ran out the ship hoist
    and hooked onto the big magnetic dredge.</p>
    <p>Then, with infinite labor, they swung the massive mechanism into the
    hold amidships. Mere short flashes of hand lamps had to suffice to
    guide the beam-head of the dredge down into the round keel opening.</p>
    <p>"Fasten half the frame bolts—they'll hold till we get into space,"
    panted Jonny.</p>
    <p>Carlin skinned his knuckles in the dark, fumbling with bolts and
    wrench. Every instant he expected to hear an alarm from Loesser that
    Control officers were coming.</p>
    <p>"That'll have to hold," said the sweating Jonny. "Run the truck off the
    tarmac. Harb, make ready for take-off!"</p>
    <hr class="chap"/>
    <p class="ph1">CHAPTER VIII</p>
    <p class="ph1"><i>Solar Struggle</i></p>
    <p>Oxygenators started throbbing, doors clanged, as the others tumbled
    aboard. Harb Land, smeared with dirt and oil, his shock of hair wild,
    climbed into the pilot seat and expertly touched controls.</p>
    <p>"Generators coming on!" sang Loesser's breathless voice from the
    interphone, as the low, deep hum began.</p>
    <p>"Stasis on," said Harb rapidly, his fingers busy. The blue cushion of
    force was around them as Carlin slumped drunkenly into a seat. "Zero,
    two and five acceleration schedule. Here we go!"</p>
    <p>And the "Phoenix" swept up with a rush from the spaceport, the
    propulsion-waves streaming from its drive-plates hurling it out and
    upward into the star-sown sky, the spaceport lamps and the southward
    blinking lights of New York falling swiftly away.</p>
    <p>"Authorization!" yelped a startled voice from the universal communic on
    the panel. "Give authorization for take-off!"</p>
    <p>"Authorization already given," Harb Land rapped back, then cut the
    communic. He laughed. "That'll puzzle them a while."</p>
    <p>Crazy, reckless, suicidal, to Carlin seemed the way that Harb was
    taking them out from Earth. The atmosphere of the planet had no sooner
    started a shrill, rising scream around them than it fell and faded as
    they came out of the envelope of air.</p>
    <p>Luna burst up out of the eastern heavens like a great globe of dull
    gold against the stars. And then Carlin's eyes were smitten by the
    flare and glare of the brilliant disk of Sol, of the Sun.</p>
    <p>And then the "Phoenix" lined out and was plunging headlong through the
    void at a speed that Carlin knew was flatly illegal to use inside any
    System, a rush toward that distant Sun flare.</p>
    <p>"Cut down, cut down!" cried Jonny to his brother. "Any more speed and
    you'll not be able to decelerate in time to orbit around the Sun."</p>
    <p>Harb Land turned a wild, dirty face aflame with emotion. "By heaven,
    we're on our way at last! We'll show them now that Earthmen can still
    blaze a space-trail nobody else has dared!"</p>
    <p>And from back amidships came a hoarse voice jubilantly singing the old
    Earth space-song:</p>
    <div class="poetry">
    <div class="stanza">
    <div class="verse">Blast away toward the stars—</div>
    </div></div>
    <p>Jonny Land's voice lashed them, his thin face dripping and determined.</p>
    <p>"You're all of you blowing your tops with excitement. This hasn't even
    started yet. Look at what we're heading for!"</p>
    <p>Carlin heard the others fall silent and himself felt a chill of awe as
    he looked ahead at the giant fire orb toward which the "Phoenix" was
    plunging.</p>
    <p>"We'll be orbiting before we have the dredge set up, unless we hurry,"
    Jonny prodded. "Come on, help me with it."</p>
    <p>The big magnetic dredge had to be bolted into place, the coils and
    pipes had to be hooked to their connections inside the ship, the cables
    to the generators, the cooling coils to the compressor, the outlets of
    the Markheim filters to the bunkers astern.</p>
    <p>Thrumming, creaking, shivering in every strut to the blind thrust of
    power that was hurling it on, the "Phoenix" rocked and shook about them
    as Carlin labored with Jonny and two of the other men to make those
    last connections. The cramped space in the hold around the dredge was
    hot, stifling, for the oxygenators couldn't keep the air there pure.</p>
    <p>"All ready!" Jonny called finally, after eternal-seeming hours of toil.
    "And none too soon. We're getting there fast. Harb has put out most of
    the heat-screens."</p>
    <p>Through the windows, the ship seemed enveloped by a halo of dim light,
    the force-screens that repelled radiations of heat.</p>
    <p>But when Carlin stumbled with Jonny into the pilot room, they were half
    blinded even through the screens by the fierce, blazing glare from
    ahead.</p>
    <p>Half the sky ahead was Sun, a gigantic abyss of roaring flame that
    crushed the mind by its magnitude. All directions of space seemed
    canceled, and they were falling, falling, into an inferno of fire.</p>
    <p>Harb turned a sweating face. "We'll cut off to orbit in less than an
    hour," he informed.</p>
    <p>Ross Floring spoke from the chair in which he was tied, and in which he
    had come back into consciousness.</p>
    <p>"Jonny, I've been waiting for you! Harb wouldn't listen to me. You've
    got to turn back!"</p>
    <p>Jonny shook his head. "No use, Ross, I know you're only doing your
    duty. And I'm sorry to drag you into this danger. But we're not
    stopping now."</p>
    <p>"But you'll never get there!" Floring exclaimed. "Control cruisers must
    already be after you. They'll have found out where I am by now."</p>
    <p>"Empty threats!" Harb jeered. "They can't know where he is."</p>
    <p>"Jonny, look at my badge!" cried Floring. "See the tiny radio bulb in
    the back of it? It's a 'finder' by which any Control officer can be
    located at any distance. When I didn't report back, they'd use it to
    spot me out here."</p>
    <p>"If that's true," said Jonny Land, his thin face suddenly haggard,
    "they'll be after us by now. Harb, cut the communic back in!"</p>
    <hr class="tb"/>
    <p>Harb obeyed. Roar of static from the gigantic orb ahead was a dull
    background to the sharp voice that came from the instrument.</p>
    <p>"Control Operations squadron four hundred thirty-three nine calling
    'Phoenix!' Last warning! We are overhauling you and will shell you
    unless you turn and surrender."</p>
    <p>Startled, Harb Land jabbed a button and twisted the knob of the
    visor-screen. The far-seeing eye quartered space behind them, and then
    the black space scene held steady. There against the stars came a
    little pattern of four tiny triangles of light. Triangles—galaxy-wide
    sign of Control.</p>
    <p>"By heaven, they actually have come after us!" cried Harb. "Jonny,
    they're only minutes behind us and pulling up fast!"</p>
    <p>"We broadside as soon as we range you unless you turn now," warned the
    steely voice from the communic.</p>
    <p>Laird Carlin, only a few weeks before, would no more have dreamed of
    disobeying a Control Operations command than he would have of picking
    stars from the sky. Galaxy citizens were trained to revere the great
    organization that had made the Universe a place of law and order.</p>
    <p>But the ancient independence of these men of Earth was strong in him
    now. They had already risked so much, had incurred certain penalty even
    if they now surrendered.</p>
    <p>"Keep going!" Carlin exclaimed. "They can't follow us once you start
    orbiting close to the Sun's photosphere. No ordinary Control cruiser
    has heavy enough heat-screens to follow us into that!"</p>
    <p>"By Jupiter, it's so!" exclaimed Harb, faint hope lighting his face.
    "But I daren't crowd on more speed now. I've got to start decelerating
    if we're to orbit correctly."</p>
    <p>"Decelerate by plan," Jonny said grimly. "They may not range us in
    time. We'll soon know."</p>
    <p>The "Phoenix," flying at a tangent toward the gigantic sphere of the
    Sun, was aiming to swing into an orbit around Sol as close as possible
    to its photosphere or gaseous surface.</p>
    <p>It had to be so. No ship would ever have power enough to go that close
    to the Sun's colossal pull and hold its position by its own energy. To
    get that close and to stay that close to Sol without being drawn in to
    it, a ship had to go into an orbit around it like a tiny satellite.</p>
    <p>The air in the "Phoenix" was already stifling hot. Jonny switched in
    another of the heat-screens, and the dim halo around the flying ship
    deepened.</p>
    <p>Harb's fingers were flashing over the controls, decelerating, steering
    the ship in a closing spiral toward the Sun.</p>
    <p>"Carlin, talk them out of this madness!" cried Ross Floring, aghast.
    "The cruisers will be broadsiding us in moments."</p>
    <p>Carlin paid no attention. His eyes were on the visor-screen where the
    four cruisers now loomed big as they came closer.</p>
    <p>Then it came. Silent, deadly, four blinding gouts of flame burst near
    the "Phoenix." Four salvos of atomic shells whose wave of force rocked
    the plunging ship. Loesser came tumbling into the pilot room, red face
    glistening.</p>
    <p>"They'll bracket us next salvo or two!" he yelled. "What's our chance?"</p>
    <p>"Turn on heat-screens Six and Seven!" roared Harb Land, without looking
    around. "I'm going into orbit now!"</p>
    <p>"It's too soon!" Jonny cried warning. "It's—"</p>
    <p>Carlin saw that Harb hadn't even heard. The giant was recklessly
    cutting the elements of their plotted course, depending on their own
    power to pull into orbit in time.</p>
    <p>The heat-screens, all they had, were on full now. Another salvo burst
    to spaceward of them. Carlin knew the men behind realized Floring was
    aboard. But Control Operations would sacrifice any men to prevent the
    Sun-mining that always before had meant disastrous solar disturbances.</p>
    <p>"Great blazing stars!" breathed Loesser, staring. "Look at that!"</p>
    <p>Forgotten, the deadly shells that were groping for them. For now the
    "Phoenix" was deep in the awesome corona of the star and was curving in
    closer through heat that was over two thousand degrees.</p>
    <p>Carlin's mind shook to the fearful spectacle that was the firmament.
    Not he, nor any other living man, had ever come so close to a star.
    They were entering a region of such violent energies that all laws of
    space and time here seemed cancelled.</p>
    <p>Blinding, eye-dazing even through the strong protective filter of the
    heat-screens, the brilliance of Sol stunned them. They looked on a
    vast, raging ocean of flaming gases, a sea of vaporized metallic and
    non-metallic elements that was like a cosmic furnace.</p>
    <hr class="tb"/>
    <p>Even through the heat-screens, the radiance heated the air in the ship
    scorchingly. But now the visor-screen showed that the Control cruisers
    were falling back and disappearing from sight behind.</p>
    <hr class="chap"/>
    <div class="figcenter">
    <img alt="" id="id-134734920588562893" src="images/illus3.jpg"/>
    <div class="caption">
    <p>Blinding, eye-dazing even through the filter of the heat-screens, the brilliance of Sol stunned them.</p>
    </div>
    </div>
    <hr class="chap"/>
    <p>"They couldn't follow us this close to the photosphere!" Harb cried
    exultantly. "We've shaken them and we're almost in orbit."</p>
    <p>"You can't orbit the Sun!" Floring pleaded. "And even if you could, the
    cruisers will lay to outside the heat and range you by locator and fire
    till they destroy us! Put about!"</p>
    <p>The man Vito, choking and gasping for breath, came into the pilot room
    from the engine rooms astern.</p>
    <p>"Heat-screens won't take another dyne! If we go closer, we're done for."</p>
    <p>"We're orbiting now," Jonny said huskily. "Wait!"</p>
    <p>Harb Land was engaged in the most difficult operation of spacemanship,
    bringing a ship into exact balanced orbit around a celestial body.</p>
    <p>Most difficult, even when the body was a planet. Impossible, nearly,
    when the body was a Titanic star!</p>
    <p>Carlin saw the giant's face a frozen mask as he centered his dial
    needles, fed force with infinite delicacy, guided, changed—and changed
    again.</p>
    <p>Harb reached and slammed open a switch. The hum of propulsion waves
    died. The "Phoenix" was without driving power. And the needle of the
    gravi-gauges remained constant, the ship's path around the Sun was
    unvarying.</p>
    <p>"We've orbited!" Harb Land's voice was a hoarse, exhausted sound.</p>
    <p>Carlin wanted to shout, "By heaven, there are no spacemen in the galaxy
    except Earthmen—none!"</p>
    <p>The "Phoenix" was circling the Sun, deep in the corona and reversing
    layer and close to the photosphere or light-emitting surface which was
    the vague boundary of the star itself.</p>
    <p>Their sensation was that of men suspended over a Universe of raging
    flame and force. The mind shook to the impact of it. They were here
    where no men, no life, had ever been intended to be. They were
    violating the sanctity of a star.</p>
    <p>"Now—the dredge," Jonny said hoarsely. "We've not power enough to
    force the heat-screens like this for long. Come on, Carlin."</p>
    <p>Carlin stumbled back with him into the stifling hold. The men around
    the towering magnetic dredge were like sooty devils staring with wild
    eyes.</p>
    <p>The metal was so hot its touch made him cry out as he closed the
    circuit of the generators with the ato-turbines. The rotors began their
    whine, building up a magnetic field.</p>
    <p>The whole ship suddenly shook and quivered. Harb came plunging back
    into the hold.</p>
    <p>"Those Control Cruisers are starting to salvo us by radiolocator!"</p>
    <p>"We only need a little time," panted Jonny Land. "The cooler coils,
    Carlin!"</p>
    <p>Carlin felt like a man in a dream as he sweated with Jonny to get the
    magnetic dredge started. The field was building steadily, and the great
    nozzles of the beam-head had been lowered below the keel. Jonny's
    brilliant eyes clung to the panel of gauges, and finally he opened the
    field-switch.</p>
    <p>"Now!"</p>
    <p>They crowded around the view-plate in the keel, peering half-blindly
    down against the glare of the raging Sun-sea below. The dredge was
    projecting a powerful, concentrated magnetic field down into that ocean
    of flaming gas like a sucking straw. But for moments they saw nothing.
    Time that seemed endless went by. Then—</p>
    <p>"Here she comes!" yelled Loesser.</p>
    <p>A column of flaming vapor was shooting up from the fiery ocean below.
    Compared to the gigantic mass of Sol, it was the merest filament, the
    flimsiest thread of fire.</p>
    <p>But it was rushing up and up toward the hovering "Phoenix," a finger
    of fiery vaporized elements drawn irresistibly up along the beam of
    magnetism to the ship.</p>
    <p>Another salvo of shells went off in space somewhere close by and rocked
    the ship with its wave of force. But next instant came a heavier
    impact, as the fiery column of gas reached the nozzles below the ship.</p>
    <p>They heard a deafening roar. That up-sucked stream of vaporized
    elements was being drawn through the heat-proof nozzles and intakes,
    through the Markheim filters that screened out its copper atoms, and
    was then being shot downward again by the kickback's negative field.</p>
    <p>"The kickback's working!" Jonny Land yelled. "If the effect of it is
    what we calculated, we've done it!"</p>
    <hr class="chap"/>
    <p class="ph1">CHAPTER IX</p>
    <p class="ph1"><i>An Earthman Comes Home</i></p>
    <p>For the moment, none of them paid any attention to the fact that
    precious copper was solidifying in the cooler coils into granules of
    metal that were being blown into the bunkers. The real test was what
    their beam of magnetic force was doing to the surface of the Sun.</p>
    <p>Did it seem incredible, as it almost did to Carlin, that such a
    fragile finger of force could in the least disturb the mighty orb
    below? He knew better. He knew the unnaturally delicate balance of a
    star's surface, which a slight change of pressure artificially induced
    could stir into a whirl that would expand in giant Sun-spots. If that
    happened, it would mean chaos.</p>
    <p>"No sign of a whirl yet," Jonny breathed, peering down through black
    glare-proof lenses. "No sign at all."</p>
    <p>There was no moment of crisis, no clean-cut moment of triumph. There
    was just the time speeding by, the flow of copper into the ship, and
    the constant reports of Jonny—"No whirl forming yet."</p>
    <p>Salvos shook the ship as the Control cruisers far outside the sun
    glare fired more and more accurately. But they went unheeded. Success
    or failure of the most audacious engineering exploit in the galaxy's
    history hinged upon Jonny's muttered reports.</p>
    <p>"No whirl yet."</p>
    <p>Jonny Land finally raised his head, looked at them as they stood with
    wild surmise on their faces.</p>
    <p>"We've done it," he said, almost unbelievingly. "We've nearly filled
    the bunkers with copper and there's no whirl down there, no disturbance
    to grow into a spot. We've made Sun-mining possible."</p>
    <p>Tears were running down Loesser's face. Harb Land looked dazed. But
    Jonny walked across the hold to the wall through which the cooler coils
    fed into the bunkers. He peered through a quartz view-plate.</p>
    <p>They looked with him. The bunker rooms were heaped high with shining
    red granules. Copper, virgin-pure, blown into the rooms and already
    almost filling them. Copper milked from the Sun!</p>
    <p>"Copper for Earth!" whispered Jonny, his thin face blazing now. "Power,
    and new life, for the old planet!"</p>
    <p>The "Phoenix" rocked wildly and metal screeched rendingly as they were
    flung from their feet by a salvo that had finally bracketed the ship.</p>
    <p>"The feed-pipes!" screeched Loesser, scrambling to his feet beside
    Carlin.</p>
    <p>Carlin saw. The ship's walls had held, but the shock had snapped
    strained cables and cooler coils. Two intake tubes were giving way,
    white-hot copper vapor forcing out through cracks in them.</p>
    <p>"Veer-clamps on those two pipes!" yelled Jonny. "If they give,
    everything goes!"</p>
    <p>Knowledge of what it meant if the pipes gave way, if super-heated
    metallic vapor blew out into the hold, flung Carlin in a crazy rush for
    the Veer-clamps and wrenches.</p>
    <p>He got a clamp around one of the pipes, and the man Vito started
    spinning shut the bolts that would hold the fracture tightly. He swung
    round toward the other pipe.</p>
    <p>"Clamp!" yelled Jonny Land, in a cry that was like a hoarse howl of
    agony.</p>
    <p>Carlin's blood left his heart as he glimpsed the most horrible and
    heroic sight he had ever beheld. The other strained tube had been
    about to blow open, and Jonny Land had flung his arms around it and
    was holding it together by agonized effort while the white-hot vapor
    sprayed his body.</p>
    <p>Harb Land wildly snatched his brother away as Carlin flung the big
    clamp around the pipe and convulsively spun its bolts shut.</p>
    <p>He staggered around then. Harb was bending over his brother.</p>
    <p>"Jonny! Jonny!"</p>
    <p>Jonny's whole chest and neck were blackened and blasted. His face was a
    ghastly, sooted mask as his eyes looked up at them.</p>
    <p>Another salvo went off close by, and again the "Phoenix" rocked wildly.</p>
    <p>"Cut the dredge!" Carlin cried. "We've proved the process is
    successful, and we can't stay here now or your brother will die!"</p>
    <p>Loesser cut off the dredge and Harb Land rushed for the pilot room.
    Carlin heard him shouting there into the communic:</p>
    <p>"Control cruisers from 'Phoenix!' We're putting out to surrender. Be
    ready to give injured man medical treatment."</p>
    <p>"Break out of your orbit at once and we'll contact you for surrender by
    locator when you're outside the corona," came the sharp, fast answer.</p>
    <hr class="tb"/>
    <p>The generators of the "Phoenix" started roaring their shrillest note as
    Harb Land frantically flung power into the drive-plates. Beneath the
    thrust of its propulsion vibrations the battered ship began to move, to
    fight its way out of the gigantic pull of Sol, breaking slowly out in a
    tangent off its orbit.</p>
    <p>Carlin, Loesser, all of them in the hold, were bending over Jonny Land
    when Floring, released by Harb, came back. The officer looked down and
    then shook his head somberly.</p>
    <p>"No chance," he said. "He won't even last until we reach the cruisers."</p>
    <p>Jonny was lying, unhearing, fighting for breath, looking up at them
    without seeing them, his sooted face a writhing mask. Carlin felt tears
    sting his eyes, and saw everything through a blur.</p>
    <p>"Jonny, we did it—you did it!" Loesser was choking. "Made Sun-mining
    possible! Why, soon now there'll be scores of ships, new, big ships,
    coming here and getting all the copper Earth needs!"</p>
    <p>He was, Carlin knew, trying to reach home to the dimming mind with that
    reassurance, that assurance that the dying man had not given away life
    in vain.</p>
    <p>It didn't reach Jonny Land. He wasn't Jonny Land any longer, he was
    just a living creature dying in pain, and he couldn't feel or know
    anything but pain. And then the pain went, and life went with it, and
    his face was a lax, empty mask that had no meaning for them.</p>
    <p>Loesser sobbed: "He didn't know—he didn't know what I was saying!"</p>
    <p>Carlin felt dull, tired, drained of emotion. He had just seen the only
    hero he had ever known die, but a hero's death was just death, just
    mortal pang and final release.</p>
    <p>He went forward to the pilot room.</p>
    <p>"Jonny's dead," he said to Harb Land.</p>
    <p>Harb's shoulders sagged, but he did not turn as he guided the "Phoenix"
    on spaceward to where the grim Control cruisers waited.</p>
    <hr class="tb"/>
    <p>Control Court here in New York was only a small room in the building
    by the spaceport. There were no officials in it except the three
    middle-aged judges who sat behind a small table and prepared to pass
    sentence on Laird Carlin and his seven comrades.</p>
    <p>There were no lawyers, no oratory, no jurymen. They were not needed.
    The government psychologists who had quietly questioned the accused men
    during their four days in prison had submitted the factual hypnosis
    records which were complete and incontrovertible evidence.</p>
    <p>The chief judge, the man in the middle, quietly read the decision as
    Carlin and the others faced him.</p>
    <p>"This court is placed in a peculiarly difficult position in assessing
    your offense. On the one hand, you men deliberately broke a Control
    Council regulation and defied its officers. On the other hand, your
    action has proved the practicability of a process of Sun-mining which
    will be of incalculable value to this and every other System in the
    galaxy.</p>
    <p>"To forgive your offense because the ultimate result was good would be
    to set a fatal precedent. It would establish the principle that illegal
    means do not matter if end-purposes are good. We cannot permit such a
    precedent to be established. Therefore, regretfully, this court must
    pass the prescribed punishment for your offense."</p>
    <p>Carlin could not deny the crystalline logic. He had known from the
    first that this must be the issue, and he was too tired to care.</p>
    <p>"You are sentenced to two years imprisonment in Rigel Prison and
    also to the loss of your spacemen's licenses or Cosmic Engineer's
    certificate, whichever you hold. Such sentence is obligatory in this
    case." He added quickly, "It is, however, within our discretion to
    suspend the prison term and to limit cancellation of your certificates
    to one year from date. Such is the sentence of this court."</p>
    <p>Loesser drew a gusty breath of relief. "For a minute, I thought it was
    Rigel for us sure enough!"</p>
    <p>The chief judge had risen. "Speaking personally," he added quietly, "we
    would like to congratulate you men upon a great achievement."</p>
    <p>Ross Floring came to their side.</p>
    <p>"A year's suspension isn't long," he said, and Carlin nodded wearily.</p>
    <p>When, with Harb Land's giant figure leading them, they emerged from the
    building into the sunlight, a roar that deafened them came from the
    waiting crowd outside. The people of Earth, at least, had no need to
    temper their gratitude.</p>
    <p>Harb was grimly silent as he pushed through the crowd toward Marn and
    old Gramp Land. Carlin found himself buffeted by eager hands, assailed
    by joyful faces and voices, as he followed.</p>
    <p>A grizzled, excited man clapped his shoulder. "We Earthmen showed 'em
    we could still conquer space, didn't we?"</p>
    <hr class="tb"/>
    <p>We Earthmen? Somehow, for the first time in all these days, Carlin's
    dulled mind felt a stir of pride as though at an accolade.</p>
    <p>He didn't like to meet Marn's pale face. But she spoke steadily.</p>
    <p>"It's all right, Laird, about Jonny. Women of Earth for two thousand
    years have seen their men go out into space—and not all come back."</p>
    <p>Floring had followed them. "I want you to see something," he said.</p>
    <p>He led the way toward the towering Monument of the Space-Pioneers.
    Carlin looked at the roll of names. Then his eyes suddenly blurred as
    he saw that, for the first time in several centuries, a new name had
    been added to the bottom of that great roll.</p>
    <p class="ph1">JON LAND</p>
    <p>Marn's eyes were shining. And her giant brother looked long, with
    haggard face somehow comforted. But old Gramp Land turned sadly away.</p>
    <p>"A name on a stone is poor exchange for my boy," he muttered. "I'm
    gettin' old."</p>
    <p>That evening, in the old house up on the ridge, they were subdued and
    silent at dinner. The table was too big, and they looked around too
    often as if listening for a familiar limping step and a cheerful voice.</p>
    <p>Carlin was doubly oppressed because of the thing that he had not yet
    told them. He hated, somehow, to break the news.</p>
    <p>"There's something they found out when they made our psycho-records for
    the trial," he said finally. "Mine showed that I had no instability of
    coordination, no star-sickness any longer."</p>
    <p>"You mean, you're cured?" said Harb, surprised. "Why, that's fine. I
    never thought of it, but you made the trip Sunward all right, so I
    should have known."</p>
    <p>"The psychos say," Carlin told them, "that some people out in the
    galaxy now and then approximate much closer to the original Earth stock
    than the average. Such people respond rapidly to Earth-treatment. I'm
    one of them, it seems." He added uncomfortably, "I can go back home to
    Canopus now, though I'll have to work at a desk job for a year. The
    only thing is that there's a ship for Canopus tonight, and there won't
    be another for weeks."</p>
    <p>"You're not going tonight?" exclaimed Harb. "Not as soon as that?"</p>
    <p>Carlin felt a little heartsick. "I wish I didn't have to, so soon. But
    there's nothing for me to do here now that I'm all okay."</p>
    <p>He had somehow expected Marn to protest too. But she did not. She only
    said quietly:</p>
    <p>"I'll drive you down to the spaceport."</p>
    <p>"I think I'd rather walk down," Carlin said slowly. "I don't know why,
    but I would. It's not far and I sent my bags on down."</p>
    <p>"Then I'll walk a little of the way with you," said Marn.</p>
    <p>Twilight had changed into soft summer darkness by the time Carlin had
    exchanged a last old-fashioned hand grip with Harb and Gramp Land, and
    started down the road with Marn.</p>
    <p>She went only around the first turn of the old road with him, and then
    stopped.</p>
    <p>"Good-by, Marn," he said, but she only averted her face.</p>
    <p>Carlin hesitated, then turned and walked on. Luna was lifting its
    shining shield in the east, and the silver summer silence lay over
    everything, hardly broken by the stir of branches and the low buzz of
    insects. The night was warm and still.</p>
    <p>He had a lump in his throat and he tried to laugh at himself because he
    had it. A man couldn't let illogical emotions overrule his reason. This
    crazy, heroic old planet Earth and its people—he would never forget
    them, but he had to return to his own life and work, he had to go home.</p>
    <p>Laird Carlin suddenly stopped. He knew, abruptly, why dull oppression
    had gnawed his mind all day. It wasn't because he was going home. It
    was because he was leaving home. He was leaving the only place where
    his spirit had ever found something it had always lacked, a peace, an
    ancient certitude, a kinship that had grown and grown.</p>
    <p>Carlin turned and strode rapidly back up the road. Not until he was
    almost upon her did he perceive that Marn Land was still standing in
    the silvered road where he had left her.</p>
    <p>"I was waiting for you," she said simply. "I knew you wouldn't go."</p>
    <p>His hands grasped her shoulders as he spoke in a rush.</p>
    <p>"Marn, I couldn't! I thought of Canopus, I thought of friends there and
    a girl who likes me and the garden cities I used to love, and it was
    all unreal, I'm tied somehow to this queer old planet, to Jonny and
    Harb and all of the others, and to you!"</p>
    <p>She came into his arms quietly. "I know. There's been more than one
    like you, more than one who came to Earth and found he somehow couldn't
    leave. This old world is in the blood of our race, Laird." She looked
    up. "A year's not long. We'll need you here to replace Jonny, to
    supervise the Sun-mining. And I need you. I always will."</p>
    <p>Carlin held her closely, all tiredness and doubts gone now, strangely
    content. He looked up at the summer stars and thought of worlds out
    there, but it was all far away, far away.</p>
    <p>And Earth was close, its ancient quiet night enfolding him. Soft wind
    stirred leafing branches in the moonlight, and the road wound up white
    and sure toward the old house, and out of the vastness of time and
    space, an Earthman had come home.</p>
    <div style="display:block; margin-top:4em"></div><section class="pg-boilerplate pgheader" id="pg-footer" lang="en">
    <div style="text-align:center">
    <span>*** END OF THE PROJECT GUTENBERG EBOOK FORGOTTEN WORLD ***</span>
    </div>
    <div style="display:block; margin:1em 0">
    Updated editions will replace the previous one—the old editions will
    be renamed.
    </div>
    <div style="display:block; margin:1em 0">
    Creating the works from print editions not protected by U.S. copyright
    law means that no one owns a United States copyright in these works,
    so the Foundation (and you!) can copy and distribute it in the United
    States without permission and without paying copyright
    royalties. Special rules, set forth in the General Terms of Use part
    of this license, apply to copying and distributing Project
    Gutenberg™ electronic works to protect the PROJECT GUTENBERG™
    concept and trademark. Project Gutenberg is a registered trademark,
    and may not be used if you charge for an eBook, except by following
    the terms of the trademark license, including paying royalties for use
    of the Project Gutenberg trademark. If you do not charge anything for
    copies of this eBook, complying with the trademark license is very
    easy. You may use this eBook for nearly any purpose such as creation
    of derivative works, reports, performances and research. Project
    Gutenberg eBooks may be modified and printed and given away—you may
    do practically ANYTHING in the United States with eBooks not protected
    by U.S. copyright law. Redistribution is subject to the trademark
    license, especially commercial redistribution.
    </div>
    <div id="project-gutenberg-license" style="margin-top:1em; font-size:1.1em; text-align:center">START: FULL LICENSE</div>
    <h2 style="text-align:center;font-size:0.9em">THE FULL PROJECT GUTENBERG LICENSE</h2>
    <div style="text-align:center;font-size:0.9em">PLEASE READ THIS BEFORE YOU DISTRIBUTE OR USE THIS WORK</div>
    <div style="display:block; margin:1em 0">
    To protect the Project Gutenberg™ mission of promoting the free
    distribution of electronic works, by using or distributing this work
    (or any other work associated in any way with the phrase “Project
    Gutenberg”), you agree to comply with all the terms of the Full
    Project Gutenberg™ License available with this file or online at
    www.gutenberg.org/license.
    </div>
    <div style="display:block; font-size:1.1em; margin:1em 0; font-weight:bold">
    Section 1. General Terms of Use and Redistributing Project Gutenberg™ electronic works
    </div>
    <div style="display:block; margin:1em 0">
    1.A. By reading or using any part of this Project Gutenberg™
    electronic work, you indicate that you have read, understand, agree to
    and accept all the terms of this license and intellectual property
    (trademark/copyright) agreement. If you do not agree to abide by all
    the terms of this agreement, you must cease using and return or
    destroy all copies of Project Gutenberg™ electronic works in your
    possession. If you paid a fee for obtaining a copy of or access to a
    Project Gutenberg™ electronic work and you do not agree to be bound
    by the terms of this agreement, you may obtain a refund from the person
    or entity to whom you paid the fee as set forth in paragraph 1.E.8.
    </div>
    <div style="display:block; margin:1em 0">
    1.B. “Project Gutenberg” is a registered trademark. It may only be
    used on or associated in any way with an electronic work by people who
    agree to be bound by the terms of this agreement. There are a few
    things that you can do with most Project Gutenberg™ electronic works
    even without complying with the full terms of this agreement. See
    paragraph 1.C below. There are a lot of things you can do with Project
    Gutenberg™ electronic works if you follow the terms of this
    agreement and help preserve free future access to Project Gutenberg™
    electronic works. See paragraph 1.E below.
    </div>
    <div style="display:block; margin:1em 0">
    1.C. The Project Gutenberg Literary Archive Foundation (“the
    Foundation” or PGLAF), owns a compilation copyright in the collection
    of Project Gutenberg™ electronic works. Nearly all the individual
    works in the collection are in the public domain in the United
    States. If an individual work is unprotected by copyright law in the
    United States and you are located in the United States, we do not
    claim a right to prevent you from copying, distributing, performing,
    displaying or creating derivative works based on the work as long as
    all references to Project Gutenberg are removed. Of course, we hope
    that you will support the Project Gutenberg™ mission of promoting
    free access to electronic works by freely sharing Project Gutenberg™
    works in compliance with the terms of this agreement for keeping the
    Project Gutenberg™ name associated with the work. You can easily
    comply with the terms of this agreement by keeping this work in the
    same format with its attached full Project Gutenberg™ License when
    you share it without charge with others.
    </div>
    <div style="display:block; margin:1em 0">
    1.D. The copyright laws of the place where you are located also govern
    what you can do with this work. Copyright laws in most countries are
    in a constant state of change. If you are outside the United States,
    check the laws of your country in addition to the terms of this
    agreement before downloading, copying, displaying, performing,
    distributing or creating derivative works based on this work or any
    other Project Gutenberg™ work. The Foundation makes no
    representations concerning the copyright status of any work in any
    country other than the United States.
    </div>
    <div style="display:block; margin:1em 0">
    1.E. Unless you have removed all references to Project Gutenberg:
    </div>
    <div style="display:block; margin:1em 0">
    1.E.1. The following sentence, with active links to, or other
    immediate access to, the full Project Gutenberg™ License must appear
    prominently whenever any copy of a Project Gutenberg™ work (any work
    on which the phrase “Project Gutenberg” appears, or with which the
    phrase “Project Gutenberg” is associated) is accessed, displayed,
    performed, viewed, copied or distributed:
    </div>
    <blockquote>
    <div style="display:block; margin:1em 0">
        This eBook is for the use of anyone anywhere in the United States and most
        other parts of the world at no cost and with almost no restrictions
        whatsoever. You may copy it, give it away or re-use it under the terms
        of the Project Gutenberg License included with this eBook or online
        at <a href="https://www.gutenberg.org">www.gutenberg.org</a>. If you
        are not located in the United States, you will have to check the laws
        of the country where you are located before using this eBook.
      </div>
    </blockquote>
    <div style="display:block; margin:1em 0">
    1.E.2. If an individual Project Gutenberg™ electronic work is
    derived from texts not protected by U.S. copyright law (does not
    contain a notice indicating that it is posted with permission of the
    copyright holder), the work can be copied and distributed to anyone in
    the United States without paying any fees or charges. If you are
    redistributing or providing access to a work with the phrase “Project
    Gutenberg” associated with or appearing on the work, you must comply
    either with the requirements of paragraphs 1.E.1 through 1.E.7 or
    obtain permission for the use of the work and the Project Gutenberg™
    trademark as set forth in paragraphs 1.E.8 or 1.E.9.
    </div>
    <div style="display:block; margin:1em 0">
    1.E.3. If an individual Project Gutenberg™ electronic work is posted
    with the permission of the copyright holder, your use and distribution
    must comply with both paragraphs 1.E.1 through 1.E.7 and any
    additional terms imposed by the copyright holder. Additional terms
    will be linked to the Project Gutenberg™ License for all works
    posted with the permission of the copyright holder found at the
    beginning of this work.
    </div>
    <div style="display:block; margin:1em 0">
    1.E.4. Do not unlink or detach or remove the full Project Gutenberg™
    License terms from this work, or any files containing a part of this
    work or any other work associated with Project Gutenberg™.
    </div>
    <div style="display:block; margin:1em 0">
    1.E.5. Do not copy, display, perform, distribute or redistribute this
    electronic work, or any part of this electronic work, without
    prominently displaying the sentence set forth in paragraph 1.E.1 with
    active links or immediate access to the full terms of the Project
    Gutenberg™ License.
    </div>
    <div style="display:block; margin:1em 0">
    1.E.6. You may convert to and distribute this work in any binary,
    compressed, marked up, nonproprietary or proprietary form, including
    any word processing or hypertext form. However, if you provide access
    to or distribute copies of a Project Gutenberg™ work in a format
    other than “Plain Vanilla ASCII” or other format used in the official
    version posted on the official Project Gutenberg™ website
    (www.gutenberg.org), you must, at no additional cost, fee or expense
    to the user, provide a copy, a means of exporting a copy, or a means
    of obtaining a copy upon request, of the work in its original “Plain
    Vanilla ASCII” or other form. Any alternate format must include the
    full Project Gutenberg™ License as specified in paragraph 1.E.1.
    </div>
    <div style="display:block; margin:1em 0">
    1.E.7. Do not charge a fee for access to, viewing, displaying,
    performing, copying or distributing any Project Gutenberg™ works
    unless you comply with paragraph 1.E.8 or 1.E.9.
    </div>
    <div style="display:block; margin:1em 0">
    1.E.8. You may charge a reasonable fee for copies of or providing
    access to or distributing Project Gutenberg™ electronic works
    provided that:
    </div>
    <div style="margin-left:0.7em;">
    <div style="text-indent:-0.7em">
            • You pay a royalty fee of 20% of the gross profits you derive from
            the use of Project Gutenberg™ works calculated using the method
            you already use to calculate your applicable taxes. The fee is owed
            to the owner of the Project Gutenberg™ trademark, but he has
            agreed to donate royalties under this paragraph to the Project
            Gutenberg Literary Archive Foundation. Royalty payments must be paid
            within 60 days following each date on which you prepare (or are
            legally required to prepare) your periodic tax returns. Royalty
            payments should be clearly marked as such and sent to the Project
            Gutenberg Literary Archive Foundation at the address specified in
            Section 4, “Information about donations to the Project Gutenberg
            Literary Archive Foundation.”
        </div>
    <div style="text-indent:-0.7em">
            • You provide a full refund of any money paid by a user who notifies
            you in writing (or by e-mail) within 30 days of receipt that s/he
            does not agree to the terms of the full Project Gutenberg™
            License. You must require such a user to return or destroy all
            copies of the works possessed in a physical medium and discontinue
            all use of and all access to other copies of Project Gutenberg™
            works.
        </div>
    <div style="text-indent:-0.7em">
            • You provide, in accordance with paragraph 1.F.3, a full refund of
            any money paid for a work or a replacement copy, if a defect in the
            electronic work is discovered and reported to you within 90 days of
            receipt of the work.
        </div>
    <div style="text-indent:-0.7em">
            • You comply with all other terms of this agreement for free
            distribution of Project Gutenberg™ works.
        </div>
    </div>
    <div style="display:block; margin:1em 0">
    1.E.9. If you wish to charge a fee or distribute a Project
    Gutenberg™ electronic work or group of works on different terms than
    are set forth in this agreement, you must obtain permission in writing
    from the Project Gutenberg Literary Archive Foundation, the manager of
    the Project Gutenberg™ trademark. Contact the Foundation as set
    forth in Section 3 below.
    </div>
    <div style="display:block; margin:1em 0">
    1.F.
    </div>
    <div style="display:block; margin:1em 0">
    1.F.1. Project Gutenberg volunteers and employees expend considerable
    effort to identify, do copyright research on, transcribe and proofread
    works not protected by U.S. copyright law in creating the Project
    Gutenberg™ collection. Despite these efforts, Project Gutenberg™
    electronic works, and the medium on which they may be stored, may
    contain “Defects,” such as, but not limited to, incomplete, inaccurate
    or corrupt data, transcription errors, a copyright or other
    intellectual property infringement, a defective or damaged disk or
    other medium, a computer virus, or computer codes that damage or
    cannot be read by your equipment.
    </div>
    <div style="display:block; margin:1em 0">
    1.F.2. LIMITED WARRANTY, DISCLAIMER OF DAMAGES - Except for the “Right
    of Replacement or Refund” described in paragraph 1.F.3, the Project
    Gutenberg Literary Archive Foundation, the owner of the Project
    Gutenberg™ trademark, and any other party distributing a Project
    Gutenberg™ electronic work under this agreement, disclaim all
    liability to you for damages, costs and expenses, including legal
    fees. YOU AGREE THAT YOU HAVE NO REMEDIES FOR NEGLIGENCE, STRICT
    LIABILITY, BREACH OF WARRANTY OR BREACH OF CONTRACT EXCEPT THOSE
    PROVIDED IN PARAGRAPH 1.F.3. YOU AGREE THAT THE FOUNDATION, THE
    TRADEMARK OWNER, AND ANY DISTRIBUTOR UNDER THIS AGREEMENT WILL NOT BE
    LIABLE TO YOU FOR ACTUAL, DIRECT, INDIRECT, CONSEQUENTIAL, PUNITIVE OR
    INCIDENTAL DAMAGES EVEN IF YOU GIVE NOTICE OF THE POSSIBILITY OF SUCH
    DAMAGE.
    </div>
    <div style="display:block; margin:1em 0">
    1.F.3. LIMITED RIGHT OF REPLACEMENT OR REFUND - If you discover a
    defect in this electronic work within 90 days of receiving it, you can
    receive a refund of the money (if any) you paid for it by sending a
    written explanation to the person you received the work from. If you
    received the work on a physical medium, you must return the medium
    with your written explanation. The person or entity that provided you
    with the defective work may elect to provide a replacement copy in
    lieu of a refund. If you received the work electronically, the person
    or entity providing it to you may choose to give you a second
    opportunity to receive the work electronically in lieu of a refund. If
    the second copy is also defective, you may demand a refund in writing
    without further opportunities to fix the problem.
    </div>
    <div style="display:block; margin:1em 0">
    1.F.4. Except for the limited right of replacement or refund set forth
    in paragraph 1.F.3, this work is provided to you ‘AS-IS’, WITH NO
    OTHER WARRANTIES OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT
    LIMITED TO WARRANTIES OF MERCHANTABILITY OR FITNESS FOR ANY PURPOSE.
    </div>
    <div style="display:block; margin:1em 0">
    1.F.5. Some states do not allow disclaimers of certain implied
    warranties or the exclusion or limitation of certain types of
    damages. If any disclaimer or limitation set forth in this agreement
    violates the law of the state applicable to this agreement, the
    agreement shall be interpreted to make the maximum disclaimer or
    limitation permitted by the applicable state law. The invalidity or
    unenforceability of any provision of this agreement shall not void the
    remaining provisions.
    </div>
    <div style="display:block; margin:1em 0">
    1.F.6. INDEMNITY - You agree to indemnify and hold the Foundation, the
    trademark owner, any agent or employee of the Foundation, anyone
    providing copies of Project Gutenberg™ electronic works in
    accordance with this agreement, and any volunteers associated with the
    production, promotion and distribution of Project Gutenberg™
    electronic works, harmless from all liability, costs and expenses,
    including legal fees, that arise directly or indirectly from any of
    the following which you do or cause to occur: (a) distribution of this
    or any Project Gutenberg™ work, (b) alteration, modification, or
    additions or deletions to any Project Gutenberg™ work, and (c) any
    Defect you cause.
    </div>
    <div style="display:block; font-size:1.1em; margin:1em 0; font-weight:bold">
    Section 2. Information about the Mission of Project Gutenberg™
    </div>
    <div style="display:block; margin:1em 0">
    Project Gutenberg™ is synonymous with the free distribution of
    electronic works in formats readable by the widest variety of
    computers including obsolete, old, middle-aged and new computers. It
    exists because of the efforts of hundreds of volunteers and donations
    from people in all walks of life.
    </div>
    <div style="display:block; margin:1em 0">
    Volunteers and financial support to provide volunteers with the
    assistance they need are critical to reaching Project Gutenberg™’s
    goals and ensuring that the Project Gutenberg™ collection will
    remain freely available for generations to come. In 2001, the Project
    Gutenberg Literary Archive Foundation was created to provide a secure
    and permanent future for Project Gutenberg™ and future
    generations. To learn more about the Project Gutenberg Literary
    Archive Foundation and how your efforts and donations can help, see
    Sections 3 and 4 and the Foundation information page at www.gutenberg.org.
    </div>
    <div style="display:block; font-size:1.1em; margin:1em 0; font-weight:bold">
    Section 3. Information about the Project Gutenberg Literary Archive Foundation
    </div>
    <div style="display:block; margin:1em 0">
    The Project Gutenberg Literary Archive Foundation is a non-profit
    501(c)(3) educational corporation organized under the laws of the
    state of Mississippi and granted tax exempt status by the Internal
    Revenue Service. The Foundation’s EIN or federal tax identification
    number is 64-6221541. Contributions to the Project Gutenberg Literary
    Archive Foundation are tax deductible to the full extent permitted by
    U.S. federal laws and your state’s laws.
    </div>
    <div style="display:block; margin:1em 0">
    The Foundation’s business office is located at 809 North 1500 West,
    Salt Lake City, UT 84116, (801) 596-1887. Email contact links and up
    to date contact information can be found at the Foundation’s website
    and official page at www.gutenberg.org/contact
    </div>
    <div style="display:block; font-size:1.1em; margin:1em 0; font-weight:bold">
    Section 4. Information about Donations to the Project Gutenberg Literary Archive Foundation
    </div>
    <div style="display:block; margin:1em 0">
    Project Gutenberg™ depends upon and cannot survive without widespread
    public support and donations to carry out its mission of
    increasing the number of public domain and licensed works that can be
    freely distributed in machine-readable form accessible by the widest
    array of equipment including outdated equipment. Many small donations
    ($1 to $5,000) are particularly important to maintaining tax exempt
    status with the IRS.
    </div>
    <div style="display:block; margin:1em 0">
    The Foundation is committed to complying with the laws regulating
    charities and charitable donations in all 50 states of the United
    States. Compliance requirements are not uniform and it takes a
    considerable effort, much paperwork and many fees to meet and keep up
    with these requirements. We do not solicit donations in locations
    where we have not received written confirmation of compliance. To SEND
    DONATIONS or determine the status of compliance for any particular state
    visit <a href="https://www.gutenberg.org/donate/">www.gutenberg.org/donate</a>.
    </div>
    <div style="display:block; margin:1em 0">
    While we cannot and do not solicit contributions from states where we
    have not met the solicitation requirements, we know of no prohibition
    against accepting unsolicited donations from donors in such states who
    approach us with offers to donate.
    </div>
    <div style="display:block; margin:1em 0">
    International donations are gratefully accepted, but we cannot make
    any statements concerning tax treatment of donations received from
    outside the United States. U.S. laws alone swamp our small staff.
    </div>
    <div style="display:block; margin:1em 0">
    Please check the Project Gutenberg web pages for current donation
    methods and addresses. Donations are accepted in a number of other
    ways including checks, online payments and credit card donations. To
    donate, please visit: www.gutenberg.org/donate
    </div>
    <div style="display:block; font-size:1.1em; margin:1em 0; font-weight:bold">
    Section 5. General Information About Project Gutenberg™ electronic works
    </div>
    <div style="display:block; margin:1em 0">
    Professor Michael S. Hart was the originator of the Project
    Gutenberg™ concept of a library of electronic works that could be
    freely shared with anyone. For forty years, he produced and
    distributed Project Gutenberg™ eBooks with only a loose network of
    volunteer support.
    </div>
    <div style="display:block; margin:1em 0">
    Project Gutenberg™ eBooks are often created from several printed
    editions, all of which are confirmed as not protected by copyright in
    the U.S. unless a copyright notice is included. Thus, we do not
    necessarily keep eBooks in compliance with any particular paper
    edition.
    </div>
    <div style="display:block; margin:1em 0">
    Most people start at our website which has the main PG search
    facility: <a href="https://www.gutenberg.org">www.gutenberg.org</a>.
    </div>
    <div style="display:block; margin:1em 0">
    This website includes information about Project Gutenberg™,
    including how to make donations to the Project Gutenberg Literary
    Archive Foundation, how to help produce our new eBooks, and how to
    subscribe to our email newsletter to hear about new eBooks.
    </div>
    </section></body>
    </html>




```python
soup.find('p')
```




    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Title</strong>: Forgotten world</p>




```python
type(soup.find('p'))
```




    bs4.element.Tag




```python
soup.find('p').name
```




    'p'




```python
soup.find('p').text
```




    'Title: Forgotten world'




```python
print(len(soup.find_all('p')))
soup.find_all('p')
```

    760





    [<p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Title</strong>: Forgotten world</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Author</strong>: Edmond Hamilton</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Release Date</strong>: November 15, 2022 [EBook #69357]</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Language</strong>: English</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Original Publication</strong>: US: , United States: Standard Magazines, Inc.,1945.</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Credits</strong>: Greg Weeks, Mary Meehan and the Online Distributed Proofreading Team at http://www.pgdp.net</p>,
     <p>[Transcriber's Note: This etext was produced from<br/>
     Thrilling Wonder Stories Winter 1946.<br/>
     Extensive research did not uncover any evidence that<br/>
     the U.S. copyright on this publication was renewed.]</p>,
     <p class="ph1">CHAPTER I</p>,
     <p class="ph1"><i>Stranger from the Stars</i></p>,
     <p>Carlin was the only one of the four hundred passengers on the "Larkoom"
     who hated the star-ship and everything about it.</p>,
     <p>He was bored with the vessel and everyone aboard. A pack of chattering
     idiots! For the hundredth time since leaving Canopus, he told himself
     that he was a monumental fool to let that psychotherapist talk him into
     this crazy trip.</p>,
     <p>A blond girl from Altair Four came tripping along the deck and favored
     Laird Carlin with the bright smile that all the younger feminine
     tourists had practised on the tall, dark, dour-looking young man.</p>,
     <p>The blonde from Altair Four favored the tall dour-looking young man with a bright smile.</p>,
     <p>"Oh, Mr, Carlin, the annunciators just said that we're only eight
     hours from Sol. By night, we'll be on Earth! Isn't it thrilling?"</p>,
     <p>"Just what is thrilling about it?" Carlin asked sourly.</p>,
     <p>The girl was a little dumfounded. "Why, I mean, Earth! All the ancient
     history we study in schools, about how men first came from there two
     thousand years ago. Or was it twenty-one hundred?"</p>,
     <p>She prattled on, voicing all the appropriate clichés.</p>,
     <p>"Just think, all of us in this ship came from different stats and
     worlds, yet long ago all our ancestors lived on that one little world
     Earth. And they say it's still much the same as it was then. Isn't it
     wonderful?"</p>,
     <p>Carlin could not see anything wonderful about it, and a little wearily
     he said so.</p>,
     <p>The girl flushed in exasperation. "Then why are you going to Earth at
     all?"</p>,
     <p>Why indeed, Carlin wondered savagely? Why the devil wasn't he back
     on the other side of the galaxy where he belonged, supervising
     establishment of the new star-ship line to Algol Six, spending his
     leaves in Sun City with Nila?</p>,
     <p>Nila—he yearned for her, for her gay, mocking humor, her cool beauty,
     her quick, clever mind. What was he doing here with a bunch of
     bird-brained tourists who were conscientiously tripping for local color
     to an old, forgotten world?</p>,
     <p>This whole part of the galaxy was a stagnant, half-dead area. This side
     of Vega there weren't a score of suns with worlds of any importance.
     And the old "Larkoom," a second-rate star-ship that couldn't make more
     than eighty light-speeds, was plodding determinedly and monotonously on
     into it.</p>,
     <p>Curse that psychotherapist anyway! Why had he been crazy enough to
     listen to the fellow? That smug, pink, blinking Arcturian had smiled as
     gently as a well-bred pussy-cat as he told Carlin what his trouble was.</p>,
     <p>"Star-sick?" Carlin had flared. "What do you mean, star-sick? I've made
     the trip to Algol ten times in the last three months."</p>,
     <p>The psychotherapist had nodded. "Yes. And that was nine times too many.
     You've been overdoing it for a long time, Mr. Carlin."</p>,
     <p>Before Carlin could protest, the other man had referred to the dossier
     on his desk.</p>,
     <p>"I have your record here. Born at Aldebaran four thirty years ago.
     Graduated at twenty-two from Canopus University with the degree
     of Cosmic Engineer. Worked since then establishing spaceports for
     star-ship lines between Rigel, Sharak, Tibor, Algol and other stars."</p>,
     <p>The psychotherapist looked up gravely. "The point is that you've spent
     fifty per cent of your time in the last eight years in star-ships. The
     average has been seventy per cent since you took charge of establishing
     the new Algol line. And that's too much time in space for any man. No
     wonder you're star-sick."</p>,
     <p>"Blast it, I'm not star-sick!" Carlin exploded. "What kind of therapist
     are you? I come here to have you treat a perfectly simple syndrome of
     reflex-fatigue, and you tell me all this!"</p>,
     <p>The Arcturian shook his head wisely. "Your case was only simple on the
     surface, Mr. Carlin. The hypnosis showed up your trouble unmistakably.
     Want to hear the record?"</p>,
     <p>Carlin heard it. And it wasn't pretty. Not pretty, to hear his
     hypnosis-freed subconscious yelling out a frantic hatred of space and
     star-ships and everything connected with them.</p>,
     <p>"You see?" said the Arcturian gently. "This has been building up in you
     for a long time."</p>,
     <p>Carlin was stunned. He had known of other men who had got star-sick and
     had had to drop their work and quit traveling space for a while. Other
     men—but he'd always laughed contemptuously at them for it.</p>,
     <p>The psychos might declare that it was perfectly natural for a man to
     develop a subconscious aversion to space if he crowded his work, but
     the hard-bitten engineers of Carlin's set believed that a star-sick man
     was nine times in ten a shirker. And now he himself was told he was
     star-sick.</p>,
     <p>"You've got to quit work and stay out of space for a while," the
     Arcturian therapist told him.</p>,
     <p>Carlin felt sick at heart. "Then all my work in building up the Algol
     line will go into young Brewer's hands."</p>,
     <p>Still, he thought after a moment, it might not be so bad. Working in
     his line's main offices here on Canopus Two, he could keep in touch.
     And he would have more time here with Nila.</p>,
     <p>But the psychotherapist shook his head quite decisively at that.</p>,
     <p>"No, Mr. Carlin. Your case is too dangerous for that. Your subconscious
     is twisted into a knot that is going to be hard to untie." He hesitated
     a moment as though he knew what reaction his next words would provoke.
     "In fact, there's only one way in which you can be normalized. That's
     the Earth-treatment."</p>,
     <p>"Earth-treatment?" Carlin didn't even know what it meant. "You mean,
     some treatment that has reference to the old planet over on the other
     side of the galaxy?"</p>,
     <p>The Arcturian nodded. "Yes, our ancestral planet Earth. Where all our
     race came from, two thousand years ago. Where you're going back to, for
     perhaps a year."</p>,
     <p>Carlin was knocked breathless by that calm statement.</p>,
     <p>"Me going to Earth for a year? Are you crazy? Why should I go there?"</p>,
     <p>"Because," the therapist said soberly, "if you don't I'm afraid you
     won't last another six months as a star-line man."</p>,
     <p>"But why can't I take a rest right here on Canopus Two?" Carlin
     demanded heatedly. "Why send me to that moldering, forgotten old planet
     where there's nothing now but a few historical monuments?"</p>,
     <p>"You've never been to Earth, I take it?" the psychotherapist asked
     thoughtfully.</p>,
     <p>Carlin made an impatient gesture. "I'm not interested in ancient
     history. That part of the galaxy is all a backwater."</p>,
     <p>"Yes," the expert said. "I know all that. But old and small and
     forgotten as it is these days, Earth is still important."</p>,
     <p>"To historians," Carlin snapped. "To people who like to poke in the
     dusty past."</p>,
     <p>The Arcturian nodded, and shrugged.</p>,
     <p>"And to psychologists," he said quietly. "Most people these days don't
     realize something. They don't realize that we, all of us, are still
     really Earthmen in a way." He held up a protesting hand. "Oh, I know
     we don't think of ourselves like that! Since those first Earthmen
     pioneered to their neighbor planets and then to the stars, since our
     civilization spread out over most of the galaxy, a hundred generations
     of us have been born on different star-worlds from Rigel to Fomalhaut.
     But except for local modifications, the type of humanity has persisted
     since our ancestors left Earth and Sol long ago.</p>,
     <p>"That's because we've altered star-world conditions to fit ourselves,
     instead of adapting ourselves to those conditions. We've cunningly
     changed atmospheres, gravities, everything, wherever we went. We've
     kept ourselves one race, one type, that way. But it's a type that is
     still indexed to that old plane Earth as its norm."</p>,
     <p>"Does that explain why I have to give up my work and go live on the old
     relic for a year?" Carlin demanded furiously.</p>,
     <p>"Yes, it does," the Arcturian replied. "We're a star-traveling race
     now. But the mind can take only so much of the strain of star-travel.
     Overdo that strain and you get a revulsion, you get star-sickness. Then
     the only cure is rest for the mind in completely normal conditions. And
     complete normality, for us descendants of Earthmen, is—Earth."</p>,
     <p>Carlin had stormed. He carried his wrathful resistance to the last
     pitch.</p>,
     <p>And then the psychotherapist had crushed him.</p>,
     <p>"I've turned in your psycho-record to your star-ship line. You'll not
     be allowed to work there until you're cured."</p>,
     <p>And that, Laird Carlin thought bitterly, was why he was sprawled in a
     deck-chair here on the "Larkoom" as the old tub creaked and labored and
     plodded through space toward the yellow spark of Sol.</p>,
     <p>"A year!" he thought in impotent rage. "A year in that hole! I might as
     well be dead."</p>,
     <p>The psychotherapist had held out the hope that it might not take a
     year. Some cases of star-sickness responded quickly to Earth-treatment.
     But even a few months seemed an eternity to Carlin.</p>,
     <p>The passengers of the "Larkoom" were crowding toward the transparent
     wall of the deck. Earth was coming into sight. And these people—men
     and women bronzed by the glare of Canopus, reddened by the desert winds
     of Rigel's worlds, paled by the mists of Altair's planets—all were
     watching with an intense and eager expectation.</p>,
     <p>Carlin walked wearily over to the deck wall and watched with them.
     Sol, ahead, was a small and undistinguished yellow sun. Its orb was
     unimpressive to eyes that had looked on Antares and Altair.</p>,
     <p>And the planets that circled it were so little that Carlin could
     hardly make them out. He remembered half-forgotten names from ancient
     history—Saturn, Jupiter, Mars. And that little gray-green dot beyond
     must be Earth.</p>,
     <p>"Isn't it tiny?" babbled a rapturous, overweight woman beside Carlin.
     "I think it's cute!"</p>,
     <p>A very young man from Mizar Seven proudly aired his knowledge.</p>,
     <p>"That satellite beyond it is Luna, its moon."</p>,
     <p>"The moon is almost as big as the little planet!" exclaimed someone,
     laughing.</p>,
     <p>Carlin found their chatter getting on his nerves, and edged further
     along the deck. In gloomy silence, he looked down as the "Larkoom"
     swept in swift, almost soundless rush toward the little planet.</p>,
     <p>A gray-green, cloud-screened ball spinning around a second-rate sun—it
     looked like the end of the universe to Carlin. And he might have to
     spend a year here! His spirits sank still lower.</p>,
     <p>"They say you can get the most wonderful souvenirs here," one of the
     tourists' voices reached him.</p>,
     <p>Carlin writhed. He would be glad to get out even at Earth, to get away
     from this bunch of babbling fools.</p>,
     <p>He realized his irritability was extreme, unreasonable. It was the
     result of his star-sickness, he supposed. But that didn't make it any
     more endurable.</p>,
     <p>"Landing in ten minutes," spoke the annunciators throughout the ship.
     "Stasis going on."</p>,
     <p>The dim glow of the force-stasis that cushioned everything in the ship
     against pressure of deceleration came on like a tangible medium around
     them. The big propulsion-wave generators droned in lower key.</p>,
     <p>Swaddled in the cushioning force, they felt no discomfort as the
     "Larkoom" quickly dropped toward the little planet. Atmosphere screamed
     briefly outside the ship. They came down through a belt of clouds.</p>,
     <p>"That's the city New York!" cried an eager voice. "The oldest human
     city in the galaxy!"</p>,
     <p class="ph1">CHAPTER II</p>,
     <p class="ph1"><i>Ancient Town</i></p>,
     <p>Carlin looked with a jaundiced eye on the scene widening out below
     them. There was a blue ocean stretching eastward, a long green coast,
     and an island that was covered by the grotesquely lofty buildings of an
     extremely antiquated type of city.</p>,
     <p>This ancient town called New York was like a memento of the primitive
     past. Not for a thousand years had men crowded their structures so
     crazily together, or built them to such insane heights.</p>,
     <p>"It's like one of the bird-people's lofts on Polaris One!" exclaimed a
     girl, laughing. "And how old it looks!"</p>,
     <p>Old? Yes. Pitifully old, like a withered beldame who endeavors still
     to maintain stiff dignity. The city looked only half-occupied, vines
     growing on some of the grotesque towers, parks ragged around the edges.</p>,
     <p>The spaceport, some distance northward amid low rolling hills, was so
     small as to be inadequate for any decent world. Carlin's practised eyes
     condemned the cracked, blackened tarmac, the ill-placed rows of docks,
     the insufficient hangar and repair buildings.</p>,
     <p>The "Larkoom" landed softly. Carlin waited wearily until the squealing
     rush of tourists was over, and then walked out into the soft yellow
     sunshine. He looked around without interest. Landing on a new world was
     no novelty to him.</p>,
     <p>But for a moment, he was startled by the air he breathed. It was so
     sweet, so buoyant, so right. It was subtly stimulating, exhilarating
     to the lungs. Then he realized the cause. All over the galaxy, the
     descendants of Earthmen had conditioned planetary atmospheres with this
     atmosphere of Earth as the desired norm.</p>,
     <p>He looked around uncertainly. The tourists were already being
     shepherded by their tour-conductors toward some old monuments at the
     far end of the spaceport. But he had no desire to follow them.</p>,
     <p>The psychotherapist had told him, "Live as nearly an ordinary Earth
     life as you can. Your cure will be quicker if you do. Best thing would
     be to lodge in some typical Earth home, if you can."</p>,
     <p>Carlin wondered where he could find such a lodging. There were a few
     Earthmen about, spacemen, port officials and the like. He could ask one
     of them.</p>,
     <p>He had met Earthmen before throughout the galaxy, for many of them
     followed space as a trade. And he didn't much like them. A proud,
     taciturn, half-sulky lot, they had always seemed to him.</p>,
     <p>"Can you tell me where I could find lodgings around here?" He asked a
     lanky, lantern-jawed man in faded clothes.</p>,
     <p>The Earthman contemplated Laird Carlin with unfriendly eyes, taking in
     his sun-darkened face, his pearl-colored synthesilk slacks and jacket,
     every detail of his appearance that was alien here.</p>,
     <p>"Well, no," the fellow drawled coolly. "Don't know where a stranger
     could get lodgin's round here."</p>,
     <p>He slouched on. Carlin flushed with anger at the scarcely veiled
     hostility in the fellow's manner.</p>,
     <p>These blasted yokels of Earth! Living here on an old, outworn,
     fifth-rate planet, resenting the progress and prosperity of the great
     star-worlds, talking of everybody but themselves as "strangers"!</p>,
     <p>"And I'm supposed to live among them for a year!" he thought bitterly.</p>,
     <p>He started across the spaceport. He had noted a spick-and-span
     chromaloy building with a half-dozen trim Control cruisers parked
     nearby, and with the Control Council emblem on its wall. He could find
     out something there.</p>,
     <p>The spaceport was a somnolent, slovenly place to Carlin's eyes. A
     few star-ships, all of them freighters except the tubby "Larkoom," a
     scattering of little inter-planet craft, a few workers lounging about.
     Even the smallest world of the great stars would be ashamed of such a
     port.</p>,
     <p>That soft yellow sun, he found, had a deceptive warmth. And walking was
     tiring after days of the ship's artificial gravity. Then Carlin stopped
     as he came abreast of a rickety little planet-ship.</p>,
     <p>Two Earthmen were inspecting its stern drive-plates—one of them a
     stocky, red-faced young man, the other a lame younger fellow with a
     crutch. Carlin asked them his question.</p>,
     <p>The red-faced individual answered with the same hostility of manner.</p>,
     <p>"You'll find no lodgings around here. Better go with the rest of your
     crowd. There's a big tourist hotel down in the city."</p>,
     <p>Carlin swore. "Blast it, I'm not a tourist. I'm an engineer sent here
     by a crazy psycho to spend a year on Earth—heaven knows why!"</p>,
     <p>The lame young Earthman looked at Carlin more closely. He had a thin,
     pleasant brown face with intelligent blue eyes.</p>,
     <p>"Oh, an Earth-treatment man?" he said. "A few come in all the time." He
     asked interestedly, "You're a Cosmic Engineer? Do you mind telling me
     what field?"</p>,
     <p>"Star-ship line chief surveyor," Carlin said wearily. "That means I lay
     out spaceport and beacon routes between star-worlds."</p>,
     <p>"I know what it means." The lame youngster nodded quietly. He
     hesitated, frowning slightly as though weighing something. Then, as if
     deciding, he spoke. "I'm Jonny Land. I think we could fix you up with
     lodgings if you don't mind putting up with a little discomfort."</p>,
     <p>"You mean, in your own home?" Carlin asked doubtfully. "Where is it?"</p>,
     <p>Jonny Land pointed to one of the low green ridges west of the spaceport.</p>,
     <p>"Just up on the ridge there. There's only my grandfather, my brother
     and sister, and myself. And we have an extra room."</p>,
     <p>The red-faced young Earthman made a sharp protest. "Jonny, what the
     blazes are you thinking of? You don't want this fellow in with you!"</p>,
     <p>The violence of his protest seemed uncalled-for to Carlin, even
     granting the general Earthman hostility to strangers.</p>,
     <p>Jonny Land quietly quelled the outburst. "I'm doing this, Loesser." He
     looked at Carlin. "Well, what about it? I warn you that you won't find
     the comforts of a big star-world apartment."</p>,
     <p>"I don't expect anything like that here," Carlin answered tiredly. He
     felt worn out by the voyage, the discouragingly primitive aspect of
     this place where he must live, the open unfriendliness. He nodded.
     "I'll try it. The name is Laird Carlin."</p>,
     <p>"If you'll get your luggage, I'll take you up," Jonny Land suggested.
     "I have a truck. I'll meet you over at the terminal."</p>,
     <p>Carlin came out of the shabby terminal a little later with his two
     kitbags and found the lame youngster waiting at the wheel of a
     disreputable-looking old ato-truck.</p>,
     <p>Loesser, the red-faced young man, was standing beside it voicing
     emphatic protest about something. Carlin overheard a few words.</p>,
     <p>"—ruin everything by taking this fellow in!" he was saying violently.
     "How do you know he isn't a Control spy?"</p>,
     <p>"I know what I'm doing, Loesser," Jonny Land repeated firmly.</p>,
     <p>They broke off as they saw Carlin coming. But Loesser gave him a hot,
     angry glare as he climbed into the machine.</p>,
     <p>The old truck ran westward across the bumpy tarmac and started climbing
     an ancient, cracked concrete road toward the green ridge.</p>,
     <p>Carlin wondered wearily what these Earthmen were up to that made them
     afraid of Control? Smuggling, maybe? He didn't much care. He was hot,
     tired, grimy with dust, and unutterably disgusted with Earth.</p>,
     <p>The concrete road that climbed the ridge looked as though it was
     centuries old. And its engineering had been timid, for it wound around
     hills instead of cutting through them, bridged small streams instead of
     trampling over them. But the battered truck had difficulty negotiating
     even these easy grades. Its ato-motor drumming noisily as it climbed.</p>,
     <p>Carlin looked out gloomily at the sunset-lit landscape. He could not
     get used to the vivid, dominating green of all vegetation here. And
     he was shocked by the unkempt, ragged look of everything. Untended
     fields of weeds and clumps of woods grew right up to the road. It was
     dismayingly different from the groomed, parklike planets of Canopus.</p>,
     <p>The houses Carlin glimpsed along the road added to his dislike. They
     were mostly old ferroconcrete dwellings half-hidden by trees and
     bright flowers, with behind them the big tanks used in hydroponic
     farming. Hydroponic farming was so old-fashioned he had thought it had
     disappeared from the galaxy. What was the matter with these people that
     they didn't directly synthesize their food as others did?</p>,
     <p>Young Jonny Land was speaking to him.</p>,
     <p>"You've never been here before? You must find Earth a little odd."</p>,
     <p>Carlin shrugged. "It's all right, I suppose. But I just can't
     understand how you people could let your planet get into this kind of
     shape. Why haven't you spread out more, instead of huddling around a
     few archaic centralized cities like that one back yonder?"</p>,
     <p>The lame young Earthman answered slowly, his thin, brown face turned to
     the road ahead.</p>,
     <p>"The answer to that is simple. One word, in fact. And that word is
     'power.' We just don't have power enough here on Earth to smooth it out
     into a garden-planet like your star-worlds, to come and go around it
     any distance at will."</p>,
     <p>"Atomic power is about the easiest thing to produce there is," Carlin
     commented skeptically.</p>,
     <p>"Yes, if you have copper fuel," Jonny Land replied. "If we had enough
     copper we could make a garden of this world too, could spread all
     around its loveliest spots and come and go by fast flier, could give
     up the old hydroponic farming and synthesize our food, and produce the
     luxuries you people have on the star-worlds.</p>,
     <p>"But we have little copper. Earth, and its sister-planets here, are all
     starved for it. Once, we had a lot. But not now. And it's economically
     impossible to haul copper in sufficient quantities from other stars.
     That's why we're power-starved, unable to progress."</p>,
     <p>Carlin made no further comment. He was not much interested. He was
     only wondering sickly how long he would have to stay on this unkempt,
     stagnant planet.</p>,
     <p>The sun was burning his neck, for the old truck was topless. He was
     jolted by holes in the ancient road. The sweetness of the air had lost
     its magic for him, for now with the twilight had appeared swarms of
     evil little gnats and midges.</p>,
     <p>"This is the house," said Jonny Land, pulling up the truck in front of
     a square dwelling.</p>,
     <p>Laird Carlin's heart sank. It was like the other houses he had seen,
     a ferroconcrete structure festooned with climbing flower-vines,
     surrounded by tall, untrimmed trees except on the side that looked down
     into the twilit valley. Primitive hydroponic tanks gleamed dully beyond
     the trees.</p>,
     <p>He followed the lame youngster into a dim, cool living room. It looked
     like an antique stage set to Carlin, with its ridiculous cloth curtains
     at the windows, its obsolete krypton light bulbs in the ceiling, its
     massive furniture that was actually made of wood.</p>,
     <p>Jonny Land had been making explanations in lowered tones to the two
     people at the other end of the room. They came forward, a spry old man
     and a girl.</p>,
     <p>"This is Gramp Land, my grandfather," Jonny introduced. "And my sister
     Marn."</p>,
     <p>The old man looked at Laird Carlin with inquisitive, bright eyes, and
     his gnarled hand reached for an old-fashioned handshake.</p>,
     <p>"Come from Canopus, do you?" he chirped. "Well, that's a long way off.
     I was there once years ago when I followed space. And my grandson Harb
     has been there lots of times when he was a star-ship man."</p>,
     <p>The girl, Marn, looked doubtful and troubled as she murmured a word of
     greeting to Carlin. He sensed that his coming had disturbed her.</p>,
     <p>She was a rather small girl, with a thick mop of ash-colored hair
     carelessly combed back. Her eyes were grave blue. She wore a faded old
     slack-suit that he thought the most barbaric feminine garment he had
     seen.</p>,
     <p>"I hope we can make you comfortable here, Mr. Carlin," she said,
     troubled. "We've never had any lodger before. I can't understand why
     Jonny made the suggestion."</p>,
     <p>A heavy step at the door cut her short. Her look of distress and worry
     deepened.</p>,
     <p>"There's my brother Harb, now."</p>,
     <p>Harb Land was a gangling young giant with a craggy face and
     slate-colored eyes that looked at Carlin with instant hostility. Jonny
     had limped forward and was quickly explaining Carlin's presence.</p>,
     <p>"He's going to live here with us for a while, Harb."</p>,
     <p>Harb Land's reaction was violent. "Have you gone out of your mind,
     Jonny?" he flared. "We can't have him here."</p>,
     <p>Disgusted, Carlin started to turn away. But Jonny Land stopped him with
     a gesture. There was a quiet, unsuspected strength in his thin brown
     face as he spoke to his lowering brother.</p>,
     <p>"He's going to stay, Harb. We'll talk about it later."</p>,
     <p>Harb Land made no reply, but glared at Carlin. And Carlin felt an
     unutterable weariness and dislike.</p>,
     <p>These primitive, backward, suspicious Earth yokels, quarreling over the
     privilege of staying in their grotesque old house. As though he would
     stay on their cursed planet one minute if he didn't have to!</p>,
     <p>"I'm very tired," he said heavily. "If you could show me where the room
     is, I should like to rest."</p>,
     <p>Marn uttered an apologetic exclamation. "Oh, I'm sorry! Of course
     you're tired. Come with me, Mr. Carlin."</p>,
     <p>She led upstairs. There was no grav-lift, just old-fashioned steps
     going up a dark hall. And the bedroom on the upper floor to which she
     took him was as bad as he had expected.</p>,
     <p>It was clean, of course, spotlessly so. But it was more like a museum
     exhibit than a sleeping chamber, to Carlin. There were no aerators,
     just open windows with crude screens across them. No somnigrav pad,
     just a high, old-style bed. There wasn't even a video.</p>,
     <p>Yet the girl made no apologies for it, seemed not to think any
     necessary.</p>,
     <p>"We'll bring your bags up after dinner," she said. "It will be soon."</p>,
     <p class="ph1">CHAPTER III</p>,
     <p class="ph1"><i>Old Planet</i></p>,
     <p>When Marn had gone, Carlin lay down wearily on the lumpy, sagging bed.
     He closed his eyes. The reaction to the long, slow voyage had set in.
     No doubt about it, he was star-sick all right. Time was when no voyage
     could have made him feel like this.</p>,
     <p>But it wasn't the voyage so much as this world to which he had been
     condemned. How was he going to live here for months, for a whole year
     maybe?</p>,
     <p>The sound of an angry voice came up dimly through the twilight, from
     the lower floor of the house. He recognized Harb Land's angry tones.</p>,
     <p>"—if Control Operations finds out what we're doing!"</p>,
     <p>There was a murmur of lower voices, and then the argument seemed to
     stop. Carlin remembered what he had overheard the red-faced Loesser
     saying at the spaceport.</p>,
     <p>What were these Earthmen doing that they were so secretive about? It
     must be something against the laws by which Control Council governed
     the galaxy, or they would not fear discovery by Control Operations.</p>,
     <p>When Carlin went down to dinner, he expected open hostility from the
     gangling older brother. But Harb Land muttered a curt greeting, his
     half-civil manner indicating his angry protests had been overridden.</p>,
     <p>Carlin stared dismayedly at the food set before them. Instead of the
     clear, colored synthetic jellies and liquids he was used to, the food
     was served in what seemed barbarically primitive state. Cooked whole
     vegetables, natural eggs, natural milk—everything rawly natural.</p>,
     <p>He ate what he could, which was little. His weariness was drugging him,
     and Harb Land's smothered hostility gave a sense of strain.</p>,
     <p>Gramp Land carried on most of the conversation, questioning Carlin
     about the far-away star-worlds. Carlin answered wearily.</p>,
     <p>"Saw a lot of them worlds myself once," the old man said. He added
     proudly, "Following space runs in my family. My mother was a direct
     descendant of Gorham Johnson himself."</p>,
     <p>"Gorham Johnson?" Carlin asked. "Who was he?"</p>,
     <p>The question was unfortunate.</p>,
     <p>"What do they teach out in your star-world schools?" Gramp exploded.
     "Don't you know that Gorham Johnson was the first man ever to travel
     space? That he was an Earthman, who took off from down in the valley
     here two thousand years ago?"</p>,
     <p>Gramp's pride was outraged. Carlin remembered the old galaxy
     proverb—"Proud as an Earthman." They were all like that, inordinately
     vain of the fact that their world's people had first conquered space.</p>,
     <p>"Sorry," he said tiredly. "I remember the name now. Anyway, I had too
     much cosmic physics to study to spend much time on ancient history."</p>,
     <p>Gramp still spluttered, but Jonny intervened, questioning Carlin on his
     work.</p>,
     <p>"Did you study sub-atomics or just straight dynamics?"</p>,
     <p>"Sub-atomics," Carlin answered. And, to another question, "Yes, I had
     electronic mechanics too."</p>,
     <p>He caught the swift, triumphant glance that Jonny Land shot at his
     brother. It puzzled him.</p>,
     <p>"Jonny knows all that stuff," boasted Gramp, his good humor restored.
     "He's a Cosmic Engineer graduate from Canopus University, too."</p>,
     <p>Laird Carlin was genuinely surprised. He looked at the quiet,
     thin-faced youngster.</p>,
     <p>"You're a Canopus graduate? Why the devil is a man of your training
     wasting your time here on Earth?"</p>,
     <p>"I just like Earth," Jonny answered evenly, "and wanted to come back
     here when my education was finished."</p>,
     <p>"Oh, sure." Carlin nodded. "But if this world is as outworn as it
     looks, there's no field here for a CE. You ought to be out at Algol."</p>,
     <p>"You star-world people are all the same—always advising us to leave
     Earth!" Harb Land interrupted with suppressed passion. "That's what
     Control Council keeps harping on as a solution to all our poverty and
     problems. They keep asking, 'Why don't you emigrate to other stars?'"</p>,
     <p>Gramp Land shook his head. "We don't leave our planet as lightly as
     some folks do. No matter how far an Earthman goes, he always comes
     home."</p>,
     <p>"Still, you can hardly blame Control Council for giving you good
     advice," Carlin said, exasperated. "After all, it's your own fault if
     you foolishly squandered the copper resources of your planet and now
     lack power."</p>,
     <p>Harb Land's craggy face darkened. "Yes, we squandered our copper
     foolishly. We did it twenty centuries ago, when Earth was opening
     up the whole galaxy to travel. We spent our copper establishing the
     galactic civilization that's forgotten all about our power-starved
     world."</p>,
     <p>"Harb, please!" said Marn in a low voice, distress in her face.</p>,
     <p>A silence fell, and they finished the dinner without further
     conversation. But Jonny Land spoke to Carlin before he went upstairs.</p>,
     <p>"Don't take Harb too seriously. A lot of people here on Earth are so
     embittered about our lack of power that they're unreasonable."</p>,
     <p>Carlin found his bedroom dark. No automatic lights came on when he
     entered, and he could not find the switch. He gave it up, and got into
     bed and lay looking heavily out into the night.</p>,
     <p>Soft wind was stirring the trees around the house. Heavy scent of
     flowers drifted on it, stirring the window curtains. Down in the valley
     gleamed the spaceport beacons, and beyond lay a thin rim of glimmering
     sea over which the quarter-phase shield of Luna was rising.</p>,
     <p>He felt utterly miserable, homesick, wretched. If he were back at
     Canopus right now, he would be dancing with Nila in Sun City ballroom,
     or wandering in Yellow Gardens.</p>,
     <p>He drifted off to sleep despite himself, in his lumpy bed....</p>,
     <p>Carlin awoke with bright sunrise splashing his face. He reached
     sleepily for the aerator and refreshment buttons—then remembered.</p>,
     <p>To his surprise, he was feeling much better. He had slept well in the
     primitive bed, and fatigue had drained out of him.</p>,
     <p>Queer, musical notes that he guessed were calls of birds came to his
     ears. The air that snapped the curtains was chill now, but pure and
     sweet, subtly intoxicating.</p>,
     <p>"They do have finer air on this old world than any aerator can
     furnish," he thought.</p>,
     <p>He put on a zipper-suit that was dark brown and rough in weave.</p>,
     <p>"Going native," he thought with a sour grin, and went downstairs.</p>,
     <p>Marn Land was the only person he found in the sunny rooms. She still
     wore those barbaric faded old slacks, but had a red flower in her ashen
     hair. A little frown of worry in her forehead disappeared as she looked
     at him.</p>,
     <p>"You're feeling better, aren't you?" she asked.</p>,
     <p>"A lot," Carlin admitted. "I'm afraid I was rather rude last night, you
     know."</p>,
     <p>"You were tired," she said gravely. "Just sit down. I'll get your
     breakfast."</p>,
     <p>It was a new experience to Carlin to sit chatting in a sunny old
     kitchen while a girl in faded slacks prepared his breakfast on an
     electrode stove. Instead of punching the refreshment-button for it.</p>,
     <p>"Jonny and Harb have gone down to the spaceport," she said over her
     shoulder. "They and a few friends have an old planet-ship there that
     they're fixing up for a trip to Mercury."</p>,
     <p>"Mercury?" he said. "Oh, that's the innermost of these planets, isn't
     it?"</p>,
     <p>"Yes. Men here on Earth are always going prospecting for copper on its
     Hot Side. Jonny got up this prospecting expedition."</p>,
     <p>The breakfast she put before Carlin was of coarse wheaten bread, more
     of the natural eggs and milk, and a curious brown beverage made from
     stewing certain dried berries. She informed him its name was coffee.
     Carlin tried it, found it bitter and unpalatable.</p>,
     <p>A little surprised by his own action, he ate nearly everything else.
     The food was coarse, but satisfying enough, and he would have to get
     used to it if he were to stay here.</p>,
     <p>"I'll try not to be any trouble to you," he told Marn. "I'm just
     supposed to take it easy, do anything I want to."</p>,
     <p>She nodded. "I know. Some of our neighbors had Earth-treatment visitors
     as lodgers. They all got to like Earth a lot before they left."</p>,
     <p>Carlin did not voice his pessimism on that point. He went to the door
     and stood looking out into the sun-bright, flowery yard.</p>,
     <p>He felt at a loss. It was baffling to find himself without anything
     to do, no work crowding up that must be hurried through, no crews of
     ato-men to supervise in blasting spaceports out of untamed planets.</p>,
     <p>Marn looked at him understandingly. "You've always been busy, haven't
     you? Earth must seem slow and dull to you."</p>,
     <p>Carlin shrugged. "I might as well get used to it. I think I'll take a
     look around."</p>,
     <p>"You'll find Gramp fishing up at the north brook if you go that far,"
     Marn called after him as he walked across the yard.</p>,
     <p>Carlin sauntered past a big, locked ferroconcrete workshop of some
     kind, and some tall storage sheds, then on past the flat, wide
     hydroponic tanks that were now loaded with their masses of green growth.</p>,
     <p>He found a road beyond them that he did not recognize as a road, at
     first. It was a mere wide track gouged northward along the wooded
     ridge, the first dirt road that he had ever seen on a civilized world.</p>,
     <p>"A poor planet, all right," Carlin thought. "Can't even build decent
     roads."</p>,
     <p>There were hardly even any ato-fliers in the sky, only an occasional
     one flitting across the blue vault.</p>,
     <p>"No wonder these poverty-stricken devils resent the rest of the
     galaxy," he thought. "I suppose I would too, if it had been my bad luck
     to be born here."</p>,
     <p>The road was crazily illogical, winding westward along the woods-clad
     ridge in serpentine fashion. It twisted accomodatingly to avoid big
     boulders, a spring, a small gully.</p>,
     <p>The woods on either side was deplorably unkempt to Carlin's eyes. Big
     and small trees jumbled together, saplings choking each other out, dead
     brush and thorns and vines everywhere. There was even wild life in the
     woods, furry rodents scuttling away, hosts of birds.</p>,
     <p>This sort of thing was what you expected on some unpeopled planet that
     hadn't yet been pioneered and civilized. But Earth was the oldest
     human-peopled world in the whole galaxy.</p>,
     <p>Yet Carlin had to admit that there were certain compensations here.
     That winelike air was still an experience to him. And walking now came
     more easily to his muscles here than on any world. It seemed odd to be
     walking with such perfect ease, without wearing a de-grav.</p>,
     <p>He could not find the brook Marn had mentioned. He sat down on a log by
     the roadside, musing on the drowsy, dull quiet of this place. There was
     not a sound of human activity. Didn't these Earth people ever get bored
     with the sleepiness of the place?</p>,
     <p>Carlin found he was still tired. He watched a small, brilliant insect
     fluttering over a flower near by. Soft wind breathed through the ragged
     woods, stirring the green leaves and making a dappled, dancing pattern
     of sunlight on the ground. A distant bird called rustily.</p>,
     <p>"An old, outworn planet, dreaming," he thought. "These people, all of
     them, living in its past."</p>,
     <p>Carlin finally got up stiffly, and lounged back along the road. He was
     surprised to find that time had passed quickly, that the sun was now at
     the zenith. And that, somehow, his taut nerves had relaxed.</p>,
     <p>The big workshop behind the house had its doors open now. He glanced
     through them and was surprised to see that the cavernous room in there
     was a fairly well-equipped atomic-engineering laboratory.</p>,
     <p>Interested, Carlin started toward it. In the center of the big room
     he had glimpsed a towering, massive machine whose inner mechanism was
     concealed by a cylindrical metal cover.</p>,
     <p>"Looks like it might be a big field-generator of some kind," he
     muttered. "I wonder what it really is?"</p>,
     <p>There was a violent exclamation as an Earthman came running out from
     behind the machine to block his entrance.</p>,
     <p>Carlin recognized the broad red face, angry eyes and stocky figure of
     Loesser, the man who had argued with Jonny at the spaceport.</p>,
     <p>"What are you doing here?" Loesser demanded harshly.</p>,
     <p>Carlin was bewildered by his vehemence. "Why, I just wanted to take a
     look at this machine."</p>,
     <p>"I thought so!" blazed Loesser, his eyes raging. "I told Jonny that was
     why you came here!"</p>,
     <p>He snatched an object from his jacket pocket. To Carlin's thunderstruck
     amazement, the object was a stubby atom-pistol that Loesser was
     furiously leveling at him.</p>,
     <p class="ph1">CHAPTER IV</p>,
     <p class="ph1"><i>Mystery Machine</i></p>,
     <p>Laird Carlin was child of a galactic civilization in which violence
     between men was rare. There was plenty of danger yet, in pioneering new
     star-worlds, but over the civilized worlds themselves the unchallenged
     law of the Control Council maintained unbroken order. A man could go a
     lifetime without ever seeing violence.</p>,
     <p>The atom-pistol in Loesser's hand and the obvious murderous intention
     in the man's face stupefied Carlin. He was simply unable to adjust his
     thinking to the possibility that the enraged Earthman before him meant
     to blast him down.</p>,
     <p>"Why, what's the matter?" he began, puzzled and stunned.</p>,
     <p>He knew later how near he had been to death. At the moment, he so
     little recognized it that he felt no relief at the interruption that
     came now. Harb and Jonny Land came running forward from the cavernous
     interior of the workshop.</p>,
     <p>"Loesser, put that gun down!" snapped Jonny.</p>,
     <p>Loesser turned violently. "This fellow was spying on us! I saw him at
     the door!"</p>,
     <p>Harb Land's craggy face darkened ominously.</p>,
     <p>"I warned you what might happen," he said harshly to his brother.</p>,
     <p>"Is this man crazy?" Laird Carlin demanded bewilderedly of Jonny.</p>,
     <p>The lame youngster limped quickly forward. "Get back to work," he told
     the other two briefly. "Carlin, I'm sorry about this. I'll explain."</p>,
     <p>He walked beside Carlin toward the house. It was not until later that
     Carlin realized how deftly and unobtrusively he had been steered away
     from the workshop.</p>,
     <p>"Harb and Loesser and I, and a few others, are planning an expedition
     to Mercury to prospect for copper," Jonny was explaining. "In that ship
     you saw down at the spaceport. We've devised a new metal-finder of the
     radiolocator type, with which we hope to be able to locate new copper
     deposits. That's the machine in the workshop.</p>,
     <p>"We've maintained a certain secrecy about it," he went on, "because
     naturally we don't want other prospectors stealing the idea of our new
     finder and beating us to it. And I'm afraid Loesser thought you were
     spying on us. People here are always a little suspicious of strangers."</p>,
     <p>"So I've noticed," Carlin answered dryly. "This is the first world in
     the galaxy where I've ever felt completely unwelcome."</p>,
     <p>"Oh, I wouldn't say that," replied the other. "But put yourself in our
     place, Carlin. Figure how you would feel if you were an Earthman, your
     world starved for power because its copper was spent to establish a
     galactic civilization that now neglects it."</p>,
     <p>Jonny's thin brown face was earnest, his blue eyes watching Carlin as
     though eager to convince him. Carlin shook his head.</p>,
     <p>"I can see your problem in lacking copper," he said. "But the remedy
     for it is so simple. Nine-tenths of you should emigrate to other,
     better worlds as the Control Council advised."</p>,
     <p>Jonny smiled. "There you come up against the obstinacy of my people.
     We've an older planetary tradition, a deeper, more ancient love for our
     world, than any other people in the galaxy."</p>,
     <p>"I think you people live too much in the past," Carlin answered
     frankly. "But it's none of my business. Anyway, I hope your expedition
     brings home copper."</p>,
     <p>"Thanks," Jonny said softly. "I think we have a good chance."</p>,
     <p>Carlin went back to the veranda of the old house and sat there
     pondering. Something about Jonny's explanation had been vaguely
     unsatisfying.</p>,
     <p>To his trained eyes, the glimpse he had had of that towering machine
     had not suggested any metal-finding device. There had somehow been a
     suggestion in its half-glimpsed bulk of something quite different;
     something vaguely disturbing, almost menacing.</p>,
     <p>"The devil, I must have knots in my subconscious to start getting
     premonitions like that," Carlin swore. "The poor devils are just
     secretive about their plans because everyone else here is that way."</p>,
     <p>He lounged boredly around the house during the hot, sleepy afternoon.
     There was no one to talk to, for the brothers stayed out in their
     workshop and Marn was out tending the big hydroponic tanks.</p>,
     <p>He tinkered with the old video set in the living room but the
     only stations he could get were local Earth ones, and lectures on
     hydroponics and gossip about unknown people didn't interest him.</p>,
     <p>He finally gave up and stretched out on the veranda, staring sleepily
     down into the green cup of the valley and cursing the psychotherapist
     whose insane idea had sent him here to die of boredom. He dozed until
     he was awakened by the sputter of an arriving ato-truck.</p>,
     <p>It contained three lanky young men, tall Earthmen who went back to
     the workshop without stopping at the house. The other partners in the
     prospecting expedition, Carlin supposed sleepily.</p>,
     <p>Again he felt that queer sense of something threatening, that vague
     premonition that had clung to him ever since he glanced into the
     workshop. If only he could remember what that machine reminded him of.</p>,
     <p>Days passed and Carlin still could not remember that, though his
     disturbing doubt persisted. There was no chance of another look into
     the workshop for it was always locked except when Jonny and Harb and
     their half-dozen partners worked in it.</p>,
     <p>"The trouble with me," Carlin told himself ironically, "is that I
     haven't anything else to occupy my mind on this blamed world."</p>,
     <p>Yet Carlin's first repelled dislike of Earth had faded much by now.
     The crudities of existence, the lack of civilized conveniences, no
     longer bothered him so much. He had to admit that whether or not
     Earth-treatment was benefiting his twisted subconscious, this sleepy
     old planet was a fine place for a rest.</p>,
     <p>He spent his mornings idly rambling the twisting roads, his afternoons
     lounging on the cool, shady veranda of the old house, or helping Marn
     tend the hydroponic tanks. Or fishing with Gramp in the foaming brook
     below the ridge, while that oldster told interminable tales of the old
     days when he had followed space.</p>,
     <p>Neighbors, hydroponic farmers up and down the valley, dropped in at
     the Land house in the evenings. Carlin did not intrude, and gradually
     their first stiff suspicion of him abated and they talked freely before
     him. The talk always swung to the paramount consideration on this
     power-starved planet—the need for copper. It made Carlin feel a little
     guilty to remember how much of it was wasted on other worlds.</p>,
     <p>"I have to drive down to the spaceport for Jonny, to get some
     instruments he left in the ship," Marn said to him after dinner one
     evening. "Do you want to go along?"</p>,
     <p>Carlin grinned. "I've legged it so much lately that riding anywhere
     would be a change."</p>,
     <p>The old ato-truck swung down the twisting road in the blaring sunset.
     The heavens behind them were a glory of fusing colors as the red ball
     of Sol dipped majestically toward the horizon.</p>,
     <p>Despite his appreciation of that wild splendor, Carlin felt a vague
     uneasiness. Why should the loveliness of the evening bring disturbing
     recollection of Jonny Land's puzzling machine into his mind?</p>,
     <p>"You're getting to like it better here, aren't you?" asked Marn.</p>,
     <p>She was usually so silent with him that Carlin glanced quickly at
     her profile as she drove. It struck him with surprise that she had a
     certain beauty. Her thick mop of ashen hair, and firm-chinned face,
     and small, competent hands grasping the wheel, were oddly attractive.
     It wasn't the fine-edged, shimmering beauty that Nila had, but it had
     appeal.</p>,
     <p>"Yes, I must be getting more accustomed to it," he answered her
     question. "And it's not as provincial as I thought. Nearly every man
     you meet here has been to space some time or other."</p>,
     <p>"Every Earth boy runs away to space sooner or later," she said, and
     smiled. "Following space is in our blood. And our planet's so poor now
     that it's the only way most of our men can make a living." She added,
     "Some of our men never come back. My father didn't. And my mother died,
     when he was lost."</p>,
     <p>It was dusk when they reached the spaceport. As he walked with the girl
     along its edge toward her brothers' ship, she drew him aside toward a
     tall shaft that loomed up spectrally in the twilight.</p>,
     <p>"This is where the first Earthman went away to space," she told him.</p>,
     <p>He looked at the deeply engraved legend on the pedestal of the soaring
     column. It was the Monument to the Space-Pioneers.</p>,
     <p>"Gorham Johnson took off in his first flight from this very spot," Marn
     said.</p>,
     <p>Carlin strained his eyes in the dusk to read the roll of names and
     dates engraved on the pedestal.</p>,
     <p class="ph1">Gorham Johnson, 1991<br/>
     Mark Carew, 1998<br/>
     Jan Wenzi, 2006<br/>
     John North, 2012</p>,
     <p>Names of the men who long ago had first dared space, the men who had
     first followed a dream to the nearby planets that then had seemed so
     far, the men who had first hurtled starward and opened up the galaxy.</p>,
     <p>"Lord, more than two thousand years ago," Carlin murmured. "Queer
     little ships they must have had."</p>,
     <p>His imagination was touched. This simple roll of names of men long dead
     somehow brought it all close to him for the first time.</p>,
     <p>Those old, pathetically flimsy ships, the enormous courage of those men
     to whom space was all one unknown abyss. He began to understand why
     tourists came from all the galaxy to see these mementoes.</p>,
     <p>"They and their little ships started it all, the whole galactic
     civilization, the vast human empire," he said musingly.</p>,
     <p>Marn was looking up at the spire towering in the dusk.</p>,
     <p>"People criticize us Earthmen for our pride. But this is why we're
     proud. We're the people who opened up the frontiers of the Universe."</p>,
     <p>Carlin nodded thoughtfully. "You've a great heritage. But perhaps you
     remember it too well. This is the present, not the past."</p>,
     <p>"You're like all the others, you think Earth's history is over," Marn
     said defiantly. "You'll find out differently. Earthmen will open up the
     last frontier of all—" She checked herself suddenly, and then said,
     crestfallen, "I'm sorry. I didn't mean to quarrel."</p>,
     <p>Carlin wanted to ask what she had meant, but Marn started on again
     through the deepening darkness toward her brother's ship.</p>,
     <p>He walked with her into the battered planet-cruiser and looked around
     curiously. It was a medium craft designed for a minimum crew, with
     oversize cyclotrons and propulsion-wave equipment, drive-plates fore
     and aft, and an unusually heavy set of heat-screen generators.</p>,
     <p>"The Hot Side of Mercury is terrible," Marn said when she saw him
     glancing at the generators. "You need the heaviest heat-screens you can
     get to prospect there."</p>,
     <p>Amidships, Carlin noticed a big, empty round room or hold. There was
     nothing in it but a skeleton of girders designed to hold something over
     a sliding plate in the floor.</p>,
     <p>He remembered Jonny's big machine in the workshop. It would fit into
     this frame. He would have liked to make further inspection but Marn had
     found the instruments she had come after.</p>,
     <p>As they emerged from the ship, a lean, uniformed figure in the dusk
     greeted them in a pleasant voice.</p>,
     <p>"Hello, Marn. I saw you walking across the tarmac. How is Jonny coming
     with his plans?"</p>,
     <p>It was a young man in the gray uniform of Control Operations, the
     agency of law and order throughout the galaxy. He bowed to Carlin.</p>,
     <p>"I'm Ross Floring, Control Operations commander here. You're the
     Earth-treatment chap staying with the Lands? Glad to meet you."</p>,
     <p>Floring was not more than thirty, an alert, clean-cut, likable young
     man. He turned back to Marn.</p>,
     <p>"How soon are Jonny and his friends planning to take off for Mercury?"</p>,
     <p>Marn looked uncomfortable. "I don't know, Ross. They have some more
     preparations to make, they say."</p>,
     <p>Carlin somehow sensed a strain in the atmosphere. There was an
     earnestness in Floring's manner that was not accounted for by his words.</p>,
     <p>"I like Jonny a lot, Marn," he said seriously. "You know that. I'd
     hate to see him have trouble on this expedition."</p>,
     <p>Marn seemed to evade his meaning. "Jonny won't have any trouble. A trip
     to Mercury is nothing for Harb and him."</p>,
     <p>"I sincerely hope he won't," Floring said quietly. "Copper isn't worth
     risking too much for. Tell him I said so, will you? And tell him I'm
     coming up some day to talk with him."</p>,
     <p>Marn was obviously eager to get away. Carlin, puzzled, followed her.</p>,
     <p>"I'll see you again, Mr. Carlin," Floring called after him pleasantly.
     "We can have a talk about home. Yes, I come from Canopus too."</p>,
     <p>It wasn't until they were in the ato-truck driving homeward that Carlin
     realized he hadn't told Floring his name or origin. Why would Control
     Operations have taken the trouble to check up on that?</p>,
     <p>"Floring seemed like a nice chap," he told Marn. The girl nodded,
     troubled.</p>,
     <p>"He is—one of the best," she said. "And he likes Jonny. But he'd
     forget everything else for his duty."</p>,
     <p>She was, obviously, thinking aloud rather than answering Carlin. He
     wondered again about that queer feeling of strain. It had sounded
     almost as though Floring were warning her.</p>,
     <p class="ph1">CHAPTER V</p>,
     <p class="ph1"><i>Desperate Play</i></p>,
     <p>The truck wheezed and groaned up the dark old road to the ridge. In the
     velvet black skies, the stars were chains of glittering light. Vega,
     Arcturus, Altair—they looked far away.</p>,
     <p>The house was dark when Marn stopped the truck behind it, though there
     were still lights out in the workshop. There was a solemn, buzzing hush
     about the starlit summer night.</p>,
     <p>"I have to take these things back to Jonny," said the girl.</p>,
     <p>"Marn, what are your brothers really planning?" Carlin asked her. "Does
     Floring know?"</p>,
     <p>She twisted uncomfortably. "Jonny told you all about their plans
     himself, didn't he?"</p>,
     <p>She was such a poor liar, she was so oddly appealing a figure in the
     starlight as she looked up at him with troubled white face, that
     sudden impulse made Carlin bend and kiss her.</p>,
     <p>Her small body was firm and warm in his hands and there was a
     breathlessness about her cool lips. But she did not move.</p>,
     <p>He looked down at her. "You don't mind, do you?" he asked.</p>,
     <p>"No, I don't mind," Marn said, her voice toneless, "It's all right for
     a star-world visitor to have a little flirtation with an Earth girl
     before he goes away, isn't it?"</p>,
     <p>"But it isn't that!" Carlin started to protest, and then stopped.</p>,
     <p>After all, what was it but that? What could it be but that?</p>,
     <p>"It's all right, but please don't again," Marn said quietly. "Good
     night, Laird."</p>,
     <p>He went into the house feeling depressed and thoughtful. He wished now
     that he hadn't had that impulse. Marn wasn't the sophisticated sort.</p>,
     <p>Lying in his bed and looking out the window at the distant spaceport
     beacons down in the valley, Carlin heard her come in and retire.
     Apparently Jonny and Harb were still working.</p>,
     <p>What were they working at really? Why had Floring been so grave in his
     veiled warning?</p>,
     <p>"Oh, the devil, it's none of my business," Carlin yawned. "There isn't
     much in this little system for them to get into trouble about. Nothing
     but eight or nine small planets and one medium sun."</p>,
     <p>Carlin suddenly sat bolt upright in bed as his mind dwelt on that last
     thought.</p>,
     <p>"The Sun? Good glory, that's what they're up to! It must be!
     Sun-mining!"</p>,
     <p>He was dismayed, horrified by the sudden flash of revelation. The
     disquieting mystery that had puzzled him since his first coming here
     suddenly shaped clearly as pieces fell together in his mind.</p>,
     <p>"They wouldn't be so crazy as to try it, surely! Yet it all fits
     together—the heat-screens on their ship, the secrecy about it all. And
     that machine I saw could be a big magnetic dredge!"</p>,
     <p>Sun-mining! Most strictly forbidden of enterprises, banned by the
     Control Council for years since the first disastrous attempts at it had
     almost wrecked certain planetary systems.</p>,
     <p>Visions of frightening possibilities crowded Carlin's mind, of a
     desperately reckless attempt unchaining catastrophe on the inner
     planets of this little system.</p>,
     <p>"But Jonny Land wouldn't try it! He's a CE, he knows what would happen."</p>,
     <p>Carlin could not convince himself. He remembered only too clearly
     Jonny's intense obsession with Earth's copper shortage, his quiet
     determination.</p>,
     <p>And Floring must suspect something of the truth! That was what had made
     the Control Officer give his grave hinted warning.</p>,
     <p>Carlin got up and feverishly dressed. He had to find out the truth,
     now, at once. If the Land brothers and their friends were really bent
     on such a mad enterprise, it would have to be stopped even if it meant
     his informing Control Operations.</p>,
     <p>"If I could get one good look at the inside of that machine of theirs,
     I could soon tell whether it's really a magnetic dredge," he thought.</p>,
     <p>He went quietly down through the dark house and out into the starlight.
     Light and sounds of activity still came from the workshop.</p>,
     <p>Carlin crept toward it. He hated this spying. But he had to know. He
     couldn't permit a crazy attempt to unloose disaster here.</p>,
     <p>The workshop was closed, and there were no windows. But as he stood
     irresolute, the big front doors opened and Loesser and two other young
     Earthmen came out, wearily mopping their brows.</p>,
     <p>"We'll be back tomorrow, Jonny," Loesser called back into the building.
     "Ought to finish her up in a few days now."</p>,
     <p>The three strode wearily toward their ato-truck and drove away. The
     doors remained open for the moment.</p>,
     <p>Carlin stepped forward and from his vantage in the dark peered into the
     big lighted room. Jonny and Harb Land were putting back the metal cover
     on the central mechanism, before they too quit work.</p>,
     <p>One glance at the interior of that machine was enough for Carlin's
     trained eyes. Those big magnetic-current coils, that massive beam-head,
     that battery of Markheim filters—he had been right, they spelled
     disaster.</p>,
     <p>A small, hard object prodded Carlin's back and a voice throbbing with
     anger spoke in his ear.</p>,
     <p>"This is an atom-pistol. Raise your hands. I don't want to harm you."</p>,
     <p>"Marn!" he exclaimed, stunned.</p>,
     <p>"Don't turn!" warned the girl. Her voice was choked with wrath. "I
     heard you get up and I followed you out here. You are a spy!"</p>,
     <p>"Don't turn!" warned the girl. "I followed you here. You are a spy!"</p>,
     <p>Carlin was so stunned with horror by his discovery of the brothers'
     catastrophic plans, that he reacted by sheer, desperate impulse to the
     weapon in his back. He swung around and grabbed for the atom-pistol.</p>,
     <p>It would have been suicidal, had another than Marn been holding the
     weapon. But Marn, as much a stranger as he to deadly violence, let her
     finger hesitate on the trigger too long. Perhaps she would not have
     fired in any case. Pondering it later, he was not sure.</p>,
     <p>What happened was that he got his hand on the slim pistol and snatched
     it out of her grasp before her hesitation ended. Marn, her face white,
     called frantically:</p>,
     <p>"Harb! Jonny!"</p>,
     <p>The two brothers came running out from the rear of the lighted
     workshop, Harb's craggy face dark and deadly as he saw them.</p>,
     <p>Carlin jumped back, leveled the weapon he had just taken from the girl.</p>,
     <p>"Get back!" he ordered hoarsely. And as Harb Land, blindly raging, came
     on: "I don't want to kill anybody!"</p>,
     <p>Jonny's voice rang command. The lame youngster's thin brown face was
     set, but he had not lost calm.</p>,
     <p>"Harb, stop!"</p>,
     <p>The thing froze into a queer sort of tableau as Harb Land pulled up
     and stood there, his giant figure quivering with wrath, his big fists
     clenched as he glared at Carlin.</p>,
     <p>"I told you," Harb said thickly over his shoulder to his brother. "I
     told you what would happen if we took him in."</p>,
     <p>Marn had run toward them, her face pale and stricken.</p>,
     <p>"It's my fault, Jonny," she said despairingly. "I heard him come out
     and followed him, but let him take my gun instead of shooting."</p>,
     <p>"Quiet, Marn," soothed Jonny. "It's going to be all right. Carlin just
     doesn't understand."</p>,
     <p>The lame youngster, in this taut moment of strain, was suddenly the
     biggest of them, the dominating personality here.</p>,
     <p>"I understand, all right," Carlin said hotly. "I guessed it tonight,
     and one look at that magnetic dredge confirmed my guess." His voice
     crackled with the rising wrath he felt. "Going to Mercury prospecting,
     were you? You never had any such plan. You and your partners have been
     getting ready to attempt sun-mining."</p>,
     <p>Jonny's eyes and voice were calm as he said:</p>,
     <p>"Carlin, Earth's starved for power. You've seen for yourself. To get
     the power that will revive our world, we've got to have copper. And
     the copper in our planets was exhausted long ago. But there's still
     billions of tons of copper in our System, in one place. The Sun. It's
     there in hot gases, more copper than Earth and our sister-planets will
     need for millenniums to come. It's our only possible source of copper
     and we intend to tap it."</p>,
     <p>"You and the others have brooded so long over your need for copper that
     you've gone crazy!" Carlin said, his voice whipped with anger.</p>,
     <p>"What's crazy about our using the copper of the Sun for our planet?"
     Jonny asked evenly.</p>,
     <p>"You, a CE, ask me that?" cried Carlin. "You know as well as I do that
     sun-mining brings catastrophe! Oh, you can get close enough to the Sun
     in your ship, I know. You can suck up all the gaseous copper you want
     from it, with that magnetic dredge. But what happens on your Sun when
     you do it?</p>,
     <p>"You know as well as I what would happen, what has always happened
     when it was tried. The suction creates a whirl in the solar surface,
     a tiny Sun-spot that grows and grows until it's grown into a terrific
     solar typhoon that pours disastrous increased heat and electric force
     onto its planets. You know it's happened every time Sun-mining was ever
     tried, and that that's why Control Council forbids Sun-mining."</p>,
     <p>Jonny Land nodded calmly. "I know all that. But suppose I've found a
     way to do Sun-mining without starting Sun-spots?"</p>,
     <p>Disbelief hardened Carlin's voice. "You haven't. Nobody ever has. There
     just isn't any way—suck out gases from any point on the Sun and you
     lower pressure at that point, and lowered pressure automatically starts
     a whirl."</p>,
     <p>"Carlin, I <i>have</i> found such a way! I tell you, with it we can suck
     unlimited copper from the Sun without creating one tiny Sun-spot!"</p>,
     <p>Laird Carlin stared. "You're telling me that, because you know I'm
     going to report your plans to Control Operations."</p>,
     <p>"You wouldn't do that!" cried Marn, incredulously.</p>,
     <p>Carlin nodded firmly. "I don't want to but I've got to. I can't let a
     bunch of crazy men bring on a disaster that might scorch life itself
     off your inner planets."</p>,
     <p>Jonny Land's thin face flared irritable emotion as he limped forward
     unheeding of the gun in Carlin's hand.</p>,
     <p>"Carlin, man, be reasonable! Why do you suppose I had you come here and
     live with us? It was because you're a CE and I'll need another trained
     engineer's help in operating this thing. And do you suppose I ever
     thought I could get your help unless I could convince you I've found
     the way to safe Sun-mining? I can convince you, Carlin!"</p>,
     <p>Carlin felt the conviction in Jonny's voice. What the crippled young
     man said did logically explain something otherwise puzzling—why they
     had taken him into their home when their work was so secret.</p>,
     <p>He remembered now that it was not until Jonny Land had learned he was
     a CE, on his first arrival on Earth, that the young Earthman had shown
     interest and offered him lodgings.</p>,
     <p>"All I ask," Jonny was saying earnestly, "is that you give me a chance
     to explain our plans to you. I know I can convince you that we can mine
     the Sun without the slightest danger of disaster."</p>,
     <p>"If that's so," Carlin demanded skeptically, "why didn't you convince
     the Control Council of that, and get permission for Sun-mining instead
     of trying to do all this in secret?"</p>,
     <p>"Carlin, I did try to convince the Council," Jonny Land declared. "I
     made one petition to them after another, giving them full details of
     my plan. But Council isn't composed of engineers. And the popular
     prejudice against Sun-mining, due to those past disasters, is so strong
     that Council refused us permission to make the attempt."</p>,
     <p>"That's why Ross Floring and the others down at Control Operations
     watch my brothers so closely, Laird," Marn added quickly. "They know
     about our petitions, and Floring suspects that Jonny is going to try
     this thing anyway."</p>,
     <p>It all fitted together logically, Carlin had to admit. Yet he still
     stood irresolute, the atom-gun in his hand.</p>,
     <p>"Here's a proposition, Carlin," said Jonny. "I'll explain every detail
     of our plan to you in the morning. If you don't admit then that the
     plan's completely without danger of disaster, I'll let you go and tell
     everything to Floring. I give you my word on it."</p>,
     <p>Carlin looked at him doubtfully. "Jonny, you'd break your word as
     cheerfully as your neck to carry out your purpose for Earth."</p>,
     <p>Jonny Land grinned crookedly. "That's true. But on the other hand,
     I'm still hoping for your help in this project. That's why I want to
     convince you, and that's the best guarantee I can give you."</p>,
     <p>Carlin shrugged, but he slowly lowered the weapon.</p>,
     <p>"I can tell you right now that I'll have no part in any such illegal
     venture," he said flatly. "But I'm willing to hear your explanation."</p>,
     <p>"Well," Jonny said, with a tired sigh, "we've had enough dramatics
     for one evening. Harb, lock up the workshop and we'll all turn in for
     tonight."</p>,
     <p>Carlin looked a little awkwardly at Marn as he handed her back the
     atom-pistol.</p>,
     <p>"I'm sorry if I appear ungrateful for your hospitality," he told her.
     "It's just that I can't stand by and do nothing if a crazy attempt
     threatens to bring on catastrophe."</p>,
     <p>"I know," Marn said soberly, and there was no hostility in her face.
     "But you'll find out that Jonny knows what he's doing."</p>,
     <p>Out of the darkness behind them spoke a shrill voice that made Laird
     Carlin swing around in astonishment.</p>,
     <p>"Well, I'm blamed glad you people quit arguin' for tonight, anyway.
     It's time all decent folks was in bed."</p>,
     <p>Gramp Land stood back there in the dark where he had apparently been
     standing for some time. There was a grin on his withered face as he
     lowered the heavy atom-gun he had been holding.</p>,
     <p>"Sure got tired holdin' this thing aimed at your back, Mr. Carlin," he
     chuckled.</p>,
     <p class="ph1">CHAPTER VI</p>,
     <p class="ph1">"<i>You Owe a Chance to Earth!</i>"</p>,
     <p>Doubts assailed Carlin almost as soon as he retired. He could not
     sleep, the rest of that night.</p>,
     <p>Had he been childish to let Jonny persuade him into giving the plan a
     hearing? Jonny was sincere enough, but he was a fanatic on this one
     subject of securing power for Earth.</p>,
     <p>The recklessness of Earthmen was proverbial. These men, made desperate
     by long brooding over the poverty of their world, might think little of
     the danger of provoking solar catastrophe in their obsessed desire to
     secure copper.</p>,
     <p>Carlin chilled. He remembered what had happened years ago at the star
     Mizar when Sun-mining had been attempted. The suck of magnetic dredges
     swiftly creating a whirl in the star's surface gases, a Sun-spot
     maelstrom that had expanded with disastrous swiftness. And then the
     engulfing of the mining ships in the sudden outpour of increased heat,
     the scorching of inner planets that wreaked ruin before the spots
     subsided.</p>,
     <p>It had been the same later at Polaris, and at Delta Gemini. No wonder
     that such a popular wrath against Sun-mining had arisen that Control
     Council had strictly forbidden further attempts! Man's science, great
     as it was, was not yet great enough to dare tampering with stars.</p>,
     <p>Yet he could see, too, how these Earthmen would inevitably turn their
     thoughts to Sun-mining. There was not any copper left in their System
     except in one body—their Sun. And that had limitless amounts of the
     power-metal, in vaporized form. No wonder they had been led into the
     plan to tap the metal of their Sun.</p>,
     <p>Carlin dozed before daybreak, but woke with the sunrise and went down,
     to find the others already at breakfast. They greeted him with a word,
     all but Harb Land who maintained a stony, dangerous silence.</p>,
     <p>"We'll go out and show you our work, as soon as you have breakfast,"
     Jonny said quietly.</p>,
     <p>Gramp Land was the only one in good spirits. The old man twitted Carlin.</p>,
     <p>"It's sure a good thing you got reasonable last night. I would have
     hated to blast you."</p>,
     <p>Marn smiled slightly. "You wouldn't have done it. You're too
     chicken-hearted even to kill a fly."</p>,
     <p>"Ho, what are you talking about?" exclaimed Gramp indignantly. "When I
     was young, they called me the toughest Earthman in space."</p>,
     <p>Carlin walked silently out to the workshop with Harb and Jonny. The
     lame youngster opened the building, and then gestured toward the tall,
     cylindrical machine.</p>,
     <p>"Take a look for yourself, first," he invited.</p>,
     <p>Carlin scanned the mechanism with trained eyes. Magnetic dredges were
     a little out of his line, yet the principle of the mechanism was clear
     enough.</p>,
     <p>"You understand the basic idea of Sun-mining?" Jonny was saying.
     "A ship approaches the photosphere or visible surface of the Sun
     as closely as possible, protected by heavy heat-screens from the
     radiation. The magnetic dredge is then turned on. The dredge generates
     a high-powered magnetic field concentrated into a beam. That beam
     drives down into the swirling super-hot gases of the solar surface.</p>,
     <p>"Those gases consist of dozens of metals and other elements in
     vaporized form—iron, copper, sodium, calcium and so on, all mixed
     together. The beam sucks a column of those solar gases up to the
     ship. For its magnetic pull powerfully attracts the iron vapor in the
     mixture, and so the whole mixture is rapidly sucked upward."</p>,
     <p>He pointed to the massive flared nozzles in the downward projector-face
     of the great machine.</p>,
     <p>"The gases are sucked in there, through Markheim filters which can be
     set to screen out the atoms of any desired element. The copper gases
     are screened out, solidified by cooling, and stored. The other gases go
     on through the filters."</p>,
     <p>Carlin nodded curtly. "And those unwanted gases are ejected into space,
     and more of the solar mixture continuously drawn up, and so on until
     your ship is filled with copper. Yes, it's the same scheme that was
     used by the Mizar and Polaris Sun-miners. And it will have exactly the
     same result! Sucking gases out of any point in the solar surface will
     lower pressure at that point. And lowered pressure at any point of the
     photosphere instantly and inevitably starts a whirl of gases, a growing
     maelstrom or Sun-spot!"</p>,
     <p>Jonny Land shook his head. "Carlin, you're jumping to conclusions. This
     dredge does not simply eject its unwanted gases into space like former
     designs. Take a look at that beam-head more closely."</p>,
     <p>Carlin looked. And he was puzzled, after a brief inspection of the
     curious concentric construction of the beam-head.</p>,
     <p>"I don't get it. It looks like you have two circular beam-heads, one
     inside the other."</p>,
     <p>"That," said Jonny, "is the secret of my scheme. Lowered pressure in
     the solar surface at the point of suction creates a whirl, a Sun-spot.
     But suppose we can suck up gases without lowering pressure?"</p>,
     <p>Carlin stared. "How?"</p>,
     <p>"The two beam-heads," reminded the lame youngster eagerly. "The inner
     one is the one that beams down a positive magnetic pull to suck up
     solar vapors. The outer one is designed to use a simultaneous negative
     magnetism to shoot the unwanted vapors back down into the Sun."</p>,
     <p>The whole meaning of the explanation flashed over Carlin, and the
     possibilities of it dawned across his brain.</p>,
     <p>He said nothing, but crawled under the towering dredge and for minutes
     inspected inside and outside of the beam-head, feed-tubes and cut-offs.
     He finally came back out to them.</p>,
     <p>"Well?" challenged Jonny Land.</p>,
     <p>Carlin bit his lip. "I've got to admit your scheme looks practical
     enough. You should be able to suck up gases without any Sun-spotting
     effect, by using that continuous kickback. But—"</p>,
     <p>"But what?" demanded Harb Land, frowning.</p>,
     <p>Carlin shook his head. "Blast it, I can't see why the Council would
     turn down your petition if this is as workable as it seems."</p>,
     <p>Jonny shrugged. "I told you why. Control Council contains the finest
     statesmen in the galaxy. Statesmen, not engineers. They admitted their
     experts' reports on this showed it theoretically workable. But they
     said it was too dangerous to take a chance on theory when it comes to
     tampering with suns. We don't need copper that badly, they said."</p>,
     <p>His fists clenched in sudden passion. "We don't need copper! The galaxy
     as a whole doesn't need it, they meant. And what does it matter if one
     little world called Earth is fading and dying for lack of the copper
     it squandered to open up the galaxy? What does it matter, except to
     Earthmen?"</p>,
     <p>It was the first time that Carlin had ever seen Jonny Land give way to
     emotion. The superhuman strain that drove and dominated this lame, thin
     youngster for a moment flared hot and anguished on his face. Then his
     narrow shoulders sagged. He stood looking at the towering dredge with
     brooding eyes, before turning to Carlin.</p>,
     <p>"Carlin," he said then, "there's only one way to prove to the Council
     this way of Sun-mining is safe—and that's by doing it! That's what
     we're going to do. We're going to the Sun and come back with a shipload
     of copper. They'll see then that it's wholly safe. They'll have to
     give permission then. And a fleet of ships equipped with dredges can
     suck enough copper from the Sun to give Earth all the power it needs
     hereafter.</p>,
     <p>"You've seen the dredge and you know our plans. You've seen enough of
     Earth to know how much our success would mean to this world. Carlin, do
     you still want to tell Floring about this?"</p>,
     <p>"You couldn't!" exclaimed Harb Land harshly. "You couldn't destroy all
     the hope that's left for our world's people. You—all you star-world
     people—you owe this chance to Earth!"</p>,
     <p>Carlin stood there, torn by conflicting feelings. Strong among them was
     his intense admiration as an engineer for the ingenuity and daring of
     Jonny Land's solution to the problem.</p>,
     <p>But there were other things to consider. There was the duty he and
     every citizen had to support the Control Council. That support was what
     kept galactic civilization going. Yet these Earthmen, this little band
     fighting so fiercely for their ancient, worn world would flout it.</p>,
     <p>"Jonny!" came Marn's sharp cry from outside. "Jonny!"</p>,
     <p>"Something's wrong!" Jonny exclaimed, limping hastily forward.</p>,
     <p>They hurried out into the sunlight. Marn was running toward them and at
     the same moment they heard the drumming of an approaching ato-car.</p>,
     <p>"It's Ross Floring coming here!" Marn panted. "I recognized his car
     coming up the hill!"</p>,
     <p>Harb uttered a fierce exclamation, but Jonny cut in quickly:</p>,
     <p>"He's only coming up here to look around. He suspects what we're up to,
     but he can't be sure. Don't show any excitement."</p>,
     <p>Harb gestured fiercely toward Carlin. "But if he says anything, Floring
     will know."</p>,
     <p>A pleasant voice hailed them. Ross Floring, lean in his gray uniform,
     drove up behind the house and climbed out of his ato-car.</p>,
     <p>"Hello, folks," he greeted. "Thought I'd come up and see you. Jonny, I
     haven't seen you for weeks. Every time you come down to the spaceport,
     you spend all your time buried in that ship."</p>,
     <p>Jonny smiled. "It's keeping us pretty busy, getting ready."</p>,
     <p>Laird Carlin sensed genuine liking between the Control Operations
     officer and the lame young engineer. Yet there was unspoken tension
     too. It showed behind Jonny's cool smile and Floring's pleasant eyes.</p>,
     <p>Floring was looking past them, through the open doors of the workshop
     at the towering magnetic dredge.</p>,
     <p>"Is that your new metal-finding dingus, Jonny? The thing you're going
     to use to locate copper on Mercury?"</p>,
     <p>He stepped toward it. Harb Land made a violent movement forward, but a
     flat look from his brother stopped him.</p>,
     <p>"Yes, that's it," Jonny said. "Want to look it over, Ross?"</p>,
     <p>Floring stood, cocking his head at the towering machine. He laughed at
     the question.</p>,
     <p>"Jonny, you know I'm no engineer. A thing like this is beyond me." He
     turned toward Carlin. "But Mr. Carlin, you're a CE. What do you think
     of this new metal-finding device of Jonny's?"</p>,
     <p>Breathless silence held the group for a moment. Floring's face was
     unmoved, pleasant, but his purpose was obvious now. Knowing that Carlin
     had come to Earth merely as an Earth-treatment case, he was counting on
     Carlin's unbiased truthfulness.</p>,
     <p>Carlin felt their eyes on him. Now was the time, he knew, to play the
     part of a good galactic citizen and inform Floring just what was going
     on. It was his duty to do it.</p>,
     <p>But he couldn't! He couldn't betray the last desperate hope of a
     gallant old planet's people in their struggle against destiny! He had
     known he couldn't, from the time Floring had first appeared. He spoke
     as casually as he could.</p>,
     <p>"Yes, I've looked it over. It's one of the most ingenious metal-finders
     I've ever seen."</p>,
     <p>Carlin felt a queer relief that was almost happiness, as he spoke. For
     he knew now that he could never have obstructed these people in their
     brave, desperate struggle to revive their planet.</p>,
     <p>But Ross Floring looked astounded. A little blank frown of surprise
     came into his face and he stared steadily at Carlin.</p>,
     <p>"Then you approve of Jonny's plans?" he said quietly, "But, of course,
     I might have known that he'd convince you."</p>,
     <p>There was double meaning to the Control officer's words, clear to all
     of them. Yet they all ignored it.</p>,
     <p>Floring was temporarily defeated. He couldn't take action without
     expert opinion that the machine before him was for Sun-mining. He had
     expected such an opinion from Carlin, and had been disappointed.</p>,
     <p>But he was not completely frustrated. Carlin found out now how
     thorough and resourceful was this pleasant young officer.</p>,
     <p>"It would be a shame, Jonny," Floring remarked casually, "if you should
     run into disaster on this trip and the design of your new apparatus be
     lost. A metal-finder like this is too valuable to lose."</p>,
     <p>They were momentarily puzzled by the comment. But in the next moment,
     Floring showed what he had in mind. He drew from his jacket pocket
     a tiny tri-dimen camera, stepped close to the towering dredge, and
     before anyone could prevent it had snapped a half-dozen pictures of its
     interior mechanism.</p>,
     <p>Harb Land started forward with a smothered oath. But it was too late.
     Floring was already pocketing the camera.</p>,
     <p>"I'll keep these films," he said calmly. "If your machine should ever
     be lost, the design of it will be preserved this way."</p>,
     <p>"You can't keep those films!" Harb Land exclaimed angrily. "You've no
     right!"</p>,
     <p>"You surely don't think I would steal the design from you?" Floring
     said, with a look of surprise.</p>,
     <p>"It isn't that," Harb protested. "But—"</p>,
     <p>"But what?" the officer asked calmly.</p>,
     <p>Harb was silent, his craggy face a mixture of emotions as he looked
     appealingly at Jonny.</p>,
     <p>Carlin understood Floring's cleverness. They could not protest the
     films without giving the real reason for their protest, and that they
     could not do.</p>,
     <p>"It's all right for him to keep those pictures, Harb," Jonny said
     quietly.</p>,
     <p>Floring turned, bidding a pleasant farewell.</p>,
     <p>"I'll be seeing you again soon," he promised.</p>,
     <p class="ph1">CHAPTER VII</p>,
     <p class="ph1"><i>Last Frontier</i></p>,
     <p>As soon as Floring's ato-car had purred away, the little group stood in
     the sunlight outside the workshop, in stricken silence.</p>,
     <p>Carlin put into words what was in all their minds.</p>,
     <p>"Jonny, you know why he took those pictures! He'll telephoto them to
     Canopus headquarters to be examined by engineer experts, and they'll
     send back word that the machine is a magnetic dredge for Sun-mining!"</p>,
     <p>Jonny nodded. "Yes, of course. Floring has suspected our plans all
     along, and now he's going to make sure."</p>,
     <p>"And when word comes back from Canopus, he'll seize our dredge and ship
     to stop our expedition!" groaned Harb.</p>,
     <p>"I know that," Jonny Land said, as his blue eyes swept them. "But it
     will take fourteen or fifteen hours before he gets that report back.
     Before that time ends, we've got to be on our way to the Sun!"</p>,
     <p>Laird Carlin felt a shock of astonishment, but before he could comment,
     Jonny was speaking swiftly on.</p>,
     <p>"It's our only chance now—to get away before Floring receives the
     proof that will authorize him to stop us! The dredge here is almost
     finished. If we can install it in the 'Phoenix' and take off tonight,
     we'll have our chance to prove to the galaxy that Sun-mining can be
     safe."</p>,
     <p>"Install the dredge tonight?" cried Harb Land. The gangling giant's
     face was sick with anxiety. "Jonny, we can't do it! Not that soon."</p>,
     <p>"We've got to!" Jonny's voice cut like a steel rapier. "Harb, you go
     get Loesser and Vito and the other boys. Have them bring the big truck
     with them. If we work hard enough, we should be able to have the dredge
     ready to roll by dark. Once we get it into the 'Phoenix', we can take
     off and complete installation in space."</p>,
     <p>"You can't do it," groaned his brother. "You know you figured on taking
     a week yet for that installation."</p>,
     <p>Carlin stepped forward. He had long ago reached his decision. He had
     reached it in that moment when he had answered Floring.</p>,
     <p>"I'm a CE, you know," he reminded. "I can help a lot in that
     installation."</p>,
     <p>Marn stared at him, amazement and dawning gladness in her eyes. And
     Harb Land's tortured face turned haggardly on Carlin.</p>,
     <p>"You'd do that? You'd help us? By heaven, if you would, we might make
     it!"</p>,
     <p>Jonny's brilliant blue eyes bored Carlin's face.</p>,
     <p>"Carlin, I was hoping for this. I knew from the first I'd need another
     engineer's help in installing and operating the dredge. I brought you
     home because I was hoping I could enlist your aid before we started on
     the expedition. But all the same, I've got to warn you. We're directly
     bucking a Control Council order. You can lose your certificate and go
     to Rigel prison, even if our plan succeeds. And if it doesn't succeed,
     it may mean perishing with us. And after all, Earth isn't your world."</p>,
     <p>"Who the devil is doing anything for Earth?" Carlin retorted. "This old
     planet of yours means nothing to me either way."</p>,
     <p>"Laird, are you so sure of that?" Marn asked him, her eyes very bright.</p>,
     <p>"Do we have to get emotional?" Carlin asked roughly. "I'm an engineer,
     and this is the biggest engineering experiment to be tried for
     centuries. Don't you think I want to be in on it?" He added crushingly,
     "And as for my getting mixed up in the blame, I'm already blasted well
     mixed in it. When I denied to Floring that this was a magnetic dredge,
     I implicated myself right there in the whole business. I've got to make
     it succeed, now."</p>,
     <p>Harb Land was already running toward his truck. Jonny shot sharp orders
     at his sister.</p>,
     <p>"Marn, I want you and Gramp to watch the road this afternoon. Floring
     might come back. Carlin, you and I haven't a moment to lose."</p>,
     <p>Carlin strode after the limping youngster into the workshop, and Jonny
     there rapidly explained what remained to be done.</p>,
     <p>"The kickback feed-pipes to the beam-head have to be hooked up, the
     cooling coils to solidify the copper are not yet in place, and the
     whole dredge has to be fastened in its frame so it'll be ready to swing
     aboard the truck tonight."</p>,
     <p>Carlin was appalled by the amount of work that remained, for two pairs
     of hands. But Jonny added an encouraging qualification.</p>,
     <p>"Loesser and Harb and the others can help in the ato-welding and cable
     work if we set it up for them. They're all veteran spacemen and know
     how to handle ordinary tools."</p>,
     <p>Carlin plunged into the work with Jonny. But as they toiled to set up
     the coils and feed-pipes of the massive mechanism, an inward aghastness
     at what he was doing oppressed Carlin's mind.</p>,
     <p>Why was he doing it, breaking Control law and endangering his
     certificate and even his liberty? Why under heaven should he be sharing
     the risks of these men for a planet he hadn't even seen until a few
     weeks ago?</p>,
     <p>"I must still be star-sick, unstable," he thought dismally. "Or I'd
     never have got mixed up in this mad business. Sun-mining!"</p>,
     <p>Blind reaction was dominating him. Curse it, he wasn't the type to
     join Quixotic forlorn hopes. He was Laird Carlin, sober, hard-working
     engineer, who ought right now to be far across the galaxy at the job to
     which he belonged.</p>,
     <p>And all the time Carlin's mind spun miserably to this whirl of
     self-reproach and foreboding, he was working with Jonny at topmost
     speed, squeezing into the frame of the great dredge where the lame
     youngster could not go, fastening Veer-clamps, hooking self-sealing
     leads to the flat Markheim filters.</p>,
     <p>The sound of ato-trucks rocked the noon air, and Harb Land came running
     heavily into the workshop.</p>,
     <p>"I got the others—Loesser's bringing in the big truck now," panted
     Harb. "What do you want us to do, Jonny?"</p>,
     <p>Loesser, and Vito, and the other four young Earthmen who came hastening
     after Harb were dominated by excitement. Loesser's broad red face was
     shining with emotion as he came up to Carlin.</p>,
     <p>"I want to apologize. I never thought any star-world stranger would
     come in with us and help us."</p>,
     <p>"Save it, and get the welders on those rear feed-pipes," Carlin
     retorted. "Get in here—I'll show you."</p>,
     <p>Through the hot afternoon hours, the hiss of ato-welders and reek of
     fusing metal stifled the workshop.</p>,
     <p>Dripping with perspiration, stiff from cramped postures, Carlin worked
     on inside the great dredge.</p>,
     <p>And all those hours, in rhythm with the welders' hiss and the clang of
     wrenches, his thoughts beat a mocking tempo through his brain.</p>,
     <p>"All this, for no reason! For somebody else's world, a world that ought
     to have been evacuated long ago! Even if it succeeds, you win nothing.
     And if it fails, the Sun licks you all up like midges."</p>,
     <p>Yet he labored blindly on. It might be crazy, but what he had started,
     he would finish.</p>,
     <p>It was work against an inexorable time limit that rapidly was
     approaching. As the shadows lengthened, as the sun went down, they
     still had not finished.</p>,
     <p>Jonny Land limped unsteadily to turn on the workshop lights. His face
     was a gray mask of fatigue and sweat as he turned to the others.</p>,
     <p>"Two more hours," he said huskily. "We can't take more, if we're to get
     the dredge into the 'Phoenix' and take off before midnight."</p>,
     <p>Those two hours, afterward, seemed weeks in length to Carlin. And the
     mocking devil in his brain kept taunting, "It's no business of yours,
     you know!"</p>,
     <p>"That's near enough!" Jonny's hoarse voice finally declared. "We can
     hook up those last cables on the way. All the work that require heavy
     tools is done—and we daren't take more time."</p>,
     <p>They were, all of them, drunk with fatigue, staggering with the furious
     drive of twelve hours of unbroken toil. Blackened by welder flare,
     glistening with sweat, they looked to Carlin like a crew of devils.</p>,
     <p>Jonny's driving energy remained unconquerable.</p>,
     <p>"Marn," he ordered, "back the big truck in here. Harb, you and Carlin
     rig the hoist."</p>,
     <p>The big, flat-bodied ato-truck backed ponderously into the workshop
     and they swung the massive magnetic dredge carefully aboard. Loesser
     and the others then hastily chained it to the bed of the truck.</p>,
     <p>Jonny limped toward the cab. "All right, we're starting. Harb, you
     drive. No, Marn—you're not going to the spaceport with us."</p>,
     <p>Marn, face white and eyes big with fear, saw the gleam of the
     atom-pistol that Harb was thrusting into his pocket.</p>,
     <p>"Oh, Jonny, not that, no matter what happens!"</p>,
     <p>Jonny's blue eyes flashed arctic light. "That, or anything, now," he
     rasped. "You know what this means to our people, Marn."</p>,
     <p>Then his face softened, and he patted her arm.</p>,
     <p>Tears streaked her cheeks as she kissed and clung to him, and then to
     Harb.</p>,
     <p>Carlin was climbing heavily onto the truck when he felt her touch on
     his arm.</p>,
     <p>"You too, Laird," she whispered, quivering lips blindly pressing his
     cheek. "All of you must come back."</p>,
     <p>"Get on!" cried Harb Land, and then the truck went into gear.</p>,
     <p>Carlin jumped for the cab, and under the starry night they were rolling
     at increasing speed down the twisting road toward the valley.</p>,
     <p>And suddenly all the nightmare mocking in Carlin's brain was gone and
     there was only the rush of sweet air against his face, and the splash
     of the lamps ahead, and the jolt and rumble of the big machine as they
     raced down toward the spaceport's distant beacons.</p>,
     <p>Earth air and Earth smells in Carlin's nostrils, sleepy Earth sounds
     in his ears; the shine of the old spaceport's beacons, and the soaring
     loom of the distant tower that marked the spot where a man of long ago
     had first dared space. This world, this little Earth, was worth risking
     death for, even for a stranger from far stars!</p>,
     <p>He knew he was a little crazy, he still had a corner of his mind that
     told him all this was mere intoxication of emotion which was sweeping
     away reason. But the mocking devil in Carlin's mind was gone, and he
     was one in mind and purpose with his companions, now.</p>,
     <p>The others too were feeling that wild reaction, for Loesser clapped
     Carlin's shoulder, crying:</p>,
     <p>"It's like getting out of prison to get started!"</p>,
     <p>"We're not off Earth yet!" warned Jonny. "Cut the lights and drive
     around to the north end of the spaceport, Harb. Ease the truck to the
     'Phoenix' as quietly as you can." A little later he warned, "Slower,
     slower. Keep to the edge of the tarmac."</p>,
     <p>Lightless, its motors a mere low rumble, the big truck crept around the
     dark edge of the spaceport toward the "Phoenix." The little planet-ship
     took black shape in the darkness, a low, torpedo bulk brooding beneath
     the stars. Harb backed the truck toward its side, as they jumped out of
     the cab.</p>,
     <p>Light flashed on them from a hand-krypton in the door of the "Phoenix!"
     A lean, uniformed figure stood there, gun in hand, looking at them.</p>,
     <p>"I thought you would be coming," said Ross Floring quietly. "Jonny, I'm
     sorry about this."</p>,
     <p>Carlin was as frozen as his companions, by the disastrous overturn of
     their attempt at secrecy. Floring stepped out of the ship.</p>,
     <p>"I've been looking through your ship while I waited," he said. "You
     have triple as much heat-screen coverage as you'd need for the Hot Side
     of Mercury. You were going to the Sun."</p>,
     <p>"You can't prove it, Ross," Jonny said levelly. "You've no proof."</p>,
     <p>"I've enough to prohibit this ship from clearing Earth until
     investigation," Floring replied. "A certain report will reach me from
     Canopus by morning. Then we'll see."</p>,
     <p>Carlin saw it then, saw the dark giant figure of Harb Land stealing
     around the truck and looming up behind Floring. He glimpsed the gleam
     of Harb's raised atom-pistol.</p>,
     <p>Then Harb struck. The butt of the weapon came down on Floring's head
     and the officer crumpled limply to the tarmac.</p>,
     <p>"See if anyone else is in the ship!" Jonny said swiftly. "Loesser,
     watch the Control station!"</p>,
     <p>Then he bent with Carlin over the unconscious man.</p>,
     <p>"We'll have to take him with us," Jonny said. "If we leave him here
     he'd soon be found, then the Control cruisers would be after us."</p>,
     <p>A few weeks before, Laird Carlin would have been aghast at seeing
     a semi-sacred officer of Control Operations struck down. With what
     spirit of reckless defiance of law had his companions infected him? He
     marveled at himself as he coolly picked up the limp figure.</p>,
     <p>"Tie him into one of the chairs in the pilot room," Jonny was saying.</p>,
     <p>Harb came plunging out of the ship. "Nobody else aboard. He came over
     here alone."</p>,
     <p>By the time Carlin had the unconscious man secured in the pilot room,
     Harb and the others had slid open the big hatch in the side of the
     "Phoenix." Hastily, fumbling in darkness, they ran out the ship hoist
     and hooked onto the big magnetic dredge.</p>,
     <p>Then, with infinite labor, they swung the massive mechanism into the
     hold amidships. Mere short flashes of hand lamps had to suffice to
     guide the beam-head of the dredge down into the round keel opening.</p>,
     <p>"Fasten half the frame bolts—they'll hold till we get into space,"
     panted Jonny.</p>,
     <p>Carlin skinned his knuckles in the dark, fumbling with bolts and
     wrench. Every instant he expected to hear an alarm from Loesser that
     Control officers were coming.</p>,
     <p>"That'll have to hold," said the sweating Jonny. "Run the truck off the
     tarmac. Harb, make ready for take-off!"</p>,
     <p class="ph1">CHAPTER VIII</p>,
     <p class="ph1"><i>Solar Struggle</i></p>,
     <p>Oxygenators started throbbing, doors clanged, as the others tumbled
     aboard. Harb Land, smeared with dirt and oil, his shock of hair wild,
     climbed into the pilot seat and expertly touched controls.</p>,
     <p>"Generators coming on!" sang Loesser's breathless voice from the
     interphone, as the low, deep hum began.</p>,
     <p>"Stasis on," said Harb rapidly, his fingers busy. The blue cushion of
     force was around them as Carlin slumped drunkenly into a seat. "Zero,
     two and five acceleration schedule. Here we go!"</p>,
     <p>And the "Phoenix" swept up with a rush from the spaceport, the
     propulsion-waves streaming from its drive-plates hurling it out and
     upward into the star-sown sky, the spaceport lamps and the southward
     blinking lights of New York falling swiftly away.</p>,
     <p>"Authorization!" yelped a startled voice from the universal communic on
     the panel. "Give authorization for take-off!"</p>,
     <p>"Authorization already given," Harb Land rapped back, then cut the
     communic. He laughed. "That'll puzzle them a while."</p>,
     <p>Crazy, reckless, suicidal, to Carlin seemed the way that Harb was
     taking them out from Earth. The atmosphere of the planet had no sooner
     started a shrill, rising scream around them than it fell and faded as
     they came out of the envelope of air.</p>,
     <p>Luna burst up out of the eastern heavens like a great globe of dull
     gold against the stars. And then Carlin's eyes were smitten by the
     flare and glare of the brilliant disk of Sol, of the Sun.</p>,
     <p>And then the "Phoenix" lined out and was plunging headlong through the
     void at a speed that Carlin knew was flatly illegal to use inside any
     System, a rush toward that distant Sun flare.</p>,
     <p>"Cut down, cut down!" cried Jonny to his brother. "Any more speed and
     you'll not be able to decelerate in time to orbit around the Sun."</p>,
     <p>Harb Land turned a wild, dirty face aflame with emotion. "By heaven,
     we're on our way at last! We'll show them now that Earthmen can still
     blaze a space-trail nobody else has dared!"</p>,
     <p>And from back amidships came a hoarse voice jubilantly singing the old
     Earth space-song:</p>,
     <p>Jonny Land's voice lashed them, his thin face dripping and determined.</p>,
     <p>"You're all of you blowing your tops with excitement. This hasn't even
     started yet. Look at what we're heading for!"</p>,
     <p>Carlin heard the others fall silent and himself felt a chill of awe as
     he looked ahead at the giant fire orb toward which the "Phoenix" was
     plunging.</p>,
     <p>"We'll be orbiting before we have the dredge set up, unless we hurry,"
     Jonny prodded. "Come on, help me with it."</p>,
     <p>The big magnetic dredge had to be bolted into place, the coils and
     pipes had to be hooked to their connections inside the ship, the cables
     to the generators, the cooling coils to the compressor, the outlets of
     the Markheim filters to the bunkers astern.</p>,
     <p>Thrumming, creaking, shivering in every strut to the blind thrust of
     power that was hurling it on, the "Phoenix" rocked and shook about them
     as Carlin labored with Jonny and two of the other men to make those
     last connections. The cramped space in the hold around the dredge was
     hot, stifling, for the oxygenators couldn't keep the air there pure.</p>,
     <p>"All ready!" Jonny called finally, after eternal-seeming hours of toil.
     "And none too soon. We're getting there fast. Harb has put out most of
     the heat-screens."</p>,
     <p>Through the windows, the ship seemed enveloped by a halo of dim light,
     the force-screens that repelled radiations of heat.</p>,
     <p>But when Carlin stumbled with Jonny into the pilot room, they were half
     blinded even through the screens by the fierce, blazing glare from
     ahead.</p>,
     <p>Half the sky ahead was Sun, a gigantic abyss of roaring flame that
     crushed the mind by its magnitude. All directions of space seemed
     canceled, and they were falling, falling, into an inferno of fire.</p>,
     <p>Harb turned a sweating face. "We'll cut off to orbit in less than an
     hour," he informed.</p>,
     <p>Ross Floring spoke from the chair in which he was tied, and in which he
     had come back into consciousness.</p>,
     <p>"Jonny, I've been waiting for you! Harb wouldn't listen to me. You've
     got to turn back!"</p>,
     <p>Jonny shook his head. "No use, Ross, I know you're only doing your
     duty. And I'm sorry to drag you into this danger. But we're not
     stopping now."</p>,
     <p>"But you'll never get there!" Floring exclaimed. "Control cruisers must
     already be after you. They'll have found out where I am by now."</p>,
     <p>"Empty threats!" Harb jeered. "They can't know where he is."</p>,
     <p>"Jonny, look at my badge!" cried Floring. "See the tiny radio bulb in
     the back of it? It's a 'finder' by which any Control officer can be
     located at any distance. When I didn't report back, they'd use it to
     spot me out here."</p>,
     <p>"If that's true," said Jonny Land, his thin face suddenly haggard,
     "they'll be after us by now. Harb, cut the communic back in!"</p>,
     <p>Harb obeyed. Roar of static from the gigantic orb ahead was a dull
     background to the sharp voice that came from the instrument.</p>,
     <p>"Control Operations squadron four hundred thirty-three nine calling
     'Phoenix!' Last warning! We are overhauling you and will shell you
     unless you turn and surrender."</p>,
     <p>Startled, Harb Land jabbed a button and twisted the knob of the
     visor-screen. The far-seeing eye quartered space behind them, and then
     the black space scene held steady. There against the stars came a
     little pattern of four tiny triangles of light. Triangles—galaxy-wide
     sign of Control.</p>,
     <p>"By heaven, they actually have come after us!" cried Harb. "Jonny,
     they're only minutes behind us and pulling up fast!"</p>,
     <p>"We broadside as soon as we range you unless you turn now," warned the
     steely voice from the communic.</p>,
     <p>Laird Carlin, only a few weeks before, would no more have dreamed of
     disobeying a Control Operations command than he would have of picking
     stars from the sky. Galaxy citizens were trained to revere the great
     organization that had made the Universe a place of law and order.</p>,
     <p>But the ancient independence of these men of Earth was strong in him
     now. They had already risked so much, had incurred certain penalty even
     if they now surrendered.</p>,
     <p>"Keep going!" Carlin exclaimed. "They can't follow us once you start
     orbiting close to the Sun's photosphere. No ordinary Control cruiser
     has heavy enough heat-screens to follow us into that!"</p>,
     <p>"By Jupiter, it's so!" exclaimed Harb, faint hope lighting his face.
     "But I daren't crowd on more speed now. I've got to start decelerating
     if we're to orbit correctly."</p>,
     <p>"Decelerate by plan," Jonny said grimly. "They may not range us in
     time. We'll soon know."</p>,
     <p>The "Phoenix," flying at a tangent toward the gigantic sphere of the
     Sun, was aiming to swing into an orbit around Sol as close as possible
     to its photosphere or gaseous surface.</p>,
     <p>It had to be so. No ship would ever have power enough to go that close
     to the Sun's colossal pull and hold its position by its own energy. To
     get that close and to stay that close to Sol without being drawn in to
     it, a ship had to go into an orbit around it like a tiny satellite.</p>,
     <p>The air in the "Phoenix" was already stifling hot. Jonny switched in
     another of the heat-screens, and the dim halo around the flying ship
     deepened.</p>,
     <p>Harb's fingers were flashing over the controls, decelerating, steering
     the ship in a closing spiral toward the Sun.</p>,
     <p>"Carlin, talk them out of this madness!" cried Ross Floring, aghast.
     "The cruisers will be broadsiding us in moments."</p>,
     <p>Carlin paid no attention. His eyes were on the visor-screen where the
     four cruisers now loomed big as they came closer.</p>,
     <p>Then it came. Silent, deadly, four blinding gouts of flame burst near
     the "Phoenix." Four salvos of atomic shells whose wave of force rocked
     the plunging ship. Loesser came tumbling into the pilot room, red face
     glistening.</p>,
     <p>"They'll bracket us next salvo or two!" he yelled. "What's our chance?"</p>,
     <p>"Turn on heat-screens Six and Seven!" roared Harb Land, without looking
     around. "I'm going into orbit now!"</p>,
     <p>"It's too soon!" Jonny cried warning. "It's—"</p>,
     <p>Carlin saw that Harb hadn't even heard. The giant was recklessly
     cutting the elements of their plotted course, depending on their own
     power to pull into orbit in time.</p>,
     <p>The heat-screens, all they had, were on full now. Another salvo burst
     to spaceward of them. Carlin knew the men behind realized Floring was
     aboard. But Control Operations would sacrifice any men to prevent the
     Sun-mining that always before had meant disastrous solar disturbances.</p>,
     <p>"Great blazing stars!" breathed Loesser, staring. "Look at that!"</p>,
     <p>Forgotten, the deadly shells that were groping for them. For now the
     "Phoenix" was deep in the awesome corona of the star and was curving in
     closer through heat that was over two thousand degrees.</p>,
     <p>Carlin's mind shook to the fearful spectacle that was the firmament.
     Not he, nor any other living man, had ever come so close to a star.
     They were entering a region of such violent energies that all laws of
     space and time here seemed cancelled.</p>,
     <p>Blinding, eye-dazing even through the strong protective filter of the
     heat-screens, the brilliance of Sol stunned them. They looked on a
     vast, raging ocean of flaming gases, a sea of vaporized metallic and
     non-metallic elements that was like a cosmic furnace.</p>,
     <p>Even through the heat-screens, the radiance heated the air in the ship
     scorchingly. But now the visor-screen showed that the Control cruisers
     were falling back and disappearing from sight behind.</p>,
     <p>Blinding, eye-dazing even through the filter of the heat-screens, the brilliance of Sol stunned them.</p>,
     <p>"They couldn't follow us this close to the photosphere!" Harb cried
     exultantly. "We've shaken them and we're almost in orbit."</p>,
     <p>"You can't orbit the Sun!" Floring pleaded. "And even if you could, the
     cruisers will lay to outside the heat and range you by locator and fire
     till they destroy us! Put about!"</p>,
     <p>The man Vito, choking and gasping for breath, came into the pilot room
     from the engine rooms astern.</p>,
     <p>"Heat-screens won't take another dyne! If we go closer, we're done for."</p>,
     <p>"We're orbiting now," Jonny said huskily. "Wait!"</p>,
     <p>Harb Land was engaged in the most difficult operation of spacemanship,
     bringing a ship into exact balanced orbit around a celestial body.</p>,
     <p>Most difficult, even when the body was a planet. Impossible, nearly,
     when the body was a Titanic star!</p>,
     <p>Carlin saw the giant's face a frozen mask as he centered his dial
     needles, fed force with infinite delicacy, guided, changed—and changed
     again.</p>,
     <p>Harb reached and slammed open a switch. The hum of propulsion waves
     died. The "Phoenix" was without driving power. And the needle of the
     gravi-gauges remained constant, the ship's path around the Sun was
     unvarying.</p>,
     <p>"We've orbited!" Harb Land's voice was a hoarse, exhausted sound.</p>,
     <p>Carlin wanted to shout, "By heaven, there are no spacemen in the galaxy
     except Earthmen—none!"</p>,
     <p>The "Phoenix" was circling the Sun, deep in the corona and reversing
     layer and close to the photosphere or light-emitting surface which was
     the vague boundary of the star itself.</p>,
     <p>Their sensation was that of men suspended over a Universe of raging
     flame and force. The mind shook to the impact of it. They were here
     where no men, no life, had ever been intended to be. They were
     violating the sanctity of a star.</p>,
     <p>"Now—the dredge," Jonny said hoarsely. "We've not power enough to
     force the heat-screens like this for long. Come on, Carlin."</p>,
     <p>Carlin stumbled back with him into the stifling hold. The men around
     the towering magnetic dredge were like sooty devils staring with wild
     eyes.</p>,
     <p>The metal was so hot its touch made him cry out as he closed the
     circuit of the generators with the ato-turbines. The rotors began their
     whine, building up a magnetic field.</p>,
     <p>The whole ship suddenly shook and quivered. Harb came plunging back
     into the hold.</p>,
     <p>"Those Control Cruisers are starting to salvo us by radiolocator!"</p>,
     <p>"We only need a little time," panted Jonny Land. "The cooler coils,
     Carlin!"</p>,
     <p>Carlin felt like a man in a dream as he sweated with Jonny to get the
     magnetic dredge started. The field was building steadily, and the great
     nozzles of the beam-head had been lowered below the keel. Jonny's
     brilliant eyes clung to the panel of gauges, and finally he opened the
     field-switch.</p>,
     <p>"Now!"</p>,
     <p>They crowded around the view-plate in the keel, peering half-blindly
     down against the glare of the raging Sun-sea below. The dredge was
     projecting a powerful, concentrated magnetic field down into that ocean
     of flaming gas like a sucking straw. But for moments they saw nothing.
     Time that seemed endless went by. Then—</p>,
     <p>"Here she comes!" yelled Loesser.</p>,
     <p>A column of flaming vapor was shooting up from the fiery ocean below.
     Compared to the gigantic mass of Sol, it was the merest filament, the
     flimsiest thread of fire.</p>,
     <p>But it was rushing up and up toward the hovering "Phoenix," a finger
     of fiery vaporized elements drawn irresistibly up along the beam of
     magnetism to the ship.</p>,
     <p>Another salvo of shells went off in space somewhere close by and rocked
     the ship with its wave of force. But next instant came a heavier
     impact, as the fiery column of gas reached the nozzles below the ship.</p>,
     <p>They heard a deafening roar. That up-sucked stream of vaporized
     elements was being drawn through the heat-proof nozzles and intakes,
     through the Markheim filters that screened out its copper atoms, and
     was then being shot downward again by the kickback's negative field.</p>,
     <p>"The kickback's working!" Jonny Land yelled. "If the effect of it is
     what we calculated, we've done it!"</p>,
     <p class="ph1">CHAPTER IX</p>,
     <p class="ph1"><i>An Earthman Comes Home</i></p>,
     <p>For the moment, none of them paid any attention to the fact that
     precious copper was solidifying in the cooler coils into granules of
     metal that were being blown into the bunkers. The real test was what
     their beam of magnetic force was doing to the surface of the Sun.</p>,
     <p>Did it seem incredible, as it almost did to Carlin, that such a
     fragile finger of force could in the least disturb the mighty orb
     below? He knew better. He knew the unnaturally delicate balance of a
     star's surface, which a slight change of pressure artificially induced
     could stir into a whirl that would expand in giant Sun-spots. If that
     happened, it would mean chaos.</p>,
     <p>"No sign of a whirl yet," Jonny breathed, peering down through black
     glare-proof lenses. "No sign at all."</p>,
     <p>There was no moment of crisis, no clean-cut moment of triumph. There
     was just the time speeding by, the flow of copper into the ship, and
     the constant reports of Jonny—"No whirl forming yet."</p>,
     <p>Salvos shook the ship as the Control cruisers far outside the sun
     glare fired more and more accurately. But they went unheeded. Success
     or failure of the most audacious engineering exploit in the galaxy's
     history hinged upon Jonny's muttered reports.</p>,
     <p>"No whirl yet."</p>,
     <p>Jonny Land finally raised his head, looked at them as they stood with
     wild surmise on their faces.</p>,
     <p>"We've done it," he said, almost unbelievingly. "We've nearly filled
     the bunkers with copper and there's no whirl down there, no disturbance
     to grow into a spot. We've made Sun-mining possible."</p>,
     <p>Tears were running down Loesser's face. Harb Land looked dazed. But
     Jonny walked across the hold to the wall through which the cooler coils
     fed into the bunkers. He peered through a quartz view-plate.</p>,
     <p>They looked with him. The bunker rooms were heaped high with shining
     red granules. Copper, virgin-pure, blown into the rooms and already
     almost filling them. Copper milked from the Sun!</p>,
     <p>"Copper for Earth!" whispered Jonny, his thin face blazing now. "Power,
     and new life, for the old planet!"</p>,
     <p>The "Phoenix" rocked wildly and metal screeched rendingly as they were
     flung from their feet by a salvo that had finally bracketed the ship.</p>,
     <p>"The feed-pipes!" screeched Loesser, scrambling to his feet beside
     Carlin.</p>,
     <p>Carlin saw. The ship's walls had held, but the shock had snapped
     strained cables and cooler coils. Two intake tubes were giving way,
     white-hot copper vapor forcing out through cracks in them.</p>,
     <p>"Veer-clamps on those two pipes!" yelled Jonny. "If they give,
     everything goes!"</p>,
     <p>Knowledge of what it meant if the pipes gave way, if super-heated
     metallic vapor blew out into the hold, flung Carlin in a crazy rush for
     the Veer-clamps and wrenches.</p>,
     <p>He got a clamp around one of the pipes, and the man Vito started
     spinning shut the bolts that would hold the fracture tightly. He swung
     round toward the other pipe.</p>,
     <p>"Clamp!" yelled Jonny Land, in a cry that was like a hoarse howl of
     agony.</p>,
     <p>Carlin's blood left his heart as he glimpsed the most horrible and
     heroic sight he had ever beheld. The other strained tube had been
     about to blow open, and Jonny Land had flung his arms around it and
     was holding it together by agonized effort while the white-hot vapor
     sprayed his body.</p>,
     <p>Harb Land wildly snatched his brother away as Carlin flung the big
     clamp around the pipe and convulsively spun its bolts shut.</p>,
     <p>He staggered around then. Harb was bending over his brother.</p>,
     <p>"Jonny! Jonny!"</p>,
     <p>Jonny's whole chest and neck were blackened and blasted. His face was a
     ghastly, sooted mask as his eyes looked up at them.</p>,
     <p>Another salvo went off close by, and again the "Phoenix" rocked wildly.</p>,
     <p>"Cut the dredge!" Carlin cried. "We've proved the process is
     successful, and we can't stay here now or your brother will die!"</p>,
     <p>Loesser cut off the dredge and Harb Land rushed for the pilot room.
     Carlin heard him shouting there into the communic:</p>,
     <p>"Control cruisers from 'Phoenix!' We're putting out to surrender. Be
     ready to give injured man medical treatment."</p>,
     <p>"Break out of your orbit at once and we'll contact you for surrender by
     locator when you're outside the corona," came the sharp, fast answer.</p>,
     <p>The generators of the "Phoenix" started roaring their shrillest note as
     Harb Land frantically flung power into the drive-plates. Beneath the
     thrust of its propulsion vibrations the battered ship began to move, to
     fight its way out of the gigantic pull of Sol, breaking slowly out in a
     tangent off its orbit.</p>,
     <p>Carlin, Loesser, all of them in the hold, were bending over Jonny Land
     when Floring, released by Harb, came back. The officer looked down and
     then shook his head somberly.</p>,
     <p>"No chance," he said. "He won't even last until we reach the cruisers."</p>,
     <p>Jonny was lying, unhearing, fighting for breath, looking up at them
     without seeing them, his sooted face a writhing mask. Carlin felt tears
     sting his eyes, and saw everything through a blur.</p>,
     <p>"Jonny, we did it—you did it!" Loesser was choking. "Made Sun-mining
     possible! Why, soon now there'll be scores of ships, new, big ships,
     coming here and getting all the copper Earth needs!"</p>,
     <p>He was, Carlin knew, trying to reach home to the dimming mind with that
     reassurance, that assurance that the dying man had not given away life
     in vain.</p>,
     <p>It didn't reach Jonny Land. He wasn't Jonny Land any longer, he was
     just a living creature dying in pain, and he couldn't feel or know
     anything but pain. And then the pain went, and life went with it, and
     his face was a lax, empty mask that had no meaning for them.</p>,
     <p>Loesser sobbed: "He didn't know—he didn't know what I was saying!"</p>,
     <p>Carlin felt dull, tired, drained of emotion. He had just seen the only
     hero he had ever known die, but a hero's death was just death, just
     mortal pang and final release.</p>,
     <p>He went forward to the pilot room.</p>,
     <p>"Jonny's dead," he said to Harb Land.</p>,
     <p>Harb's shoulders sagged, but he did not turn as he guided the "Phoenix"
     on spaceward to where the grim Control cruisers waited.</p>,
     <p>Control Court here in New York was only a small room in the building
     by the spaceport. There were no officials in it except the three
     middle-aged judges who sat behind a small table and prepared to pass
     sentence on Laird Carlin and his seven comrades.</p>,
     <p>There were no lawyers, no oratory, no jurymen. They were not needed.
     The government psychologists who had quietly questioned the accused men
     during their four days in prison had submitted the factual hypnosis
     records which were complete and incontrovertible evidence.</p>,
     <p>The chief judge, the man in the middle, quietly read the decision as
     Carlin and the others faced him.</p>,
     <p>"This court is placed in a peculiarly difficult position in assessing
     your offense. On the one hand, you men deliberately broke a Control
     Council regulation and defied its officers. On the other hand, your
     action has proved the practicability of a process of Sun-mining which
     will be of incalculable value to this and every other System in the
     galaxy.</p>,
     <p>"To forgive your offense because the ultimate result was good would be
     to set a fatal precedent. It would establish the principle that illegal
     means do not matter if end-purposes are good. We cannot permit such a
     precedent to be established. Therefore, regretfully, this court must
     pass the prescribed punishment for your offense."</p>,
     <p>Carlin could not deny the crystalline logic. He had known from the
     first that this must be the issue, and he was too tired to care.</p>,
     <p>"You are sentenced to two years imprisonment in Rigel Prison and
     also to the loss of your spacemen's licenses or Cosmic Engineer's
     certificate, whichever you hold. Such sentence is obligatory in this
     case." He added quickly, "It is, however, within our discretion to
     suspend the prison term and to limit cancellation of your certificates
     to one year from date. Such is the sentence of this court."</p>,
     <p>Loesser drew a gusty breath of relief. "For a minute, I thought it was
     Rigel for us sure enough!"</p>,
     <p>The chief judge had risen. "Speaking personally," he added quietly, "we
     would like to congratulate you men upon a great achievement."</p>,
     <p>Ross Floring came to their side.</p>,
     <p>"A year's suspension isn't long," he said, and Carlin nodded wearily.</p>,
     <p>When, with Harb Land's giant figure leading them, they emerged from the
     building into the sunlight, a roar that deafened them came from the
     waiting crowd outside. The people of Earth, at least, had no need to
     temper their gratitude.</p>,
     <p>Harb was grimly silent as he pushed through the crowd toward Marn and
     old Gramp Land. Carlin found himself buffeted by eager hands, assailed
     by joyful faces and voices, as he followed.</p>,
     <p>A grizzled, excited man clapped his shoulder. "We Earthmen showed 'em
     we could still conquer space, didn't we?"</p>,
     <p>We Earthmen? Somehow, for the first time in all these days, Carlin's
     dulled mind felt a stir of pride as though at an accolade.</p>,
     <p>He didn't like to meet Marn's pale face. But she spoke steadily.</p>,
     <p>"It's all right, Laird, about Jonny. Women of Earth for two thousand
     years have seen their men go out into space—and not all come back."</p>,
     <p>Floring had followed them. "I want you to see something," he said.</p>,
     <p>He led the way toward the towering Monument of the Space-Pioneers.
     Carlin looked at the roll of names. Then his eyes suddenly blurred as
     he saw that, for the first time in several centuries, a new name had
     been added to the bottom of that great roll.</p>,
     <p class="ph1">JON LAND</p>,
     <p>Marn's eyes were shining. And her giant brother looked long, with
     haggard face somehow comforted. But old Gramp Land turned sadly away.</p>,
     <p>"A name on a stone is poor exchange for my boy," he muttered. "I'm
     gettin' old."</p>,
     <p>That evening, in the old house up on the ridge, they were subdued and
     silent at dinner. The table was too big, and they looked around too
     often as if listening for a familiar limping step and a cheerful voice.</p>,
     <p>Carlin was doubly oppressed because of the thing that he had not yet
     told them. He hated, somehow, to break the news.</p>,
     <p>"There's something they found out when they made our psycho-records for
     the trial," he said finally. "Mine showed that I had no instability of
     coordination, no star-sickness any longer."</p>,
     <p>"You mean, you're cured?" said Harb, surprised. "Why, that's fine. I
     never thought of it, but you made the trip Sunward all right, so I
     should have known."</p>,
     <p>"The psychos say," Carlin told them, "that some people out in the
     galaxy now and then approximate much closer to the original Earth stock
     than the average. Such people respond rapidly to Earth-treatment. I'm
     one of them, it seems." He added uncomfortably, "I can go back home to
     Canopus now, though I'll have to work at a desk job for a year. The
     only thing is that there's a ship for Canopus tonight, and there won't
     be another for weeks."</p>,
     <p>"You're not going tonight?" exclaimed Harb. "Not as soon as that?"</p>,
     <p>Carlin felt a little heartsick. "I wish I didn't have to, so soon. But
     there's nothing for me to do here now that I'm all okay."</p>,
     <p>He had somehow expected Marn to protest too. But she did not. She only
     said quietly:</p>,
     <p>"I'll drive you down to the spaceport."</p>,
     <p>"I think I'd rather walk down," Carlin said slowly. "I don't know why,
     but I would. It's not far and I sent my bags on down."</p>,
     <p>"Then I'll walk a little of the way with you," said Marn.</p>,
     <p>Twilight had changed into soft summer darkness by the time Carlin had
     exchanged a last old-fashioned hand grip with Harb and Gramp Land, and
     started down the road with Marn.</p>,
     <p>She went only around the first turn of the old road with him, and then
     stopped.</p>,
     <p>"Good-by, Marn," he said, but she only averted her face.</p>,
     <p>Carlin hesitated, then turned and walked on. Luna was lifting its
     shining shield in the east, and the silver summer silence lay over
     everything, hardly broken by the stir of branches and the low buzz of
     insects. The night was warm and still.</p>,
     <p>He had a lump in his throat and he tried to laugh at himself because he
     had it. A man couldn't let illogical emotions overrule his reason. This
     crazy, heroic old planet Earth and its people—he would never forget
     them, but he had to return to his own life and work, he had to go home.</p>,
     <p>Laird Carlin suddenly stopped. He knew, abruptly, why dull oppression
     had gnawed his mind all day. It wasn't because he was going home. It
     was because he was leaving home. He was leaving the only place where
     his spirit had ever found something it had always lacked, a peace, an
     ancient certitude, a kinship that had grown and grown.</p>,
     <p>Carlin turned and strode rapidly back up the road. Not until he was
     almost upon her did he perceive that Marn Land was still standing in
     the silvered road where he had left her.</p>,
     <p>"I was waiting for you," she said simply. "I knew you wouldn't go."</p>,
     <p>His hands grasped her shoulders as he spoke in a rush.</p>,
     <p>"Marn, I couldn't! I thought of Canopus, I thought of friends there and
     a girl who likes me and the garden cities I used to love, and it was
     all unreal, I'm tied somehow to this queer old planet, to Jonny and
     Harb and all of the others, and to you!"</p>,
     <p>She came into his arms quietly. "I know. There's been more than one
     like you, more than one who came to Earth and found he somehow couldn't
     leave. This old world is in the blood of our race, Laird." She looked
     up. "A year's not long. We'll need you here to replace Jonny, to
     supervise the Sun-mining. And I need you. I always will."</p>,
     <p>Carlin held her closely, all tiredness and doubts gone now, strangely
     content. He looked up at the summer stars and thought of worlds out
     there, but it was all far away, far away.</p>,
     <p>And Earth was close, its ancient quiet night enfolding him. Soft wind
     stirred leafing branches in the moonlight, and the road wound up white
     and sure toward the old house, and out of the vastness of time and
     space, an Earthman had come home.</p>]




```python
print(len(soup.find_all('p')))
soup.find_all('p')
```

    760





    [<p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Title</strong>: Forgotten world</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Author</strong>: Edmond Hamilton</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Release Date</strong>: November 15, 2022 [EBook #69357]</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Language</strong>: English</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Original Publication</strong>: US: , United States: Standard Magazines, Inc.,1945.</p>,
     <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Credits</strong>: Greg Weeks, Mary Meehan and the Online Distributed Proofreading Team at http://www.pgdp.net</p>,
     <p>[Transcriber's Note: This etext was produced from<br/>
     Thrilling Wonder Stories Winter 1946.<br/>
     Extensive research did not uncover any evidence that<br/>
     the U.S. copyright on this publication was renewed.]</p>,
     <p class="ph1">CHAPTER I</p>,
     <p class="ph1"><i>Stranger from the Stars</i></p>,
     <p>Carlin was the only one of the four hundred passengers on the "Larkoom"
     who hated the star-ship and everything about it.</p>,
     <p>He was bored with the vessel and everyone aboard. A pack of chattering
     idiots! For the hundredth time since leaving Canopus, he told himself
     that he was a monumental fool to let that psychotherapist talk him into
     this crazy trip.</p>,
     <p>A blond girl from Altair Four came tripping along the deck and favored
     Laird Carlin with the bright smile that all the younger feminine
     tourists had practised on the tall, dark, dour-looking young man.</p>,
     <p>The blonde from Altair Four favored the tall dour-looking young man with a bright smile.</p>,
     <p>"Oh, Mr, Carlin, the annunciators just said that we're only eight
     hours from Sol. By night, we'll be on Earth! Isn't it thrilling?"</p>,
     <p>"Just what is thrilling about it?" Carlin asked sourly.</p>,
     <p>The girl was a little dumfounded. "Why, I mean, Earth! All the ancient
     history we study in schools, about how men first came from there two
     thousand years ago. Or was it twenty-one hundred?"</p>,
     <p>She prattled on, voicing all the appropriate clichés.</p>,
     <p>"Just think, all of us in this ship came from different stats and
     worlds, yet long ago all our ancestors lived on that one little world
     Earth. And they say it's still much the same as it was then. Isn't it
     wonderful?"</p>,
     <p>Carlin could not see anything wonderful about it, and a little wearily
     he said so.</p>,
     <p>The girl flushed in exasperation. "Then why are you going to Earth at
     all?"</p>,
     <p>Why indeed, Carlin wondered savagely? Why the devil wasn't he back
     on the other side of the galaxy where he belonged, supervising
     establishment of the new star-ship line to Algol Six, spending his
     leaves in Sun City with Nila?</p>,
     <p>Nila—he yearned for her, for her gay, mocking humor, her cool beauty,
     her quick, clever mind. What was he doing here with a bunch of
     bird-brained tourists who were conscientiously tripping for local color
     to an old, forgotten world?</p>,
     <p>This whole part of the galaxy was a stagnant, half-dead area. This side
     of Vega there weren't a score of suns with worlds of any importance.
     And the old "Larkoom," a second-rate star-ship that couldn't make more
     than eighty light-speeds, was plodding determinedly and monotonously on
     into it.</p>,
     <p>Curse that psychotherapist anyway! Why had he been crazy enough to
     listen to the fellow? That smug, pink, blinking Arcturian had smiled as
     gently as a well-bred pussy-cat as he told Carlin what his trouble was.</p>,
     <p>"Star-sick?" Carlin had flared. "What do you mean, star-sick? I've made
     the trip to Algol ten times in the last three months."</p>,
     <p>The psychotherapist had nodded. "Yes. And that was nine times too many.
     You've been overdoing it for a long time, Mr. Carlin."</p>,
     <p>Before Carlin could protest, the other man had referred to the dossier
     on his desk.</p>,
     <p>"I have your record here. Born at Aldebaran four thirty years ago.
     Graduated at twenty-two from Canopus University with the degree
     of Cosmic Engineer. Worked since then establishing spaceports for
     star-ship lines between Rigel, Sharak, Tibor, Algol and other stars."</p>,
     <p>The psychotherapist looked up gravely. "The point is that you've spent
     fifty per cent of your time in the last eight years in star-ships. The
     average has been seventy per cent since you took charge of establishing
     the new Algol line. And that's too much time in space for any man. No
     wonder you're star-sick."</p>,
     <p>"Blast it, I'm not star-sick!" Carlin exploded. "What kind of therapist
     are you? I come here to have you treat a perfectly simple syndrome of
     reflex-fatigue, and you tell me all this!"</p>,
     <p>The Arcturian shook his head wisely. "Your case was only simple on the
     surface, Mr. Carlin. The hypnosis showed up your trouble unmistakably.
     Want to hear the record?"</p>,
     <p>Carlin heard it. And it wasn't pretty. Not pretty, to hear his
     hypnosis-freed subconscious yelling out a frantic hatred of space and
     star-ships and everything connected with them.</p>,
     <p>"You see?" said the Arcturian gently. "This has been building up in you
     for a long time."</p>,
     <p>Carlin was stunned. He had known of other men who had got star-sick and
     had had to drop their work and quit traveling space for a while. Other
     men—but he'd always laughed contemptuously at them for it.</p>,
     <p>The psychos might declare that it was perfectly natural for a man to
     develop a subconscious aversion to space if he crowded his work, but
     the hard-bitten engineers of Carlin's set believed that a star-sick man
     was nine times in ten a shirker. And now he himself was told he was
     star-sick.</p>,
     <p>"You've got to quit work and stay out of space for a while," the
     Arcturian therapist told him.</p>,
     <p>Carlin felt sick at heart. "Then all my work in building up the Algol
     line will go into young Brewer's hands."</p>,
     <p>Still, he thought after a moment, it might not be so bad. Working in
     his line's main offices here on Canopus Two, he could keep in touch.
     And he would have more time here with Nila.</p>,
     <p>But the psychotherapist shook his head quite decisively at that.</p>,
     <p>"No, Mr. Carlin. Your case is too dangerous for that. Your subconscious
     is twisted into a knot that is going to be hard to untie." He hesitated
     a moment as though he knew what reaction his next words would provoke.
     "In fact, there's only one way in which you can be normalized. That's
     the Earth-treatment."</p>,
     <p>"Earth-treatment?" Carlin didn't even know what it meant. "You mean,
     some treatment that has reference to the old planet over on the other
     side of the galaxy?"</p>,
     <p>The Arcturian nodded. "Yes, our ancestral planet Earth. Where all our
     race came from, two thousand years ago. Where you're going back to, for
     perhaps a year."</p>,
     <p>Carlin was knocked breathless by that calm statement.</p>,
     <p>"Me going to Earth for a year? Are you crazy? Why should I go there?"</p>,
     <p>"Because," the therapist said soberly, "if you don't I'm afraid you
     won't last another six months as a star-line man."</p>,
     <p>"But why can't I take a rest right here on Canopus Two?" Carlin
     demanded heatedly. "Why send me to that moldering, forgotten old planet
     where there's nothing now but a few historical monuments?"</p>,
     <p>"You've never been to Earth, I take it?" the psychotherapist asked
     thoughtfully.</p>,
     <p>Carlin made an impatient gesture. "I'm not interested in ancient
     history. That part of the galaxy is all a backwater."</p>,
     <p>"Yes," the expert said. "I know all that. But old and small and
     forgotten as it is these days, Earth is still important."</p>,
     <p>"To historians," Carlin snapped. "To people who like to poke in the
     dusty past."</p>,
     <p>The Arcturian nodded, and shrugged.</p>,
     <p>"And to psychologists," he said quietly. "Most people these days don't
     realize something. They don't realize that we, all of us, are still
     really Earthmen in a way." He held up a protesting hand. "Oh, I know
     we don't think of ourselves like that! Since those first Earthmen
     pioneered to their neighbor planets and then to the stars, since our
     civilization spread out over most of the galaxy, a hundred generations
     of us have been born on different star-worlds from Rigel to Fomalhaut.
     But except for local modifications, the type of humanity has persisted
     since our ancestors left Earth and Sol long ago.</p>,
     <p>"That's because we've altered star-world conditions to fit ourselves,
     instead of adapting ourselves to those conditions. We've cunningly
     changed atmospheres, gravities, everything, wherever we went. We've
     kept ourselves one race, one type, that way. But it's a type that is
     still indexed to that old plane Earth as its norm."</p>,
     <p>"Does that explain why I have to give up my work and go live on the old
     relic for a year?" Carlin demanded furiously.</p>,
     <p>"Yes, it does," the Arcturian replied. "We're a star-traveling race
     now. But the mind can take only so much of the strain of star-travel.
     Overdo that strain and you get a revulsion, you get star-sickness. Then
     the only cure is rest for the mind in completely normal conditions. And
     complete normality, for us descendants of Earthmen, is—Earth."</p>,
     <p>Carlin had stormed. He carried his wrathful resistance to the last
     pitch.</p>,
     <p>And then the psychotherapist had crushed him.</p>,
     <p>"I've turned in your psycho-record to your star-ship line. You'll not
     be allowed to work there until you're cured."</p>,
     <p>And that, Laird Carlin thought bitterly, was why he was sprawled in a
     deck-chair here on the "Larkoom" as the old tub creaked and labored and
     plodded through space toward the yellow spark of Sol.</p>,
     <p>"A year!" he thought in impotent rage. "A year in that hole! I might as
     well be dead."</p>,
     <p>The psychotherapist had held out the hope that it might not take a
     year. Some cases of star-sickness responded quickly to Earth-treatment.
     But even a few months seemed an eternity to Carlin.</p>,
     <p>The passengers of the "Larkoom" were crowding toward the transparent
     wall of the deck. Earth was coming into sight. And these people—men
     and women bronzed by the glare of Canopus, reddened by the desert winds
     of Rigel's worlds, paled by the mists of Altair's planets—all were
     watching with an intense and eager expectation.</p>,
     <p>Carlin walked wearily over to the deck wall and watched with them.
     Sol, ahead, was a small and undistinguished yellow sun. Its orb was
     unimpressive to eyes that had looked on Antares and Altair.</p>,
     <p>And the planets that circled it were so little that Carlin could
     hardly make them out. He remembered half-forgotten names from ancient
     history—Saturn, Jupiter, Mars. And that little gray-green dot beyond
     must be Earth.</p>,
     <p>"Isn't it tiny?" babbled a rapturous, overweight woman beside Carlin.
     "I think it's cute!"</p>,
     <p>A very young man from Mizar Seven proudly aired his knowledge.</p>,
     <p>"That satellite beyond it is Luna, its moon."</p>,
     <p>"The moon is almost as big as the little planet!" exclaimed someone,
     laughing.</p>,
     <p>Carlin found their chatter getting on his nerves, and edged further
     along the deck. In gloomy silence, he looked down as the "Larkoom"
     swept in swift, almost soundless rush toward the little planet.</p>,
     <p>A gray-green, cloud-screened ball spinning around a second-rate sun—it
     looked like the end of the universe to Carlin. And he might have to
     spend a year here! His spirits sank still lower.</p>,
     <p>"They say you can get the most wonderful souvenirs here," one of the
     tourists' voices reached him.</p>,
     <p>Carlin writhed. He would be glad to get out even at Earth, to get away
     from this bunch of babbling fools.</p>,
     <p>He realized his irritability was extreme, unreasonable. It was the
     result of his star-sickness, he supposed. But that didn't make it any
     more endurable.</p>,
     <p>"Landing in ten minutes," spoke the annunciators throughout the ship.
     "Stasis going on."</p>,
     <p>The dim glow of the force-stasis that cushioned everything in the ship
     against pressure of deceleration came on like a tangible medium around
     them. The big propulsion-wave generators droned in lower key.</p>,
     <p>Swaddled in the cushioning force, they felt no discomfort as the
     "Larkoom" quickly dropped toward the little planet. Atmosphere screamed
     briefly outside the ship. They came down through a belt of clouds.</p>,
     <p>"That's the city New York!" cried an eager voice. "The oldest human
     city in the galaxy!"</p>,
     <p class="ph1">CHAPTER II</p>,
     <p class="ph1"><i>Ancient Town</i></p>,
     <p>Carlin looked with a jaundiced eye on the scene widening out below
     them. There was a blue ocean stretching eastward, a long green coast,
     and an island that was covered by the grotesquely lofty buildings of an
     extremely antiquated type of city.</p>,
     <p>This ancient town called New York was like a memento of the primitive
     past. Not for a thousand years had men crowded their structures so
     crazily together, or built them to such insane heights.</p>,
     <p>"It's like one of the bird-people's lofts on Polaris One!" exclaimed a
     girl, laughing. "And how old it looks!"</p>,
     <p>Old? Yes. Pitifully old, like a withered beldame who endeavors still
     to maintain stiff dignity. The city looked only half-occupied, vines
     growing on some of the grotesque towers, parks ragged around the edges.</p>,
     <p>The spaceport, some distance northward amid low rolling hills, was so
     small as to be inadequate for any decent world. Carlin's practised eyes
     condemned the cracked, blackened tarmac, the ill-placed rows of docks,
     the insufficient hangar and repair buildings.</p>,
     <p>The "Larkoom" landed softly. Carlin waited wearily until the squealing
     rush of tourists was over, and then walked out into the soft yellow
     sunshine. He looked around without interest. Landing on a new world was
     no novelty to him.</p>,
     <p>But for a moment, he was startled by the air he breathed. It was so
     sweet, so buoyant, so right. It was subtly stimulating, exhilarating
     to the lungs. Then he realized the cause. All over the galaxy, the
     descendants of Earthmen had conditioned planetary atmospheres with this
     atmosphere of Earth as the desired norm.</p>,
     <p>He looked around uncertainly. The tourists were already being
     shepherded by their tour-conductors toward some old monuments at the
     far end of the spaceport. But he had no desire to follow them.</p>,
     <p>The psychotherapist had told him, "Live as nearly an ordinary Earth
     life as you can. Your cure will be quicker if you do. Best thing would
     be to lodge in some typical Earth home, if you can."</p>,
     <p>Carlin wondered where he could find such a lodging. There were a few
     Earthmen about, spacemen, port officials and the like. He could ask one
     of them.</p>,
     <p>He had met Earthmen before throughout the galaxy, for many of them
     followed space as a trade. And he didn't much like them. A proud,
     taciturn, half-sulky lot, they had always seemed to him.</p>,
     <p>"Can you tell me where I could find lodgings around here?" He asked a
     lanky, lantern-jawed man in faded clothes.</p>,
     <p>The Earthman contemplated Laird Carlin with unfriendly eyes, taking in
     his sun-darkened face, his pearl-colored synthesilk slacks and jacket,
     every detail of his appearance that was alien here.</p>,
     <p>"Well, no," the fellow drawled coolly. "Don't know where a stranger
     could get lodgin's round here."</p>,
     <p>He slouched on. Carlin flushed with anger at the scarcely veiled
     hostility in the fellow's manner.</p>,
     <p>These blasted yokels of Earth! Living here on an old, outworn,
     fifth-rate planet, resenting the progress and prosperity of the great
     star-worlds, talking of everybody but themselves as "strangers"!</p>,
     <p>"And I'm supposed to live among them for a year!" he thought bitterly.</p>,
     <p>He started across the spaceport. He had noted a spick-and-span
     chromaloy building with a half-dozen trim Control cruisers parked
     nearby, and with the Control Council emblem on its wall. He could find
     out something there.</p>,
     <p>The spaceport was a somnolent, slovenly place to Carlin's eyes. A
     few star-ships, all of them freighters except the tubby "Larkoom," a
     scattering of little inter-planet craft, a few workers lounging about.
     Even the smallest world of the great stars would be ashamed of such a
     port.</p>,
     <p>That soft yellow sun, he found, had a deceptive warmth. And walking was
     tiring after days of the ship's artificial gravity. Then Carlin stopped
     as he came abreast of a rickety little planet-ship.</p>,
     <p>Two Earthmen were inspecting its stern drive-plates—one of them a
     stocky, red-faced young man, the other a lame younger fellow with a
     crutch. Carlin asked them his question.</p>,
     <p>The red-faced individual answered with the same hostility of manner.</p>,
     <p>"You'll find no lodgings around here. Better go with the rest of your
     crowd. There's a big tourist hotel down in the city."</p>,
     <p>Carlin swore. "Blast it, I'm not a tourist. I'm an engineer sent here
     by a crazy psycho to spend a year on Earth—heaven knows why!"</p>,
     <p>The lame young Earthman looked at Carlin more closely. He had a thin,
     pleasant brown face with intelligent blue eyes.</p>,
     <p>"Oh, an Earth-treatment man?" he said. "A few come in all the time." He
     asked interestedly, "You're a Cosmic Engineer? Do you mind telling me
     what field?"</p>,
     <p>"Star-ship line chief surveyor," Carlin said wearily. "That means I lay
     out spaceport and beacon routes between star-worlds."</p>,
     <p>"I know what it means." The lame youngster nodded quietly. He
     hesitated, frowning slightly as though weighing something. Then, as if
     deciding, he spoke. "I'm Jonny Land. I think we could fix you up with
     lodgings if you don't mind putting up with a little discomfort."</p>,
     <p>"You mean, in your own home?" Carlin asked doubtfully. "Where is it?"</p>,
     <p>Jonny Land pointed to one of the low green ridges west of the spaceport.</p>,
     <p>"Just up on the ridge there. There's only my grandfather, my brother
     and sister, and myself. And we have an extra room."</p>,
     <p>The red-faced young Earthman made a sharp protest. "Jonny, what the
     blazes are you thinking of? You don't want this fellow in with you!"</p>,
     <p>The violence of his protest seemed uncalled-for to Carlin, even
     granting the general Earthman hostility to strangers.</p>,
     <p>Jonny Land quietly quelled the outburst. "I'm doing this, Loesser." He
     looked at Carlin. "Well, what about it? I warn you that you won't find
     the comforts of a big star-world apartment."</p>,
     <p>"I don't expect anything like that here," Carlin answered tiredly. He
     felt worn out by the voyage, the discouragingly primitive aspect of
     this place where he must live, the open unfriendliness. He nodded.
     "I'll try it. The name is Laird Carlin."</p>,
     <p>"If you'll get your luggage, I'll take you up," Jonny Land suggested.
     "I have a truck. I'll meet you over at the terminal."</p>,
     <p>Carlin came out of the shabby terminal a little later with his two
     kitbags and found the lame youngster waiting at the wheel of a
     disreputable-looking old ato-truck.</p>,
     <p>Loesser, the red-faced young man, was standing beside it voicing
     emphatic protest about something. Carlin overheard a few words.</p>,
     <p>"—ruin everything by taking this fellow in!" he was saying violently.
     "How do you know he isn't a Control spy?"</p>,
     <p>"I know what I'm doing, Loesser," Jonny Land repeated firmly.</p>,
     <p>They broke off as they saw Carlin coming. But Loesser gave him a hot,
     angry glare as he climbed into the machine.</p>,
     <p>The old truck ran westward across the bumpy tarmac and started climbing
     an ancient, cracked concrete road toward the green ridge.</p>,
     <p>Carlin wondered wearily what these Earthmen were up to that made them
     afraid of Control? Smuggling, maybe? He didn't much care. He was hot,
     tired, grimy with dust, and unutterably disgusted with Earth.</p>,
     <p>The concrete road that climbed the ridge looked as though it was
     centuries old. And its engineering had been timid, for it wound around
     hills instead of cutting through them, bridged small streams instead of
     trampling over them. But the battered truck had difficulty negotiating
     even these easy grades. Its ato-motor drumming noisily as it climbed.</p>,
     <p>Carlin looked out gloomily at the sunset-lit landscape. He could not
     get used to the vivid, dominating green of all vegetation here. And
     he was shocked by the unkempt, ragged look of everything. Untended
     fields of weeds and clumps of woods grew right up to the road. It was
     dismayingly different from the groomed, parklike planets of Canopus.</p>,
     <p>The houses Carlin glimpsed along the road added to his dislike. They
     were mostly old ferroconcrete dwellings half-hidden by trees and
     bright flowers, with behind them the big tanks used in hydroponic
     farming. Hydroponic farming was so old-fashioned he had thought it had
     disappeared from the galaxy. What was the matter with these people that
     they didn't directly synthesize their food as others did?</p>,
     <p>Young Jonny Land was speaking to him.</p>,
     <p>"You've never been here before? You must find Earth a little odd."</p>,
     <p>Carlin shrugged. "It's all right, I suppose. But I just can't
     understand how you people could let your planet get into this kind of
     shape. Why haven't you spread out more, instead of huddling around a
     few archaic centralized cities like that one back yonder?"</p>,
     <p>The lame young Earthman answered slowly, his thin, brown face turned to
     the road ahead.</p>,
     <p>"The answer to that is simple. One word, in fact. And that word is
     'power.' We just don't have power enough here on Earth to smooth it out
     into a garden-planet like your star-worlds, to come and go around it
     any distance at will."</p>,
     <p>"Atomic power is about the easiest thing to produce there is," Carlin
     commented skeptically.</p>,
     <p>"Yes, if you have copper fuel," Jonny Land replied. "If we had enough
     copper we could make a garden of this world too, could spread all
     around its loveliest spots and come and go by fast flier, could give
     up the old hydroponic farming and synthesize our food, and produce the
     luxuries you people have on the star-worlds.</p>,
     <p>"But we have little copper. Earth, and its sister-planets here, are all
     starved for it. Once, we had a lot. But not now. And it's economically
     impossible to haul copper in sufficient quantities from other stars.
     That's why we're power-starved, unable to progress."</p>,
     <p>Carlin made no further comment. He was not much interested. He was
     only wondering sickly how long he would have to stay on this unkempt,
     stagnant planet.</p>,
     <p>The sun was burning his neck, for the old truck was topless. He was
     jolted by holes in the ancient road. The sweetness of the air had lost
     its magic for him, for now with the twilight had appeared swarms of
     evil little gnats and midges.</p>,
     <p>"This is the house," said Jonny Land, pulling up the truck in front of
     a square dwelling.</p>,
     <p>Laird Carlin's heart sank. It was like the other houses he had seen,
     a ferroconcrete structure festooned with climbing flower-vines,
     surrounded by tall, untrimmed trees except on the side that looked down
     into the twilit valley. Primitive hydroponic tanks gleamed dully beyond
     the trees.</p>,
     <p>He followed the lame youngster into a dim, cool living room. It looked
     like an antique stage set to Carlin, with its ridiculous cloth curtains
     at the windows, its obsolete krypton light bulbs in the ceiling, its
     massive furniture that was actually made of wood.</p>,
     <p>Jonny Land had been making explanations in lowered tones to the two
     people at the other end of the room. They came forward, a spry old man
     and a girl.</p>,
     <p>"This is Gramp Land, my grandfather," Jonny introduced. "And my sister
     Marn."</p>,
     <p>The old man looked at Laird Carlin with inquisitive, bright eyes, and
     his gnarled hand reached for an old-fashioned handshake.</p>,
     <p>"Come from Canopus, do you?" he chirped. "Well, that's a long way off.
     I was there once years ago when I followed space. And my grandson Harb
     has been there lots of times when he was a star-ship man."</p>,
     <p>The girl, Marn, looked doubtful and troubled as she murmured a word of
     greeting to Carlin. He sensed that his coming had disturbed her.</p>,
     <p>She was a rather small girl, with a thick mop of ash-colored hair
     carelessly combed back. Her eyes were grave blue. She wore a faded old
     slack-suit that he thought the most barbaric feminine garment he had
     seen.</p>,
     <p>"I hope we can make you comfortable here, Mr. Carlin," she said,
     troubled. "We've never had any lodger before. I can't understand why
     Jonny made the suggestion."</p>,
     <p>A heavy step at the door cut her short. Her look of distress and worry
     deepened.</p>,
     <p>"There's my brother Harb, now."</p>,
     <p>Harb Land was a gangling young giant with a craggy face and
     slate-colored eyes that looked at Carlin with instant hostility. Jonny
     had limped forward and was quickly explaining Carlin's presence.</p>,
     <p>"He's going to live here with us for a while, Harb."</p>,
     <p>Harb Land's reaction was violent. "Have you gone out of your mind,
     Jonny?" he flared. "We can't have him here."</p>,
     <p>Disgusted, Carlin started to turn away. But Jonny Land stopped him with
     a gesture. There was a quiet, unsuspected strength in his thin brown
     face as he spoke to his lowering brother.</p>,
     <p>"He's going to stay, Harb. We'll talk about it later."</p>,
     <p>Harb Land made no reply, but glared at Carlin. And Carlin felt an
     unutterable weariness and dislike.</p>,
     <p>These primitive, backward, suspicious Earth yokels, quarreling over the
     privilege of staying in their grotesque old house. As though he would
     stay on their cursed planet one minute if he didn't have to!</p>,
     <p>"I'm very tired," he said heavily. "If you could show me where the room
     is, I should like to rest."</p>,
     <p>Marn uttered an apologetic exclamation. "Oh, I'm sorry! Of course
     you're tired. Come with me, Mr. Carlin."</p>,
     <p>She led upstairs. There was no grav-lift, just old-fashioned steps
     going up a dark hall. And the bedroom on the upper floor to which she
     took him was as bad as he had expected.</p>,
     <p>It was clean, of course, spotlessly so. But it was more like a museum
     exhibit than a sleeping chamber, to Carlin. There were no aerators,
     just open windows with crude screens across them. No somnigrav pad,
     just a high, old-style bed. There wasn't even a video.</p>,
     <p>Yet the girl made no apologies for it, seemed not to think any
     necessary.</p>,
     <p>"We'll bring your bags up after dinner," she said. "It will be soon."</p>,
     <p class="ph1">CHAPTER III</p>,
     <p class="ph1"><i>Old Planet</i></p>,
     <p>When Marn had gone, Carlin lay down wearily on the lumpy, sagging bed.
     He closed his eyes. The reaction to the long, slow voyage had set in.
     No doubt about it, he was star-sick all right. Time was when no voyage
     could have made him feel like this.</p>,
     <p>But it wasn't the voyage so much as this world to which he had been
     condemned. How was he going to live here for months, for a whole year
     maybe?</p>,
     <p>The sound of an angry voice came up dimly through the twilight, from
     the lower floor of the house. He recognized Harb Land's angry tones.</p>,
     <p>"—if Control Operations finds out what we're doing!"</p>,
     <p>There was a murmur of lower voices, and then the argument seemed to
     stop. Carlin remembered what he had overheard the red-faced Loesser
     saying at the spaceport.</p>,
     <p>What were these Earthmen doing that they were so secretive about? It
     must be something against the laws by which Control Council governed
     the galaxy, or they would not fear discovery by Control Operations.</p>,
     <p>When Carlin went down to dinner, he expected open hostility from the
     gangling older brother. But Harb Land muttered a curt greeting, his
     half-civil manner indicating his angry protests had been overridden.</p>,
     <p>Carlin stared dismayedly at the food set before them. Instead of the
     clear, colored synthetic jellies and liquids he was used to, the food
     was served in what seemed barbarically primitive state. Cooked whole
     vegetables, natural eggs, natural milk—everything rawly natural.</p>,
     <p>He ate what he could, which was little. His weariness was drugging him,
     and Harb Land's smothered hostility gave a sense of strain.</p>,
     <p>Gramp Land carried on most of the conversation, questioning Carlin
     about the far-away star-worlds. Carlin answered wearily.</p>,
     <p>"Saw a lot of them worlds myself once," the old man said. He added
     proudly, "Following space runs in my family. My mother was a direct
     descendant of Gorham Johnson himself."</p>,
     <p>"Gorham Johnson?" Carlin asked. "Who was he?"</p>,
     <p>The question was unfortunate.</p>,
     <p>"What do they teach out in your star-world schools?" Gramp exploded.
     "Don't you know that Gorham Johnson was the first man ever to travel
     space? That he was an Earthman, who took off from down in the valley
     here two thousand years ago?"</p>,
     <p>Gramp's pride was outraged. Carlin remembered the old galaxy
     proverb—"Proud as an Earthman." They were all like that, inordinately
     vain of the fact that their world's people had first conquered space.</p>,
     <p>"Sorry," he said tiredly. "I remember the name now. Anyway, I had too
     much cosmic physics to study to spend much time on ancient history."</p>,
     <p>Gramp still spluttered, but Jonny intervened, questioning Carlin on his
     work.</p>,
     <p>"Did you study sub-atomics or just straight dynamics?"</p>,
     <p>"Sub-atomics," Carlin answered. And, to another question, "Yes, I had
     electronic mechanics too."</p>,
     <p>He caught the swift, triumphant glance that Jonny Land shot at his
     brother. It puzzled him.</p>,
     <p>"Jonny knows all that stuff," boasted Gramp, his good humor restored.
     "He's a Cosmic Engineer graduate from Canopus University, too."</p>,
     <p>Laird Carlin was genuinely surprised. He looked at the quiet,
     thin-faced youngster.</p>,
     <p>"You're a Canopus graduate? Why the devil is a man of your training
     wasting your time here on Earth?"</p>,
     <p>"I just like Earth," Jonny answered evenly, "and wanted to come back
     here when my education was finished."</p>,
     <p>"Oh, sure." Carlin nodded. "But if this world is as outworn as it
     looks, there's no field here for a CE. You ought to be out at Algol."</p>,
     <p>"You star-world people are all the same—always advising us to leave
     Earth!" Harb Land interrupted with suppressed passion. "That's what
     Control Council keeps harping on as a solution to all our poverty and
     problems. They keep asking, 'Why don't you emigrate to other stars?'"</p>,
     <p>Gramp Land shook his head. "We don't leave our planet as lightly as
     some folks do. No matter how far an Earthman goes, he always comes
     home."</p>,
     <p>"Still, you can hardly blame Control Council for giving you good
     advice," Carlin said, exasperated. "After all, it's your own fault if
     you foolishly squandered the copper resources of your planet and now
     lack power."</p>,
     <p>Harb Land's craggy face darkened. "Yes, we squandered our copper
     foolishly. We did it twenty centuries ago, when Earth was opening
     up the whole galaxy to travel. We spent our copper establishing the
     galactic civilization that's forgotten all about our power-starved
     world."</p>,
     <p>"Harb, please!" said Marn in a low voice, distress in her face.</p>,
     <p>A silence fell, and they finished the dinner without further
     conversation. But Jonny Land spoke to Carlin before he went upstairs.</p>,
     <p>"Don't take Harb too seriously. A lot of people here on Earth are so
     embittered about our lack of power that they're unreasonable."</p>,
     <p>Carlin found his bedroom dark. No automatic lights came on when he
     entered, and he could not find the switch. He gave it up, and got into
     bed and lay looking heavily out into the night.</p>,
     <p>Soft wind was stirring the trees around the house. Heavy scent of
     flowers drifted on it, stirring the window curtains. Down in the valley
     gleamed the spaceport beacons, and beyond lay a thin rim of glimmering
     sea over which the quarter-phase shield of Luna was rising.</p>,
     <p>He felt utterly miserable, homesick, wretched. If he were back at
     Canopus right now, he would be dancing with Nila in Sun City ballroom,
     or wandering in Yellow Gardens.</p>,
     <p>He drifted off to sleep despite himself, in his lumpy bed....</p>,
     <p>Carlin awoke with bright sunrise splashing his face. He reached
     sleepily for the aerator and refreshment buttons—then remembered.</p>,
     <p>To his surprise, he was feeling much better. He had slept well in the
     primitive bed, and fatigue had drained out of him.</p>,
     <p>Queer, musical notes that he guessed were calls of birds came to his
     ears. The air that snapped the curtains was chill now, but pure and
     sweet, subtly intoxicating.</p>,
     <p>"They do have finer air on this old world than any aerator can
     furnish," he thought.</p>,
     <p>He put on a zipper-suit that was dark brown and rough in weave.</p>,
     <p>"Going native," he thought with a sour grin, and went downstairs.</p>,
     <p>Marn Land was the only person he found in the sunny rooms. She still
     wore those barbaric faded old slacks, but had a red flower in her ashen
     hair. A little frown of worry in her forehead disappeared as she looked
     at him.</p>,
     <p>"You're feeling better, aren't you?" she asked.</p>,
     <p>"A lot," Carlin admitted. "I'm afraid I was rather rude last night, you
     know."</p>,
     <p>"You were tired," she said gravely. "Just sit down. I'll get your
     breakfast."</p>,
     <p>It was a new experience to Carlin to sit chatting in a sunny old
     kitchen while a girl in faded slacks prepared his breakfast on an
     electrode stove. Instead of punching the refreshment-button for it.</p>,
     <p>"Jonny and Harb have gone down to the spaceport," she said over her
     shoulder. "They and a few friends have an old planet-ship there that
     they're fixing up for a trip to Mercury."</p>,
     <p>"Mercury?" he said. "Oh, that's the innermost of these planets, isn't
     it?"</p>,
     <p>"Yes. Men here on Earth are always going prospecting for copper on its
     Hot Side. Jonny got up this prospecting expedition."</p>,
     <p>The breakfast she put before Carlin was of coarse wheaten bread, more
     of the natural eggs and milk, and a curious brown beverage made from
     stewing certain dried berries. She informed him its name was coffee.
     Carlin tried it, found it bitter and unpalatable.</p>,
     <p>A little surprised by his own action, he ate nearly everything else.
     The food was coarse, but satisfying enough, and he would have to get
     used to it if he were to stay here.</p>,
     <p>"I'll try not to be any trouble to you," he told Marn. "I'm just
     supposed to take it easy, do anything I want to."</p>,
     <p>She nodded. "I know. Some of our neighbors had Earth-treatment visitors
     as lodgers. They all got to like Earth a lot before they left."</p>,
     <p>Carlin did not voice his pessimism on that point. He went to the door
     and stood looking out into the sun-bright, flowery yard.</p>,
     <p>He felt at a loss. It was baffling to find himself without anything
     to do, no work crowding up that must be hurried through, no crews of
     ato-men to supervise in blasting spaceports out of untamed planets.</p>,
     <p>Marn looked at him understandingly. "You've always been busy, haven't
     you? Earth must seem slow and dull to you."</p>,
     <p>Carlin shrugged. "I might as well get used to it. I think I'll take a
     look around."</p>,
     <p>"You'll find Gramp fishing up at the north brook if you go that far,"
     Marn called after him as he walked across the yard.</p>,
     <p>Carlin sauntered past a big, locked ferroconcrete workshop of some
     kind, and some tall storage sheds, then on past the flat, wide
     hydroponic tanks that were now loaded with their masses of green growth.</p>,
     <p>He found a road beyond them that he did not recognize as a road, at
     first. It was a mere wide track gouged northward along the wooded
     ridge, the first dirt road that he had ever seen on a civilized world.</p>,
     <p>"A poor planet, all right," Carlin thought. "Can't even build decent
     roads."</p>,
     <p>There were hardly even any ato-fliers in the sky, only an occasional
     one flitting across the blue vault.</p>,
     <p>"No wonder these poverty-stricken devils resent the rest of the
     galaxy," he thought. "I suppose I would too, if it had been my bad luck
     to be born here."</p>,
     <p>The road was crazily illogical, winding westward along the woods-clad
     ridge in serpentine fashion. It twisted accomodatingly to avoid big
     boulders, a spring, a small gully.</p>,
     <p>The woods on either side was deplorably unkempt to Carlin's eyes. Big
     and small trees jumbled together, saplings choking each other out, dead
     brush and thorns and vines everywhere. There was even wild life in the
     woods, furry rodents scuttling away, hosts of birds.</p>,
     <p>This sort of thing was what you expected on some unpeopled planet that
     hadn't yet been pioneered and civilized. But Earth was the oldest
     human-peopled world in the whole galaxy.</p>,
     <p>Yet Carlin had to admit that there were certain compensations here.
     That winelike air was still an experience to him. And walking now came
     more easily to his muscles here than on any world. It seemed odd to be
     walking with such perfect ease, without wearing a de-grav.</p>,
     <p>He could not find the brook Marn had mentioned. He sat down on a log by
     the roadside, musing on the drowsy, dull quiet of this place. There was
     not a sound of human activity. Didn't these Earth people ever get bored
     with the sleepiness of the place?</p>,
     <p>Carlin found he was still tired. He watched a small, brilliant insect
     fluttering over a flower near by. Soft wind breathed through the ragged
     woods, stirring the green leaves and making a dappled, dancing pattern
     of sunlight on the ground. A distant bird called rustily.</p>,
     <p>"An old, outworn planet, dreaming," he thought. "These people, all of
     them, living in its past."</p>,
     <p>Carlin finally got up stiffly, and lounged back along the road. He was
     surprised to find that time had passed quickly, that the sun was now at
     the zenith. And that, somehow, his taut nerves had relaxed.</p>,
     <p>The big workshop behind the house had its doors open now. He glanced
     through them and was surprised to see that the cavernous room in there
     was a fairly well-equipped atomic-engineering laboratory.</p>,
     <p>Interested, Carlin started toward it. In the center of the big room
     he had glimpsed a towering, massive machine whose inner mechanism was
     concealed by a cylindrical metal cover.</p>,
     <p>"Looks like it might be a big field-generator of some kind," he
     muttered. "I wonder what it really is?"</p>,
     <p>There was a violent exclamation as an Earthman came running out from
     behind the machine to block his entrance.</p>,
     <p>Carlin recognized the broad red face, angry eyes and stocky figure of
     Loesser, the man who had argued with Jonny at the spaceport.</p>,
     <p>"What are you doing here?" Loesser demanded harshly.</p>,
     <p>Carlin was bewildered by his vehemence. "Why, I just wanted to take a
     look at this machine."</p>,
     <p>"I thought so!" blazed Loesser, his eyes raging. "I told Jonny that was
     why you came here!"</p>,
     <p>He snatched an object from his jacket pocket. To Carlin's thunderstruck
     amazement, the object was a stubby atom-pistol that Loesser was
     furiously leveling at him.</p>,
     <p class="ph1">CHAPTER IV</p>,
     <p class="ph1"><i>Mystery Machine</i></p>,
     <p>Laird Carlin was child of a galactic civilization in which violence
     between men was rare. There was plenty of danger yet, in pioneering new
     star-worlds, but over the civilized worlds themselves the unchallenged
     law of the Control Council maintained unbroken order. A man could go a
     lifetime without ever seeing violence.</p>,
     <p>The atom-pistol in Loesser's hand and the obvious murderous intention
     in the man's face stupefied Carlin. He was simply unable to adjust his
     thinking to the possibility that the enraged Earthman before him meant
     to blast him down.</p>,
     <p>"Why, what's the matter?" he began, puzzled and stunned.</p>,
     <p>He knew later how near he had been to death. At the moment, he so
     little recognized it that he felt no relief at the interruption that
     came now. Harb and Jonny Land came running forward from the cavernous
     interior of the workshop.</p>,
     <p>"Loesser, put that gun down!" snapped Jonny.</p>,
     <p>Loesser turned violently. "This fellow was spying on us! I saw him at
     the door!"</p>,
     <p>Harb Land's craggy face darkened ominously.</p>,
     <p>"I warned you what might happen," he said harshly to his brother.</p>,
     <p>"Is this man crazy?" Laird Carlin demanded bewilderedly of Jonny.</p>,
     <p>The lame youngster limped quickly forward. "Get back to work," he told
     the other two briefly. "Carlin, I'm sorry about this. I'll explain."</p>,
     <p>He walked beside Carlin toward the house. It was not until later that
     Carlin realized how deftly and unobtrusively he had been steered away
     from the workshop.</p>,
     <p>"Harb and Loesser and I, and a few others, are planning an expedition
     to Mercury to prospect for copper," Jonny was explaining. "In that ship
     you saw down at the spaceport. We've devised a new metal-finder of the
     radiolocator type, with which we hope to be able to locate new copper
     deposits. That's the machine in the workshop.</p>,
     <p>"We've maintained a certain secrecy about it," he went on, "because
     naturally we don't want other prospectors stealing the idea of our new
     finder and beating us to it. And I'm afraid Loesser thought you were
     spying on us. People here are always a little suspicious of strangers."</p>,
     <p>"So I've noticed," Carlin answered dryly. "This is the first world in
     the galaxy where I've ever felt completely unwelcome."</p>,
     <p>"Oh, I wouldn't say that," replied the other. "But put yourself in our
     place, Carlin. Figure how you would feel if you were an Earthman, your
     world starved for power because its copper was spent to establish a
     galactic civilization that now neglects it."</p>,
     <p>Jonny's thin brown face was earnest, his blue eyes watching Carlin as
     though eager to convince him. Carlin shook his head.</p>,
     <p>"I can see your problem in lacking copper," he said. "But the remedy
     for it is so simple. Nine-tenths of you should emigrate to other,
     better worlds as the Control Council advised."</p>,
     <p>Jonny smiled. "There you come up against the obstinacy of my people.
     We've an older planetary tradition, a deeper, more ancient love for our
     world, than any other people in the galaxy."</p>,
     <p>"I think you people live too much in the past," Carlin answered
     frankly. "But it's none of my business. Anyway, I hope your expedition
     brings home copper."</p>,
     <p>"Thanks," Jonny said softly. "I think we have a good chance."</p>,
     <p>Carlin went back to the veranda of the old house and sat there
     pondering. Something about Jonny's explanation had been vaguely
     unsatisfying.</p>,
     <p>To his trained eyes, the glimpse he had had of that towering machine
     had not suggested any metal-finding device. There had somehow been a
     suggestion in its half-glimpsed bulk of something quite different;
     something vaguely disturbing, almost menacing.</p>,
     <p>"The devil, I must have knots in my subconscious to start getting
     premonitions like that," Carlin swore. "The poor devils are just
     secretive about their plans because everyone else here is that way."</p>,
     <p>He lounged boredly around the house during the hot, sleepy afternoon.
     There was no one to talk to, for the brothers stayed out in their
     workshop and Marn was out tending the big hydroponic tanks.</p>,
     <p>He tinkered with the old video set in the living room but the
     only stations he could get were local Earth ones, and lectures on
     hydroponics and gossip about unknown people didn't interest him.</p>,
     <p>He finally gave up and stretched out on the veranda, staring sleepily
     down into the green cup of the valley and cursing the psychotherapist
     whose insane idea had sent him here to die of boredom. He dozed until
     he was awakened by the sputter of an arriving ato-truck.</p>,
     <p>It contained three lanky young men, tall Earthmen who went back to
     the workshop without stopping at the house. The other partners in the
     prospecting expedition, Carlin supposed sleepily.</p>,
     <p>Again he felt that queer sense of something threatening, that vague
     premonition that had clung to him ever since he glanced into the
     workshop. If only he could remember what that machine reminded him of.</p>,
     <p>Days passed and Carlin still could not remember that, though his
     disturbing doubt persisted. There was no chance of another look into
     the workshop for it was always locked except when Jonny and Harb and
     their half-dozen partners worked in it.</p>,
     <p>"The trouble with me," Carlin told himself ironically, "is that I
     haven't anything else to occupy my mind on this blamed world."</p>,
     <p>Yet Carlin's first repelled dislike of Earth had faded much by now.
     The crudities of existence, the lack of civilized conveniences, no
     longer bothered him so much. He had to admit that whether or not
     Earth-treatment was benefiting his twisted subconscious, this sleepy
     old planet was a fine place for a rest.</p>,
     <p>He spent his mornings idly rambling the twisting roads, his afternoons
     lounging on the cool, shady veranda of the old house, or helping Marn
     tend the hydroponic tanks. Or fishing with Gramp in the foaming brook
     below the ridge, while that oldster told interminable tales of the old
     days when he had followed space.</p>,
     <p>Neighbors, hydroponic farmers up and down the valley, dropped in at
     the Land house in the evenings. Carlin did not intrude, and gradually
     their first stiff suspicion of him abated and they talked freely before
     him. The talk always swung to the paramount consideration on this
     power-starved planet—the need for copper. It made Carlin feel a little
     guilty to remember how much of it was wasted on other worlds.</p>,
     <p>"I have to drive down to the spaceport for Jonny, to get some
     instruments he left in the ship," Marn said to him after dinner one
     evening. "Do you want to go along?"</p>,
     <p>Carlin grinned. "I've legged it so much lately that riding anywhere
     would be a change."</p>,
     <p>The old ato-truck swung down the twisting road in the blaring sunset.
     The heavens behind them were a glory of fusing colors as the red ball
     of Sol dipped majestically toward the horizon.</p>,
     <p>Despite his appreciation of that wild splendor, Carlin felt a vague
     uneasiness. Why should the loveliness of the evening bring disturbing
     recollection of Jonny Land's puzzling machine into his mind?</p>,
     <p>"You're getting to like it better here, aren't you?" asked Marn.</p>,
     <p>She was usually so silent with him that Carlin glanced quickly at
     her profile as she drove. It struck him with surprise that she had a
     certain beauty. Her thick mop of ashen hair, and firm-chinned face,
     and small, competent hands grasping the wheel, were oddly attractive.
     It wasn't the fine-edged, shimmering beauty that Nila had, but it had
     appeal.</p>,
     <p>"Yes, I must be getting more accustomed to it," he answered her
     question. "And it's not as provincial as I thought. Nearly every man
     you meet here has been to space some time or other."</p>,
     <p>"Every Earth boy runs away to space sooner or later," she said, and
     smiled. "Following space is in our blood. And our planet's so poor now
     that it's the only way most of our men can make a living." She added,
     "Some of our men never come back. My father didn't. And my mother died,
     when he was lost."</p>,
     <p>It was dusk when they reached the spaceport. As he walked with the girl
     along its edge toward her brothers' ship, she drew him aside toward a
     tall shaft that loomed up spectrally in the twilight.</p>,
     <p>"This is where the first Earthman went away to space," she told him.</p>,
     <p>He looked at the deeply engraved legend on the pedestal of the soaring
     column. It was the Monument to the Space-Pioneers.</p>,
     <p>"Gorham Johnson took off in his first flight from this very spot," Marn
     said.</p>,
     <p>Carlin strained his eyes in the dusk to read the roll of names and
     dates engraved on the pedestal.</p>,
     <p class="ph1">Gorham Johnson, 1991<br/>
     Mark Carew, 1998<br/>
     Jan Wenzi, 2006<br/>
     John North, 2012</p>,
     <p>Names of the men who long ago had first dared space, the men who had
     first followed a dream to the nearby planets that then had seemed so
     far, the men who had first hurtled starward and opened up the galaxy.</p>,
     <p>"Lord, more than two thousand years ago," Carlin murmured. "Queer
     little ships they must have had."</p>,
     <p>His imagination was touched. This simple roll of names of men long dead
     somehow brought it all close to him for the first time.</p>,
     <p>Those old, pathetically flimsy ships, the enormous courage of those men
     to whom space was all one unknown abyss. He began to understand why
     tourists came from all the galaxy to see these mementoes.</p>,
     <p>"They and their little ships started it all, the whole galactic
     civilization, the vast human empire," he said musingly.</p>,
     <p>Marn was looking up at the spire towering in the dusk.</p>,
     <p>"People criticize us Earthmen for our pride. But this is why we're
     proud. We're the people who opened up the frontiers of the Universe."</p>,
     <p>Carlin nodded thoughtfully. "You've a great heritage. But perhaps you
     remember it too well. This is the present, not the past."</p>,
     <p>"You're like all the others, you think Earth's history is over," Marn
     said defiantly. "You'll find out differently. Earthmen will open up the
     last frontier of all—" She checked herself suddenly, and then said,
     crestfallen, "I'm sorry. I didn't mean to quarrel."</p>,
     <p>Carlin wanted to ask what she had meant, but Marn started on again
     through the deepening darkness toward her brother's ship.</p>,
     <p>He walked with her into the battered planet-cruiser and looked around
     curiously. It was a medium craft designed for a minimum crew, with
     oversize cyclotrons and propulsion-wave equipment, drive-plates fore
     and aft, and an unusually heavy set of heat-screen generators.</p>,
     <p>"The Hot Side of Mercury is terrible," Marn said when she saw him
     glancing at the generators. "You need the heaviest heat-screens you can
     get to prospect there."</p>,
     <p>Amidships, Carlin noticed a big, empty round room or hold. There was
     nothing in it but a skeleton of girders designed to hold something over
     a sliding plate in the floor.</p>,
     <p>He remembered Jonny's big machine in the workshop. It would fit into
     this frame. He would have liked to make further inspection but Marn had
     found the instruments she had come after.</p>,
     <p>As they emerged from the ship, a lean, uniformed figure in the dusk
     greeted them in a pleasant voice.</p>,
     <p>"Hello, Marn. I saw you walking across the tarmac. How is Jonny coming
     with his plans?"</p>,
     <p>It was a young man in the gray uniform of Control Operations, the
     agency of law and order throughout the galaxy. He bowed to Carlin.</p>,
     <p>"I'm Ross Floring, Control Operations commander here. You're the
     Earth-treatment chap staying with the Lands? Glad to meet you."</p>,
     <p>Floring was not more than thirty, an alert, clean-cut, likable young
     man. He turned back to Marn.</p>,
     <p>"How soon are Jonny and his friends planning to take off for Mercury?"</p>,
     <p>Marn looked uncomfortable. "I don't know, Ross. They have some more
     preparations to make, they say."</p>,
     <p>Carlin somehow sensed a strain in the atmosphere. There was an
     earnestness in Floring's manner that was not accounted for by his words.</p>,
     <p>"I like Jonny a lot, Marn," he said seriously. "You know that. I'd
     hate to see him have trouble on this expedition."</p>,
     <p>Marn seemed to evade his meaning. "Jonny won't have any trouble. A trip
     to Mercury is nothing for Harb and him."</p>,
     <p>"I sincerely hope he won't," Floring said quietly. "Copper isn't worth
     risking too much for. Tell him I said so, will you? And tell him I'm
     coming up some day to talk with him."</p>,
     <p>Marn was obviously eager to get away. Carlin, puzzled, followed her.</p>,
     <p>"I'll see you again, Mr. Carlin," Floring called after him pleasantly.
     "We can have a talk about home. Yes, I come from Canopus too."</p>,
     <p>It wasn't until they were in the ato-truck driving homeward that Carlin
     realized he hadn't told Floring his name or origin. Why would Control
     Operations have taken the trouble to check up on that?</p>,
     <p>"Floring seemed like a nice chap," he told Marn. The girl nodded,
     troubled.</p>,
     <p>"He is—one of the best," she said. "And he likes Jonny. But he'd
     forget everything else for his duty."</p>,
     <p>She was, obviously, thinking aloud rather than answering Carlin. He
     wondered again about that queer feeling of strain. It had sounded
     almost as though Floring were warning her.</p>,
     <p class="ph1">CHAPTER V</p>,
     <p class="ph1"><i>Desperate Play</i></p>,
     <p>The truck wheezed and groaned up the dark old road to the ridge. In the
     velvet black skies, the stars were chains of glittering light. Vega,
     Arcturus, Altair—they looked far away.</p>,
     <p>The house was dark when Marn stopped the truck behind it, though there
     were still lights out in the workshop. There was a solemn, buzzing hush
     about the starlit summer night.</p>,
     <p>"I have to take these things back to Jonny," said the girl.</p>,
     <p>"Marn, what are your brothers really planning?" Carlin asked her. "Does
     Floring know?"</p>,
     <p>She twisted uncomfortably. "Jonny told you all about their plans
     himself, didn't he?"</p>,
     <p>She was such a poor liar, she was so oddly appealing a figure in the
     starlight as she looked up at him with troubled white face, that
     sudden impulse made Carlin bend and kiss her.</p>,
     <p>Her small body was firm and warm in his hands and there was a
     breathlessness about her cool lips. But she did not move.</p>,
     <p>He looked down at her. "You don't mind, do you?" he asked.</p>,
     <p>"No, I don't mind," Marn said, her voice toneless, "It's all right for
     a star-world visitor to have a little flirtation with an Earth girl
     before he goes away, isn't it?"</p>,
     <p>"But it isn't that!" Carlin started to protest, and then stopped.</p>,
     <p>After all, what was it but that? What could it be but that?</p>,
     <p>"It's all right, but please don't again," Marn said quietly. "Good
     night, Laird."</p>,
     <p>He went into the house feeling depressed and thoughtful. He wished now
     that he hadn't had that impulse. Marn wasn't the sophisticated sort.</p>,
     <p>Lying in his bed and looking out the window at the distant spaceport
     beacons down in the valley, Carlin heard her come in and retire.
     Apparently Jonny and Harb were still working.</p>,
     <p>What were they working at really? Why had Floring been so grave in his
     veiled warning?</p>,
     <p>"Oh, the devil, it's none of my business," Carlin yawned. "There isn't
     much in this little system for them to get into trouble about. Nothing
     but eight or nine small planets and one medium sun."</p>,
     <p>Carlin suddenly sat bolt upright in bed as his mind dwelt on that last
     thought.</p>,
     <p>"The Sun? Good glory, that's what they're up to! It must be!
     Sun-mining!"</p>,
     <p>He was dismayed, horrified by the sudden flash of revelation. The
     disquieting mystery that had puzzled him since his first coming here
     suddenly shaped clearly as pieces fell together in his mind.</p>,
     <p>"They wouldn't be so crazy as to try it, surely! Yet it all fits
     together—the heat-screens on their ship, the secrecy about it all. And
     that machine I saw could be a big magnetic dredge!"</p>,
     <p>Sun-mining! Most strictly forbidden of enterprises, banned by the
     Control Council for years since the first disastrous attempts at it had
     almost wrecked certain planetary systems.</p>,
     <p>Visions of frightening possibilities crowded Carlin's mind, of a
     desperately reckless attempt unchaining catastrophe on the inner
     planets of this little system.</p>,
     <p>"But Jonny Land wouldn't try it! He's a CE, he knows what would happen."</p>,
     <p>Carlin could not convince himself. He remembered only too clearly
     Jonny's intense obsession with Earth's copper shortage, his quiet
     determination.</p>,
     <p>And Floring must suspect something of the truth! That was what had made
     the Control Officer give his grave hinted warning.</p>,
     <p>Carlin got up and feverishly dressed. He had to find out the truth,
     now, at once. If the Land brothers and their friends were really bent
     on such a mad enterprise, it would have to be stopped even if it meant
     his informing Control Operations.</p>,
     <p>"If I could get one good look at the inside of that machine of theirs,
     I could soon tell whether it's really a magnetic dredge," he thought.</p>,
     <p>He went quietly down through the dark house and out into the starlight.
     Light and sounds of activity still came from the workshop.</p>,
     <p>Carlin crept toward it. He hated this spying. But he had to know. He
     couldn't permit a crazy attempt to unloose disaster here.</p>,
     <p>The workshop was closed, and there were no windows. But as he stood
     irresolute, the big front doors opened and Loesser and two other young
     Earthmen came out, wearily mopping their brows.</p>,
     <p>"We'll be back tomorrow, Jonny," Loesser called back into the building.
     "Ought to finish her up in a few days now."</p>,
     <p>The three strode wearily toward their ato-truck and drove away. The
     doors remained open for the moment.</p>,
     <p>Carlin stepped forward and from his vantage in the dark peered into the
     big lighted room. Jonny and Harb Land were putting back the metal cover
     on the central mechanism, before they too quit work.</p>,
     <p>One glance at the interior of that machine was enough for Carlin's
     trained eyes. Those big magnetic-current coils, that massive beam-head,
     that battery of Markheim filters—he had been right, they spelled
     disaster.</p>,
     <p>A small, hard object prodded Carlin's back and a voice throbbing with
     anger spoke in his ear.</p>,
     <p>"This is an atom-pistol. Raise your hands. I don't want to harm you."</p>,
     <p>"Marn!" he exclaimed, stunned.</p>,
     <p>"Don't turn!" warned the girl. Her voice was choked with wrath. "I
     heard you get up and I followed you out here. You are a spy!"</p>,
     <p>"Don't turn!" warned the girl. "I followed you here. You are a spy!"</p>,
     <p>Carlin was so stunned with horror by his discovery of the brothers'
     catastrophic plans, that he reacted by sheer, desperate impulse to the
     weapon in his back. He swung around and grabbed for the atom-pistol.</p>,
     <p>It would have been suicidal, had another than Marn been holding the
     weapon. But Marn, as much a stranger as he to deadly violence, let her
     finger hesitate on the trigger too long. Perhaps she would not have
     fired in any case. Pondering it later, he was not sure.</p>,
     <p>What happened was that he got his hand on the slim pistol and snatched
     it out of her grasp before her hesitation ended. Marn, her face white,
     called frantically:</p>,
     <p>"Harb! Jonny!"</p>,
     <p>The two brothers came running out from the rear of the lighted
     workshop, Harb's craggy face dark and deadly as he saw them.</p>,
     <p>Carlin jumped back, leveled the weapon he had just taken from the girl.</p>,
     <p>"Get back!" he ordered hoarsely. And as Harb Land, blindly raging, came
     on: "I don't want to kill anybody!"</p>,
     <p>Jonny's voice rang command. The lame youngster's thin brown face was
     set, but he had not lost calm.</p>,
     <p>"Harb, stop!"</p>,
     <p>The thing froze into a queer sort of tableau as Harb Land pulled up
     and stood there, his giant figure quivering with wrath, his big fists
     clenched as he glared at Carlin.</p>,
     <p>"I told you," Harb said thickly over his shoulder to his brother. "I
     told you what would happen if we took him in."</p>,
     <p>Marn had run toward them, her face pale and stricken.</p>,
     <p>"It's my fault, Jonny," she said despairingly. "I heard him come out
     and followed him, but let him take my gun instead of shooting."</p>,
     <p>"Quiet, Marn," soothed Jonny. "It's going to be all right. Carlin just
     doesn't understand."</p>,
     <p>The lame youngster, in this taut moment of strain, was suddenly the
     biggest of them, the dominating personality here.</p>,
     <p>"I understand, all right," Carlin said hotly. "I guessed it tonight,
     and one look at that magnetic dredge confirmed my guess." His voice
     crackled with the rising wrath he felt. "Going to Mercury prospecting,
     were you? You never had any such plan. You and your partners have been
     getting ready to attempt sun-mining."</p>,
     <p>Jonny's eyes and voice were calm as he said:</p>,
     <p>"Carlin, Earth's starved for power. You've seen for yourself. To get
     the power that will revive our world, we've got to have copper. And
     the copper in our planets was exhausted long ago. But there's still
     billions of tons of copper in our System, in one place. The Sun. It's
     there in hot gases, more copper than Earth and our sister-planets will
     need for millenniums to come. It's our only possible source of copper
     and we intend to tap it."</p>,
     <p>"You and the others have brooded so long over your need for copper that
     you've gone crazy!" Carlin said, his voice whipped with anger.</p>,
     <p>"What's crazy about our using the copper of the Sun for our planet?"
     Jonny asked evenly.</p>,
     <p>"You, a CE, ask me that?" cried Carlin. "You know as well as I do that
     sun-mining brings catastrophe! Oh, you can get close enough to the Sun
     in your ship, I know. You can suck up all the gaseous copper you want
     from it, with that magnetic dredge. But what happens on your Sun when
     you do it?</p>,
     <p>"You know as well as I what would happen, what has always happened
     when it was tried. The suction creates a whirl in the solar surface,
     a tiny Sun-spot that grows and grows until it's grown into a terrific
     solar typhoon that pours disastrous increased heat and electric force
     onto its planets. You know it's happened every time Sun-mining was ever
     tried, and that that's why Control Council forbids Sun-mining."</p>,
     <p>Jonny Land nodded calmly. "I know all that. But suppose I've found a
     way to do Sun-mining without starting Sun-spots?"</p>,
     <p>Disbelief hardened Carlin's voice. "You haven't. Nobody ever has. There
     just isn't any way—suck out gases from any point on the Sun and you
     lower pressure at that point, and lowered pressure automatically starts
     a whirl."</p>,
     <p>"Carlin, I <i>have</i> found such a way! I tell you, with it we can suck
     unlimited copper from the Sun without creating one tiny Sun-spot!"</p>,
     <p>Laird Carlin stared. "You're telling me that, because you know I'm
     going to report your plans to Control Operations."</p>,
     <p>"You wouldn't do that!" cried Marn, incredulously.</p>,
     <p>Carlin nodded firmly. "I don't want to but I've got to. I can't let a
     bunch of crazy men bring on a disaster that might scorch life itself
     off your inner planets."</p>,
     <p>Jonny Land's thin face flared irritable emotion as he limped forward
     unheeding of the gun in Carlin's hand.</p>,
     <p>"Carlin, man, be reasonable! Why do you suppose I had you come here and
     live with us? It was because you're a CE and I'll need another trained
     engineer's help in operating this thing. And do you suppose I ever
     thought I could get your help unless I could convince you I've found
     the way to safe Sun-mining? I can convince you, Carlin!"</p>,
     <p>Carlin felt the conviction in Jonny's voice. What the crippled young
     man said did logically explain something otherwise puzzling—why they
     had taken him into their home when their work was so secret.</p>,
     <p>He remembered now that it was not until Jonny Land had learned he was
     a CE, on his first arrival on Earth, that the young Earthman had shown
     interest and offered him lodgings.</p>,
     <p>"All I ask," Jonny was saying earnestly, "is that you give me a chance
     to explain our plans to you. I know I can convince you that we can mine
     the Sun without the slightest danger of disaster."</p>,
     <p>"If that's so," Carlin demanded skeptically, "why didn't you convince
     the Control Council of that, and get permission for Sun-mining instead
     of trying to do all this in secret?"</p>,
     <p>"Carlin, I did try to convince the Council," Jonny Land declared. "I
     made one petition to them after another, giving them full details of
     my plan. But Council isn't composed of engineers. And the popular
     prejudice against Sun-mining, due to those past disasters, is so strong
     that Council refused us permission to make the attempt."</p>,
     <p>"That's why Ross Floring and the others down at Control Operations
     watch my brothers so closely, Laird," Marn added quickly. "They know
     about our petitions, and Floring suspects that Jonny is going to try
     this thing anyway."</p>,
     <p>It all fitted together logically, Carlin had to admit. Yet he still
     stood irresolute, the atom-gun in his hand.</p>,
     <p>"Here's a proposition, Carlin," said Jonny. "I'll explain every detail
     of our plan to you in the morning. If you don't admit then that the
     plan's completely without danger of disaster, I'll let you go and tell
     everything to Floring. I give you my word on it."</p>,
     <p>Carlin looked at him doubtfully. "Jonny, you'd break your word as
     cheerfully as your neck to carry out your purpose for Earth."</p>,
     <p>Jonny Land grinned crookedly. "That's true. But on the other hand,
     I'm still hoping for your help in this project. That's why I want to
     convince you, and that's the best guarantee I can give you."</p>,
     <p>Carlin shrugged, but he slowly lowered the weapon.</p>,
     <p>"I can tell you right now that I'll have no part in any such illegal
     venture," he said flatly. "But I'm willing to hear your explanation."</p>,
     <p>"Well," Jonny said, with a tired sigh, "we've had enough dramatics
     for one evening. Harb, lock up the workshop and we'll all turn in for
     tonight."</p>,
     <p>Carlin looked a little awkwardly at Marn as he handed her back the
     atom-pistol.</p>,
     <p>"I'm sorry if I appear ungrateful for your hospitality," he told her.
     "It's just that I can't stand by and do nothing if a crazy attempt
     threatens to bring on catastrophe."</p>,
     <p>"I know," Marn said soberly, and there was no hostility in her face.
     "But you'll find out that Jonny knows what he's doing."</p>,
     <p>Out of the darkness behind them spoke a shrill voice that made Laird
     Carlin swing around in astonishment.</p>,
     <p>"Well, I'm blamed glad you people quit arguin' for tonight, anyway.
     It's time all decent folks was in bed."</p>,
     <p>Gramp Land stood back there in the dark where he had apparently been
     standing for some time. There was a grin on his withered face as he
     lowered the heavy atom-gun he had been holding.</p>,
     <p>"Sure got tired holdin' this thing aimed at your back, Mr. Carlin," he
     chuckled.</p>,
     <p class="ph1">CHAPTER VI</p>,
     <p class="ph1">"<i>You Owe a Chance to Earth!</i>"</p>,
     <p>Doubts assailed Carlin almost as soon as he retired. He could not
     sleep, the rest of that night.</p>,
     <p>Had he been childish to let Jonny persuade him into giving the plan a
     hearing? Jonny was sincere enough, but he was a fanatic on this one
     subject of securing power for Earth.</p>,
     <p>The recklessness of Earthmen was proverbial. These men, made desperate
     by long brooding over the poverty of their world, might think little of
     the danger of provoking solar catastrophe in their obsessed desire to
     secure copper.</p>,
     <p>Carlin chilled. He remembered what had happened years ago at the star
     Mizar when Sun-mining had been attempted. The suck of magnetic dredges
     swiftly creating a whirl in the star's surface gases, a Sun-spot
     maelstrom that had expanded with disastrous swiftness. And then the
     engulfing of the mining ships in the sudden outpour of increased heat,
     the scorching of inner planets that wreaked ruin before the spots
     subsided.</p>,
     <p>It had been the same later at Polaris, and at Delta Gemini. No wonder
     that such a popular wrath against Sun-mining had arisen that Control
     Council had strictly forbidden further attempts! Man's science, great
     as it was, was not yet great enough to dare tampering with stars.</p>,
     <p>Yet he could see, too, how these Earthmen would inevitably turn their
     thoughts to Sun-mining. There was not any copper left in their System
     except in one body—their Sun. And that had limitless amounts of the
     power-metal, in vaporized form. No wonder they had been led into the
     plan to tap the metal of their Sun.</p>,
     <p>Carlin dozed before daybreak, but woke with the sunrise and went down,
     to find the others already at breakfast. They greeted him with a word,
     all but Harb Land who maintained a stony, dangerous silence.</p>,
     <p>"We'll go out and show you our work, as soon as you have breakfast,"
     Jonny said quietly.</p>,
     <p>Gramp Land was the only one in good spirits. The old man twitted Carlin.</p>,
     <p>"It's sure a good thing you got reasonable last night. I would have
     hated to blast you."</p>,
     <p>Marn smiled slightly. "You wouldn't have done it. You're too
     chicken-hearted even to kill a fly."</p>,
     <p>"Ho, what are you talking about?" exclaimed Gramp indignantly. "When I
     was young, they called me the toughest Earthman in space."</p>,
     <p>Carlin walked silently out to the workshop with Harb and Jonny. The
     lame youngster opened the building, and then gestured toward the tall,
     cylindrical machine.</p>,
     <p>"Take a look for yourself, first," he invited.</p>,
     <p>Carlin scanned the mechanism with trained eyes. Magnetic dredges were
     a little out of his line, yet the principle of the mechanism was clear
     enough.</p>,
     <p>"You understand the basic idea of Sun-mining?" Jonny was saying.
     "A ship approaches the photosphere or visible surface of the Sun
     as closely as possible, protected by heavy heat-screens from the
     radiation. The magnetic dredge is then turned on. The dredge generates
     a high-powered magnetic field concentrated into a beam. That beam
     drives down into the swirling super-hot gases of the solar surface.</p>,
     <p>"Those gases consist of dozens of metals and other elements in
     vaporized form—iron, copper, sodium, calcium and so on, all mixed
     together. The beam sucks a column of those solar gases up to the
     ship. For its magnetic pull powerfully attracts the iron vapor in the
     mixture, and so the whole mixture is rapidly sucked upward."</p>,
     <p>He pointed to the massive flared nozzles in the downward projector-face
     of the great machine.</p>,
     <p>"The gases are sucked in there, through Markheim filters which can be
     set to screen out the atoms of any desired element. The copper gases
     are screened out, solidified by cooling, and stored. The other gases go
     on through the filters."</p>,
     <p>Carlin nodded curtly. "And those unwanted gases are ejected into space,
     and more of the solar mixture continuously drawn up, and so on until
     your ship is filled with copper. Yes, it's the same scheme that was
     used by the Mizar and Polaris Sun-miners. And it will have exactly the
     same result! Sucking gases out of any point in the solar surface will
     lower pressure at that point. And lowered pressure at any point of the
     photosphere instantly and inevitably starts a whirl of gases, a growing
     maelstrom or Sun-spot!"</p>,
     <p>Jonny Land shook his head. "Carlin, you're jumping to conclusions. This
     dredge does not simply eject its unwanted gases into space like former
     designs. Take a look at that beam-head more closely."</p>,
     <p>Carlin looked. And he was puzzled, after a brief inspection of the
     curious concentric construction of the beam-head.</p>,
     <p>"I don't get it. It looks like you have two circular beam-heads, one
     inside the other."</p>,
     <p>"That," said Jonny, "is the secret of my scheme. Lowered pressure in
     the solar surface at the point of suction creates a whirl, a Sun-spot.
     But suppose we can suck up gases without lowering pressure?"</p>,
     <p>Carlin stared. "How?"</p>,
     <p>"The two beam-heads," reminded the lame youngster eagerly. "The inner
     one is the one that beams down a positive magnetic pull to suck up
     solar vapors. The outer one is designed to use a simultaneous negative
     magnetism to shoot the unwanted vapors back down into the Sun."</p>,
     <p>The whole meaning of the explanation flashed over Carlin, and the
     possibilities of it dawned across his brain.</p>,
     <p>He said nothing, but crawled under the towering dredge and for minutes
     inspected inside and outside of the beam-head, feed-tubes and cut-offs.
     He finally came back out to them.</p>,
     <p>"Well?" challenged Jonny Land.</p>,
     <p>Carlin bit his lip. "I've got to admit your scheme looks practical
     enough. You should be able to suck up gases without any Sun-spotting
     effect, by using that continuous kickback. But—"</p>,
     <p>"But what?" demanded Harb Land, frowning.</p>,
     <p>Carlin shook his head. "Blast it, I can't see why the Council would
     turn down your petition if this is as workable as it seems."</p>,
     <p>Jonny shrugged. "I told you why. Control Council contains the finest
     statesmen in the galaxy. Statesmen, not engineers. They admitted their
     experts' reports on this showed it theoretically workable. But they
     said it was too dangerous to take a chance on theory when it comes to
     tampering with suns. We don't need copper that badly, they said."</p>,
     <p>His fists clenched in sudden passion. "We don't need copper! The galaxy
     as a whole doesn't need it, they meant. And what does it matter if one
     little world called Earth is fading and dying for lack of the copper
     it squandered to open up the galaxy? What does it matter, except to
     Earthmen?"</p>,
     <p>It was the first time that Carlin had ever seen Jonny Land give way to
     emotion. The superhuman strain that drove and dominated this lame, thin
     youngster for a moment flared hot and anguished on his face. Then his
     narrow shoulders sagged. He stood looking at the towering dredge with
     brooding eyes, before turning to Carlin.</p>,
     <p>"Carlin," he said then, "there's only one way to prove to the Council
     this way of Sun-mining is safe—and that's by doing it! That's what
     we're going to do. We're going to the Sun and come back with a shipload
     of copper. They'll see then that it's wholly safe. They'll have to
     give permission then. And a fleet of ships equipped with dredges can
     suck enough copper from the Sun to give Earth all the power it needs
     hereafter.</p>,
     <p>"You've seen the dredge and you know our plans. You've seen enough of
     Earth to know how much our success would mean to this world. Carlin, do
     you still want to tell Floring about this?"</p>,
     <p>"You couldn't!" exclaimed Harb Land harshly. "You couldn't destroy all
     the hope that's left for our world's people. You—all you star-world
     people—you owe this chance to Earth!"</p>,
     <p>Carlin stood there, torn by conflicting feelings. Strong among them was
     his intense admiration as an engineer for the ingenuity and daring of
     Jonny Land's solution to the problem.</p>,
     <p>But there were other things to consider. There was the duty he and
     every citizen had to support the Control Council. That support was what
     kept galactic civilization going. Yet these Earthmen, this little band
     fighting so fiercely for their ancient, worn world would flout it.</p>,
     <p>"Jonny!" came Marn's sharp cry from outside. "Jonny!"</p>,
     <p>"Something's wrong!" Jonny exclaimed, limping hastily forward.</p>,
     <p>They hurried out into the sunlight. Marn was running toward them and at
     the same moment they heard the drumming of an approaching ato-car.</p>,
     <p>"It's Ross Floring coming here!" Marn panted. "I recognized his car
     coming up the hill!"</p>,
     <p>Harb uttered a fierce exclamation, but Jonny cut in quickly:</p>,
     <p>"He's only coming up here to look around. He suspects what we're up to,
     but he can't be sure. Don't show any excitement."</p>,
     <p>Harb gestured fiercely toward Carlin. "But if he says anything, Floring
     will know."</p>,
     <p>A pleasant voice hailed them. Ross Floring, lean in his gray uniform,
     drove up behind the house and climbed out of his ato-car.</p>,
     <p>"Hello, folks," he greeted. "Thought I'd come up and see you. Jonny, I
     haven't seen you for weeks. Every time you come down to the spaceport,
     you spend all your time buried in that ship."</p>,
     <p>Jonny smiled. "It's keeping us pretty busy, getting ready."</p>,
     <p>Laird Carlin sensed genuine liking between the Control Operations
     officer and the lame young engineer. Yet there was unspoken tension
     too. It showed behind Jonny's cool smile and Floring's pleasant eyes.</p>,
     <p>Floring was looking past them, through the open doors of the workshop
     at the towering magnetic dredge.</p>,
     <p>"Is that your new metal-finding dingus, Jonny? The thing you're going
     to use to locate copper on Mercury?"</p>,
     <p>He stepped toward it. Harb Land made a violent movement forward, but a
     flat look from his brother stopped him.</p>,
     <p>"Yes, that's it," Jonny said. "Want to look it over, Ross?"</p>,
     <p>Floring stood, cocking his head at the towering machine. He laughed at
     the question.</p>,
     <p>"Jonny, you know I'm no engineer. A thing like this is beyond me." He
     turned toward Carlin. "But Mr. Carlin, you're a CE. What do you think
     of this new metal-finding device of Jonny's?"</p>,
     <p>Breathless silence held the group for a moment. Floring's face was
     unmoved, pleasant, but his purpose was obvious now. Knowing that Carlin
     had come to Earth merely as an Earth-treatment case, he was counting on
     Carlin's unbiased truthfulness.</p>,
     <p>Carlin felt their eyes on him. Now was the time, he knew, to play the
     part of a good galactic citizen and inform Floring just what was going
     on. It was his duty to do it.</p>,
     <p>But he couldn't! He couldn't betray the last desperate hope of a
     gallant old planet's people in their struggle against destiny! He had
     known he couldn't, from the time Floring had first appeared. He spoke
     as casually as he could.</p>,
     <p>"Yes, I've looked it over. It's one of the most ingenious metal-finders
     I've ever seen."</p>,
     <p>Carlin felt a queer relief that was almost happiness, as he spoke. For
     he knew now that he could never have obstructed these people in their
     brave, desperate struggle to revive their planet.</p>,
     <p>But Ross Floring looked astounded. A little blank frown of surprise
     came into his face and he stared steadily at Carlin.</p>,
     <p>"Then you approve of Jonny's plans?" he said quietly, "But, of course,
     I might have known that he'd convince you."</p>,
     <p>There was double meaning to the Control officer's words, clear to all
     of them. Yet they all ignored it.</p>,
     <p>Floring was temporarily defeated. He couldn't take action without
     expert opinion that the machine before him was for Sun-mining. He had
     expected such an opinion from Carlin, and had been disappointed.</p>,
     <p>But he was not completely frustrated. Carlin found out now how
     thorough and resourceful was this pleasant young officer.</p>,
     <p>"It would be a shame, Jonny," Floring remarked casually, "if you should
     run into disaster on this trip and the design of your new apparatus be
     lost. A metal-finder like this is too valuable to lose."</p>,
     <p>They were momentarily puzzled by the comment. But in the next moment,
     Floring showed what he had in mind. He drew from his jacket pocket
     a tiny tri-dimen camera, stepped close to the towering dredge, and
     before anyone could prevent it had snapped a half-dozen pictures of its
     interior mechanism.</p>,
     <p>Harb Land started forward with a smothered oath. But it was too late.
     Floring was already pocketing the camera.</p>,
     <p>"I'll keep these films," he said calmly. "If your machine should ever
     be lost, the design of it will be preserved this way."</p>,
     <p>"You can't keep those films!" Harb Land exclaimed angrily. "You've no
     right!"</p>,
     <p>"You surely don't think I would steal the design from you?" Floring
     said, with a look of surprise.</p>,
     <p>"It isn't that," Harb protested. "But—"</p>,
     <p>"But what?" the officer asked calmly.</p>,
     <p>Harb was silent, his craggy face a mixture of emotions as he looked
     appealingly at Jonny.</p>,
     <p>Carlin understood Floring's cleverness. They could not protest the
     films without giving the real reason for their protest, and that they
     could not do.</p>,
     <p>"It's all right for him to keep those pictures, Harb," Jonny said
     quietly.</p>,
     <p>Floring turned, bidding a pleasant farewell.</p>,
     <p>"I'll be seeing you again soon," he promised.</p>,
     <p class="ph1">CHAPTER VII</p>,
     <p class="ph1"><i>Last Frontier</i></p>,
     <p>As soon as Floring's ato-car had purred away, the little group stood in
     the sunlight outside the workshop, in stricken silence.</p>,
     <p>Carlin put into words what was in all their minds.</p>,
     <p>"Jonny, you know why he took those pictures! He'll telephoto them to
     Canopus headquarters to be examined by engineer experts, and they'll
     send back word that the machine is a magnetic dredge for Sun-mining!"</p>,
     <p>Jonny nodded. "Yes, of course. Floring has suspected our plans all
     along, and now he's going to make sure."</p>,
     <p>"And when word comes back from Canopus, he'll seize our dredge and ship
     to stop our expedition!" groaned Harb.</p>,
     <p>"I know that," Jonny Land said, as his blue eyes swept them. "But it
     will take fourteen or fifteen hours before he gets that report back.
     Before that time ends, we've got to be on our way to the Sun!"</p>,
     <p>Laird Carlin felt a shock of astonishment, but before he could comment,
     Jonny was speaking swiftly on.</p>,
     <p>"It's our only chance now—to get away before Floring receives the
     proof that will authorize him to stop us! The dredge here is almost
     finished. If we can install it in the 'Phoenix' and take off tonight,
     we'll have our chance to prove to the galaxy that Sun-mining can be
     safe."</p>,
     <p>"Install the dredge tonight?" cried Harb Land. The gangling giant's
     face was sick with anxiety. "Jonny, we can't do it! Not that soon."</p>,
     <p>"We've got to!" Jonny's voice cut like a steel rapier. "Harb, you go
     get Loesser and Vito and the other boys. Have them bring the big truck
     with them. If we work hard enough, we should be able to have the dredge
     ready to roll by dark. Once we get it into the 'Phoenix', we can take
     off and complete installation in space."</p>,
     <p>"You can't do it," groaned his brother. "You know you figured on taking
     a week yet for that installation."</p>,
     <p>Carlin stepped forward. He had long ago reached his decision. He had
     reached it in that moment when he had answered Floring.</p>,
     <p>"I'm a CE, you know," he reminded. "I can help a lot in that
     installation."</p>,
     <p>Marn stared at him, amazement and dawning gladness in her eyes. And
     Harb Land's tortured face turned haggardly on Carlin.</p>,
     <p>"You'd do that? You'd help us? By heaven, if you would, we might make
     it!"</p>,
     <p>Jonny's brilliant blue eyes bored Carlin's face.</p>,
     <p>"Carlin, I was hoping for this. I knew from the first I'd need another
     engineer's help in installing and operating the dredge. I brought you
     home because I was hoping I could enlist your aid before we started on
     the expedition. But all the same, I've got to warn you. We're directly
     bucking a Control Council order. You can lose your certificate and go
     to Rigel prison, even if our plan succeeds. And if it doesn't succeed,
     it may mean perishing with us. And after all, Earth isn't your world."</p>,
     <p>"Who the devil is doing anything for Earth?" Carlin retorted. "This old
     planet of yours means nothing to me either way."</p>,
     <p>"Laird, are you so sure of that?" Marn asked him, her eyes very bright.</p>,
     <p>"Do we have to get emotional?" Carlin asked roughly. "I'm an engineer,
     and this is the biggest engineering experiment to be tried for
     centuries. Don't you think I want to be in on it?" He added crushingly,
     "And as for my getting mixed up in the blame, I'm already blasted well
     mixed in it. When I denied to Floring that this was a magnetic dredge,
     I implicated myself right there in the whole business. I've got to make
     it succeed, now."</p>,
     <p>Harb Land was already running toward his truck. Jonny shot sharp orders
     at his sister.</p>,
     <p>"Marn, I want you and Gramp to watch the road this afternoon. Floring
     might come back. Carlin, you and I haven't a moment to lose."</p>,
     <p>Carlin strode after the limping youngster into the workshop, and Jonny
     there rapidly explained what remained to be done.</p>,
     <p>"The kickback feed-pipes to the beam-head have to be hooked up, the
     cooling coils to solidify the copper are not yet in place, and the
     whole dredge has to be fastened in its frame so it'll be ready to swing
     aboard the truck tonight."</p>,
     <p>Carlin was appalled by the amount of work that remained, for two pairs
     of hands. But Jonny added an encouraging qualification.</p>,
     <p>"Loesser and Harb and the others can help in the ato-welding and cable
     work if we set it up for them. They're all veteran spacemen and know
     how to handle ordinary tools."</p>,
     <p>Carlin plunged into the work with Jonny. But as they toiled to set up
     the coils and feed-pipes of the massive mechanism, an inward aghastness
     at what he was doing oppressed Carlin's mind.</p>,
     <p>Why was he doing it, breaking Control law and endangering his
     certificate and even his liberty? Why under heaven should he be sharing
     the risks of these men for a planet he hadn't even seen until a few
     weeks ago?</p>,
     <p>"I must still be star-sick, unstable," he thought dismally. "Or I'd
     never have got mixed up in this mad business. Sun-mining!"</p>,
     <p>Blind reaction was dominating him. Curse it, he wasn't the type to
     join Quixotic forlorn hopes. He was Laird Carlin, sober, hard-working
     engineer, who ought right now to be far across the galaxy at the job to
     which he belonged.</p>,
     <p>And all the time Carlin's mind spun miserably to this whirl of
     self-reproach and foreboding, he was working with Jonny at topmost
     speed, squeezing into the frame of the great dredge where the lame
     youngster could not go, fastening Veer-clamps, hooking self-sealing
     leads to the flat Markheim filters.</p>,
     <p>The sound of ato-trucks rocked the noon air, and Harb Land came running
     heavily into the workshop.</p>,
     <p>"I got the others—Loesser's bringing in the big truck now," panted
     Harb. "What do you want us to do, Jonny?"</p>,
     <p>Loesser, and Vito, and the other four young Earthmen who came hastening
     after Harb were dominated by excitement. Loesser's broad red face was
     shining with emotion as he came up to Carlin.</p>,
     <p>"I want to apologize. I never thought any star-world stranger would
     come in with us and help us."</p>,
     <p>"Save it, and get the welders on those rear feed-pipes," Carlin
     retorted. "Get in here—I'll show you."</p>,
     <p>Through the hot afternoon hours, the hiss of ato-welders and reek of
     fusing metal stifled the workshop.</p>,
     <p>Dripping with perspiration, stiff from cramped postures, Carlin worked
     on inside the great dredge.</p>,
     <p>And all those hours, in rhythm with the welders' hiss and the clang of
     wrenches, his thoughts beat a mocking tempo through his brain.</p>,
     <p>"All this, for no reason! For somebody else's world, a world that ought
     to have been evacuated long ago! Even if it succeeds, you win nothing.
     And if it fails, the Sun licks you all up like midges."</p>,
     <p>Yet he labored blindly on. It might be crazy, but what he had started,
     he would finish.</p>,
     <p>It was work against an inexorable time limit that rapidly was
     approaching. As the shadows lengthened, as the sun went down, they
     still had not finished.</p>,
     <p>Jonny Land limped unsteadily to turn on the workshop lights. His face
     was a gray mask of fatigue and sweat as he turned to the others.</p>,
     <p>"Two more hours," he said huskily. "We can't take more, if we're to get
     the dredge into the 'Phoenix' and take off before midnight."</p>,
     <p>Those two hours, afterward, seemed weeks in length to Carlin. And the
     mocking devil in his brain kept taunting, "It's no business of yours,
     you know!"</p>,
     <p>"That's near enough!" Jonny's hoarse voice finally declared. "We can
     hook up those last cables on the way. All the work that require heavy
     tools is done—and we daren't take more time."</p>,
     <p>They were, all of them, drunk with fatigue, staggering with the furious
     drive of twelve hours of unbroken toil. Blackened by welder flare,
     glistening with sweat, they looked to Carlin like a crew of devils.</p>,
     <p>Jonny's driving energy remained unconquerable.</p>,
     <p>"Marn," he ordered, "back the big truck in here. Harb, you and Carlin
     rig the hoist."</p>,
     <p>The big, flat-bodied ato-truck backed ponderously into the workshop
     and they swung the massive magnetic dredge carefully aboard. Loesser
     and the others then hastily chained it to the bed of the truck.</p>,
     <p>Jonny limped toward the cab. "All right, we're starting. Harb, you
     drive. No, Marn—you're not going to the spaceport with us."</p>,
     <p>Marn, face white and eyes big with fear, saw the gleam of the
     atom-pistol that Harb was thrusting into his pocket.</p>,
     <p>"Oh, Jonny, not that, no matter what happens!"</p>,
     <p>Jonny's blue eyes flashed arctic light. "That, or anything, now," he
     rasped. "You know what this means to our people, Marn."</p>,
     <p>Then his face softened, and he patted her arm.</p>,
     <p>Tears streaked her cheeks as she kissed and clung to him, and then to
     Harb.</p>,
     <p>Carlin was climbing heavily onto the truck when he felt her touch on
     his arm.</p>,
     <p>"You too, Laird," she whispered, quivering lips blindly pressing his
     cheek. "All of you must come back."</p>,
     <p>"Get on!" cried Harb Land, and then the truck went into gear.</p>,
     <p>Carlin jumped for the cab, and under the starry night they were rolling
     at increasing speed down the twisting road toward the valley.</p>,
     <p>And suddenly all the nightmare mocking in Carlin's brain was gone and
     there was only the rush of sweet air against his face, and the splash
     of the lamps ahead, and the jolt and rumble of the big machine as they
     raced down toward the spaceport's distant beacons.</p>,
     <p>Earth air and Earth smells in Carlin's nostrils, sleepy Earth sounds
     in his ears; the shine of the old spaceport's beacons, and the soaring
     loom of the distant tower that marked the spot where a man of long ago
     had first dared space. This world, this little Earth, was worth risking
     death for, even for a stranger from far stars!</p>,
     <p>He knew he was a little crazy, he still had a corner of his mind that
     told him all this was mere intoxication of emotion which was sweeping
     away reason. But the mocking devil in Carlin's mind was gone, and he
     was one in mind and purpose with his companions, now.</p>,
     <p>The others too were feeling that wild reaction, for Loesser clapped
     Carlin's shoulder, crying:</p>,
     <p>"It's like getting out of prison to get started!"</p>,
     <p>"We're not off Earth yet!" warned Jonny. "Cut the lights and drive
     around to the north end of the spaceport, Harb. Ease the truck to the
     'Phoenix' as quietly as you can." A little later he warned, "Slower,
     slower. Keep to the edge of the tarmac."</p>,
     <p>Lightless, its motors a mere low rumble, the big truck crept around the
     dark edge of the spaceport toward the "Phoenix." The little planet-ship
     took black shape in the darkness, a low, torpedo bulk brooding beneath
     the stars. Harb backed the truck toward its side, as they jumped out of
     the cab.</p>,
     <p>Light flashed on them from a hand-krypton in the door of the "Phoenix!"
     A lean, uniformed figure stood there, gun in hand, looking at them.</p>,
     <p>"I thought you would be coming," said Ross Floring quietly. "Jonny, I'm
     sorry about this."</p>,
     <p>Carlin was as frozen as his companions, by the disastrous overturn of
     their attempt at secrecy. Floring stepped out of the ship.</p>,
     <p>"I've been looking through your ship while I waited," he said. "You
     have triple as much heat-screen coverage as you'd need for the Hot Side
     of Mercury. You were going to the Sun."</p>,
     <p>"You can't prove it, Ross," Jonny said levelly. "You've no proof."</p>,
     <p>"I've enough to prohibit this ship from clearing Earth until
     investigation," Floring replied. "A certain report will reach me from
     Canopus by morning. Then we'll see."</p>,
     <p>Carlin saw it then, saw the dark giant figure of Harb Land stealing
     around the truck and looming up behind Floring. He glimpsed the gleam
     of Harb's raised atom-pistol.</p>,
     <p>Then Harb struck. The butt of the weapon came down on Floring's head
     and the officer crumpled limply to the tarmac.</p>,
     <p>"See if anyone else is in the ship!" Jonny said swiftly. "Loesser,
     watch the Control station!"</p>,
     <p>Then he bent with Carlin over the unconscious man.</p>,
     <p>"We'll have to take him with us," Jonny said. "If we leave him here
     he'd soon be found, then the Control cruisers would be after us."</p>,
     <p>A few weeks before, Laird Carlin would have been aghast at seeing
     a semi-sacred officer of Control Operations struck down. With what
     spirit of reckless defiance of law had his companions infected him? He
     marveled at himself as he coolly picked up the limp figure.</p>,
     <p>"Tie him into one of the chairs in the pilot room," Jonny was saying.</p>,
     <p>Harb came plunging out of the ship. "Nobody else aboard. He came over
     here alone."</p>,
     <p>By the time Carlin had the unconscious man secured in the pilot room,
     Harb and the others had slid open the big hatch in the side of the
     "Phoenix." Hastily, fumbling in darkness, they ran out the ship hoist
     and hooked onto the big magnetic dredge.</p>,
     <p>Then, with infinite labor, they swung the massive mechanism into the
     hold amidships. Mere short flashes of hand lamps had to suffice to
     guide the beam-head of the dredge down into the round keel opening.</p>,
     <p>"Fasten half the frame bolts—they'll hold till we get into space,"
     panted Jonny.</p>,
     <p>Carlin skinned his knuckles in the dark, fumbling with bolts and
     wrench. Every instant he expected to hear an alarm from Loesser that
     Control officers were coming.</p>,
     <p>"That'll have to hold," said the sweating Jonny. "Run the truck off the
     tarmac. Harb, make ready for take-off!"</p>,
     <p class="ph1">CHAPTER VIII</p>,
     <p class="ph1"><i>Solar Struggle</i></p>,
     <p>Oxygenators started throbbing, doors clanged, as the others tumbled
     aboard. Harb Land, smeared with dirt and oil, his shock of hair wild,
     climbed into the pilot seat and expertly touched controls.</p>,
     <p>"Generators coming on!" sang Loesser's breathless voice from the
     interphone, as the low, deep hum began.</p>,
     <p>"Stasis on," said Harb rapidly, his fingers busy. The blue cushion of
     force was around them as Carlin slumped drunkenly into a seat. "Zero,
     two and five acceleration schedule. Here we go!"</p>,
     <p>And the "Phoenix" swept up with a rush from the spaceport, the
     propulsion-waves streaming from its drive-plates hurling it out and
     upward into the star-sown sky, the spaceport lamps and the southward
     blinking lights of New York falling swiftly away.</p>,
     <p>"Authorization!" yelped a startled voice from the universal communic on
     the panel. "Give authorization for take-off!"</p>,
     <p>"Authorization already given," Harb Land rapped back, then cut the
     communic. He laughed. "That'll puzzle them a while."</p>,
     <p>Crazy, reckless, suicidal, to Carlin seemed the way that Harb was
     taking them out from Earth. The atmosphere of the planet had no sooner
     started a shrill, rising scream around them than it fell and faded as
     they came out of the envelope of air.</p>,
     <p>Luna burst up out of the eastern heavens like a great globe of dull
     gold against the stars. And then Carlin's eyes were smitten by the
     flare and glare of the brilliant disk of Sol, of the Sun.</p>,
     <p>And then the "Phoenix" lined out and was plunging headlong through the
     void at a speed that Carlin knew was flatly illegal to use inside any
     System, a rush toward that distant Sun flare.</p>,
     <p>"Cut down, cut down!" cried Jonny to his brother. "Any more speed and
     you'll not be able to decelerate in time to orbit around the Sun."</p>,
     <p>Harb Land turned a wild, dirty face aflame with emotion. "By heaven,
     we're on our way at last! We'll show them now that Earthmen can still
     blaze a space-trail nobody else has dared!"</p>,
     <p>And from back amidships came a hoarse voice jubilantly singing the old
     Earth space-song:</p>,
     <p>Jonny Land's voice lashed them, his thin face dripping and determined.</p>,
     <p>"You're all of you blowing your tops with excitement. This hasn't even
     started yet. Look at what we're heading for!"</p>,
     <p>Carlin heard the others fall silent and himself felt a chill of awe as
     he looked ahead at the giant fire orb toward which the "Phoenix" was
     plunging.</p>,
     <p>"We'll be orbiting before we have the dredge set up, unless we hurry,"
     Jonny prodded. "Come on, help me with it."</p>,
     <p>The big magnetic dredge had to be bolted into place, the coils and
     pipes had to be hooked to their connections inside the ship, the cables
     to the generators, the cooling coils to the compressor, the outlets of
     the Markheim filters to the bunkers astern.</p>,
     <p>Thrumming, creaking, shivering in every strut to the blind thrust of
     power that was hurling it on, the "Phoenix" rocked and shook about them
     as Carlin labored with Jonny and two of the other men to make those
     last connections. The cramped space in the hold around the dredge was
     hot, stifling, for the oxygenators couldn't keep the air there pure.</p>,
     <p>"All ready!" Jonny called finally, after eternal-seeming hours of toil.
     "And none too soon. We're getting there fast. Harb has put out most of
     the heat-screens."</p>,
     <p>Through the windows, the ship seemed enveloped by a halo of dim light,
     the force-screens that repelled radiations of heat.</p>,
     <p>But when Carlin stumbled with Jonny into the pilot room, they were half
     blinded even through the screens by the fierce, blazing glare from
     ahead.</p>,
     <p>Half the sky ahead was Sun, a gigantic abyss of roaring flame that
     crushed the mind by its magnitude. All directions of space seemed
     canceled, and they were falling, falling, into an inferno of fire.</p>,
     <p>Harb turned a sweating face. "We'll cut off to orbit in less than an
     hour," he informed.</p>,
     <p>Ross Floring spoke from the chair in which he was tied, and in which he
     had come back into consciousness.</p>,
     <p>"Jonny, I've been waiting for you! Harb wouldn't listen to me. You've
     got to turn back!"</p>,
     <p>Jonny shook his head. "No use, Ross, I know you're only doing your
     duty. And I'm sorry to drag you into this danger. But we're not
     stopping now."</p>,
     <p>"But you'll never get there!" Floring exclaimed. "Control cruisers must
     already be after you. They'll have found out where I am by now."</p>,
     <p>"Empty threats!" Harb jeered. "They can't know where he is."</p>,
     <p>"Jonny, look at my badge!" cried Floring. "See the tiny radio bulb in
     the back of it? It's a 'finder' by which any Control officer can be
     located at any distance. When I didn't report back, they'd use it to
     spot me out here."</p>,
     <p>"If that's true," said Jonny Land, his thin face suddenly haggard,
     "they'll be after us by now. Harb, cut the communic back in!"</p>,
     <p>Harb obeyed. Roar of static from the gigantic orb ahead was a dull
     background to the sharp voice that came from the instrument.</p>,
     <p>"Control Operations squadron four hundred thirty-three nine calling
     'Phoenix!' Last warning! We are overhauling you and will shell you
     unless you turn and surrender."</p>,
     <p>Startled, Harb Land jabbed a button and twisted the knob of the
     visor-screen. The far-seeing eye quartered space behind them, and then
     the black space scene held steady. There against the stars came a
     little pattern of four tiny triangles of light. Triangles—galaxy-wide
     sign of Control.</p>,
     <p>"By heaven, they actually have come after us!" cried Harb. "Jonny,
     they're only minutes behind us and pulling up fast!"</p>,
     <p>"We broadside as soon as we range you unless you turn now," warned the
     steely voice from the communic.</p>,
     <p>Laird Carlin, only a few weeks before, would no more have dreamed of
     disobeying a Control Operations command than he would have of picking
     stars from the sky. Galaxy citizens were trained to revere the great
     organization that had made the Universe a place of law and order.</p>,
     <p>But the ancient independence of these men of Earth was strong in him
     now. They had already risked so much, had incurred certain penalty even
     if they now surrendered.</p>,
     <p>"Keep going!" Carlin exclaimed. "They can't follow us once you start
     orbiting close to the Sun's photosphere. No ordinary Control cruiser
     has heavy enough heat-screens to follow us into that!"</p>,
     <p>"By Jupiter, it's so!" exclaimed Harb, faint hope lighting his face.
     "But I daren't crowd on more speed now. I've got to start decelerating
     if we're to orbit correctly."</p>,
     <p>"Decelerate by plan," Jonny said grimly. "They may not range us in
     time. We'll soon know."</p>,
     <p>The "Phoenix," flying at a tangent toward the gigantic sphere of the
     Sun, was aiming to swing into an orbit around Sol as close as possible
     to its photosphere or gaseous surface.</p>,
     <p>It had to be so. No ship would ever have power enough to go that close
     to the Sun's colossal pull and hold its position by its own energy. To
     get that close and to stay that close to Sol without being drawn in to
     it, a ship had to go into an orbit around it like a tiny satellite.</p>,
     <p>The air in the "Phoenix" was already stifling hot. Jonny switched in
     another of the heat-screens, and the dim halo around the flying ship
     deepened.</p>,
     <p>Harb's fingers were flashing over the controls, decelerating, steering
     the ship in a closing spiral toward the Sun.</p>,
     <p>"Carlin, talk them out of this madness!" cried Ross Floring, aghast.
     "The cruisers will be broadsiding us in moments."</p>,
     <p>Carlin paid no attention. His eyes were on the visor-screen where the
     four cruisers now loomed big as they came closer.</p>,
     <p>Then it came. Silent, deadly, four blinding gouts of flame burst near
     the "Phoenix." Four salvos of atomic shells whose wave of force rocked
     the plunging ship. Loesser came tumbling into the pilot room, red face
     glistening.</p>,
     <p>"They'll bracket us next salvo or two!" he yelled. "What's our chance?"</p>,
     <p>"Turn on heat-screens Six and Seven!" roared Harb Land, without looking
     around. "I'm going into orbit now!"</p>,
     <p>"It's too soon!" Jonny cried warning. "It's—"</p>,
     <p>Carlin saw that Harb hadn't even heard. The giant was recklessly
     cutting the elements of their plotted course, depending on their own
     power to pull into orbit in time.</p>,
     <p>The heat-screens, all they had, were on full now. Another salvo burst
     to spaceward of them. Carlin knew the men behind realized Floring was
     aboard. But Control Operations would sacrifice any men to prevent the
     Sun-mining that always before had meant disastrous solar disturbances.</p>,
     <p>"Great blazing stars!" breathed Loesser, staring. "Look at that!"</p>,
     <p>Forgotten, the deadly shells that were groping for them. For now the
     "Phoenix" was deep in the awesome corona of the star and was curving in
     closer through heat that was over two thousand degrees.</p>,
     <p>Carlin's mind shook to the fearful spectacle that was the firmament.
     Not he, nor any other living man, had ever come so close to a star.
     They were entering a region of such violent energies that all laws of
     space and time here seemed cancelled.</p>,
     <p>Blinding, eye-dazing even through the strong protective filter of the
     heat-screens, the brilliance of Sol stunned them. They looked on a
     vast, raging ocean of flaming gases, a sea of vaporized metallic and
     non-metallic elements that was like a cosmic furnace.</p>,
     <p>Even through the heat-screens, the radiance heated the air in the ship
     scorchingly. But now the visor-screen showed that the Control cruisers
     were falling back and disappearing from sight behind.</p>,
     <p>Blinding, eye-dazing even through the filter of the heat-screens, the brilliance of Sol stunned them.</p>,
     <p>"They couldn't follow us this close to the photosphere!" Harb cried
     exultantly. "We've shaken them and we're almost in orbit."</p>,
     <p>"You can't orbit the Sun!" Floring pleaded. "And even if you could, the
     cruisers will lay to outside the heat and range you by locator and fire
     till they destroy us! Put about!"</p>,
     <p>The man Vito, choking and gasping for breath, came into the pilot room
     from the engine rooms astern.</p>,
     <p>"Heat-screens won't take another dyne! If we go closer, we're done for."</p>,
     <p>"We're orbiting now," Jonny said huskily. "Wait!"</p>,
     <p>Harb Land was engaged in the most difficult operation of spacemanship,
     bringing a ship into exact balanced orbit around a celestial body.</p>,
     <p>Most difficult, even when the body was a planet. Impossible, nearly,
     when the body was a Titanic star!</p>,
     <p>Carlin saw the giant's face a frozen mask as he centered his dial
     needles, fed force with infinite delicacy, guided, changed—and changed
     again.</p>,
     <p>Harb reached and slammed open a switch. The hum of propulsion waves
     died. The "Phoenix" was without driving power. And the needle of the
     gravi-gauges remained constant, the ship's path around the Sun was
     unvarying.</p>,
     <p>"We've orbited!" Harb Land's voice was a hoarse, exhausted sound.</p>,
     <p>Carlin wanted to shout, "By heaven, there are no spacemen in the galaxy
     except Earthmen—none!"</p>,
     <p>The "Phoenix" was circling the Sun, deep in the corona and reversing
     layer and close to the photosphere or light-emitting surface which was
     the vague boundary of the star itself.</p>,
     <p>Their sensation was that of men suspended over a Universe of raging
     flame and force. The mind shook to the impact of it. They were here
     where no men, no life, had ever been intended to be. They were
     violating the sanctity of a star.</p>,
     <p>"Now—the dredge," Jonny said hoarsely. "We've not power enough to
     force the heat-screens like this for long. Come on, Carlin."</p>,
     <p>Carlin stumbled back with him into the stifling hold. The men around
     the towering magnetic dredge were like sooty devils staring with wild
     eyes.</p>,
     <p>The metal was so hot its touch made him cry out as he closed the
     circuit of the generators with the ato-turbines. The rotors began their
     whine, building up a magnetic field.</p>,
     <p>The whole ship suddenly shook and quivered. Harb came plunging back
     into the hold.</p>,
     <p>"Those Control Cruisers are starting to salvo us by radiolocator!"</p>,
     <p>"We only need a little time," panted Jonny Land. "The cooler coils,
     Carlin!"</p>,
     <p>Carlin felt like a man in a dream as he sweated with Jonny to get the
     magnetic dredge started. The field was building steadily, and the great
     nozzles of the beam-head had been lowered below the keel. Jonny's
     brilliant eyes clung to the panel of gauges, and finally he opened the
     field-switch.</p>,
     <p>"Now!"</p>,
     <p>They crowded around the view-plate in the keel, peering half-blindly
     down against the glare of the raging Sun-sea below. The dredge was
     projecting a powerful, concentrated magnetic field down into that ocean
     of flaming gas like a sucking straw. But for moments they saw nothing.
     Time that seemed endless went by. Then—</p>,
     <p>"Here she comes!" yelled Loesser.</p>,
     <p>A column of flaming vapor was shooting up from the fiery ocean below.
     Compared to the gigantic mass of Sol, it was the merest filament, the
     flimsiest thread of fire.</p>,
     <p>But it was rushing up and up toward the hovering "Phoenix," a finger
     of fiery vaporized elements drawn irresistibly up along the beam of
     magnetism to the ship.</p>,
     <p>Another salvo of shells went off in space somewhere close by and rocked
     the ship with its wave of force. But next instant came a heavier
     impact, as the fiery column of gas reached the nozzles below the ship.</p>,
     <p>They heard a deafening roar. That up-sucked stream of vaporized
     elements was being drawn through the heat-proof nozzles and intakes,
     through the Markheim filters that screened out its copper atoms, and
     was then being shot downward again by the kickback's negative field.</p>,
     <p>"The kickback's working!" Jonny Land yelled. "If the effect of it is
     what we calculated, we've done it!"</p>,
     <p class="ph1">CHAPTER IX</p>,
     <p class="ph1"><i>An Earthman Comes Home</i></p>,
     <p>For the moment, none of them paid any attention to the fact that
     precious copper was solidifying in the cooler coils into granules of
     metal that were being blown into the bunkers. The real test was what
     their beam of magnetic force was doing to the surface of the Sun.</p>,
     <p>Did it seem incredible, as it almost did to Carlin, that such a
     fragile finger of force could in the least disturb the mighty orb
     below? He knew better. He knew the unnaturally delicate balance of a
     star's surface, which a slight change of pressure artificially induced
     could stir into a whirl that would expand in giant Sun-spots. If that
     happened, it would mean chaos.</p>,
     <p>"No sign of a whirl yet," Jonny breathed, peering down through black
     glare-proof lenses. "No sign at all."</p>,
     <p>There was no moment of crisis, no clean-cut moment of triumph. There
     was just the time speeding by, the flow of copper into the ship, and
     the constant reports of Jonny—"No whirl forming yet."</p>,
     <p>Salvos shook the ship as the Control cruisers far outside the sun
     glare fired more and more accurately. But they went unheeded. Success
     or failure of the most audacious engineering exploit in the galaxy's
     history hinged upon Jonny's muttered reports.</p>,
     <p>"No whirl yet."</p>,
     <p>Jonny Land finally raised his head, looked at them as they stood with
     wild surmise on their faces.</p>,
     <p>"We've done it," he said, almost unbelievingly. "We've nearly filled
     the bunkers with copper and there's no whirl down there, no disturbance
     to grow into a spot. We've made Sun-mining possible."</p>,
     <p>Tears were running down Loesser's face. Harb Land looked dazed. But
     Jonny walked across the hold to the wall through which the cooler coils
     fed into the bunkers. He peered through a quartz view-plate.</p>,
     <p>They looked with him. The bunker rooms were heaped high with shining
     red granules. Copper, virgin-pure, blown into the rooms and already
     almost filling them. Copper milked from the Sun!</p>,
     <p>"Copper for Earth!" whispered Jonny, his thin face blazing now. "Power,
     and new life, for the old planet!"</p>,
     <p>The "Phoenix" rocked wildly and metal screeched rendingly as they were
     flung from their feet by a salvo that had finally bracketed the ship.</p>,
     <p>"The feed-pipes!" screeched Loesser, scrambling to his feet beside
     Carlin.</p>,
     <p>Carlin saw. The ship's walls had held, but the shock had snapped
     strained cables and cooler coils. Two intake tubes were giving way,
     white-hot copper vapor forcing out through cracks in them.</p>,
     <p>"Veer-clamps on those two pipes!" yelled Jonny. "If they give,
     everything goes!"</p>,
     <p>Knowledge of what it meant if the pipes gave way, if super-heated
     metallic vapor blew out into the hold, flung Carlin in a crazy rush for
     the Veer-clamps and wrenches.</p>,
     <p>He got a clamp around one of the pipes, and the man Vito started
     spinning shut the bolts that would hold the fracture tightly. He swung
     round toward the other pipe.</p>,
     <p>"Clamp!" yelled Jonny Land, in a cry that was like a hoarse howl of
     agony.</p>,
     <p>Carlin's blood left his heart as he glimpsed the most horrible and
     heroic sight he had ever beheld. The other strained tube had been
     about to blow open, and Jonny Land had flung his arms around it and
     was holding it together by agonized effort while the white-hot vapor
     sprayed his body.</p>,
     <p>Harb Land wildly snatched his brother away as Carlin flung the big
     clamp around the pipe and convulsively spun its bolts shut.</p>,
     <p>He staggered around then. Harb was bending over his brother.</p>,
     <p>"Jonny! Jonny!"</p>,
     <p>Jonny's whole chest and neck were blackened and blasted. His face was a
     ghastly, sooted mask as his eyes looked up at them.</p>,
     <p>Another salvo went off close by, and again the "Phoenix" rocked wildly.</p>,
     <p>"Cut the dredge!" Carlin cried. "We've proved the process is
     successful, and we can't stay here now or your brother will die!"</p>,
     <p>Loesser cut off the dredge and Harb Land rushed for the pilot room.
     Carlin heard him shouting there into the communic:</p>,
     <p>"Control cruisers from 'Phoenix!' We're putting out to surrender. Be
     ready to give injured man medical treatment."</p>,
     <p>"Break out of your orbit at once and we'll contact you for surrender by
     locator when you're outside the corona," came the sharp, fast answer.</p>,
     <p>The generators of the "Phoenix" started roaring their shrillest note as
     Harb Land frantically flung power into the drive-plates. Beneath the
     thrust of its propulsion vibrations the battered ship began to move, to
     fight its way out of the gigantic pull of Sol, breaking slowly out in a
     tangent off its orbit.</p>,
     <p>Carlin, Loesser, all of them in the hold, were bending over Jonny Land
     when Floring, released by Harb, came back. The officer looked down and
     then shook his head somberly.</p>,
     <p>"No chance," he said. "He won't even last until we reach the cruisers."</p>,
     <p>Jonny was lying, unhearing, fighting for breath, looking up at them
     without seeing them, his sooted face a writhing mask. Carlin felt tears
     sting his eyes, and saw everything through a blur.</p>,
     <p>"Jonny, we did it—you did it!" Loesser was choking. "Made Sun-mining
     possible! Why, soon now there'll be scores of ships, new, big ships,
     coming here and getting all the copper Earth needs!"</p>,
     <p>He was, Carlin knew, trying to reach home to the dimming mind with that
     reassurance, that assurance that the dying man had not given away life
     in vain.</p>,
     <p>It didn't reach Jonny Land. He wasn't Jonny Land any longer, he was
     just a living creature dying in pain, and he couldn't feel or know
     anything but pain. And then the pain went, and life went with it, and
     his face was a lax, empty mask that had no meaning for them.</p>,
     <p>Loesser sobbed: "He didn't know—he didn't know what I was saying!"</p>,
     <p>Carlin felt dull, tired, drained of emotion. He had just seen the only
     hero he had ever known die, but a hero's death was just death, just
     mortal pang and final release.</p>,
     <p>He went forward to the pilot room.</p>,
     <p>"Jonny's dead," he said to Harb Land.</p>,
     <p>Harb's shoulders sagged, but he did not turn as he guided the "Phoenix"
     on spaceward to where the grim Control cruisers waited.</p>,
     <p>Control Court here in New York was only a small room in the building
     by the spaceport. There were no officials in it except the three
     middle-aged judges who sat behind a small table and prepared to pass
     sentence on Laird Carlin and his seven comrades.</p>,
     <p>There were no lawyers, no oratory, no jurymen. They were not needed.
     The government psychologists who had quietly questioned the accused men
     during their four days in prison had submitted the factual hypnosis
     records which were complete and incontrovertible evidence.</p>,
     <p>The chief judge, the man in the middle, quietly read the decision as
     Carlin and the others faced him.</p>,
     <p>"This court is placed in a peculiarly difficult position in assessing
     your offense. On the one hand, you men deliberately broke a Control
     Council regulation and defied its officers. On the other hand, your
     action has proved the practicability of a process of Sun-mining which
     will be of incalculable value to this and every other System in the
     galaxy.</p>,
     <p>"To forgive your offense because the ultimate result was good would be
     to set a fatal precedent. It would establish the principle that illegal
     means do not matter if end-purposes are good. We cannot permit such a
     precedent to be established. Therefore, regretfully, this court must
     pass the prescribed punishment for your offense."</p>,
     <p>Carlin could not deny the crystalline logic. He had known from the
     first that this must be the issue, and he was too tired to care.</p>,
     <p>"You are sentenced to two years imprisonment in Rigel Prison and
     also to the loss of your spacemen's licenses or Cosmic Engineer's
     certificate, whichever you hold. Such sentence is obligatory in this
     case." He added quickly, "It is, however, within our discretion to
     suspend the prison term and to limit cancellation of your certificates
     to one year from date. Such is the sentence of this court."</p>,
     <p>Loesser drew a gusty breath of relief. "For a minute, I thought it was
     Rigel for us sure enough!"</p>,
     <p>The chief judge had risen. "Speaking personally," he added quietly, "we
     would like to congratulate you men upon a great achievement."</p>,
     <p>Ross Floring came to their side.</p>,
     <p>"A year's suspension isn't long," he said, and Carlin nodded wearily.</p>,
     <p>When, with Harb Land's giant figure leading them, they emerged from the
     building into the sunlight, a roar that deafened them came from the
     waiting crowd outside. The people of Earth, at least, had no need to
     temper their gratitude.</p>,
     <p>Harb was grimly silent as he pushed through the crowd toward Marn and
     old Gramp Land. Carlin found himself buffeted by eager hands, assailed
     by joyful faces and voices, as he followed.</p>,
     <p>A grizzled, excited man clapped his shoulder. "We Earthmen showed 'em
     we could still conquer space, didn't we?"</p>,
     <p>We Earthmen? Somehow, for the first time in all these days, Carlin's
     dulled mind felt a stir of pride as though at an accolade.</p>,
     <p>He didn't like to meet Marn's pale face. But she spoke steadily.</p>,
     <p>"It's all right, Laird, about Jonny. Women of Earth for two thousand
     years have seen their men go out into space—and not all come back."</p>,
     <p>Floring had followed them. "I want you to see something," he said.</p>,
     <p>He led the way toward the towering Monument of the Space-Pioneers.
     Carlin looked at the roll of names. Then his eyes suddenly blurred as
     he saw that, for the first time in several centuries, a new name had
     been added to the bottom of that great roll.</p>,
     <p class="ph1">JON LAND</p>,
     <p>Marn's eyes were shining. And her giant brother looked long, with
     haggard face somehow comforted. But old Gramp Land turned sadly away.</p>,
     <p>"A name on a stone is poor exchange for my boy," he muttered. "I'm
     gettin' old."</p>,
     <p>That evening, in the old house up on the ridge, they were subdued and
     silent at dinner. The table was too big, and they looked around too
     often as if listening for a familiar limping step and a cheerful voice.</p>,
     <p>Carlin was doubly oppressed because of the thing that he had not yet
     told them. He hated, somehow, to break the news.</p>,
     <p>"There's something they found out when they made our psycho-records for
     the trial," he said finally. "Mine showed that I had no instability of
     coordination, no star-sickness any longer."</p>,
     <p>"You mean, you're cured?" said Harb, surprised. "Why, that's fine. I
     never thought of it, but you made the trip Sunward all right, so I
     should have known."</p>,
     <p>"The psychos say," Carlin told them, "that some people out in the
     galaxy now and then approximate much closer to the original Earth stock
     than the average. Such people respond rapidly to Earth-treatment. I'm
     one of them, it seems." He added uncomfortably, "I can go back home to
     Canopus now, though I'll have to work at a desk job for a year. The
     only thing is that there's a ship for Canopus tonight, and there won't
     be another for weeks."</p>,
     <p>"You're not going tonight?" exclaimed Harb. "Not as soon as that?"</p>,
     <p>Carlin felt a little heartsick. "I wish I didn't have to, so soon. But
     there's nothing for me to do here now that I'm all okay."</p>,
     <p>He had somehow expected Marn to protest too. But she did not. She only
     said quietly:</p>,
     <p>"I'll drive you down to the spaceport."</p>,
     <p>"I think I'd rather walk down," Carlin said slowly. "I don't know why,
     but I would. It's not far and I sent my bags on down."</p>,
     <p>"Then I'll walk a little of the way with you," said Marn.</p>,
     <p>Twilight had changed into soft summer darkness by the time Carlin had
     exchanged a last old-fashioned hand grip with Harb and Gramp Land, and
     started down the road with Marn.</p>,
     <p>She went only around the first turn of the old road with him, and then
     stopped.</p>,
     <p>"Good-by, Marn," he said, but she only averted her face.</p>,
     <p>Carlin hesitated, then turned and walked on. Luna was lifting its
     shining shield in the east, and the silver summer silence lay over
     everything, hardly broken by the stir of branches and the low buzz of
     insects. The night was warm and still.</p>,
     <p>He had a lump in his throat and he tried to laugh at himself because he
     had it. A man couldn't let illogical emotions overrule his reason. This
     crazy, heroic old planet Earth and its people—he would never forget
     them, but he had to return to his own life and work, he had to go home.</p>,
     <p>Laird Carlin suddenly stopped. He knew, abruptly, why dull oppression
     had gnawed his mind all day. It wasn't because he was going home. It
     was because he was leaving home. He was leaving the only place where
     his spirit had ever found something it had always lacked, a peace, an
     ancient certitude, a kinship that had grown and grown.</p>,
     <p>Carlin turned and strode rapidly back up the road. Not until he was
     almost upon her did he perceive that Marn Land was still standing in
     the silvered road where he had left her.</p>,
     <p>"I was waiting for you," she said simply. "I knew you wouldn't go."</p>,
     <p>His hands grasped her shoulders as he spoke in a rush.</p>,
     <p>"Marn, I couldn't! I thought of Canopus, I thought of friends there and
     a girl who likes me and the garden cities I used to love, and it was
     all unreal, I'm tied somehow to this queer old planet, to Jonny and
     Harb and all of the others, and to you!"</p>,
     <p>She came into his arms quietly. "I know. There's been more than one
     like you, more than one who came to Earth and found he somehow couldn't
     leave. This old world is in the blood of our race, Laird." She looked
     up. "A year's not long. We'll need you here to replace Jonny, to
     supervise the Sun-mining. And I need you. I always will."</p>,
     <p>Carlin held her closely, all tiredness and doubts gone now, strangely
     content. He looked up at the summer stars and thought of worlds out
     there, but it was all far away, far away.</p>,
     <p>And Earth was close, its ancient quiet night enfolding him. Soft wind
     stirred leafing branches in the moonlight, and the road wound up white
     and sure toward the old house, and out of the vastness of time and
     space, an Earthman had come home.</p>]




```python
len(soup.find_all('hr',attrs={'class':'chap'}))
```




    16




```python
soup.find_all('hr',attrs={'class':'chap'})[3].find_all('p',attrs={'class':'ph1'})
```




    []




```python
for p in soup.find_all('p',attrs={'class':'ph1'}): 
    print(p) #print the chapter names
```

    <p class="ph1">CHAPTER I</p>
    <p class="ph1"><i>Stranger from the Stars</i></p>
    <p class="ph1">CHAPTER II</p>
    <p class="ph1"><i>Ancient Town</i></p>
    <p class="ph1">CHAPTER III</p>
    <p class="ph1"><i>Old Planet</i></p>
    <p class="ph1">CHAPTER IV</p>
    <p class="ph1"><i>Mystery Machine</i></p>
    <p class="ph1">Gorham Johnson, 1991<br/>
    Mark Carew, 1998<br/>
    Jan Wenzi, 2006<br/>
    John North, 2012</p>
    <p class="ph1">CHAPTER V</p>
    <p class="ph1"><i>Desperate Play</i></p>
    <p class="ph1">CHAPTER VI</p>
    <p class="ph1">"<i>You Owe a Chance to Earth!</i>"</p>
    <p class="ph1">CHAPTER VII</p>
    <p class="ph1"><i>Last Frontier</i></p>
    <p class="ph1">CHAPTER VIII</p>
    <p class="ph1"><i>Solar Struggle</i></p>
    <p class="ph1">CHAPTER IX</p>
    <p class="ph1"><i>An Earthman Comes Home</i></p>
    <p class="ph1">JON LAND</p>



```python
for p in soup.find_all('p'):
    print(p) #print each paragraph
```

    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Title</strong>: Forgotten world</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Author</strong>: Edmond Hamilton</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Release Date</strong>: November 15, 2022 [EBook #69357]</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Language</strong>: English</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Original Publication</strong>: US: , United States: Standard Magazines, Inc.,1945.</p>
    <p style="display:block; margin-top:1em; margin-bottom:1em; margin-left:2em; text-indent:-2em"><strong>Credits</strong>: Greg Weeks, Mary Meehan and the Online Distributed Proofreading Team at http://www.pgdp.net</p>
    <p>[Transcriber's Note: This etext was produced from<br/>
    Thrilling Wonder Stories Winter 1946.<br/>
    Extensive research did not uncover any evidence that<br/>
    the U.S. copyright on this publication was renewed.]</p>
    <p class="ph1">CHAPTER I</p>
    <p class="ph1"><i>Stranger from the Stars</i></p>
    <p>Carlin was the only one of the four hundred passengers on the "Larkoom"
    who hated the star-ship and everything about it.</p>
    <p>He was bored with the vessel and everyone aboard. A pack of chattering
    idiots! For the hundredth time since leaving Canopus, he told himself
    that he was a monumental fool to let that psychotherapist talk him into
    this crazy trip.</p>
    <p>A blond girl from Altair Four came tripping along the deck and favored
    Laird Carlin with the bright smile that all the younger feminine
    tourists had practised on the tall, dark, dour-looking young man.</p>
    <p>The blonde from Altair Four favored the tall dour-looking young man with a bright smile.</p>
    <p>"Oh, Mr, Carlin, the annunciators just said that we're only eight
    hours from Sol. By night, we'll be on Earth! Isn't it thrilling?"</p>
    <p>"Just what is thrilling about it?" Carlin asked sourly.</p>
    <p>The girl was a little dumfounded. "Why, I mean, Earth! All the ancient
    history we study in schools, about how men first came from there two
    thousand years ago. Or was it twenty-one hundred?"</p>
    <p>She prattled on, voicing all the appropriate clichés.</p>
    <p>"Just think, all of us in this ship came from different stats and
    worlds, yet long ago all our ancestors lived on that one little world
    Earth. And they say it's still much the same as it was then. Isn't it
    wonderful?"</p>
    <p>Carlin could not see anything wonderful about it, and a little wearily
    he said so.</p>
    <p>The girl flushed in exasperation. "Then why are you going to Earth at
    all?"</p>
    <p>Why indeed, Carlin wondered savagely? Why the devil wasn't he back
    on the other side of the galaxy where he belonged, supervising
    establishment of the new star-ship line to Algol Six, spending his
    leaves in Sun City with Nila?</p>
    <p>Nila—he yearned for her, for her gay, mocking humor, her cool beauty,
    her quick, clever mind. What was he doing here with a bunch of
    bird-brained tourists who were conscientiously tripping for local color
    to an old, forgotten world?</p>
    <p>This whole part of the galaxy was a stagnant, half-dead area. This side
    of Vega there weren't a score of suns with worlds of any importance.
    And the old "Larkoom," a second-rate star-ship that couldn't make more
    than eighty light-speeds, was plodding determinedly and monotonously on
    into it.</p>
    <p>Curse that psychotherapist anyway! Why had he been crazy enough to
    listen to the fellow? That smug, pink, blinking Arcturian had smiled as
    gently as a well-bred pussy-cat as he told Carlin what his trouble was.</p>
    <p>"Star-sick?" Carlin had flared. "What do you mean, star-sick? I've made
    the trip to Algol ten times in the last three months."</p>
    <p>The psychotherapist had nodded. "Yes. And that was nine times too many.
    You've been overdoing it for a long time, Mr. Carlin."</p>
    <p>Before Carlin could protest, the other man had referred to the dossier
    on his desk.</p>
    <p>"I have your record here. Born at Aldebaran four thirty years ago.
    Graduated at twenty-two from Canopus University with the degree
    of Cosmic Engineer. Worked since then establishing spaceports for
    star-ship lines between Rigel, Sharak, Tibor, Algol and other stars."</p>
    <p>The psychotherapist looked up gravely. "The point is that you've spent
    fifty per cent of your time in the last eight years in star-ships. The
    average has been seventy per cent since you took charge of establishing
    the new Algol line. And that's too much time in space for any man. No
    wonder you're star-sick."</p>
    <p>"Blast it, I'm not star-sick!" Carlin exploded. "What kind of therapist
    are you? I come here to have you treat a perfectly simple syndrome of
    reflex-fatigue, and you tell me all this!"</p>
    <p>The Arcturian shook his head wisely. "Your case was only simple on the
    surface, Mr. Carlin. The hypnosis showed up your trouble unmistakably.
    Want to hear the record?"</p>
    <p>Carlin heard it. And it wasn't pretty. Not pretty, to hear his
    hypnosis-freed subconscious yelling out a frantic hatred of space and
    star-ships and everything connected with them.</p>
    <p>"You see?" said the Arcturian gently. "This has been building up in you
    for a long time."</p>
    <p>Carlin was stunned. He had known of other men who had got star-sick and
    had had to drop their work and quit traveling space for a while. Other
    men—but he'd always laughed contemptuously at them for it.</p>
    <p>The psychos might declare that it was perfectly natural for a man to
    develop a subconscious aversion to space if he crowded his work, but
    the hard-bitten engineers of Carlin's set believed that a star-sick man
    was nine times in ten a shirker. And now he himself was told he was
    star-sick.</p>
    <p>"You've got to quit work and stay out of space for a while," the
    Arcturian therapist told him.</p>
    <p>Carlin felt sick at heart. "Then all my work in building up the Algol
    line will go into young Brewer's hands."</p>
    <p>Still, he thought after a moment, it might not be so bad. Working in
    his line's main offices here on Canopus Two, he could keep in touch.
    And he would have more time here with Nila.</p>
    <p>But the psychotherapist shook his head quite decisively at that.</p>
    <p>"No, Mr. Carlin. Your case is too dangerous for that. Your subconscious
    is twisted into a knot that is going to be hard to untie." He hesitated
    a moment as though he knew what reaction his next words would provoke.
    "In fact, there's only one way in which you can be normalized. That's
    the Earth-treatment."</p>
    <p>"Earth-treatment?" Carlin didn't even know what it meant. "You mean,
    some treatment that has reference to the old planet over on the other
    side of the galaxy?"</p>
    <p>The Arcturian nodded. "Yes, our ancestral planet Earth. Where all our
    race came from, two thousand years ago. Where you're going back to, for
    perhaps a year."</p>
    <p>Carlin was knocked breathless by that calm statement.</p>
    <p>"Me going to Earth for a year? Are you crazy? Why should I go there?"</p>
    <p>"Because," the therapist said soberly, "if you don't I'm afraid you
    won't last another six months as a star-line man."</p>
    <p>"But why can't I take a rest right here on Canopus Two?" Carlin
    demanded heatedly. "Why send me to that moldering, forgotten old planet
    where there's nothing now but a few historical monuments?"</p>
    <p>"You've never been to Earth, I take it?" the psychotherapist asked
    thoughtfully.</p>
    <p>Carlin made an impatient gesture. "I'm not interested in ancient
    history. That part of the galaxy is all a backwater."</p>
    <p>"Yes," the expert said. "I know all that. But old and small and
    forgotten as it is these days, Earth is still important."</p>
    <p>"To historians," Carlin snapped. "To people who like to poke in the
    dusty past."</p>
    <p>The Arcturian nodded, and shrugged.</p>
    <p>"And to psychologists," he said quietly. "Most people these days don't
    realize something. They don't realize that we, all of us, are still
    really Earthmen in a way." He held up a protesting hand. "Oh, I know
    we don't think of ourselves like that! Since those first Earthmen
    pioneered to their neighbor planets and then to the stars, since our
    civilization spread out over most of the galaxy, a hundred generations
    of us have been born on different star-worlds from Rigel to Fomalhaut.
    But except for local modifications, the type of humanity has persisted
    since our ancestors left Earth and Sol long ago.</p>
    <p>"That's because we've altered star-world conditions to fit ourselves,
    instead of adapting ourselves to those conditions. We've cunningly
    changed atmospheres, gravities, everything, wherever we went. We've
    kept ourselves one race, one type, that way. But it's a type that is
    still indexed to that old plane Earth as its norm."</p>
    <p>"Does that explain why I have to give up my work and go live on the old
    relic for a year?" Carlin demanded furiously.</p>
    <p>"Yes, it does," the Arcturian replied. "We're a star-traveling race
    now. But the mind can take only so much of the strain of star-travel.
    Overdo that strain and you get a revulsion, you get star-sickness. Then
    the only cure is rest for the mind in completely normal conditions. And
    complete normality, for us descendants of Earthmen, is—Earth."</p>
    <p>Carlin had stormed. He carried his wrathful resistance to the last
    pitch.</p>
    <p>And then the psychotherapist had crushed him.</p>
    <p>"I've turned in your psycho-record to your star-ship line. You'll not
    be allowed to work there until you're cured."</p>
    <p>And that, Laird Carlin thought bitterly, was why he was sprawled in a
    deck-chair here on the "Larkoom" as the old tub creaked and labored and
    plodded through space toward the yellow spark of Sol.</p>
    <p>"A year!" he thought in impotent rage. "A year in that hole! I might as
    well be dead."</p>
    <p>The psychotherapist had held out the hope that it might not take a
    year. Some cases of star-sickness responded quickly to Earth-treatment.
    But even a few months seemed an eternity to Carlin.</p>
    <p>The passengers of the "Larkoom" were crowding toward the transparent
    wall of the deck. Earth was coming into sight. And these people—men
    and women bronzed by the glare of Canopus, reddened by the desert winds
    of Rigel's worlds, paled by the mists of Altair's planets—all were
    watching with an intense and eager expectation.</p>
    <p>Carlin walked wearily over to the deck wall and watched with them.
    Sol, ahead, was a small and undistinguished yellow sun. Its orb was
    unimpressive to eyes that had looked on Antares and Altair.</p>
    <p>And the planets that circled it were so little that Carlin could
    hardly make them out. He remembered half-forgotten names from ancient
    history—Saturn, Jupiter, Mars. And that little gray-green dot beyond
    must be Earth.</p>
    <p>"Isn't it tiny?" babbled a rapturous, overweight woman beside Carlin.
    "I think it's cute!"</p>
    <p>A very young man from Mizar Seven proudly aired his knowledge.</p>
    <p>"That satellite beyond it is Luna, its moon."</p>
    <p>"The moon is almost as big as the little planet!" exclaimed someone,
    laughing.</p>
    <p>Carlin found their chatter getting on his nerves, and edged further
    along the deck. In gloomy silence, he looked down as the "Larkoom"
    swept in swift, almost soundless rush toward the little planet.</p>
    <p>A gray-green, cloud-screened ball spinning around a second-rate sun—it
    looked like the end of the universe to Carlin. And he might have to
    spend a year here! His spirits sank still lower.</p>
    <p>"They say you can get the most wonderful souvenirs here," one of the
    tourists' voices reached him.</p>
    <p>Carlin writhed. He would be glad to get out even at Earth, to get away
    from this bunch of babbling fools.</p>
    <p>He realized his irritability was extreme, unreasonable. It was the
    result of his star-sickness, he supposed. But that didn't make it any
    more endurable.</p>
    <p>"Landing in ten minutes," spoke the annunciators throughout the ship.
    "Stasis going on."</p>
    <p>The dim glow of the force-stasis that cushioned everything in the ship
    against pressure of deceleration came on like a tangible medium around
    them. The big propulsion-wave generators droned in lower key.</p>
    <p>Swaddled in the cushioning force, they felt no discomfort as the
    "Larkoom" quickly dropped toward the little planet. Atmosphere screamed
    briefly outside the ship. They came down through a belt of clouds.</p>
    <p>"That's the city New York!" cried an eager voice. "The oldest human
    city in the galaxy!"</p>
    <p class="ph1">CHAPTER II</p>
    <p class="ph1"><i>Ancient Town</i></p>
    <p>Carlin looked with a jaundiced eye on the scene widening out below
    them. There was a blue ocean stretching eastward, a long green coast,
    and an island that was covered by the grotesquely lofty buildings of an
    extremely antiquated type of city.</p>
    <p>This ancient town called New York was like a memento of the primitive
    past. Not for a thousand years had men crowded their structures so
    crazily together, or built them to such insane heights.</p>
    <p>"It's like one of the bird-people's lofts on Polaris One!" exclaimed a
    girl, laughing. "And how old it looks!"</p>
    <p>Old? Yes. Pitifully old, like a withered beldame who endeavors still
    to maintain stiff dignity. The city looked only half-occupied, vines
    growing on some of the grotesque towers, parks ragged around the edges.</p>
    <p>The spaceport, some distance northward amid low rolling hills, was so
    small as to be inadequate for any decent world. Carlin's practised eyes
    condemned the cracked, blackened tarmac, the ill-placed rows of docks,
    the insufficient hangar and repair buildings.</p>
    <p>The "Larkoom" landed softly. Carlin waited wearily until the squealing
    rush of tourists was over, and then walked out into the soft yellow
    sunshine. He looked around without interest. Landing on a new world was
    no novelty to him.</p>
    <p>But for a moment, he was startled by the air he breathed. It was so
    sweet, so buoyant, so right. It was subtly stimulating, exhilarating
    to the lungs. Then he realized the cause. All over the galaxy, the
    descendants of Earthmen had conditioned planetary atmospheres with this
    atmosphere of Earth as the desired norm.</p>
    <p>He looked around uncertainly. The tourists were already being
    shepherded by their tour-conductors toward some old monuments at the
    far end of the spaceport. But he had no desire to follow them.</p>
    <p>The psychotherapist had told him, "Live as nearly an ordinary Earth
    life as you can. Your cure will be quicker if you do. Best thing would
    be to lodge in some typical Earth home, if you can."</p>
    <p>Carlin wondered where he could find such a lodging. There were a few
    Earthmen about, spacemen, port officials and the like. He could ask one
    of them.</p>
    <p>He had met Earthmen before throughout the galaxy, for many of them
    followed space as a trade. And he didn't much like them. A proud,
    taciturn, half-sulky lot, they had always seemed to him.</p>
    <p>"Can you tell me where I could find lodgings around here?" He asked a
    lanky, lantern-jawed man in faded clothes.</p>
    <p>The Earthman contemplated Laird Carlin with unfriendly eyes, taking in
    his sun-darkened face, his pearl-colored synthesilk slacks and jacket,
    every detail of his appearance that was alien here.</p>
    <p>"Well, no," the fellow drawled coolly. "Don't know where a stranger
    could get lodgin's round here."</p>
    <p>He slouched on. Carlin flushed with anger at the scarcely veiled
    hostility in the fellow's manner.</p>
    <p>These blasted yokels of Earth! Living here on an old, outworn,
    fifth-rate planet, resenting the progress and prosperity of the great
    star-worlds, talking of everybody but themselves as "strangers"!</p>
    <p>"And I'm supposed to live among them for a year!" he thought bitterly.</p>
    <p>He started across the spaceport. He had noted a spick-and-span
    chromaloy building with a half-dozen trim Control cruisers parked
    nearby, and with the Control Council emblem on its wall. He could find
    out something there.</p>
    <p>The spaceport was a somnolent, slovenly place to Carlin's eyes. A
    few star-ships, all of them freighters except the tubby "Larkoom," a
    scattering of little inter-planet craft, a few workers lounging about.
    Even the smallest world of the great stars would be ashamed of such a
    port.</p>
    <p>That soft yellow sun, he found, had a deceptive warmth. And walking was
    tiring after days of the ship's artificial gravity. Then Carlin stopped
    as he came abreast of a rickety little planet-ship.</p>
    <p>Two Earthmen were inspecting its stern drive-plates—one of them a
    stocky, red-faced young man, the other a lame younger fellow with a
    crutch. Carlin asked them his question.</p>
    <p>The red-faced individual answered with the same hostility of manner.</p>
    <p>"You'll find no lodgings around here. Better go with the rest of your
    crowd. There's a big tourist hotel down in the city."</p>
    <p>Carlin swore. "Blast it, I'm not a tourist. I'm an engineer sent here
    by a crazy psycho to spend a year on Earth—heaven knows why!"</p>
    <p>The lame young Earthman looked at Carlin more closely. He had a thin,
    pleasant brown face with intelligent blue eyes.</p>
    <p>"Oh, an Earth-treatment man?" he said. "A few come in all the time." He
    asked interestedly, "You're a Cosmic Engineer? Do you mind telling me
    what field?"</p>
    <p>"Star-ship line chief surveyor," Carlin said wearily. "That means I lay
    out spaceport and beacon routes between star-worlds."</p>
    <p>"I know what it means." The lame youngster nodded quietly. He
    hesitated, frowning slightly as though weighing something. Then, as if
    deciding, he spoke. "I'm Jonny Land. I think we could fix you up with
    lodgings if you don't mind putting up with a little discomfort."</p>
    <p>"You mean, in your own home?" Carlin asked doubtfully. "Where is it?"</p>
    <p>Jonny Land pointed to one of the low green ridges west of the spaceport.</p>
    <p>"Just up on the ridge there. There's only my grandfather, my brother
    and sister, and myself. And we have an extra room."</p>
    <p>The red-faced young Earthman made a sharp protest. "Jonny, what the
    blazes are you thinking of? You don't want this fellow in with you!"</p>
    <p>The violence of his protest seemed uncalled-for to Carlin, even
    granting the general Earthman hostility to strangers.</p>
    <p>Jonny Land quietly quelled the outburst. "I'm doing this, Loesser." He
    looked at Carlin. "Well, what about it? I warn you that you won't find
    the comforts of a big star-world apartment."</p>
    <p>"I don't expect anything like that here," Carlin answered tiredly. He
    felt worn out by the voyage, the discouragingly primitive aspect of
    this place where he must live, the open unfriendliness. He nodded.
    "I'll try it. The name is Laird Carlin."</p>
    <p>"If you'll get your luggage, I'll take you up," Jonny Land suggested.
    "I have a truck. I'll meet you over at the terminal."</p>
    <p>Carlin came out of the shabby terminal a little later with his two
    kitbags and found the lame youngster waiting at the wheel of a
    disreputable-looking old ato-truck.</p>
    <p>Loesser, the red-faced young man, was standing beside it voicing
    emphatic protest about something. Carlin overheard a few words.</p>
    <p>"—ruin everything by taking this fellow in!" he was saying violently.
    "How do you know he isn't a Control spy?"</p>
    <p>"I know what I'm doing, Loesser," Jonny Land repeated firmly.</p>
    <p>They broke off as they saw Carlin coming. But Loesser gave him a hot,
    angry glare as he climbed into the machine.</p>
    <p>The old truck ran westward across the bumpy tarmac and started climbing
    an ancient, cracked concrete road toward the green ridge.</p>
    <p>Carlin wondered wearily what these Earthmen were up to that made them
    afraid of Control? Smuggling, maybe? He didn't much care. He was hot,
    tired, grimy with dust, and unutterably disgusted with Earth.</p>
    <p>The concrete road that climbed the ridge looked as though it was
    centuries old. And its engineering had been timid, for it wound around
    hills instead of cutting through them, bridged small streams instead of
    trampling over them. But the battered truck had difficulty negotiating
    even these easy grades. Its ato-motor drumming noisily as it climbed.</p>
    <p>Carlin looked out gloomily at the sunset-lit landscape. He could not
    get used to the vivid, dominating green of all vegetation here. And
    he was shocked by the unkempt, ragged look of everything. Untended
    fields of weeds and clumps of woods grew right up to the road. It was
    dismayingly different from the groomed, parklike planets of Canopus.</p>
    <p>The houses Carlin glimpsed along the road added to his dislike. They
    were mostly old ferroconcrete dwellings half-hidden by trees and
    bright flowers, with behind them the big tanks used in hydroponic
    farming. Hydroponic farming was so old-fashioned he had thought it had
    disappeared from the galaxy. What was the matter with these people that
    they didn't directly synthesize their food as others did?</p>
    <p>Young Jonny Land was speaking to him.</p>
    <p>"You've never been here before? You must find Earth a little odd."</p>
    <p>Carlin shrugged. "It's all right, I suppose. But I just can't
    understand how you people could let your planet get into this kind of
    shape. Why haven't you spread out more, instead of huddling around a
    few archaic centralized cities like that one back yonder?"</p>
    <p>The lame young Earthman answered slowly, his thin, brown face turned to
    the road ahead.</p>
    <p>"The answer to that is simple. One word, in fact. And that word is
    'power.' We just don't have power enough here on Earth to smooth it out
    into a garden-planet like your star-worlds, to come and go around it
    any distance at will."</p>
    <p>"Atomic power is about the easiest thing to produce there is," Carlin
    commented skeptically.</p>
    <p>"Yes, if you have copper fuel," Jonny Land replied. "If we had enough
    copper we could make a garden of this world too, could spread all
    around its loveliest spots and come and go by fast flier, could give
    up the old hydroponic farming and synthesize our food, and produce the
    luxuries you people have on the star-worlds.</p>
    <p>"But we have little copper. Earth, and its sister-planets here, are all
    starved for it. Once, we had a lot. But not now. And it's economically
    impossible to haul copper in sufficient quantities from other stars.
    That's why we're power-starved, unable to progress."</p>
    <p>Carlin made no further comment. He was not much interested. He was
    only wondering sickly how long he would have to stay on this unkempt,
    stagnant planet.</p>
    <p>The sun was burning his neck, for the old truck was topless. He was
    jolted by holes in the ancient road. The sweetness of the air had lost
    its magic for him, for now with the twilight had appeared swarms of
    evil little gnats and midges.</p>
    <p>"This is the house," said Jonny Land, pulling up the truck in front of
    a square dwelling.</p>
    <p>Laird Carlin's heart sank. It was like the other houses he had seen,
    a ferroconcrete structure festooned with climbing flower-vines,
    surrounded by tall, untrimmed trees except on the side that looked down
    into the twilit valley. Primitive hydroponic tanks gleamed dully beyond
    the trees.</p>
    <p>He followed the lame youngster into a dim, cool living room. It looked
    like an antique stage set to Carlin, with its ridiculous cloth curtains
    at the windows, its obsolete krypton light bulbs in the ceiling, its
    massive furniture that was actually made of wood.</p>
    <p>Jonny Land had been making explanations in lowered tones to the two
    people at the other end of the room. They came forward, a spry old man
    and a girl.</p>
    <p>"This is Gramp Land, my grandfather," Jonny introduced. "And my sister
    Marn."</p>
    <p>The old man looked at Laird Carlin with inquisitive, bright eyes, and
    his gnarled hand reached for an old-fashioned handshake.</p>
    <p>"Come from Canopus, do you?" he chirped. "Well, that's a long way off.
    I was there once years ago when I followed space. And my grandson Harb
    has been there lots of times when he was a star-ship man."</p>
    <p>The girl, Marn, looked doubtful and troubled as she murmured a word of
    greeting to Carlin. He sensed that his coming had disturbed her.</p>
    <p>She was a rather small girl, with a thick mop of ash-colored hair
    carelessly combed back. Her eyes were grave blue. She wore a faded old
    slack-suit that he thought the most barbaric feminine garment he had
    seen.</p>
    <p>"I hope we can make you comfortable here, Mr. Carlin," she said,
    troubled. "We've never had any lodger before. I can't understand why
    Jonny made the suggestion."</p>
    <p>A heavy step at the door cut her short. Her look of distress and worry
    deepened.</p>
    <p>"There's my brother Harb, now."</p>
    <p>Harb Land was a gangling young giant with a craggy face and
    slate-colored eyes that looked at Carlin with instant hostility. Jonny
    had limped forward and was quickly explaining Carlin's presence.</p>
    <p>"He's going to live here with us for a while, Harb."</p>
    <p>Harb Land's reaction was violent. "Have you gone out of your mind,
    Jonny?" he flared. "We can't have him here."</p>
    <p>Disgusted, Carlin started to turn away. But Jonny Land stopped him with
    a gesture. There was a quiet, unsuspected strength in his thin brown
    face as he spoke to his lowering brother.</p>
    <p>"He's going to stay, Harb. We'll talk about it later."</p>
    <p>Harb Land made no reply, but glared at Carlin. And Carlin felt an
    unutterable weariness and dislike.</p>
    <p>These primitive, backward, suspicious Earth yokels, quarreling over the
    privilege of staying in their grotesque old house. As though he would
    stay on their cursed planet one minute if he didn't have to!</p>
    <p>"I'm very tired," he said heavily. "If you could show me where the room
    is, I should like to rest."</p>
    <p>Marn uttered an apologetic exclamation. "Oh, I'm sorry! Of course
    you're tired. Come with me, Mr. Carlin."</p>
    <p>She led upstairs. There was no grav-lift, just old-fashioned steps
    going up a dark hall. And the bedroom on the upper floor to which she
    took him was as bad as he had expected.</p>
    <p>It was clean, of course, spotlessly so. But it was more like a museum
    exhibit than a sleeping chamber, to Carlin. There were no aerators,
    just open windows with crude screens across them. No somnigrav pad,
    just a high, old-style bed. There wasn't even a video.</p>
    <p>Yet the girl made no apologies for it, seemed not to think any
    necessary.</p>
    <p>"We'll bring your bags up after dinner," she said. "It will be soon."</p>
    <p class="ph1">CHAPTER III</p>
    <p class="ph1"><i>Old Planet</i></p>
    <p>When Marn had gone, Carlin lay down wearily on the lumpy, sagging bed.
    He closed his eyes. The reaction to the long, slow voyage had set in.
    No doubt about it, he was star-sick all right. Time was when no voyage
    could have made him feel like this.</p>
    <p>But it wasn't the voyage so much as this world to which he had been
    condemned. How was he going to live here for months, for a whole year
    maybe?</p>
    <p>The sound of an angry voice came up dimly through the twilight, from
    the lower floor of the house. He recognized Harb Land's angry tones.</p>
    <p>"—if Control Operations finds out what we're doing!"</p>
    <p>There was a murmur of lower voices, and then the argument seemed to
    stop. Carlin remembered what he had overheard the red-faced Loesser
    saying at the spaceport.</p>
    <p>What were these Earthmen doing that they were so secretive about? It
    must be something against the laws by which Control Council governed
    the galaxy, or they would not fear discovery by Control Operations.</p>
    <p>When Carlin went down to dinner, he expected open hostility from the
    gangling older brother. But Harb Land muttered a curt greeting, his
    half-civil manner indicating his angry protests had been overridden.</p>
    <p>Carlin stared dismayedly at the food set before them. Instead of the
    clear, colored synthetic jellies and liquids he was used to, the food
    was served in what seemed barbarically primitive state. Cooked whole
    vegetables, natural eggs, natural milk—everything rawly natural.</p>
    <p>He ate what he could, which was little. His weariness was drugging him,
    and Harb Land's smothered hostility gave a sense of strain.</p>
    <p>Gramp Land carried on most of the conversation, questioning Carlin
    about the far-away star-worlds. Carlin answered wearily.</p>
    <p>"Saw a lot of them worlds myself once," the old man said. He added
    proudly, "Following space runs in my family. My mother was a direct
    descendant of Gorham Johnson himself."</p>
    <p>"Gorham Johnson?" Carlin asked. "Who was he?"</p>
    <p>The question was unfortunate.</p>
    <p>"What do they teach out in your star-world schools?" Gramp exploded.
    "Don't you know that Gorham Johnson was the first man ever to travel
    space? That he was an Earthman, who took off from down in the valley
    here two thousand years ago?"</p>
    <p>Gramp's pride was outraged. Carlin remembered the old galaxy
    proverb—"Proud as an Earthman." They were all like that, inordinately
    vain of the fact that their world's people had first conquered space.</p>
    <p>"Sorry," he said tiredly. "I remember the name now. Anyway, I had too
    much cosmic physics to study to spend much time on ancient history."</p>
    <p>Gramp still spluttered, but Jonny intervened, questioning Carlin on his
    work.</p>
    <p>"Did you study sub-atomics or just straight dynamics?"</p>
    <p>"Sub-atomics," Carlin answered. And, to another question, "Yes, I had
    electronic mechanics too."</p>
    <p>He caught the swift, triumphant glance that Jonny Land shot at his
    brother. It puzzled him.</p>
    <p>"Jonny knows all that stuff," boasted Gramp, his good humor restored.
    "He's a Cosmic Engineer graduate from Canopus University, too."</p>
    <p>Laird Carlin was genuinely surprised. He looked at the quiet,
    thin-faced youngster.</p>
    <p>"You're a Canopus graduate? Why the devil is a man of your training
    wasting your time here on Earth?"</p>
    <p>"I just like Earth," Jonny answered evenly, "and wanted to come back
    here when my education was finished."</p>
    <p>"Oh, sure." Carlin nodded. "But if this world is as outworn as it
    looks, there's no field here for a CE. You ought to be out at Algol."</p>
    <p>"You star-world people are all the same—always advising us to leave
    Earth!" Harb Land interrupted with suppressed passion. "That's what
    Control Council keeps harping on as a solution to all our poverty and
    problems. They keep asking, 'Why don't you emigrate to other stars?'"</p>
    <p>Gramp Land shook his head. "We don't leave our planet as lightly as
    some folks do. No matter how far an Earthman goes, he always comes
    home."</p>
    <p>"Still, you can hardly blame Control Council for giving you good
    advice," Carlin said, exasperated. "After all, it's your own fault if
    you foolishly squandered the copper resources of your planet and now
    lack power."</p>
    <p>Harb Land's craggy face darkened. "Yes, we squandered our copper
    foolishly. We did it twenty centuries ago, when Earth was opening
    up the whole galaxy to travel. We spent our copper establishing the
    galactic civilization that's forgotten all about our power-starved
    world."</p>
    <p>"Harb, please!" said Marn in a low voice, distress in her face.</p>
    <p>A silence fell, and they finished the dinner without further
    conversation. But Jonny Land spoke to Carlin before he went upstairs.</p>
    <p>"Don't take Harb too seriously. A lot of people here on Earth are so
    embittered about our lack of power that they're unreasonable."</p>
    <p>Carlin found his bedroom dark. No automatic lights came on when he
    entered, and he could not find the switch. He gave it up, and got into
    bed and lay looking heavily out into the night.</p>
    <p>Soft wind was stirring the trees around the house. Heavy scent of
    flowers drifted on it, stirring the window curtains. Down in the valley
    gleamed the spaceport beacons, and beyond lay a thin rim of glimmering
    sea over which the quarter-phase shield of Luna was rising.</p>
    <p>He felt utterly miserable, homesick, wretched. If he were back at
    Canopus right now, he would be dancing with Nila in Sun City ballroom,
    or wandering in Yellow Gardens.</p>
    <p>He drifted off to sleep despite himself, in his lumpy bed....</p>
    <p>Carlin awoke with bright sunrise splashing his face. He reached
    sleepily for the aerator and refreshment buttons—then remembered.</p>
    <p>To his surprise, he was feeling much better. He had slept well in the
    primitive bed, and fatigue had drained out of him.</p>
    <p>Queer, musical notes that he guessed were calls of birds came to his
    ears. The air that snapped the curtains was chill now, but pure and
    sweet, subtly intoxicating.</p>
    <p>"They do have finer air on this old world than any aerator can
    furnish," he thought.</p>
    <p>He put on a zipper-suit that was dark brown and rough in weave.</p>
    <p>"Going native," he thought with a sour grin, and went downstairs.</p>
    <p>Marn Land was the only person he found in the sunny rooms. She still
    wore those barbaric faded old slacks, but had a red flower in her ashen
    hair. A little frown of worry in her forehead disappeared as she looked
    at him.</p>
    <p>"You're feeling better, aren't you?" she asked.</p>
    <p>"A lot," Carlin admitted. "I'm afraid I was rather rude last night, you
    know."</p>
    <p>"You were tired," she said gravely. "Just sit down. I'll get your
    breakfast."</p>
    <p>It was a new experience to Carlin to sit chatting in a sunny old
    kitchen while a girl in faded slacks prepared his breakfast on an
    electrode stove. Instead of punching the refreshment-button for it.</p>
    <p>"Jonny and Harb have gone down to the spaceport," she said over her
    shoulder. "They and a few friends have an old planet-ship there that
    they're fixing up for a trip to Mercury."</p>
    <p>"Mercury?" he said. "Oh, that's the innermost of these planets, isn't
    it?"</p>
    <p>"Yes. Men here on Earth are always going prospecting for copper on its
    Hot Side. Jonny got up this prospecting expedition."</p>
    <p>The breakfast she put before Carlin was of coarse wheaten bread, more
    of the natural eggs and milk, and a curious brown beverage made from
    stewing certain dried berries. She informed him its name was coffee.
    Carlin tried it, found it bitter and unpalatable.</p>
    <p>A little surprised by his own action, he ate nearly everything else.
    The food was coarse, but satisfying enough, and he would have to get
    used to it if he were to stay here.</p>
    <p>"I'll try not to be any trouble to you," he told Marn. "I'm just
    supposed to take it easy, do anything I want to."</p>
    <p>She nodded. "I know. Some of our neighbors had Earth-treatment visitors
    as lodgers. They all got to like Earth a lot before they left."</p>
    <p>Carlin did not voice his pessimism on that point. He went to the door
    and stood looking out into the sun-bright, flowery yard.</p>
    <p>He felt at a loss. It was baffling to find himself without anything
    to do, no work crowding up that must be hurried through, no crews of
    ato-men to supervise in blasting spaceports out of untamed planets.</p>
    <p>Marn looked at him understandingly. "You've always been busy, haven't
    you? Earth must seem slow and dull to you."</p>
    <p>Carlin shrugged. "I might as well get used to it. I think I'll take a
    look around."</p>
    <p>"You'll find Gramp fishing up at the north brook if you go that far,"
    Marn called after him as he walked across the yard.</p>
    <p>Carlin sauntered past a big, locked ferroconcrete workshop of some
    kind, and some tall storage sheds, then on past the flat, wide
    hydroponic tanks that were now loaded with their masses of green growth.</p>
    <p>He found a road beyond them that he did not recognize as a road, at
    first. It was a mere wide track gouged northward along the wooded
    ridge, the first dirt road that he had ever seen on a civilized world.</p>
    <p>"A poor planet, all right," Carlin thought. "Can't even build decent
    roads."</p>
    <p>There were hardly even any ato-fliers in the sky, only an occasional
    one flitting across the blue vault.</p>
    <p>"No wonder these poverty-stricken devils resent the rest of the
    galaxy," he thought. "I suppose I would too, if it had been my bad luck
    to be born here."</p>
    <p>The road was crazily illogical, winding westward along the woods-clad
    ridge in serpentine fashion. It twisted accomodatingly to avoid big
    boulders, a spring, a small gully.</p>
    <p>The woods on either side was deplorably unkempt to Carlin's eyes. Big
    and small trees jumbled together, saplings choking each other out, dead
    brush and thorns and vines everywhere. There was even wild life in the
    woods, furry rodents scuttling away, hosts of birds.</p>
    <p>This sort of thing was what you expected on some unpeopled planet that
    hadn't yet been pioneered and civilized. But Earth was the oldest
    human-peopled world in the whole galaxy.</p>
    <p>Yet Carlin had to admit that there were certain compensations here.
    That winelike air was still an experience to him. And walking now came
    more easily to his muscles here than on any world. It seemed odd to be
    walking with such perfect ease, without wearing a de-grav.</p>
    <p>He could not find the brook Marn had mentioned. He sat down on a log by
    the roadside, musing on the drowsy, dull quiet of this place. There was
    not a sound of human activity. Didn't these Earth people ever get bored
    with the sleepiness of the place?</p>
    <p>Carlin found he was still tired. He watched a small, brilliant insect
    fluttering over a flower near by. Soft wind breathed through the ragged
    woods, stirring the green leaves and making a dappled, dancing pattern
    of sunlight on the ground. A distant bird called rustily.</p>
    <p>"An old, outworn planet, dreaming," he thought. "These people, all of
    them, living in its past."</p>
    <p>Carlin finally got up stiffly, and lounged back along the road. He was
    surprised to find that time had passed quickly, that the sun was now at
    the zenith. And that, somehow, his taut nerves had relaxed.</p>
    <p>The big workshop behind the house had its doors open now. He glanced
    through them and was surprised to see that the cavernous room in there
    was a fairly well-equipped atomic-engineering laboratory.</p>
    <p>Interested, Carlin started toward it. In the center of the big room
    he had glimpsed a towering, massive machine whose inner mechanism was
    concealed by a cylindrical metal cover.</p>
    <p>"Looks like it might be a big field-generator of some kind," he
    muttered. "I wonder what it really is?"</p>
    <p>There was a violent exclamation as an Earthman came running out from
    behind the machine to block his entrance.</p>
    <p>Carlin recognized the broad red face, angry eyes and stocky figure of
    Loesser, the man who had argued with Jonny at the spaceport.</p>
    <p>"What are you doing here?" Loesser demanded harshly.</p>
    <p>Carlin was bewildered by his vehemence. "Why, I just wanted to take a
    look at this machine."</p>
    <p>"I thought so!" blazed Loesser, his eyes raging. "I told Jonny that was
    why you came here!"</p>
    <p>He snatched an object from his jacket pocket. To Carlin's thunderstruck
    amazement, the object was a stubby atom-pistol that Loesser was
    furiously leveling at him.</p>
    <p class="ph1">CHAPTER IV</p>
    <p class="ph1"><i>Mystery Machine</i></p>
    <p>Laird Carlin was child of a galactic civilization in which violence
    between men was rare. There was plenty of danger yet, in pioneering new
    star-worlds, but over the civilized worlds themselves the unchallenged
    law of the Control Council maintained unbroken order. A man could go a
    lifetime without ever seeing violence.</p>
    <p>The atom-pistol in Loesser's hand and the obvious murderous intention
    in the man's face stupefied Carlin. He was simply unable to adjust his
    thinking to the possibility that the enraged Earthman before him meant
    to blast him down.</p>
    <p>"Why, what's the matter?" he began, puzzled and stunned.</p>
    <p>He knew later how near he had been to death. At the moment, he so
    little recognized it that he felt no relief at the interruption that
    came now. Harb and Jonny Land came running forward from the cavernous
    interior of the workshop.</p>
    <p>"Loesser, put that gun down!" snapped Jonny.</p>
    <p>Loesser turned violently. "This fellow was spying on us! I saw him at
    the door!"</p>
    <p>Harb Land's craggy face darkened ominously.</p>
    <p>"I warned you what might happen," he said harshly to his brother.</p>
    <p>"Is this man crazy?" Laird Carlin demanded bewilderedly of Jonny.</p>
    <p>The lame youngster limped quickly forward. "Get back to work," he told
    the other two briefly. "Carlin, I'm sorry about this. I'll explain."</p>
    <p>He walked beside Carlin toward the house. It was not until later that
    Carlin realized how deftly and unobtrusively he had been steered away
    from the workshop.</p>
    <p>"Harb and Loesser and I, and a few others, are planning an expedition
    to Mercury to prospect for copper," Jonny was explaining. "In that ship
    you saw down at the spaceport. We've devised a new metal-finder of the
    radiolocator type, with which we hope to be able to locate new copper
    deposits. That's the machine in the workshop.</p>
    <p>"We've maintained a certain secrecy about it," he went on, "because
    naturally we don't want other prospectors stealing the idea of our new
    finder and beating us to it. And I'm afraid Loesser thought you were
    spying on us. People here are always a little suspicious of strangers."</p>
    <p>"So I've noticed," Carlin answered dryly. "This is the first world in
    the galaxy where I've ever felt completely unwelcome."</p>
    <p>"Oh, I wouldn't say that," replied the other. "But put yourself in our
    place, Carlin. Figure how you would feel if you were an Earthman, your
    world starved for power because its copper was spent to establish a
    galactic civilization that now neglects it."</p>
    <p>Jonny's thin brown face was earnest, his blue eyes watching Carlin as
    though eager to convince him. Carlin shook his head.</p>
    <p>"I can see your problem in lacking copper," he said. "But the remedy
    for it is so simple. Nine-tenths of you should emigrate to other,
    better worlds as the Control Council advised."</p>
    <p>Jonny smiled. "There you come up against the obstinacy of my people.
    We've an older planetary tradition, a deeper, more ancient love for our
    world, than any other people in the galaxy."</p>
    <p>"I think you people live too much in the past," Carlin answered
    frankly. "But it's none of my business. Anyway, I hope your expedition
    brings home copper."</p>
    <p>"Thanks," Jonny said softly. "I think we have a good chance."</p>
    <p>Carlin went back to the veranda of the old house and sat there
    pondering. Something about Jonny's explanation had been vaguely
    unsatisfying.</p>
    <p>To his trained eyes, the glimpse he had had of that towering machine
    had not suggested any metal-finding device. There had somehow been a
    suggestion in its half-glimpsed bulk of something quite different;
    something vaguely disturbing, almost menacing.</p>
    <p>"The devil, I must have knots in my subconscious to start getting
    premonitions like that," Carlin swore. "The poor devils are just
    secretive about their plans because everyone else here is that way."</p>
    <p>He lounged boredly around the house during the hot, sleepy afternoon.
    There was no one to talk to, for the brothers stayed out in their
    workshop and Marn was out tending the big hydroponic tanks.</p>
    <p>He tinkered with the old video set in the living room but the
    only stations he could get were local Earth ones, and lectures on
    hydroponics and gossip about unknown people didn't interest him.</p>
    <p>He finally gave up and stretched out on the veranda, staring sleepily
    down into the green cup of the valley and cursing the psychotherapist
    whose insane idea had sent him here to die of boredom. He dozed until
    he was awakened by the sputter of an arriving ato-truck.</p>
    <p>It contained three lanky young men, tall Earthmen who went back to
    the workshop without stopping at the house. The other partners in the
    prospecting expedition, Carlin supposed sleepily.</p>
    <p>Again he felt that queer sense of something threatening, that vague
    premonition that had clung to him ever since he glanced into the
    workshop. If only he could remember what that machine reminded him of.</p>
    <p>Days passed and Carlin still could not remember that, though his
    disturbing doubt persisted. There was no chance of another look into
    the workshop for it was always locked except when Jonny and Harb and
    their half-dozen partners worked in it.</p>
    <p>"The trouble with me," Carlin told himself ironically, "is that I
    haven't anything else to occupy my mind on this blamed world."</p>
    <p>Yet Carlin's first repelled dislike of Earth had faded much by now.
    The crudities of existence, the lack of civilized conveniences, no
    longer bothered him so much. He had to admit that whether or not
    Earth-treatment was benefiting his twisted subconscious, this sleepy
    old planet was a fine place for a rest.</p>
    <p>He spent his mornings idly rambling the twisting roads, his afternoons
    lounging on the cool, shady veranda of the old house, or helping Marn
    tend the hydroponic tanks. Or fishing with Gramp in the foaming brook
    below the ridge, while that oldster told interminable tales of the old
    days when he had followed space.</p>
    <p>Neighbors, hydroponic farmers up and down the valley, dropped in at
    the Land house in the evenings. Carlin did not intrude, and gradually
    their first stiff suspicion of him abated and they talked freely before
    him. The talk always swung to the paramount consideration on this
    power-starved planet—the need for copper. It made Carlin feel a little
    guilty to remember how much of it was wasted on other worlds.</p>
    <p>"I have to drive down to the spaceport for Jonny, to get some
    instruments he left in the ship," Marn said to him after dinner one
    evening. "Do you want to go along?"</p>
    <p>Carlin grinned. "I've legged it so much lately that riding anywhere
    would be a change."</p>
    <p>The old ato-truck swung down the twisting road in the blaring sunset.
    The heavens behind them were a glory of fusing colors as the red ball
    of Sol dipped majestically toward the horizon.</p>
    <p>Despite his appreciation of that wild splendor, Carlin felt a vague
    uneasiness. Why should the loveliness of the evening bring disturbing
    recollection of Jonny Land's puzzling machine into his mind?</p>
    <p>"You're getting to like it better here, aren't you?" asked Marn.</p>
    <p>She was usually so silent with him that Carlin glanced quickly at
    her profile as she drove. It struck him with surprise that she had a
    certain beauty. Her thick mop of ashen hair, and firm-chinned face,
    and small, competent hands grasping the wheel, were oddly attractive.
    It wasn't the fine-edged, shimmering beauty that Nila had, but it had
    appeal.</p>
    <p>"Yes, I must be getting more accustomed to it," he answered her
    question. "And it's not as provincial as I thought. Nearly every man
    you meet here has been to space some time or other."</p>
    <p>"Every Earth boy runs away to space sooner or later," she said, and
    smiled. "Following space is in our blood. And our planet's so poor now
    that it's the only way most of our men can make a living." She added,
    "Some of our men never come back. My father didn't. And my mother died,
    when he was lost."</p>
    <p>It was dusk when they reached the spaceport. As he walked with the girl
    along its edge toward her brothers' ship, she drew him aside toward a
    tall shaft that loomed up spectrally in the twilight.</p>
    <p>"This is where the first Earthman went away to space," she told him.</p>
    <p>He looked at the deeply engraved legend on the pedestal of the soaring
    column. It was the Monument to the Space-Pioneers.</p>
    <p>"Gorham Johnson took off in his first flight from this very spot," Marn
    said.</p>
    <p>Carlin strained his eyes in the dusk to read the roll of names and
    dates engraved on the pedestal.</p>
    <p class="ph1">Gorham Johnson, 1991<br/>
    Mark Carew, 1998<br/>
    Jan Wenzi, 2006<br/>
    John North, 2012</p>
    <p>Names of the men who long ago had first dared space, the men who had
    first followed a dream to the nearby planets that then had seemed so
    far, the men who had first hurtled starward and opened up the galaxy.</p>
    <p>"Lord, more than two thousand years ago," Carlin murmured. "Queer
    little ships they must have had."</p>
    <p>His imagination was touched. This simple roll of names of men long dead
    somehow brought it all close to him for the first time.</p>
    <p>Those old, pathetically flimsy ships, the enormous courage of those men
    to whom space was all one unknown abyss. He began to understand why
    tourists came from all the galaxy to see these mementoes.</p>
    <p>"They and their little ships started it all, the whole galactic
    civilization, the vast human empire," he said musingly.</p>
    <p>Marn was looking up at the spire towering in the dusk.</p>
    <p>"People criticize us Earthmen for our pride. But this is why we're
    proud. We're the people who opened up the frontiers of the Universe."</p>
    <p>Carlin nodded thoughtfully. "You've a great heritage. But perhaps you
    remember it too well. This is the present, not the past."</p>
    <p>"You're like all the others, you think Earth's history is over," Marn
    said defiantly. "You'll find out differently. Earthmen will open up the
    last frontier of all—" She checked herself suddenly, and then said,
    crestfallen, "I'm sorry. I didn't mean to quarrel."</p>
    <p>Carlin wanted to ask what she had meant, but Marn started on again
    through the deepening darkness toward her brother's ship.</p>
    <p>He walked with her into the battered planet-cruiser and looked around
    curiously. It was a medium craft designed for a minimum crew, with
    oversize cyclotrons and propulsion-wave equipment, drive-plates fore
    and aft, and an unusually heavy set of heat-screen generators.</p>
    <p>"The Hot Side of Mercury is terrible," Marn said when she saw him
    glancing at the generators. "You need the heaviest heat-screens you can
    get to prospect there."</p>
    <p>Amidships, Carlin noticed a big, empty round room or hold. There was
    nothing in it but a skeleton of girders designed to hold something over
    a sliding plate in the floor.</p>
    <p>He remembered Jonny's big machine in the workshop. It would fit into
    this frame. He would have liked to make further inspection but Marn had
    found the instruments she had come after.</p>
    <p>As they emerged from the ship, a lean, uniformed figure in the dusk
    greeted them in a pleasant voice.</p>
    <p>"Hello, Marn. I saw you walking across the tarmac. How is Jonny coming
    with his plans?"</p>
    <p>It was a young man in the gray uniform of Control Operations, the
    agency of law and order throughout the galaxy. He bowed to Carlin.</p>
    <p>"I'm Ross Floring, Control Operations commander here. You're the
    Earth-treatment chap staying with the Lands? Glad to meet you."</p>
    <p>Floring was not more than thirty, an alert, clean-cut, likable young
    man. He turned back to Marn.</p>
    <p>"How soon are Jonny and his friends planning to take off for Mercury?"</p>
    <p>Marn looked uncomfortable. "I don't know, Ross. They have some more
    preparations to make, they say."</p>
    <p>Carlin somehow sensed a strain in the atmosphere. There was an
    earnestness in Floring's manner that was not accounted for by his words.</p>
    <p>"I like Jonny a lot, Marn," he said seriously. "You know that. I'd
    hate to see him have trouble on this expedition."</p>
    <p>Marn seemed to evade his meaning. "Jonny won't have any trouble. A trip
    to Mercury is nothing for Harb and him."</p>
    <p>"I sincerely hope he won't," Floring said quietly. "Copper isn't worth
    risking too much for. Tell him I said so, will you? And tell him I'm
    coming up some day to talk with him."</p>
    <p>Marn was obviously eager to get away. Carlin, puzzled, followed her.</p>
    <p>"I'll see you again, Mr. Carlin," Floring called after him pleasantly.
    "We can have a talk about home. Yes, I come from Canopus too."</p>
    <p>It wasn't until they were in the ato-truck driving homeward that Carlin
    realized he hadn't told Floring his name or origin. Why would Control
    Operations have taken the trouble to check up on that?</p>
    <p>"Floring seemed like a nice chap," he told Marn. The girl nodded,
    troubled.</p>
    <p>"He is—one of the best," she said. "And he likes Jonny. But he'd
    forget everything else for his duty."</p>
    <p>She was, obviously, thinking aloud rather than answering Carlin. He
    wondered again about that queer feeling of strain. It had sounded
    almost as though Floring were warning her.</p>
    <p class="ph1">CHAPTER V</p>
    <p class="ph1"><i>Desperate Play</i></p>
    <p>The truck wheezed and groaned up the dark old road to the ridge. In the
    velvet black skies, the stars were chains of glittering light. Vega,
    Arcturus, Altair—they looked far away.</p>
    <p>The house was dark when Marn stopped the truck behind it, though there
    were still lights out in the workshop. There was a solemn, buzzing hush
    about the starlit summer night.</p>
    <p>"I have to take these things back to Jonny," said the girl.</p>
    <p>"Marn, what are your brothers really planning?" Carlin asked her. "Does
    Floring know?"</p>
    <p>She twisted uncomfortably. "Jonny told you all about their plans
    himself, didn't he?"</p>
    <p>She was such a poor liar, she was so oddly appealing a figure in the
    starlight as she looked up at him with troubled white face, that
    sudden impulse made Carlin bend and kiss her.</p>
    <p>Her small body was firm and warm in his hands and there was a
    breathlessness about her cool lips. But she did not move.</p>
    <p>He looked down at her. "You don't mind, do you?" he asked.</p>
    <p>"No, I don't mind," Marn said, her voice toneless, "It's all right for
    a star-world visitor to have a little flirtation with an Earth girl
    before he goes away, isn't it?"</p>
    <p>"But it isn't that!" Carlin started to protest, and then stopped.</p>
    <p>After all, what was it but that? What could it be but that?</p>
    <p>"It's all right, but please don't again," Marn said quietly. "Good
    night, Laird."</p>
    <p>He went into the house feeling depressed and thoughtful. He wished now
    that he hadn't had that impulse. Marn wasn't the sophisticated sort.</p>
    <p>Lying in his bed and looking out the window at the distant spaceport
    beacons down in the valley, Carlin heard her come in and retire.
    Apparently Jonny and Harb were still working.</p>
    <p>What were they working at really? Why had Floring been so grave in his
    veiled warning?</p>
    <p>"Oh, the devil, it's none of my business," Carlin yawned. "There isn't
    much in this little system for them to get into trouble about. Nothing
    but eight or nine small planets and one medium sun."</p>
    <p>Carlin suddenly sat bolt upright in bed as his mind dwelt on that last
    thought.</p>
    <p>"The Sun? Good glory, that's what they're up to! It must be!
    Sun-mining!"</p>
    <p>He was dismayed, horrified by the sudden flash of revelation. The
    disquieting mystery that had puzzled him since his first coming here
    suddenly shaped clearly as pieces fell together in his mind.</p>
    <p>"They wouldn't be so crazy as to try it, surely! Yet it all fits
    together—the heat-screens on their ship, the secrecy about it all. And
    that machine I saw could be a big magnetic dredge!"</p>
    <p>Sun-mining! Most strictly forbidden of enterprises, banned by the
    Control Council for years since the first disastrous attempts at it had
    almost wrecked certain planetary systems.</p>
    <p>Visions of frightening possibilities crowded Carlin's mind, of a
    desperately reckless attempt unchaining catastrophe on the inner
    planets of this little system.</p>
    <p>"But Jonny Land wouldn't try it! He's a CE, he knows what would happen."</p>
    <p>Carlin could not convince himself. He remembered only too clearly
    Jonny's intense obsession with Earth's copper shortage, his quiet
    determination.</p>
    <p>And Floring must suspect something of the truth! That was what had made
    the Control Officer give his grave hinted warning.</p>
    <p>Carlin got up and feverishly dressed. He had to find out the truth,
    now, at once. If the Land brothers and their friends were really bent
    on such a mad enterprise, it would have to be stopped even if it meant
    his informing Control Operations.</p>
    <p>"If I could get one good look at the inside of that machine of theirs,
    I could soon tell whether it's really a magnetic dredge," he thought.</p>
    <p>He went quietly down through the dark house and out into the starlight.
    Light and sounds of activity still came from the workshop.</p>
    <p>Carlin crept toward it. He hated this spying. But he had to know. He
    couldn't permit a crazy attempt to unloose disaster here.</p>
    <p>The workshop was closed, and there were no windows. But as he stood
    irresolute, the big front doors opened and Loesser and two other young
    Earthmen came out, wearily mopping their brows.</p>
    <p>"We'll be back tomorrow, Jonny," Loesser called back into the building.
    "Ought to finish her up in a few days now."</p>
    <p>The three strode wearily toward their ato-truck and drove away. The
    doors remained open for the moment.</p>
    <p>Carlin stepped forward and from his vantage in the dark peered into the
    big lighted room. Jonny and Harb Land were putting back the metal cover
    on the central mechanism, before they too quit work.</p>
    <p>One glance at the interior of that machine was enough for Carlin's
    trained eyes. Those big magnetic-current coils, that massive beam-head,
    that battery of Markheim filters—he had been right, they spelled
    disaster.</p>
    <p>A small, hard object prodded Carlin's back and a voice throbbing with
    anger spoke in his ear.</p>
    <p>"This is an atom-pistol. Raise your hands. I don't want to harm you."</p>
    <p>"Marn!" he exclaimed, stunned.</p>
    <p>"Don't turn!" warned the girl. Her voice was choked with wrath. "I
    heard you get up and I followed you out here. You are a spy!"</p>
    <p>"Don't turn!" warned the girl. "I followed you here. You are a spy!"</p>
    <p>Carlin was so stunned with horror by his discovery of the brothers'
    catastrophic plans, that he reacted by sheer, desperate impulse to the
    weapon in his back. He swung around and grabbed for the atom-pistol.</p>
    <p>It would have been suicidal, had another than Marn been holding the
    weapon. But Marn, as much a stranger as he to deadly violence, let her
    finger hesitate on the trigger too long. Perhaps she would not have
    fired in any case. Pondering it later, he was not sure.</p>
    <p>What happened was that he got his hand on the slim pistol and snatched
    it out of her grasp before her hesitation ended. Marn, her face white,
    called frantically:</p>
    <p>"Harb! Jonny!"</p>
    <p>The two brothers came running out from the rear of the lighted
    workshop, Harb's craggy face dark and deadly as he saw them.</p>
    <p>Carlin jumped back, leveled the weapon he had just taken from the girl.</p>
    <p>"Get back!" he ordered hoarsely. And as Harb Land, blindly raging, came
    on: "I don't want to kill anybody!"</p>
    <p>Jonny's voice rang command. The lame youngster's thin brown face was
    set, but he had not lost calm.</p>
    <p>"Harb, stop!"</p>
    <p>The thing froze into a queer sort of tableau as Harb Land pulled up
    and stood there, his giant figure quivering with wrath, his big fists
    clenched as he glared at Carlin.</p>
    <p>"I told you," Harb said thickly over his shoulder to his brother. "I
    told you what would happen if we took him in."</p>
    <p>Marn had run toward them, her face pale and stricken.</p>
    <p>"It's my fault, Jonny," she said despairingly. "I heard him come out
    and followed him, but let him take my gun instead of shooting."</p>
    <p>"Quiet, Marn," soothed Jonny. "It's going to be all right. Carlin just
    doesn't understand."</p>
    <p>The lame youngster, in this taut moment of strain, was suddenly the
    biggest of them, the dominating personality here.</p>
    <p>"I understand, all right," Carlin said hotly. "I guessed it tonight,
    and one look at that magnetic dredge confirmed my guess." His voice
    crackled with the rising wrath he felt. "Going to Mercury prospecting,
    were you? You never had any such plan. You and your partners have been
    getting ready to attempt sun-mining."</p>
    <p>Jonny's eyes and voice were calm as he said:</p>
    <p>"Carlin, Earth's starved for power. You've seen for yourself. To get
    the power that will revive our world, we've got to have copper. And
    the copper in our planets was exhausted long ago. But there's still
    billions of tons of copper in our System, in one place. The Sun. It's
    there in hot gases, more copper than Earth and our sister-planets will
    need for millenniums to come. It's our only possible source of copper
    and we intend to tap it."</p>
    <p>"You and the others have brooded so long over your need for copper that
    you've gone crazy!" Carlin said, his voice whipped with anger.</p>
    <p>"What's crazy about our using the copper of the Sun for our planet?"
    Jonny asked evenly.</p>
    <p>"You, a CE, ask me that?" cried Carlin. "You know as well as I do that
    sun-mining brings catastrophe! Oh, you can get close enough to the Sun
    in your ship, I know. You can suck up all the gaseous copper you want
    from it, with that magnetic dredge. But what happens on your Sun when
    you do it?</p>
    <p>"You know as well as I what would happen, what has always happened
    when it was tried. The suction creates a whirl in the solar surface,
    a tiny Sun-spot that grows and grows until it's grown into a terrific
    solar typhoon that pours disastrous increased heat and electric force
    onto its planets. You know it's happened every time Sun-mining was ever
    tried, and that that's why Control Council forbids Sun-mining."</p>
    <p>Jonny Land nodded calmly. "I know all that. But suppose I've found a
    way to do Sun-mining without starting Sun-spots?"</p>
    <p>Disbelief hardened Carlin's voice. "You haven't. Nobody ever has. There
    just isn't any way—suck out gases from any point on the Sun and you
    lower pressure at that point, and lowered pressure automatically starts
    a whirl."</p>
    <p>"Carlin, I <i>have</i> found such a way! I tell you, with it we can suck
    unlimited copper from the Sun without creating one tiny Sun-spot!"</p>
    <p>Laird Carlin stared. "You're telling me that, because you know I'm
    going to report your plans to Control Operations."</p>
    <p>"You wouldn't do that!" cried Marn, incredulously.</p>
    <p>Carlin nodded firmly. "I don't want to but I've got to. I can't let a
    bunch of crazy men bring on a disaster that might scorch life itself
    off your inner planets."</p>
    <p>Jonny Land's thin face flared irritable emotion as he limped forward
    unheeding of the gun in Carlin's hand.</p>
    <p>"Carlin, man, be reasonable! Why do you suppose I had you come here and
    live with us? It was because you're a CE and I'll need another trained
    engineer's help in operating this thing. And do you suppose I ever
    thought I could get your help unless I could convince you I've found
    the way to safe Sun-mining? I can convince you, Carlin!"</p>
    <p>Carlin felt the conviction in Jonny's voice. What the crippled young
    man said did logically explain something otherwise puzzling—why they
    had taken him into their home when their work was so secret.</p>
    <p>He remembered now that it was not until Jonny Land had learned he was
    a CE, on his first arrival on Earth, that the young Earthman had shown
    interest and offered him lodgings.</p>
    <p>"All I ask," Jonny was saying earnestly, "is that you give me a chance
    to explain our plans to you. I know I can convince you that we can mine
    the Sun without the slightest danger of disaster."</p>
    <p>"If that's so," Carlin demanded skeptically, "why didn't you convince
    the Control Council of that, and get permission for Sun-mining instead
    of trying to do all this in secret?"</p>
    <p>"Carlin, I did try to convince the Council," Jonny Land declared. "I
    made one petition to them after another, giving them full details of
    my plan. But Council isn't composed of engineers. And the popular
    prejudice against Sun-mining, due to those past disasters, is so strong
    that Council refused us permission to make the attempt."</p>
    <p>"That's why Ross Floring and the others down at Control Operations
    watch my brothers so closely, Laird," Marn added quickly. "They know
    about our petitions, and Floring suspects that Jonny is going to try
    this thing anyway."</p>
    <p>It all fitted together logically, Carlin had to admit. Yet he still
    stood irresolute, the atom-gun in his hand.</p>
    <p>"Here's a proposition, Carlin," said Jonny. "I'll explain every detail
    of our plan to you in the morning. If you don't admit then that the
    plan's completely without danger of disaster, I'll let you go and tell
    everything to Floring. I give you my word on it."</p>
    <p>Carlin looked at him doubtfully. "Jonny, you'd break your word as
    cheerfully as your neck to carry out your purpose for Earth."</p>
    <p>Jonny Land grinned crookedly. "That's true. But on the other hand,
    I'm still hoping for your help in this project. That's why I want to
    convince you, and that's the best guarantee I can give you."</p>
    <p>Carlin shrugged, but he slowly lowered the weapon.</p>
    <p>"I can tell you right now that I'll have no part in any such illegal
    venture," he said flatly. "But I'm willing to hear your explanation."</p>
    <p>"Well," Jonny said, with a tired sigh, "we've had enough dramatics
    for one evening. Harb, lock up the workshop and we'll all turn in for
    tonight."</p>
    <p>Carlin looked a little awkwardly at Marn as he handed her back the
    atom-pistol.</p>
    <p>"I'm sorry if I appear ungrateful for your hospitality," he told her.
    "It's just that I can't stand by and do nothing if a crazy attempt
    threatens to bring on catastrophe."</p>
    <p>"I know," Marn said soberly, and there was no hostility in her face.
    "But you'll find out that Jonny knows what he's doing."</p>
    <p>Out of the darkness behind them spoke a shrill voice that made Laird
    Carlin swing around in astonishment.</p>
    <p>"Well, I'm blamed glad you people quit arguin' for tonight, anyway.
    It's time all decent folks was in bed."</p>
    <p>Gramp Land stood back there in the dark where he had apparently been
    standing for some time. There was a grin on his withered face as he
    lowered the heavy atom-gun he had been holding.</p>
    <p>"Sure got tired holdin' this thing aimed at your back, Mr. Carlin," he
    chuckled.</p>
    <p class="ph1">CHAPTER VI</p>
    <p class="ph1">"<i>You Owe a Chance to Earth!</i>"</p>
    <p>Doubts assailed Carlin almost as soon as he retired. He could not
    sleep, the rest of that night.</p>
    <p>Had he been childish to let Jonny persuade him into giving the plan a
    hearing? Jonny was sincere enough, but he was a fanatic on this one
    subject of securing power for Earth.</p>
    <p>The recklessness of Earthmen was proverbial. These men, made desperate
    by long brooding over the poverty of their world, might think little of
    the danger of provoking solar catastrophe in their obsessed desire to
    secure copper.</p>
    <p>Carlin chilled. He remembered what had happened years ago at the star
    Mizar when Sun-mining had been attempted. The suck of magnetic dredges
    swiftly creating a whirl in the star's surface gases, a Sun-spot
    maelstrom that had expanded with disastrous swiftness. And then the
    engulfing of the mining ships in the sudden outpour of increased heat,
    the scorching of inner planets that wreaked ruin before the spots
    subsided.</p>
    <p>It had been the same later at Polaris, and at Delta Gemini. No wonder
    that such a popular wrath against Sun-mining had arisen that Control
    Council had strictly forbidden further attempts! Man's science, great
    as it was, was not yet great enough to dare tampering with stars.</p>
    <p>Yet he could see, too, how these Earthmen would inevitably turn their
    thoughts to Sun-mining. There was not any copper left in their System
    except in one body—their Sun. And that had limitless amounts of the
    power-metal, in vaporized form. No wonder they had been led into the
    plan to tap the metal of their Sun.</p>
    <p>Carlin dozed before daybreak, but woke with the sunrise and went down,
    to find the others already at breakfast. They greeted him with a word,
    all but Harb Land who maintained a stony, dangerous silence.</p>
    <p>"We'll go out and show you our work, as soon as you have breakfast,"
    Jonny said quietly.</p>
    <p>Gramp Land was the only one in good spirits. The old man twitted Carlin.</p>
    <p>"It's sure a good thing you got reasonable last night. I would have
    hated to blast you."</p>
    <p>Marn smiled slightly. "You wouldn't have done it. You're too
    chicken-hearted even to kill a fly."</p>
    <p>"Ho, what are you talking about?" exclaimed Gramp indignantly. "When I
    was young, they called me the toughest Earthman in space."</p>
    <p>Carlin walked silently out to the workshop with Harb and Jonny. The
    lame youngster opened the building, and then gestured toward the tall,
    cylindrical machine.</p>
    <p>"Take a look for yourself, first," he invited.</p>
    <p>Carlin scanned the mechanism with trained eyes. Magnetic dredges were
    a little out of his line, yet the principle of the mechanism was clear
    enough.</p>
    <p>"You understand the basic idea of Sun-mining?" Jonny was saying.
    "A ship approaches the photosphere or visible surface of the Sun
    as closely as possible, protected by heavy heat-screens from the
    radiation. The magnetic dredge is then turned on. The dredge generates
    a high-powered magnetic field concentrated into a beam. That beam
    drives down into the swirling super-hot gases of the solar surface.</p>
    <p>"Those gases consist of dozens of metals and other elements in
    vaporized form—iron, copper, sodium, calcium and so on, all mixed
    together. The beam sucks a column of those solar gases up to the
    ship. For its magnetic pull powerfully attracts the iron vapor in the
    mixture, and so the whole mixture is rapidly sucked upward."</p>
    <p>He pointed to the massive flared nozzles in the downward projector-face
    of the great machine.</p>
    <p>"The gases are sucked in there, through Markheim filters which can be
    set to screen out the atoms of any desired element. The copper gases
    are screened out, solidified by cooling, and stored. The other gases go
    on through the filters."</p>
    <p>Carlin nodded curtly. "And those unwanted gases are ejected into space,
    and more of the solar mixture continuously drawn up, and so on until
    your ship is filled with copper. Yes, it's the same scheme that was
    used by the Mizar and Polaris Sun-miners. And it will have exactly the
    same result! Sucking gases out of any point in the solar surface will
    lower pressure at that point. And lowered pressure at any point of the
    photosphere instantly and inevitably starts a whirl of gases, a growing
    maelstrom or Sun-spot!"</p>
    <p>Jonny Land shook his head. "Carlin, you're jumping to conclusions. This
    dredge does not simply eject its unwanted gases into space like former
    designs. Take a look at that beam-head more closely."</p>
    <p>Carlin looked. And he was puzzled, after a brief inspection of the
    curious concentric construction of the beam-head.</p>
    <p>"I don't get it. It looks like you have two circular beam-heads, one
    inside the other."</p>
    <p>"That," said Jonny, "is the secret of my scheme. Lowered pressure in
    the solar surface at the point of suction creates a whirl, a Sun-spot.
    But suppose we can suck up gases without lowering pressure?"</p>
    <p>Carlin stared. "How?"</p>
    <p>"The two beam-heads," reminded the lame youngster eagerly. "The inner
    one is the one that beams down a positive magnetic pull to suck up
    solar vapors. The outer one is designed to use a simultaneous negative
    magnetism to shoot the unwanted vapors back down into the Sun."</p>
    <p>The whole meaning of the explanation flashed over Carlin, and the
    possibilities of it dawned across his brain.</p>
    <p>He said nothing, but crawled under the towering dredge and for minutes
    inspected inside and outside of the beam-head, feed-tubes and cut-offs.
    He finally came back out to them.</p>
    <p>"Well?" challenged Jonny Land.</p>
    <p>Carlin bit his lip. "I've got to admit your scheme looks practical
    enough. You should be able to suck up gases without any Sun-spotting
    effect, by using that continuous kickback. But—"</p>
    <p>"But what?" demanded Harb Land, frowning.</p>
    <p>Carlin shook his head. "Blast it, I can't see why the Council would
    turn down your petition if this is as workable as it seems."</p>
    <p>Jonny shrugged. "I told you why. Control Council contains the finest
    statesmen in the galaxy. Statesmen, not engineers. They admitted their
    experts' reports on this showed it theoretically workable. But they
    said it was too dangerous to take a chance on theory when it comes to
    tampering with suns. We don't need copper that badly, they said."</p>
    <p>His fists clenched in sudden passion. "We don't need copper! The galaxy
    as a whole doesn't need it, they meant. And what does it matter if one
    little world called Earth is fading and dying for lack of the copper
    it squandered to open up the galaxy? What does it matter, except to
    Earthmen?"</p>
    <p>It was the first time that Carlin had ever seen Jonny Land give way to
    emotion. The superhuman strain that drove and dominated this lame, thin
    youngster for a moment flared hot and anguished on his face. Then his
    narrow shoulders sagged. He stood looking at the towering dredge with
    brooding eyes, before turning to Carlin.</p>
    <p>"Carlin," he said then, "there's only one way to prove to the Council
    this way of Sun-mining is safe—and that's by doing it! That's what
    we're going to do. We're going to the Sun and come back with a shipload
    of copper. They'll see then that it's wholly safe. They'll have to
    give permission then. And a fleet of ships equipped with dredges can
    suck enough copper from the Sun to give Earth all the power it needs
    hereafter.</p>
    <p>"You've seen the dredge and you know our plans. You've seen enough of
    Earth to know how much our success would mean to this world. Carlin, do
    you still want to tell Floring about this?"</p>
    <p>"You couldn't!" exclaimed Harb Land harshly. "You couldn't destroy all
    the hope that's left for our world's people. You—all you star-world
    people—you owe this chance to Earth!"</p>
    <p>Carlin stood there, torn by conflicting feelings. Strong among them was
    his intense admiration as an engineer for the ingenuity and daring of
    Jonny Land's solution to the problem.</p>
    <p>But there were other things to consider. There was the duty he and
    every citizen had to support the Control Council. That support was what
    kept galactic civilization going. Yet these Earthmen, this little band
    fighting so fiercely for their ancient, worn world would flout it.</p>
    <p>"Jonny!" came Marn's sharp cry from outside. "Jonny!"</p>
    <p>"Something's wrong!" Jonny exclaimed, limping hastily forward.</p>
    <p>They hurried out into the sunlight. Marn was running toward them and at
    the same moment they heard the drumming of an approaching ato-car.</p>
    <p>"It's Ross Floring coming here!" Marn panted. "I recognized his car
    coming up the hill!"</p>
    <p>Harb uttered a fierce exclamation, but Jonny cut in quickly:</p>
    <p>"He's only coming up here to look around. He suspects what we're up to,
    but he can't be sure. Don't show any excitement."</p>
    <p>Harb gestured fiercely toward Carlin. "But if he says anything, Floring
    will know."</p>
    <p>A pleasant voice hailed them. Ross Floring, lean in his gray uniform,
    drove up behind the house and climbed out of his ato-car.</p>
    <p>"Hello, folks," he greeted. "Thought I'd come up and see you. Jonny, I
    haven't seen you for weeks. Every time you come down to the spaceport,
    you spend all your time buried in that ship."</p>
    <p>Jonny smiled. "It's keeping us pretty busy, getting ready."</p>
    <p>Laird Carlin sensed genuine liking between the Control Operations
    officer and the lame young engineer. Yet there was unspoken tension
    too. It showed behind Jonny's cool smile and Floring's pleasant eyes.</p>
    <p>Floring was looking past them, through the open doors of the workshop
    at the towering magnetic dredge.</p>
    <p>"Is that your new metal-finding dingus, Jonny? The thing you're going
    to use to locate copper on Mercury?"</p>
    <p>He stepped toward it. Harb Land made a violent movement forward, but a
    flat look from his brother stopped him.</p>
    <p>"Yes, that's it," Jonny said. "Want to look it over, Ross?"</p>
    <p>Floring stood, cocking his head at the towering machine. He laughed at
    the question.</p>
    <p>"Jonny, you know I'm no engineer. A thing like this is beyond me." He
    turned toward Carlin. "But Mr. Carlin, you're a CE. What do you think
    of this new metal-finding device of Jonny's?"</p>
    <p>Breathless silence held the group for a moment. Floring's face was
    unmoved, pleasant, but his purpose was obvious now. Knowing that Carlin
    had come to Earth merely as an Earth-treatment case, he was counting on
    Carlin's unbiased truthfulness.</p>
    <p>Carlin felt their eyes on him. Now was the time, he knew, to play the
    part of a good galactic citizen and inform Floring just what was going
    on. It was his duty to do it.</p>
    <p>But he couldn't! He couldn't betray the last desperate hope of a
    gallant old planet's people in their struggle against destiny! He had
    known he couldn't, from the time Floring had first appeared. He spoke
    as casually as he could.</p>
    <p>"Yes, I've looked it over. It's one of the most ingenious metal-finders
    I've ever seen."</p>
    <p>Carlin felt a queer relief that was almost happiness, as he spoke. For
    he knew now that he could never have obstructed these people in their
    brave, desperate struggle to revive their planet.</p>
    <p>But Ross Floring looked astounded. A little blank frown of surprise
    came into his face and he stared steadily at Carlin.</p>
    <p>"Then you approve of Jonny's plans?" he said quietly, "But, of course,
    I might have known that he'd convince you."</p>
    <p>There was double meaning to the Control officer's words, clear to all
    of them. Yet they all ignored it.</p>
    <p>Floring was temporarily defeated. He couldn't take action without
    expert opinion that the machine before him was for Sun-mining. He had
    expected such an opinion from Carlin, and had been disappointed.</p>
    <p>But he was not completely frustrated. Carlin found out now how
    thorough and resourceful was this pleasant young officer.</p>
    <p>"It would be a shame, Jonny," Floring remarked casually, "if you should
    run into disaster on this trip and the design of your new apparatus be
    lost. A metal-finder like this is too valuable to lose."</p>
    <p>They were momentarily puzzled by the comment. But in the next moment,
    Floring showed what he had in mind. He drew from his jacket pocket
    a tiny tri-dimen camera, stepped close to the towering dredge, and
    before anyone could prevent it had snapped a half-dozen pictures of its
    interior mechanism.</p>
    <p>Harb Land started forward with a smothered oath. But it was too late.
    Floring was already pocketing the camera.</p>
    <p>"I'll keep these films," he said calmly. "If your machine should ever
    be lost, the design of it will be preserved this way."</p>
    <p>"You can't keep those films!" Harb Land exclaimed angrily. "You've no
    right!"</p>
    <p>"You surely don't think I would steal the design from you?" Floring
    said, with a look of surprise.</p>
    <p>"It isn't that," Harb protested. "But—"</p>
    <p>"But what?" the officer asked calmly.</p>
    <p>Harb was silent, his craggy face a mixture of emotions as he looked
    appealingly at Jonny.</p>
    <p>Carlin understood Floring's cleverness. They could not protest the
    films without giving the real reason for their protest, and that they
    could not do.</p>
    <p>"It's all right for him to keep those pictures, Harb," Jonny said
    quietly.</p>
    <p>Floring turned, bidding a pleasant farewell.</p>
    <p>"I'll be seeing you again soon," he promised.</p>
    <p class="ph1">CHAPTER VII</p>
    <p class="ph1"><i>Last Frontier</i></p>
    <p>As soon as Floring's ato-car had purred away, the little group stood in
    the sunlight outside the workshop, in stricken silence.</p>
    <p>Carlin put into words what was in all their minds.</p>
    <p>"Jonny, you know why he took those pictures! He'll telephoto them to
    Canopus headquarters to be examined by engineer experts, and they'll
    send back word that the machine is a magnetic dredge for Sun-mining!"</p>
    <p>Jonny nodded. "Yes, of course. Floring has suspected our plans all
    along, and now he's going to make sure."</p>
    <p>"And when word comes back from Canopus, he'll seize our dredge and ship
    to stop our expedition!" groaned Harb.</p>
    <p>"I know that," Jonny Land said, as his blue eyes swept them. "But it
    will take fourteen or fifteen hours before he gets that report back.
    Before that time ends, we've got to be on our way to the Sun!"</p>
    <p>Laird Carlin felt a shock of astonishment, but before he could comment,
    Jonny was speaking swiftly on.</p>
    <p>"It's our only chance now—to get away before Floring receives the
    proof that will authorize him to stop us! The dredge here is almost
    finished. If we can install it in the 'Phoenix' and take off tonight,
    we'll have our chance to prove to the galaxy that Sun-mining can be
    safe."</p>
    <p>"Install the dredge tonight?" cried Harb Land. The gangling giant's
    face was sick with anxiety. "Jonny, we can't do it! Not that soon."</p>
    <p>"We've got to!" Jonny's voice cut like a steel rapier. "Harb, you go
    get Loesser and Vito and the other boys. Have them bring the big truck
    with them. If we work hard enough, we should be able to have the dredge
    ready to roll by dark. Once we get it into the 'Phoenix', we can take
    off and complete installation in space."</p>
    <p>"You can't do it," groaned his brother. "You know you figured on taking
    a week yet for that installation."</p>
    <p>Carlin stepped forward. He had long ago reached his decision. He had
    reached it in that moment when he had answered Floring.</p>
    <p>"I'm a CE, you know," he reminded. "I can help a lot in that
    installation."</p>
    <p>Marn stared at him, amazement and dawning gladness in her eyes. And
    Harb Land's tortured face turned haggardly on Carlin.</p>
    <p>"You'd do that? You'd help us? By heaven, if you would, we might make
    it!"</p>
    <p>Jonny's brilliant blue eyes bored Carlin's face.</p>
    <p>"Carlin, I was hoping for this. I knew from the first I'd need another
    engineer's help in installing and operating the dredge. I brought you
    home because I was hoping I could enlist your aid before we started on
    the expedition. But all the same, I've got to warn you. We're directly
    bucking a Control Council order. You can lose your certificate and go
    to Rigel prison, even if our plan succeeds. And if it doesn't succeed,
    it may mean perishing with us. And after all, Earth isn't your world."</p>
    <p>"Who the devil is doing anything for Earth?" Carlin retorted. "This old
    planet of yours means nothing to me either way."</p>
    <p>"Laird, are you so sure of that?" Marn asked him, her eyes very bright.</p>
    <p>"Do we have to get emotional?" Carlin asked roughly. "I'm an engineer,
    and this is the biggest engineering experiment to be tried for
    centuries. Don't you think I want to be in on it?" He added crushingly,
    "And as for my getting mixed up in the blame, I'm already blasted well
    mixed in it. When I denied to Floring that this was a magnetic dredge,
    I implicated myself right there in the whole business. I've got to make
    it succeed, now."</p>
    <p>Harb Land was already running toward his truck. Jonny shot sharp orders
    at his sister.</p>
    <p>"Marn, I want you and Gramp to watch the road this afternoon. Floring
    might come back. Carlin, you and I haven't a moment to lose."</p>
    <p>Carlin strode after the limping youngster into the workshop, and Jonny
    there rapidly explained what remained to be done.</p>
    <p>"The kickback feed-pipes to the beam-head have to be hooked up, the
    cooling coils to solidify the copper are not yet in place, and the
    whole dredge has to be fastened in its frame so it'll be ready to swing
    aboard the truck tonight."</p>
    <p>Carlin was appalled by the amount of work that remained, for two pairs
    of hands. But Jonny added an encouraging qualification.</p>
    <p>"Loesser and Harb and the others can help in the ato-welding and cable
    work if we set it up for them. They're all veteran spacemen and know
    how to handle ordinary tools."</p>
    <p>Carlin plunged into the work with Jonny. But as they toiled to set up
    the coils and feed-pipes of the massive mechanism, an inward aghastness
    at what he was doing oppressed Carlin's mind.</p>
    <p>Why was he doing it, breaking Control law and endangering his
    certificate and even his liberty? Why under heaven should he be sharing
    the risks of these men for a planet he hadn't even seen until a few
    weeks ago?</p>
    <p>"I must still be star-sick, unstable," he thought dismally. "Or I'd
    never have got mixed up in this mad business. Sun-mining!"</p>
    <p>Blind reaction was dominating him. Curse it, he wasn't the type to
    join Quixotic forlorn hopes. He was Laird Carlin, sober, hard-working
    engineer, who ought right now to be far across the galaxy at the job to
    which he belonged.</p>
    <p>And all the time Carlin's mind spun miserably to this whirl of
    self-reproach and foreboding, he was working with Jonny at topmost
    speed, squeezing into the frame of the great dredge where the lame
    youngster could not go, fastening Veer-clamps, hooking self-sealing
    leads to the flat Markheim filters.</p>
    <p>The sound of ato-trucks rocked the noon air, and Harb Land came running
    heavily into the workshop.</p>
    <p>"I got the others—Loesser's bringing in the big truck now," panted
    Harb. "What do you want us to do, Jonny?"</p>
    <p>Loesser, and Vito, and the other four young Earthmen who came hastening
    after Harb were dominated by excitement. Loesser's broad red face was
    shining with emotion as he came up to Carlin.</p>
    <p>"I want to apologize. I never thought any star-world stranger would
    come in with us and help us."</p>
    <p>"Save it, and get the welders on those rear feed-pipes," Carlin
    retorted. "Get in here—I'll show you."</p>
    <p>Through the hot afternoon hours, the hiss of ato-welders and reek of
    fusing metal stifled the workshop.</p>
    <p>Dripping with perspiration, stiff from cramped postures, Carlin worked
    on inside the great dredge.</p>
    <p>And all those hours, in rhythm with the welders' hiss and the clang of
    wrenches, his thoughts beat a mocking tempo through his brain.</p>
    <p>"All this, for no reason! For somebody else's world, a world that ought
    to have been evacuated long ago! Even if it succeeds, you win nothing.
    And if it fails, the Sun licks you all up like midges."</p>
    <p>Yet he labored blindly on. It might be crazy, but what he had started,
    he would finish.</p>
    <p>It was work against an inexorable time limit that rapidly was
    approaching. As the shadows lengthened, as the sun went down, they
    still had not finished.</p>
    <p>Jonny Land limped unsteadily to turn on the workshop lights. His face
    was a gray mask of fatigue and sweat as he turned to the others.</p>
    <p>"Two more hours," he said huskily. "We can't take more, if we're to get
    the dredge into the 'Phoenix' and take off before midnight."</p>
    <p>Those two hours, afterward, seemed weeks in length to Carlin. And the
    mocking devil in his brain kept taunting, "It's no business of yours,
    you know!"</p>
    <p>"That's near enough!" Jonny's hoarse voice finally declared. "We can
    hook up those last cables on the way. All the work that require heavy
    tools is done—and we daren't take more time."</p>
    <p>They were, all of them, drunk with fatigue, staggering with the furious
    drive of twelve hours of unbroken toil. Blackened by welder flare,
    glistening with sweat, they looked to Carlin like a crew of devils.</p>
    <p>Jonny's driving energy remained unconquerable.</p>
    <p>"Marn," he ordered, "back the big truck in here. Harb, you and Carlin
    rig the hoist."</p>
    <p>The big, flat-bodied ato-truck backed ponderously into the workshop
    and they swung the massive magnetic dredge carefully aboard. Loesser
    and the others then hastily chained it to the bed of the truck.</p>
    <p>Jonny limped toward the cab. "All right, we're starting. Harb, you
    drive. No, Marn—you're not going to the spaceport with us."</p>
    <p>Marn, face white and eyes big with fear, saw the gleam of the
    atom-pistol that Harb was thrusting into his pocket.</p>
    <p>"Oh, Jonny, not that, no matter what happens!"</p>
    <p>Jonny's blue eyes flashed arctic light. "That, or anything, now," he
    rasped. "You know what this means to our people, Marn."</p>
    <p>Then his face softened, and he patted her arm.</p>
    <p>Tears streaked her cheeks as she kissed and clung to him, and then to
    Harb.</p>
    <p>Carlin was climbing heavily onto the truck when he felt her touch on
    his arm.</p>
    <p>"You too, Laird," she whispered, quivering lips blindly pressing his
    cheek. "All of you must come back."</p>
    <p>"Get on!" cried Harb Land, and then the truck went into gear.</p>
    <p>Carlin jumped for the cab, and under the starry night they were rolling
    at increasing speed down the twisting road toward the valley.</p>
    <p>And suddenly all the nightmare mocking in Carlin's brain was gone and
    there was only the rush of sweet air against his face, and the splash
    of the lamps ahead, and the jolt and rumble of the big machine as they
    raced down toward the spaceport's distant beacons.</p>
    <p>Earth air and Earth smells in Carlin's nostrils, sleepy Earth sounds
    in his ears; the shine of the old spaceport's beacons, and the soaring
    loom of the distant tower that marked the spot where a man of long ago
    had first dared space. This world, this little Earth, was worth risking
    death for, even for a stranger from far stars!</p>
    <p>He knew he was a little crazy, he still had a corner of his mind that
    told him all this was mere intoxication of emotion which was sweeping
    away reason. But the mocking devil in Carlin's mind was gone, and he
    was one in mind and purpose with his companions, now.</p>
    <p>The others too were feeling that wild reaction, for Loesser clapped
    Carlin's shoulder, crying:</p>
    <p>"It's like getting out of prison to get started!"</p>
    <p>"We're not off Earth yet!" warned Jonny. "Cut the lights and drive
    around to the north end of the spaceport, Harb. Ease the truck to the
    'Phoenix' as quietly as you can." A little later he warned, "Slower,
    slower. Keep to the edge of the tarmac."</p>
    <p>Lightless, its motors a mere low rumble, the big truck crept around the
    dark edge of the spaceport toward the "Phoenix." The little planet-ship
    took black shape in the darkness, a low, torpedo bulk brooding beneath
    the stars. Harb backed the truck toward its side, as they jumped out of
    the cab.</p>
    <p>Light flashed on them from a hand-krypton in the door of the "Phoenix!"
    A lean, uniformed figure stood there, gun in hand, looking at them.</p>
    <p>"I thought you would be coming," said Ross Floring quietly. "Jonny, I'm
    sorry about this."</p>
    <p>Carlin was as frozen as his companions, by the disastrous overturn of
    their attempt at secrecy. Floring stepped out of the ship.</p>
    <p>"I've been looking through your ship while I waited," he said. "You
    have triple as much heat-screen coverage as you'd need for the Hot Side
    of Mercury. You were going to the Sun."</p>
    <p>"You can't prove it, Ross," Jonny said levelly. "You've no proof."</p>
    <p>"I've enough to prohibit this ship from clearing Earth until
    investigation," Floring replied. "A certain report will reach me from
    Canopus by morning. Then we'll see."</p>
    <p>Carlin saw it then, saw the dark giant figure of Harb Land stealing
    around the truck and looming up behind Floring. He glimpsed the gleam
    of Harb's raised atom-pistol.</p>
    <p>Then Harb struck. The butt of the weapon came down on Floring's head
    and the officer crumpled limply to the tarmac.</p>
    <p>"See if anyone else is in the ship!" Jonny said swiftly. "Loesser,
    watch the Control station!"</p>
    <p>Then he bent with Carlin over the unconscious man.</p>
    <p>"We'll have to take him with us," Jonny said. "If we leave him here
    he'd soon be found, then the Control cruisers would be after us."</p>
    <p>A few weeks before, Laird Carlin would have been aghast at seeing
    a semi-sacred officer of Control Operations struck down. With what
    spirit of reckless defiance of law had his companions infected him? He
    marveled at himself as he coolly picked up the limp figure.</p>
    <p>"Tie him into one of the chairs in the pilot room," Jonny was saying.</p>
    <p>Harb came plunging out of the ship. "Nobody else aboard. He came over
    here alone."</p>
    <p>By the time Carlin had the unconscious man secured in the pilot room,
    Harb and the others had slid open the big hatch in the side of the
    "Phoenix." Hastily, fumbling in darkness, they ran out the ship hoist
    and hooked onto the big magnetic dredge.</p>
    <p>Then, with infinite labor, they swung the massive mechanism into the
    hold amidships. Mere short flashes of hand lamps had to suffice to
    guide the beam-head of the dredge down into the round keel opening.</p>
    <p>"Fasten half the frame bolts—they'll hold till we get into space,"
    panted Jonny.</p>
    <p>Carlin skinned his knuckles in the dark, fumbling with bolts and
    wrench. Every instant he expected to hear an alarm from Loesser that
    Control officers were coming.</p>
    <p>"That'll have to hold," said the sweating Jonny. "Run the truck off the
    tarmac. Harb, make ready for take-off!"</p>
    <p class="ph1">CHAPTER VIII</p>
    <p class="ph1"><i>Solar Struggle</i></p>
    <p>Oxygenators started throbbing, doors clanged, as the others tumbled
    aboard. Harb Land, smeared with dirt and oil, his shock of hair wild,
    climbed into the pilot seat and expertly touched controls.</p>
    <p>"Generators coming on!" sang Loesser's breathless voice from the
    interphone, as the low, deep hum began.</p>
    <p>"Stasis on," said Harb rapidly, his fingers busy. The blue cushion of
    force was around them as Carlin slumped drunkenly into a seat. "Zero,
    two and five acceleration schedule. Here we go!"</p>
    <p>And the "Phoenix" swept up with a rush from the spaceport, the
    propulsion-waves streaming from its drive-plates hurling it out and
    upward into the star-sown sky, the spaceport lamps and the southward
    blinking lights of New York falling swiftly away.</p>
    <p>"Authorization!" yelped a startled voice from the universal communic on
    the panel. "Give authorization for take-off!"</p>
    <p>"Authorization already given," Harb Land rapped back, then cut the
    communic. He laughed. "That'll puzzle them a while."</p>
    <p>Crazy, reckless, suicidal, to Carlin seemed the way that Harb was
    taking them out from Earth. The atmosphere of the planet had no sooner
    started a shrill, rising scream around them than it fell and faded as
    they came out of the envelope of air.</p>
    <p>Luna burst up out of the eastern heavens like a great globe of dull
    gold against the stars. And then Carlin's eyes were smitten by the
    flare and glare of the brilliant disk of Sol, of the Sun.</p>
    <p>And then the "Phoenix" lined out and was plunging headlong through the
    void at a speed that Carlin knew was flatly illegal to use inside any
    System, a rush toward that distant Sun flare.</p>
    <p>"Cut down, cut down!" cried Jonny to his brother. "Any more speed and
    you'll not be able to decelerate in time to orbit around the Sun."</p>
    <p>Harb Land turned a wild, dirty face aflame with emotion. "By heaven,
    we're on our way at last! We'll show them now that Earthmen can still
    blaze a space-trail nobody else has dared!"</p>
    <p>And from back amidships came a hoarse voice jubilantly singing the old
    Earth space-song:</p>
    <p>Jonny Land's voice lashed them, his thin face dripping and determined.</p>
    <p>"You're all of you blowing your tops with excitement. This hasn't even
    started yet. Look at what we're heading for!"</p>
    <p>Carlin heard the others fall silent and himself felt a chill of awe as
    he looked ahead at the giant fire orb toward which the "Phoenix" was
    plunging.</p>
    <p>"We'll be orbiting before we have the dredge set up, unless we hurry,"
    Jonny prodded. "Come on, help me with it."</p>
    <p>The big magnetic dredge had to be bolted into place, the coils and
    pipes had to be hooked to their connections inside the ship, the cables
    to the generators, the cooling coils to the compressor, the outlets of
    the Markheim filters to the bunkers astern.</p>
    <p>Thrumming, creaking, shivering in every strut to the blind thrust of
    power that was hurling it on, the "Phoenix" rocked and shook about them
    as Carlin labored with Jonny and two of the other men to make those
    last connections. The cramped space in the hold around the dredge was
    hot, stifling, for the oxygenators couldn't keep the air there pure.</p>
    <p>"All ready!" Jonny called finally, after eternal-seeming hours of toil.
    "And none too soon. We're getting there fast. Harb has put out most of
    the heat-screens."</p>
    <p>Through the windows, the ship seemed enveloped by a halo of dim light,
    the force-screens that repelled radiations of heat.</p>
    <p>But when Carlin stumbled with Jonny into the pilot room, they were half
    blinded even through the screens by the fierce, blazing glare from
    ahead.</p>
    <p>Half the sky ahead was Sun, a gigantic abyss of roaring flame that
    crushed the mind by its magnitude. All directions of space seemed
    canceled, and they were falling, falling, into an inferno of fire.</p>
    <p>Harb turned a sweating face. "We'll cut off to orbit in less than an
    hour," he informed.</p>
    <p>Ross Floring spoke from the chair in which he was tied, and in which he
    had come back into consciousness.</p>
    <p>"Jonny, I've been waiting for you! Harb wouldn't listen to me. You've
    got to turn back!"</p>
    <p>Jonny shook his head. "No use, Ross, I know you're only doing your
    duty. And I'm sorry to drag you into this danger. But we're not
    stopping now."</p>
    <p>"But you'll never get there!" Floring exclaimed. "Control cruisers must
    already be after you. They'll have found out where I am by now."</p>
    <p>"Empty threats!" Harb jeered. "They can't know where he is."</p>
    <p>"Jonny, look at my badge!" cried Floring. "See the tiny radio bulb in
    the back of it? It's a 'finder' by which any Control officer can be
    located at any distance. When I didn't report back, they'd use it to
    spot me out here."</p>
    <p>"If that's true," said Jonny Land, his thin face suddenly haggard,
    "they'll be after us by now. Harb, cut the communic back in!"</p>
    <p>Harb obeyed. Roar of static from the gigantic orb ahead was a dull
    background to the sharp voice that came from the instrument.</p>
    <p>"Control Operations squadron four hundred thirty-three nine calling
    'Phoenix!' Last warning! We are overhauling you and will shell you
    unless you turn and surrender."</p>
    <p>Startled, Harb Land jabbed a button and twisted the knob of the
    visor-screen. The far-seeing eye quartered space behind them, and then
    the black space scene held steady. There against the stars came a
    little pattern of four tiny triangles of light. Triangles—galaxy-wide
    sign of Control.</p>
    <p>"By heaven, they actually have come after us!" cried Harb. "Jonny,
    they're only minutes behind us and pulling up fast!"</p>
    <p>"We broadside as soon as we range you unless you turn now," warned the
    steely voice from the communic.</p>
    <p>Laird Carlin, only a few weeks before, would no more have dreamed of
    disobeying a Control Operations command than he would have of picking
    stars from the sky. Galaxy citizens were trained to revere the great
    organization that had made the Universe a place of law and order.</p>
    <p>But the ancient independence of these men of Earth was strong in him
    now. They had already risked so much, had incurred certain penalty even
    if they now surrendered.</p>
    <p>"Keep going!" Carlin exclaimed. "They can't follow us once you start
    orbiting close to the Sun's photosphere. No ordinary Control cruiser
    has heavy enough heat-screens to follow us into that!"</p>
    <p>"By Jupiter, it's so!" exclaimed Harb, faint hope lighting his face.
    "But I daren't crowd on more speed now. I've got to start decelerating
    if we're to orbit correctly."</p>
    <p>"Decelerate by plan," Jonny said grimly. "They may not range us in
    time. We'll soon know."</p>
    <p>The "Phoenix," flying at a tangent toward the gigantic sphere of the
    Sun, was aiming to swing into an orbit around Sol as close as possible
    to its photosphere or gaseous surface.</p>
    <p>It had to be so. No ship would ever have power enough to go that close
    to the Sun's colossal pull and hold its position by its own energy. To
    get that close and to stay that close to Sol without being drawn in to
    it, a ship had to go into an orbit around it like a tiny satellite.</p>
    <p>The air in the "Phoenix" was already stifling hot. Jonny switched in
    another of the heat-screens, and the dim halo around the flying ship
    deepened.</p>
    <p>Harb's fingers were flashing over the controls, decelerating, steering
    the ship in a closing spiral toward the Sun.</p>
    <p>"Carlin, talk them out of this madness!" cried Ross Floring, aghast.
    "The cruisers will be broadsiding us in moments."</p>
    <p>Carlin paid no attention. His eyes were on the visor-screen where the
    four cruisers now loomed big as they came closer.</p>
    <p>Then it came. Silent, deadly, four blinding gouts of flame burst near
    the "Phoenix." Four salvos of atomic shells whose wave of force rocked
    the plunging ship. Loesser came tumbling into the pilot room, red face
    glistening.</p>
    <p>"They'll bracket us next salvo or two!" he yelled. "What's our chance?"</p>
    <p>"Turn on heat-screens Six and Seven!" roared Harb Land, without looking
    around. "I'm going into orbit now!"</p>
    <p>"It's too soon!" Jonny cried warning. "It's—"</p>
    <p>Carlin saw that Harb hadn't even heard. The giant was recklessly
    cutting the elements of their plotted course, depending on their own
    power to pull into orbit in time.</p>
    <p>The heat-screens, all they had, were on full now. Another salvo burst
    to spaceward of them. Carlin knew the men behind realized Floring was
    aboard. But Control Operations would sacrifice any men to prevent the
    Sun-mining that always before had meant disastrous solar disturbances.</p>
    <p>"Great blazing stars!" breathed Loesser, staring. "Look at that!"</p>
    <p>Forgotten, the deadly shells that were groping for them. For now the
    "Phoenix" was deep in the awesome corona of the star and was curving in
    closer through heat that was over two thousand degrees.</p>
    <p>Carlin's mind shook to the fearful spectacle that was the firmament.
    Not he, nor any other living man, had ever come so close to a star.
    They were entering a region of such violent energies that all laws of
    space and time here seemed cancelled.</p>
    <p>Blinding, eye-dazing even through the strong protective filter of the
    heat-screens, the brilliance of Sol stunned them. They looked on a
    vast, raging ocean of flaming gases, a sea of vaporized metallic and
    non-metallic elements that was like a cosmic furnace.</p>
    <p>Even through the heat-screens, the radiance heated the air in the ship
    scorchingly. But now the visor-screen showed that the Control cruisers
    were falling back and disappearing from sight behind.</p>
    <p>Blinding, eye-dazing even through the filter of the heat-screens, the brilliance of Sol stunned them.</p>
    <p>"They couldn't follow us this close to the photosphere!" Harb cried
    exultantly. "We've shaken them and we're almost in orbit."</p>
    <p>"You can't orbit the Sun!" Floring pleaded. "And even if you could, the
    cruisers will lay to outside the heat and range you by locator and fire
    till they destroy us! Put about!"</p>
    <p>The man Vito, choking and gasping for breath, came into the pilot room
    from the engine rooms astern.</p>
    <p>"Heat-screens won't take another dyne! If we go closer, we're done for."</p>
    <p>"We're orbiting now," Jonny said huskily. "Wait!"</p>
    <p>Harb Land was engaged in the most difficult operation of spacemanship,
    bringing a ship into exact balanced orbit around a celestial body.</p>
    <p>Most difficult, even when the body was a planet. Impossible, nearly,
    when the body was a Titanic star!</p>
    <p>Carlin saw the giant's face a frozen mask as he centered his dial
    needles, fed force with infinite delicacy, guided, changed—and changed
    again.</p>
    <p>Harb reached and slammed open a switch. The hum of propulsion waves
    died. The "Phoenix" was without driving power. And the needle of the
    gravi-gauges remained constant, the ship's path around the Sun was
    unvarying.</p>
    <p>"We've orbited!" Harb Land's voice was a hoarse, exhausted sound.</p>
    <p>Carlin wanted to shout, "By heaven, there are no spacemen in the galaxy
    except Earthmen—none!"</p>
    <p>The "Phoenix" was circling the Sun, deep in the corona and reversing
    layer and close to the photosphere or light-emitting surface which was
    the vague boundary of the star itself.</p>
    <p>Their sensation was that of men suspended over a Universe of raging
    flame and force. The mind shook to the impact of it. They were here
    where no men, no life, had ever been intended to be. They were
    violating the sanctity of a star.</p>
    <p>"Now—the dredge," Jonny said hoarsely. "We've not power enough to
    force the heat-screens like this for long. Come on, Carlin."</p>
    <p>Carlin stumbled back with him into the stifling hold. The men around
    the towering magnetic dredge were like sooty devils staring with wild
    eyes.</p>
    <p>The metal was so hot its touch made him cry out as he closed the
    circuit of the generators with the ato-turbines. The rotors began their
    whine, building up a magnetic field.</p>
    <p>The whole ship suddenly shook and quivered. Harb came plunging back
    into the hold.</p>
    <p>"Those Control Cruisers are starting to salvo us by radiolocator!"</p>
    <p>"We only need a little time," panted Jonny Land. "The cooler coils,
    Carlin!"</p>
    <p>Carlin felt like a man in a dream as he sweated with Jonny to get the
    magnetic dredge started. The field was building steadily, and the great
    nozzles of the beam-head had been lowered below the keel. Jonny's
    brilliant eyes clung to the panel of gauges, and finally he opened the
    field-switch.</p>
    <p>"Now!"</p>
    <p>They crowded around the view-plate in the keel, peering half-blindly
    down against the glare of the raging Sun-sea below. The dredge was
    projecting a powerful, concentrated magnetic field down into that ocean
    of flaming gas like a sucking straw. But for moments they saw nothing.
    Time that seemed endless went by. Then—</p>
    <p>"Here she comes!" yelled Loesser.</p>
    <p>A column of flaming vapor was shooting up from the fiery ocean below.
    Compared to the gigantic mass of Sol, it was the merest filament, the
    flimsiest thread of fire.</p>
    <p>But it was rushing up and up toward the hovering "Phoenix," a finger
    of fiery vaporized elements drawn irresistibly up along the beam of
    magnetism to the ship.</p>
    <p>Another salvo of shells went off in space somewhere close by and rocked
    the ship with its wave of force. But next instant came a heavier
    impact, as the fiery column of gas reached the nozzles below the ship.</p>
    <p>They heard a deafening roar. That up-sucked stream of vaporized
    elements was being drawn through the heat-proof nozzles and intakes,
    through the Markheim filters that screened out its copper atoms, and
    was then being shot downward again by the kickback's negative field.</p>
    <p>"The kickback's working!" Jonny Land yelled. "If the effect of it is
    what we calculated, we've done it!"</p>
    <p class="ph1">CHAPTER IX</p>
    <p class="ph1"><i>An Earthman Comes Home</i></p>
    <p>For the moment, none of them paid any attention to the fact that
    precious copper was solidifying in the cooler coils into granules of
    metal that were being blown into the bunkers. The real test was what
    their beam of magnetic force was doing to the surface of the Sun.</p>
    <p>Did it seem incredible, as it almost did to Carlin, that such a
    fragile finger of force could in the least disturb the mighty orb
    below? He knew better. He knew the unnaturally delicate balance of a
    star's surface, which a slight change of pressure artificially induced
    could stir into a whirl that would expand in giant Sun-spots. If that
    happened, it would mean chaos.</p>
    <p>"No sign of a whirl yet," Jonny breathed, peering down through black
    glare-proof lenses. "No sign at all."</p>
    <p>There was no moment of crisis, no clean-cut moment of triumph. There
    was just the time speeding by, the flow of copper into the ship, and
    the constant reports of Jonny—"No whirl forming yet."</p>
    <p>Salvos shook the ship as the Control cruisers far outside the sun
    glare fired more and more accurately. But they went unheeded. Success
    or failure of the most audacious engineering exploit in the galaxy's
    history hinged upon Jonny's muttered reports.</p>
    <p>"No whirl yet."</p>
    <p>Jonny Land finally raised his head, looked at them as they stood with
    wild surmise on their faces.</p>
    <p>"We've done it," he said, almost unbelievingly. "We've nearly filled
    the bunkers with copper and there's no whirl down there, no disturbance
    to grow into a spot. We've made Sun-mining possible."</p>
    <p>Tears were running down Loesser's face. Harb Land looked dazed. But
    Jonny walked across the hold to the wall through which the cooler coils
    fed into the bunkers. He peered through a quartz view-plate.</p>
    <p>They looked with him. The bunker rooms were heaped high with shining
    red granules. Copper, virgin-pure, blown into the rooms and already
    almost filling them. Copper milked from the Sun!</p>
    <p>"Copper for Earth!" whispered Jonny, his thin face blazing now. "Power,
    and new life, for the old planet!"</p>
    <p>The "Phoenix" rocked wildly and metal screeched rendingly as they were
    flung from their feet by a salvo that had finally bracketed the ship.</p>
    <p>"The feed-pipes!" screeched Loesser, scrambling to his feet beside
    Carlin.</p>
    <p>Carlin saw. The ship's walls had held, but the shock had snapped
    strained cables and cooler coils. Two intake tubes were giving way,
    white-hot copper vapor forcing out through cracks in them.</p>
    <p>"Veer-clamps on those two pipes!" yelled Jonny. "If they give,
    everything goes!"</p>
    <p>Knowledge of what it meant if the pipes gave way, if super-heated
    metallic vapor blew out into the hold, flung Carlin in a crazy rush for
    the Veer-clamps and wrenches.</p>
    <p>He got a clamp around one of the pipes, and the man Vito started
    spinning shut the bolts that would hold the fracture tightly. He swung
    round toward the other pipe.</p>
    <p>"Clamp!" yelled Jonny Land, in a cry that was like a hoarse howl of
    agony.</p>
    <p>Carlin's blood left his heart as he glimpsed the most horrible and
    heroic sight he had ever beheld. The other strained tube had been
    about to blow open, and Jonny Land had flung his arms around it and
    was holding it together by agonized effort while the white-hot vapor
    sprayed his body.</p>
    <p>Harb Land wildly snatched his brother away as Carlin flung the big
    clamp around the pipe and convulsively spun its bolts shut.</p>
    <p>He staggered around then. Harb was bending over his brother.</p>
    <p>"Jonny! Jonny!"</p>
    <p>Jonny's whole chest and neck were blackened and blasted. His face was a
    ghastly, sooted mask as his eyes looked up at them.</p>
    <p>Another salvo went off close by, and again the "Phoenix" rocked wildly.</p>
    <p>"Cut the dredge!" Carlin cried. "We've proved the process is
    successful, and we can't stay here now or your brother will die!"</p>
    <p>Loesser cut off the dredge and Harb Land rushed for the pilot room.
    Carlin heard him shouting there into the communic:</p>
    <p>"Control cruisers from 'Phoenix!' We're putting out to surrender. Be
    ready to give injured man medical treatment."</p>
    <p>"Break out of your orbit at once and we'll contact you for surrender by
    locator when you're outside the corona," came the sharp, fast answer.</p>
    <p>The generators of the "Phoenix" started roaring their shrillest note as
    Harb Land frantically flung power into the drive-plates. Beneath the
    thrust of its propulsion vibrations the battered ship began to move, to
    fight its way out of the gigantic pull of Sol, breaking slowly out in a
    tangent off its orbit.</p>
    <p>Carlin, Loesser, all of them in the hold, were bending over Jonny Land
    when Floring, released by Harb, came back. The officer looked down and
    then shook his head somberly.</p>
    <p>"No chance," he said. "He won't even last until we reach the cruisers."</p>
    <p>Jonny was lying, unhearing, fighting for breath, looking up at them
    without seeing them, his sooted face a writhing mask. Carlin felt tears
    sting his eyes, and saw everything through a blur.</p>
    <p>"Jonny, we did it—you did it!" Loesser was choking. "Made Sun-mining
    possible! Why, soon now there'll be scores of ships, new, big ships,
    coming here and getting all the copper Earth needs!"</p>
    <p>He was, Carlin knew, trying to reach home to the dimming mind with that
    reassurance, that assurance that the dying man had not given away life
    in vain.</p>
    <p>It didn't reach Jonny Land. He wasn't Jonny Land any longer, he was
    just a living creature dying in pain, and he couldn't feel or know
    anything but pain. And then the pain went, and life went with it, and
    his face was a lax, empty mask that had no meaning for them.</p>
    <p>Loesser sobbed: "He didn't know—he didn't know what I was saying!"</p>
    <p>Carlin felt dull, tired, drained of emotion. He had just seen the only
    hero he had ever known die, but a hero's death was just death, just
    mortal pang and final release.</p>
    <p>He went forward to the pilot room.</p>
    <p>"Jonny's dead," he said to Harb Land.</p>
    <p>Harb's shoulders sagged, but he did not turn as he guided the "Phoenix"
    on spaceward to where the grim Control cruisers waited.</p>
    <p>Control Court here in New York was only a small room in the building
    by the spaceport. There were no officials in it except the three
    middle-aged judges who sat behind a small table and prepared to pass
    sentence on Laird Carlin and his seven comrades.</p>
    <p>There were no lawyers, no oratory, no jurymen. They were not needed.
    The government psychologists who had quietly questioned the accused men
    during their four days in prison had submitted the factual hypnosis
    records which were complete and incontrovertible evidence.</p>
    <p>The chief judge, the man in the middle, quietly read the decision as
    Carlin and the others faced him.</p>
    <p>"This court is placed in a peculiarly difficult position in assessing
    your offense. On the one hand, you men deliberately broke a Control
    Council regulation and defied its officers. On the other hand, your
    action has proved the practicability of a process of Sun-mining which
    will be of incalculable value to this and every other System in the
    galaxy.</p>
    <p>"To forgive your offense because the ultimate result was good would be
    to set a fatal precedent. It would establish the principle that illegal
    means do not matter if end-purposes are good. We cannot permit such a
    precedent to be established. Therefore, regretfully, this court must
    pass the prescribed punishment for your offense."</p>
    <p>Carlin could not deny the crystalline logic. He had known from the
    first that this must be the issue, and he was too tired to care.</p>
    <p>"You are sentenced to two years imprisonment in Rigel Prison and
    also to the loss of your spacemen's licenses or Cosmic Engineer's
    certificate, whichever you hold. Such sentence is obligatory in this
    case." He added quickly, "It is, however, within our discretion to
    suspend the prison term and to limit cancellation of your certificates
    to one year from date. Such is the sentence of this court."</p>
    <p>Loesser drew a gusty breath of relief. "For a minute, I thought it was
    Rigel for us sure enough!"</p>
    <p>The chief judge had risen. "Speaking personally," he added quietly, "we
    would like to congratulate you men upon a great achievement."</p>
    <p>Ross Floring came to their side.</p>
    <p>"A year's suspension isn't long," he said, and Carlin nodded wearily.</p>
    <p>When, with Harb Land's giant figure leading them, they emerged from the
    building into the sunlight, a roar that deafened them came from the
    waiting crowd outside. The people of Earth, at least, had no need to
    temper their gratitude.</p>
    <p>Harb was grimly silent as he pushed through the crowd toward Marn and
    old Gramp Land. Carlin found himself buffeted by eager hands, assailed
    by joyful faces and voices, as he followed.</p>
    <p>A grizzled, excited man clapped his shoulder. "We Earthmen showed 'em
    we could still conquer space, didn't we?"</p>
    <p>We Earthmen? Somehow, for the first time in all these days, Carlin's
    dulled mind felt a stir of pride as though at an accolade.</p>
    <p>He didn't like to meet Marn's pale face. But she spoke steadily.</p>
    <p>"It's all right, Laird, about Jonny. Women of Earth for two thousand
    years have seen their men go out into space—and not all come back."</p>
    <p>Floring had followed them. "I want you to see something," he said.</p>
    <p>He led the way toward the towering Monument of the Space-Pioneers.
    Carlin looked at the roll of names. Then his eyes suddenly blurred as
    he saw that, for the first time in several centuries, a new name had
    been added to the bottom of that great roll.</p>
    <p class="ph1">JON LAND</p>
    <p>Marn's eyes were shining. And her giant brother looked long, with
    haggard face somehow comforted. But old Gramp Land turned sadly away.</p>
    <p>"A name on a stone is poor exchange for my boy," he muttered. "I'm
    gettin' old."</p>
    <p>That evening, in the old house up on the ridge, they were subdued and
    silent at dinner. The table was too big, and they looked around too
    often as if listening for a familiar limping step and a cheerful voice.</p>
    <p>Carlin was doubly oppressed because of the thing that he had not yet
    told them. He hated, somehow, to break the news.</p>
    <p>"There's something they found out when they made our psycho-records for
    the trial," he said finally. "Mine showed that I had no instability of
    coordination, no star-sickness any longer."</p>
    <p>"You mean, you're cured?" said Harb, surprised. "Why, that's fine. I
    never thought of it, but you made the trip Sunward all right, so I
    should have known."</p>
    <p>"The psychos say," Carlin told them, "that some people out in the
    galaxy now and then approximate much closer to the original Earth stock
    than the average. Such people respond rapidly to Earth-treatment. I'm
    one of them, it seems." He added uncomfortably, "I can go back home to
    Canopus now, though I'll have to work at a desk job for a year. The
    only thing is that there's a ship for Canopus tonight, and there won't
    be another for weeks."</p>
    <p>"You're not going tonight?" exclaimed Harb. "Not as soon as that?"</p>
    <p>Carlin felt a little heartsick. "I wish I didn't have to, so soon. But
    there's nothing for me to do here now that I'm all okay."</p>
    <p>He had somehow expected Marn to protest too. But she did not. She only
    said quietly:</p>
    <p>"I'll drive you down to the spaceport."</p>
    <p>"I think I'd rather walk down," Carlin said slowly. "I don't know why,
    but I would. It's not far and I sent my bags on down."</p>
    <p>"Then I'll walk a little of the way with you," said Marn.</p>
    <p>Twilight had changed into soft summer darkness by the time Carlin had
    exchanged a last old-fashioned hand grip with Harb and Gramp Land, and
    started down the road with Marn.</p>
    <p>She went only around the first turn of the old road with him, and then
    stopped.</p>
    <p>"Good-by, Marn," he said, but she only averted her face.</p>
    <p>Carlin hesitated, then turned and walked on. Luna was lifting its
    shining shield in the east, and the silver summer silence lay over
    everything, hardly broken by the stir of branches and the low buzz of
    insects. The night was warm and still.</p>
    <p>He had a lump in his throat and he tried to laugh at himself because he
    had it. A man couldn't let illogical emotions overrule his reason. This
    crazy, heroic old planet Earth and its people—he would never forget
    them, but he had to return to his own life and work, he had to go home.</p>
    <p>Laird Carlin suddenly stopped. He knew, abruptly, why dull oppression
    had gnawed his mind all day. It wasn't because he was going home. It
    was because he was leaving home. He was leaving the only place where
    his spirit had ever found something it had always lacked, a peace, an
    ancient certitude, a kinship that had grown and grown.</p>
    <p>Carlin turned and strode rapidly back up the road. Not until he was
    almost upon her did he perceive that Marn Land was still standing in
    the silvered road where he had left her.</p>
    <p>"I was waiting for you," she said simply. "I knew you wouldn't go."</p>
    <p>His hands grasped her shoulders as he spoke in a rush.</p>
    <p>"Marn, I couldn't! I thought of Canopus, I thought of friends there and
    a girl who likes me and the garden cities I used to love, and it was
    all unreal, I'm tied somehow to this queer old planet, to Jonny and
    Harb and all of the others, and to you!"</p>
    <p>She came into his arms quietly. "I know. There's been more than one
    like you, more than one who came to Earth and found he somehow couldn't
    leave. This old world is in the blood of our race, Laird." She looked
    up. "A year's not long. We'll need you here to replace Jonny, to
    supervise the Sun-mining. And I need you. I always will."</p>
    <p>Carlin held her closely, all tiredness and doubts gone now, strangely
    content. He looked up at the summer stars and thought of worlds out
    there, but it was all far away, far away.</p>
    <p>And Earth was close, its ancient quiet night enfolding him. Soft wind
    stirred leafing branches in the moonlight, and the road wound up white
    and sure toward the old house, and out of the vastness of time and
    space, an Earthman had come home.</p>



```python
import collections
from bs4.element import NavigableString 
chapter_dict = collections.defaultdict(str) # gives us an unlimited dict full of empty strings
pnum = 0
# for p in soup.find_all('p'):
#     if not ":" in p.text: #Get rid of non-story lines
#         if "CHAPTER" in p.text:
#             pdict = collections.defaultdict(str)
#             pnum = 0
#             chapter_dict[p.text] = pdict
#         else:
#             if pnum == 0:
#                 pdict['Title'] = p.text.replace('\r\n',' ')
#             else:
#                 pdict[f'Paragraph {pnum}'] = p.text.replace('\r\n',' ')
#             pnum += 1
# print(chapter_dict)

for p in soup.find_all('p'):
    if not ":" in p.text: #Get rid of non-story lines
        if "CHAPTER" in p.text:
            pnum = 0
            plist = []
            chapter_dict[p.text] = plist
        else:
            plist.append(p.text.replace('\r\n',' '))
            pnum += 1
print(chapter_dict)
```

    defaultdict(<class 'str'>, {'CHAPTER I': ['Stranger from the Stars', 'Carlin was the only one of the four hundred passengers on the "Larkoom" who hated the star-ship and everything about it.', 'He was bored with the vessel and everyone aboard. A pack of chattering idiots! For the hundredth time since leaving Canopus, he told himself that he was a monumental fool to let that psychotherapist talk him into this crazy trip.', 'A blond girl from Altair Four came tripping along the deck and favored Laird Carlin with the bright smile that all the younger feminine tourists had practised on the tall, dark, dour-looking young man.', 'The blonde from Altair Four favored the tall dour-looking young man with a bright smile.', '"Oh, Mr, Carlin, the annunciators just said that we\'re only eight hours from Sol. By night, we\'ll be on Earth! Isn\'t it thrilling?"', '"Just what is thrilling about it?" Carlin asked sourly.', 'The girl was a little dumfounded. "Why, I mean, Earth! All the ancient history we study in schools, about how men first came from there two thousand years ago. Or was it twenty-one hundred?"', 'She prattled on, voicing all the appropriate clichés.', '"Just think, all of us in this ship came from different stats and worlds, yet long ago all our ancestors lived on that one little world Earth. And they say it\'s still much the same as it was then. Isn\'t it wonderful?"', 'Carlin could not see anything wonderful about it, and a little wearily he said so.', 'The girl flushed in exasperation. "Then why are you going to Earth at all?"', "Why indeed, Carlin wondered savagely? Why the devil wasn't he back on the other side of the galaxy where he belonged, supervising establishment of the new star-ship line to Algol Six, spending his leaves in Sun City with Nila?", 'Nila—he yearned for her, for her gay, mocking humor, her cool beauty, her quick, clever mind. What was he doing here with a bunch of bird-brained tourists who were conscientiously tripping for local color to an old, forgotten world?', 'This whole part of the galaxy was a stagnant, half-dead area. This side of Vega there weren\'t a score of suns with worlds of any importance. And the old "Larkoom," a second-rate star-ship that couldn\'t make more than eighty light-speeds, was plodding determinedly and monotonously on into it.', 'Curse that psychotherapist anyway! Why had he been crazy enough to listen to the fellow? That smug, pink, blinking Arcturian had smiled as gently as a well-bred pussy-cat as he told Carlin what his trouble was.', '"Star-sick?" Carlin had flared. "What do you mean, star-sick? I\'ve made the trip to Algol ten times in the last three months."', 'The psychotherapist had nodded. "Yes. And that was nine times too many. You\'ve been overdoing it for a long time, Mr. Carlin."', 'Before Carlin could protest, the other man had referred to the dossier on his desk.', '"I have your record here. Born at Aldebaran four thirty years ago. Graduated at twenty-two from Canopus University with the degree of Cosmic Engineer. Worked since then establishing spaceports for star-ship lines between Rigel, Sharak, Tibor, Algol and other stars."', 'The psychotherapist looked up gravely. "The point is that you\'ve spent fifty per cent of your time in the last eight years in star-ships. The average has been seventy per cent since you took charge of establishing the new Algol line. And that\'s too much time in space for any man. No wonder you\'re star-sick."', '"Blast it, I\'m not star-sick!" Carlin exploded. "What kind of therapist are you? I come here to have you treat a perfectly simple syndrome of reflex-fatigue, and you tell me all this!"', 'The Arcturian shook his head wisely. "Your case was only simple on the surface, Mr. Carlin. The hypnosis showed up your trouble unmistakably. Want to hear the record?"', "Carlin heard it. And it wasn't pretty. Not pretty, to hear his hypnosis-freed subconscious yelling out a frantic hatred of space and star-ships and everything connected with them.", '"You see?" said the Arcturian gently. "This has been building up in you for a long time."', "Carlin was stunned. He had known of other men who had got star-sick and had had to drop their work and quit traveling space for a while. Other men—but he'd always laughed contemptuously at them for it.", "The psychos might declare that it was perfectly natural for a man to develop a subconscious aversion to space if he crowded his work, but the hard-bitten engineers of Carlin's set believed that a star-sick man was nine times in ten a shirker. And now he himself was told he was star-sick.", '"You\'ve got to quit work and stay out of space for a while," the Arcturian therapist told him.', 'Carlin felt sick at heart. "Then all my work in building up the Algol line will go into young Brewer\'s hands."', "Still, he thought after a moment, it might not be so bad. Working in his line's main offices here on Canopus Two, he could keep in touch. And he would have more time here with Nila.", 'But the psychotherapist shook his head quite decisively at that.', '"No, Mr. Carlin. Your case is too dangerous for that. Your subconscious is twisted into a knot that is going to be hard to untie." He hesitated a moment as though he knew what reaction his next words would provoke. "In fact, there\'s only one way in which you can be normalized. That\'s the Earth-treatment."', '"Earth-treatment?" Carlin didn\'t even know what it meant. "You mean, some treatment that has reference to the old planet over on the other side of the galaxy?"', 'The Arcturian nodded. "Yes, our ancestral planet Earth. Where all our race came from, two thousand years ago. Where you\'re going back to, for perhaps a year."', 'Carlin was knocked breathless by that calm statement.', '"Me going to Earth for a year? Are you crazy? Why should I go there?"', '"Because," the therapist said soberly, "if you don\'t I\'m afraid you won\'t last another six months as a star-line man."', '"But why can\'t I take a rest right here on Canopus Two?" Carlin demanded heatedly. "Why send me to that moldering, forgotten old planet where there\'s nothing now but a few historical monuments?"', '"You\'ve never been to Earth, I take it?" the psychotherapist asked thoughtfully.', 'Carlin made an impatient gesture. "I\'m not interested in ancient history. That part of the galaxy is all a backwater."', '"Yes," the expert said. "I know all that. But old and small and forgotten as it is these days, Earth is still important."', '"To historians," Carlin snapped. "To people who like to poke in the dusty past."', 'The Arcturian nodded, and shrugged.', '"And to psychologists," he said quietly. "Most people these days don\'t realize something. They don\'t realize that we, all of us, are still really Earthmen in a way." He held up a protesting hand. "Oh, I know we don\'t think of ourselves like that! Since those first Earthmen pioneered to their neighbor planets and then to the stars, since our civilization spread out over most of the galaxy, a hundred generations of us have been born on different star-worlds from Rigel to Fomalhaut. But except for local modifications, the type of humanity has persisted since our ancestors left Earth and Sol long ago.', '"That\'s because we\'ve altered star-world conditions to fit ourselves, instead of adapting ourselves to those conditions. We\'ve cunningly changed atmospheres, gravities, everything, wherever we went. We\'ve kept ourselves one race, one type, that way. But it\'s a type that is still indexed to that old plane Earth as its norm."', '"Does that explain why I have to give up my work and go live on the old relic for a year?" Carlin demanded furiously.', '"Yes, it does," the Arcturian replied. "We\'re a star-traveling race now. But the mind can take only so much of the strain of star-travel. Overdo that strain and you get a revulsion, you get star-sickness. Then the only cure is rest for the mind in completely normal conditions. And complete normality, for us descendants of Earthmen, is—Earth."', 'Carlin had stormed. He carried his wrathful resistance to the last pitch.', 'And then the psychotherapist had crushed him.', '"I\'ve turned in your psycho-record to your star-ship line. You\'ll not be allowed to work there until you\'re cured."', 'And that, Laird Carlin thought bitterly, was why he was sprawled in a deck-chair here on the "Larkoom" as the old tub creaked and labored and plodded through space toward the yellow spark of Sol.', '"A year!" he thought in impotent rage. "A year in that hole! I might as well be dead."', 'The psychotherapist had held out the hope that it might not take a year. Some cases of star-sickness responded quickly to Earth-treatment. But even a few months seemed an eternity to Carlin.', 'The passengers of the "Larkoom" were crowding toward the transparent wall of the deck. Earth was coming into sight. And these people—men and women bronzed by the glare of Canopus, reddened by the desert winds of Rigel\'s worlds, paled by the mists of Altair\'s planets—all were watching with an intense and eager expectation.', 'Carlin walked wearily over to the deck wall and watched with them. Sol, ahead, was a small and undistinguished yellow sun. Its orb was unimpressive to eyes that had looked on Antares and Altair.', 'And the planets that circled it were so little that Carlin could hardly make them out. He remembered half-forgotten names from ancient history—Saturn, Jupiter, Mars. And that little gray-green dot beyond must be Earth.', '"Isn\'t it tiny?" babbled a rapturous, overweight woman beside Carlin. "I think it\'s cute!"', 'A very young man from Mizar Seven proudly aired his knowledge.', '"That satellite beyond it is Luna, its moon."', '"The moon is almost as big as the little planet!" exclaimed someone, laughing.', 'Carlin found their chatter getting on his nerves, and edged further along the deck. In gloomy silence, he looked down as the "Larkoom" swept in swift, almost soundless rush toward the little planet.', 'A gray-green, cloud-screened ball spinning around a second-rate sun—it looked like the end of the universe to Carlin. And he might have to spend a year here! His spirits sank still lower.', '"They say you can get the most wonderful souvenirs here," one of the tourists\' voices reached him.', 'Carlin writhed. He would be glad to get out even at Earth, to get away from this bunch of babbling fools.', "He realized his irritability was extreme, unreasonable. It was the result of his star-sickness, he supposed. But that didn't make it any more endurable.", '"Landing in ten minutes," spoke the annunciators throughout the ship. "Stasis going on."', 'The dim glow of the force-stasis that cushioned everything in the ship against pressure of deceleration came on like a tangible medium around them. The big propulsion-wave generators droned in lower key.', 'Swaddled in the cushioning force, they felt no discomfort as the "Larkoom" quickly dropped toward the little planet. Atmosphere screamed briefly outside the ship. They came down through a belt of clouds.', '"That\'s the city New York!" cried an eager voice. "The oldest human city in the galaxy!"'], 'CHAPTER II': ['Ancient Town', 'Carlin looked with a jaundiced eye on the scene widening out below them. There was a blue ocean stretching eastward, a long green coast, and an island that was covered by the grotesquely lofty buildings of an extremely antiquated type of city.', 'This ancient town called New York was like a memento of the primitive past. Not for a thousand years had men crowded their structures so crazily together, or built them to such insane heights.', '"It\'s like one of the bird-people\'s lofts on Polaris One!" exclaimed a girl, laughing. "And how old it looks!"', 'Old? Yes. Pitifully old, like a withered beldame who endeavors still to maintain stiff dignity. The city looked only half-occupied, vines growing on some of the grotesque towers, parks ragged around the edges.', "The spaceport, some distance northward amid low rolling hills, was so small as to be inadequate for any decent world. Carlin's practised eyes condemned the cracked, blackened tarmac, the ill-placed rows of docks, the insufficient hangar and repair buildings.", 'The "Larkoom" landed softly. Carlin waited wearily until the squealing rush of tourists was over, and then walked out into the soft yellow sunshine. He looked around without interest. Landing on a new world was no novelty to him.', 'But for a moment, he was startled by the air he breathed. It was so sweet, so buoyant, so right. It was subtly stimulating, exhilarating to the lungs. Then he realized the cause. All over the galaxy, the descendants of Earthmen had conditioned planetary atmospheres with this atmosphere of Earth as the desired norm.', 'He looked around uncertainly. The tourists were already being shepherded by their tour-conductors toward some old monuments at the far end of the spaceport. But he had no desire to follow them.', 'The psychotherapist had told him, "Live as nearly an ordinary Earth life as you can. Your cure will be quicker if you do. Best thing would be to lodge in some typical Earth home, if you can."', 'Carlin wondered where he could find such a lodging. There were a few Earthmen about, spacemen, port officials and the like. He could ask one of them.', "He had met Earthmen before throughout the galaxy, for many of them followed space as a trade. And he didn't much like them. A proud, taciturn, half-sulky lot, they had always seemed to him.", '"Can you tell me where I could find lodgings around here?" He asked a lanky, lantern-jawed man in faded clothes.', 'The Earthman contemplated Laird Carlin with unfriendly eyes, taking in his sun-darkened face, his pearl-colored synthesilk slacks and jacket, every detail of his appearance that was alien here.', '"Well, no," the fellow drawled coolly. "Don\'t know where a stranger could get lodgin\'s round here."', "He slouched on. Carlin flushed with anger at the scarcely veiled hostility in the fellow's manner.", 'These blasted yokels of Earth! Living here on an old, outworn, fifth-rate planet, resenting the progress and prosperity of the great star-worlds, talking of everybody but themselves as "strangers"!', '"And I\'m supposed to live among them for a year!" he thought bitterly.', 'He started across the spaceport. He had noted a spick-and-span chromaloy building with a half-dozen trim Control cruisers parked nearby, and with the Control Council emblem on its wall. He could find out something there.', 'The spaceport was a somnolent, slovenly place to Carlin\'s eyes. A few star-ships, all of them freighters except the tubby "Larkoom," a scattering of little inter-planet craft, a few workers lounging about. Even the smallest world of the great stars would be ashamed of such a port.', "That soft yellow sun, he found, had a deceptive warmth. And walking was tiring after days of the ship's artificial gravity. Then Carlin stopped as he came abreast of a rickety little planet-ship.", 'Two Earthmen were inspecting its stern drive-plates—one of them a stocky, red-faced young man, the other a lame younger fellow with a crutch. Carlin asked them his question.', 'The red-faced individual answered with the same hostility of manner.', '"You\'ll find no lodgings around here. Better go with the rest of your crowd. There\'s a big tourist hotel down in the city."', 'Carlin swore. "Blast it, I\'m not a tourist. I\'m an engineer sent here by a crazy psycho to spend a year on Earth—heaven knows why!"', 'The lame young Earthman looked at Carlin more closely. He had a thin, pleasant brown face with intelligent blue eyes.', '"Oh, an Earth-treatment man?" he said. "A few come in all the time." He asked interestedly, "You\'re a Cosmic Engineer? Do you mind telling me what field?"', '"Star-ship line chief surveyor," Carlin said wearily. "That means I lay out spaceport and beacon routes between star-worlds."', '"I know what it means." The lame youngster nodded quietly. He hesitated, frowning slightly as though weighing something. Then, as if deciding, he spoke. "I\'m Jonny Land. I think we could fix you up with lodgings if you don\'t mind putting up with a little discomfort."', '"You mean, in your own home?" Carlin asked doubtfully. "Where is it?"', 'Jonny Land pointed to one of the low green ridges west of the spaceport.', '"Just up on the ridge there. There\'s only my grandfather, my brother and sister, and myself. And we have an extra room."', 'The red-faced young Earthman made a sharp protest. "Jonny, what the blazes are you thinking of? You don\'t want this fellow in with you!"', 'The violence of his protest seemed uncalled-for to Carlin, even granting the general Earthman hostility to strangers.', 'Jonny Land quietly quelled the outburst. "I\'m doing this, Loesser." He looked at Carlin. "Well, what about it? I warn you that you won\'t find the comforts of a big star-world apartment."', '"I don\'t expect anything like that here," Carlin answered tiredly. He felt worn out by the voyage, the discouragingly primitive aspect of this place where he must live, the open unfriendliness. He nodded. "I\'ll try it. The name is Laird Carlin."', '"If you\'ll get your luggage, I\'ll take you up," Jonny Land suggested. "I have a truck. I\'ll meet you over at the terminal."', 'Carlin came out of the shabby terminal a little later with his two kitbags and found the lame youngster waiting at the wheel of a disreputable-looking old ato-truck.', 'Loesser, the red-faced young man, was standing beside it voicing emphatic protest about something. Carlin overheard a few words.', '"—ruin everything by taking this fellow in!" he was saying violently. "How do you know he isn\'t a Control spy?"', '"I know what I\'m doing, Loesser," Jonny Land repeated firmly.', 'They broke off as they saw Carlin coming. But Loesser gave him a hot, angry glare as he climbed into the machine.', 'The old truck ran westward across the bumpy tarmac and started climbing an ancient, cracked concrete road toward the green ridge.', "Carlin wondered wearily what these Earthmen were up to that made them afraid of Control? Smuggling, maybe? He didn't much care. He was hot, tired, grimy with dust, and unutterably disgusted with Earth.", 'The concrete road that climbed the ridge looked as though it was centuries old. And its engineering had been timid, for it wound around hills instead of cutting through them, bridged small streams instead of trampling over them. But the battered truck had difficulty negotiating even these easy grades. Its ato-motor drumming noisily as it climbed.', 'Carlin looked out gloomily at the sunset-lit landscape. He could not get used to the vivid, dominating green of all vegetation here. And he was shocked by the unkempt, ragged look of everything. Untended fields of weeds and clumps of woods grew right up to the road. It was dismayingly different from the groomed, parklike planets of Canopus.', "The houses Carlin glimpsed along the road added to his dislike. They were mostly old ferroconcrete dwellings half-hidden by trees and bright flowers, with behind them the big tanks used in hydroponic farming. Hydroponic farming was so old-fashioned he had thought it had disappeared from the galaxy. What was the matter with these people that they didn't directly synthesize their food as others did?", 'Young Jonny Land was speaking to him.', '"You\'ve never been here before? You must find Earth a little odd."', 'Carlin shrugged. "It\'s all right, I suppose. But I just can\'t understand how you people could let your planet get into this kind of shape. Why haven\'t you spread out more, instead of huddling around a few archaic centralized cities like that one back yonder?"', 'The lame young Earthman answered slowly, his thin, brown face turned to the road ahead.', '"The answer to that is simple. One word, in fact. And that word is \'power.\' We just don\'t have power enough here on Earth to smooth it out into a garden-planet like your star-worlds, to come and go around it any distance at will."', '"Atomic power is about the easiest thing to produce there is," Carlin commented skeptically.', '"Yes, if you have copper fuel," Jonny Land replied. "If we had enough copper we could make a garden of this world too, could spread all around its loveliest spots and come and go by fast flier, could give up the old hydroponic farming and synthesize our food, and produce the luxuries you people have on the star-worlds.', '"But we have little copper. Earth, and its sister-planets here, are all starved for it. Once, we had a lot. But not now. And it\'s economically impossible to haul copper in sufficient quantities from other stars. That\'s why we\'re power-starved, unable to progress."', 'Carlin made no further comment. He was not much interested. He was only wondering sickly how long he would have to stay on this unkempt, stagnant planet.', 'The sun was burning his neck, for the old truck was topless. He was jolted by holes in the ancient road. The sweetness of the air had lost its magic for him, for now with the twilight had appeared swarms of evil little gnats and midges.', '"This is the house," said Jonny Land, pulling up the truck in front of a square dwelling.', "Laird Carlin's heart sank. It was like the other houses he had seen, a ferroconcrete structure festooned with climbing flower-vines, surrounded by tall, untrimmed trees except on the side that looked down into the twilit valley. Primitive hydroponic tanks gleamed dully beyond the trees.", 'He followed the lame youngster into a dim, cool living room. It looked like an antique stage set to Carlin, with its ridiculous cloth curtains at the windows, its obsolete krypton light bulbs in the ceiling, its massive furniture that was actually made of wood.', 'Jonny Land had been making explanations in lowered tones to the two people at the other end of the room. They came forward, a spry old man and a girl.', '"This is Gramp Land, my grandfather," Jonny introduced. "And my sister Marn."', 'The old man looked at Laird Carlin with inquisitive, bright eyes, and his gnarled hand reached for an old-fashioned handshake.', '"Come from Canopus, do you?" he chirped. "Well, that\'s a long way off. I was there once years ago when I followed space. And my grandson Harb has been there lots of times when he was a star-ship man."', 'The girl, Marn, looked doubtful and troubled as she murmured a word of greeting to Carlin. He sensed that his coming had disturbed her.', 'She was a rather small girl, with a thick mop of ash-colored hair carelessly combed back. Her eyes were grave blue. She wore a faded old slack-suit that he thought the most barbaric feminine garment he had seen.', '"I hope we can make you comfortable here, Mr. Carlin," she said, troubled. "We\'ve never had any lodger before. I can\'t understand why Jonny made the suggestion."', 'A heavy step at the door cut her short. Her look of distress and worry deepened.', '"There\'s my brother Harb, now."', "Harb Land was a gangling young giant with a craggy face and slate-colored eyes that looked at Carlin with instant hostility. Jonny had limped forward and was quickly explaining Carlin's presence.", '"He\'s going to live here with us for a while, Harb."', 'Harb Land\'s reaction was violent. "Have you gone out of your mind, Jonny?" he flared. "We can\'t have him here."', 'Disgusted, Carlin started to turn away. But Jonny Land stopped him with a gesture. There was a quiet, unsuspected strength in his thin brown face as he spoke to his lowering brother.', '"He\'s going to stay, Harb. We\'ll talk about it later."', 'Harb Land made no reply, but glared at Carlin. And Carlin felt an unutterable weariness and dislike.', "These primitive, backward, suspicious Earth yokels, quarreling over the privilege of staying in their grotesque old house. As though he would stay on their cursed planet one minute if he didn't have to!", '"I\'m very tired," he said heavily. "If you could show me where the room is, I should like to rest."', 'Marn uttered an apologetic exclamation. "Oh, I\'m sorry! Of course you\'re tired. Come with me, Mr. Carlin."', 'She led upstairs. There was no grav-lift, just old-fashioned steps going up a dark hall. And the bedroom on the upper floor to which she took him was as bad as he had expected.', "It was clean, of course, spotlessly so. But it was more like a museum exhibit than a sleeping chamber, to Carlin. There were no aerators, just open windows with crude screens across them. No somnigrav pad, just a high, old-style bed. There wasn't even a video.", 'Yet the girl made no apologies for it, seemed not to think any necessary.', '"We\'ll bring your bags up after dinner," she said. "It will be soon."'], 'CHAPTER III': ['Old Planet', 'When Marn had gone, Carlin lay down wearily on the lumpy, sagging bed. He closed his eyes. The reaction to the long, slow voyage had set in. No doubt about it, he was star-sick all right. Time was when no voyage could have made him feel like this.', "But it wasn't the voyage so much as this world to which he had been condemned. How was he going to live here for months, for a whole year maybe?", "The sound of an angry voice came up dimly through the twilight, from the lower floor of the house. He recognized Harb Land's angry tones.", '"—if Control Operations finds out what we\'re doing!"', 'There was a murmur of lower voices, and then the argument seemed to stop. Carlin remembered what he had overheard the red-faced Loesser saying at the spaceport.', 'What were these Earthmen doing that they were so secretive about? It must be something against the laws by which Control Council governed the galaxy, or they would not fear discovery by Control Operations.', 'When Carlin went down to dinner, he expected open hostility from the gangling older brother. But Harb Land muttered a curt greeting, his half-civil manner indicating his angry protests had been overridden.', 'Carlin stared dismayedly at the food set before them. Instead of the clear, colored synthetic jellies and liquids he was used to, the food was served in what seemed barbarically primitive state. Cooked whole vegetables, natural eggs, natural milk—everything rawly natural.', "He ate what he could, which was little. His weariness was drugging him, and Harb Land's smothered hostility gave a sense of strain.", 'Gramp Land carried on most of the conversation, questioning Carlin about the far-away star-worlds. Carlin answered wearily.', '"Saw a lot of them worlds myself once," the old man said. He added proudly, "Following space runs in my family. My mother was a direct descendant of Gorham Johnson himself."', '"Gorham Johnson?" Carlin asked. "Who was he?"', 'The question was unfortunate.', '"What do they teach out in your star-world schools?" Gramp exploded. "Don\'t you know that Gorham Johnson was the first man ever to travel space? That he was an Earthman, who took off from down in the valley here two thousand years ago?"', 'Gramp\'s pride was outraged. Carlin remembered the old galaxy proverb—"Proud as an Earthman." They were all like that, inordinately vain of the fact that their world\'s people had first conquered space.', '"Sorry," he said tiredly. "I remember the name now. Anyway, I had too much cosmic physics to study to spend much time on ancient history."', 'Gramp still spluttered, but Jonny intervened, questioning Carlin on his work.', '"Did you study sub-atomics or just straight dynamics?"', '"Sub-atomics," Carlin answered. And, to another question, "Yes, I had electronic mechanics too."', 'He caught the swift, triumphant glance that Jonny Land shot at his brother. It puzzled him.', '"Jonny knows all that stuff," boasted Gramp, his good humor restored. "He\'s a Cosmic Engineer graduate from Canopus University, too."', 'Laird Carlin was genuinely surprised. He looked at the quiet, thin-faced youngster.', '"You\'re a Canopus graduate? Why the devil is a man of your training wasting your time here on Earth?"', '"I just like Earth," Jonny answered evenly, "and wanted to come back here when my education was finished."', '"Oh, sure." Carlin nodded. "But if this world is as outworn as it looks, there\'s no field here for a CE. You ought to be out at Algol."', '"You star-world people are all the same—always advising us to leave Earth!" Harb Land interrupted with suppressed passion. "That\'s what Control Council keeps harping on as a solution to all our poverty and problems. They keep asking, \'Why don\'t you emigrate to other stars?\'"', 'Gramp Land shook his head. "We don\'t leave our planet as lightly as some folks do. No matter how far an Earthman goes, he always comes home."', '"Still, you can hardly blame Control Council for giving you good advice," Carlin said, exasperated. "After all, it\'s your own fault if you foolishly squandered the copper resources of your planet and now lack power."', 'Harb Land\'s craggy face darkened. "Yes, we squandered our copper foolishly. We did it twenty centuries ago, when Earth was opening up the whole galaxy to travel. We spent our copper establishing the galactic civilization that\'s forgotten all about our power-starved world."', '"Harb, please!" said Marn in a low voice, distress in her face.', 'A silence fell, and they finished the dinner without further conversation. But Jonny Land spoke to Carlin before he went upstairs.', '"Don\'t take Harb too seriously. A lot of people here on Earth are so embittered about our lack of power that they\'re unreasonable."', 'Carlin found his bedroom dark. No automatic lights came on when he entered, and he could not find the switch. He gave it up, and got into bed and lay looking heavily out into the night.', 'Soft wind was stirring the trees around the house. Heavy scent of flowers drifted on it, stirring the window curtains. Down in the valley gleamed the spaceport beacons, and beyond lay a thin rim of glimmering sea over which the quarter-phase shield of Luna was rising.', 'He felt utterly miserable, homesick, wretched. If he were back at Canopus right now, he would be dancing with Nila in Sun City ballroom, or wandering in Yellow Gardens.', 'He drifted off to sleep despite himself, in his lumpy bed....', 'Carlin awoke with bright sunrise splashing his face. He reached sleepily for the aerator and refreshment buttons—then remembered.', 'To his surprise, he was feeling much better. He had slept well in the primitive bed, and fatigue had drained out of him.', 'Queer, musical notes that he guessed were calls of birds came to his ears. The air that snapped the curtains was chill now, but pure and sweet, subtly intoxicating.', '"They do have finer air on this old world than any aerator can furnish," he thought.', 'He put on a zipper-suit that was dark brown and rough in weave.', '"Going native," he thought with a sour grin, and went downstairs.', 'Marn Land was the only person he found in the sunny rooms. She still wore those barbaric faded old slacks, but had a red flower in her ashen hair. A little frown of worry in her forehead disappeared as she looked at him.', '"You\'re feeling better, aren\'t you?" she asked.', '"A lot," Carlin admitted. "I\'m afraid I was rather rude last night, you know."', '"You were tired," she said gravely. "Just sit down. I\'ll get your breakfast."', 'It was a new experience to Carlin to sit chatting in a sunny old kitchen while a girl in faded slacks prepared his breakfast on an electrode stove. Instead of punching the refreshment-button for it.', '"Jonny and Harb have gone down to the spaceport," she said over her shoulder. "They and a few friends have an old planet-ship there that they\'re fixing up for a trip to Mercury."', '"Mercury?" he said. "Oh, that\'s the innermost of these planets, isn\'t it?"', '"Yes. Men here on Earth are always going prospecting for copper on its Hot Side. Jonny got up this prospecting expedition."', 'The breakfast she put before Carlin was of coarse wheaten bread, more of the natural eggs and milk, and a curious brown beverage made from stewing certain dried berries. She informed him its name was coffee. Carlin tried it, found it bitter and unpalatable.', 'A little surprised by his own action, he ate nearly everything else. The food was coarse, but satisfying enough, and he would have to get used to it if he were to stay here.', '"I\'ll try not to be any trouble to you," he told Marn. "I\'m just supposed to take it easy, do anything I want to."', 'She nodded. "I know. Some of our neighbors had Earth-treatment visitors as lodgers. They all got to like Earth a lot before they left."', 'Carlin did not voice his pessimism on that point. He went to the door and stood looking out into the sun-bright, flowery yard.', 'He felt at a loss. It was baffling to find himself without anything to do, no work crowding up that must be hurried through, no crews of ato-men to supervise in blasting spaceports out of untamed planets.', 'Marn looked at him understandingly. "You\'ve always been busy, haven\'t you? Earth must seem slow and dull to you."', 'Carlin shrugged. "I might as well get used to it. I think I\'ll take a look around."', '"You\'ll find Gramp fishing up at the north brook if you go that far," Marn called after him as he walked across the yard.', 'Carlin sauntered past a big, locked ferroconcrete workshop of some kind, and some tall storage sheds, then on past the flat, wide hydroponic tanks that were now loaded with their masses of green growth.', 'He found a road beyond them that he did not recognize as a road, at first. It was a mere wide track gouged northward along the wooded ridge, the first dirt road that he had ever seen on a civilized world.', '"A poor planet, all right," Carlin thought. "Can\'t even build decent roads."', 'There were hardly even any ato-fliers in the sky, only an occasional one flitting across the blue vault.', '"No wonder these poverty-stricken devils resent the rest of the galaxy," he thought. "I suppose I would too, if it had been my bad luck to be born here."', 'The road was crazily illogical, winding westward along the woods-clad ridge in serpentine fashion. It twisted accomodatingly to avoid big boulders, a spring, a small gully.', "The woods on either side was deplorably unkempt to Carlin's eyes. Big and small trees jumbled together, saplings choking each other out, dead brush and thorns and vines everywhere. There was even wild life in the woods, furry rodents scuttling away, hosts of birds.", "This sort of thing was what you expected on some unpeopled planet that hadn't yet been pioneered and civilized. But Earth was the oldest human-peopled world in the whole galaxy.", 'Yet Carlin had to admit that there were certain compensations here. That winelike air was still an experience to him. And walking now came more easily to his muscles here than on any world. It seemed odd to be walking with such perfect ease, without wearing a de-grav.', "He could not find the brook Marn had mentioned. He sat down on a log by the roadside, musing on the drowsy, dull quiet of this place. There was not a sound of human activity. Didn't these Earth people ever get bored with the sleepiness of the place?", 'Carlin found he was still tired. He watched a small, brilliant insect fluttering over a flower near by. Soft wind breathed through the ragged woods, stirring the green leaves and making a dappled, dancing pattern of sunlight on the ground. A distant bird called rustily.', '"An old, outworn planet, dreaming," he thought. "These people, all of them, living in its past."', 'Carlin finally got up stiffly, and lounged back along the road. He was surprised to find that time had passed quickly, that the sun was now at the zenith. And that, somehow, his taut nerves had relaxed.', 'The big workshop behind the house had its doors open now. He glanced through them and was surprised to see that the cavernous room in there was a fairly well-equipped atomic-engineering laboratory.', 'Interested, Carlin started toward it. In the center of the big room he had glimpsed a towering, massive machine whose inner mechanism was concealed by a cylindrical metal cover.', '"Looks like it might be a big field-generator of some kind," he muttered. "I wonder what it really is?"', 'There was a violent exclamation as an Earthman came running out from behind the machine to block his entrance.', 'Carlin recognized the broad red face, angry eyes and stocky figure of Loesser, the man who had argued with Jonny at the spaceport.', '"What are you doing here?" Loesser demanded harshly.', 'Carlin was bewildered by his vehemence. "Why, I just wanted to take a look at this machine."', '"I thought so!" blazed Loesser, his eyes raging. "I told Jonny that was why you came here!"', "He snatched an object from his jacket pocket. To Carlin's thunderstruck amazement, the object was a stubby atom-pistol that Loesser was furiously leveling at him."], 'CHAPTER IV': ['Mystery Machine', 'Laird Carlin was child of a galactic civilization in which violence between men was rare. There was plenty of danger yet, in pioneering new star-worlds, but over the civilized worlds themselves the unchallenged law of the Control Council maintained unbroken order. A man could go a lifetime without ever seeing violence.', "The atom-pistol in Loesser's hand and the obvious murderous intention in the man's face stupefied Carlin. He was simply unable to adjust his thinking to the possibility that the enraged Earthman before him meant to blast him down.", '"Why, what\'s the matter?" he began, puzzled and stunned.', 'He knew later how near he had been to death. At the moment, he so little recognized it that he felt no relief at the interruption that came now. Harb and Jonny Land came running forward from the cavernous interior of the workshop.', '"Loesser, put that gun down!" snapped Jonny.', 'Loesser turned violently. "This fellow was spying on us! I saw him at the door!"', "Harb Land's craggy face darkened ominously.", '"I warned you what might happen," he said harshly to his brother.', '"Is this man crazy?" Laird Carlin demanded bewilderedly of Jonny.', 'The lame youngster limped quickly forward. "Get back to work," he told the other two briefly. "Carlin, I\'m sorry about this. I\'ll explain."', 'He walked beside Carlin toward the house. It was not until later that Carlin realized how deftly and unobtrusively he had been steered away from the workshop.', '"Harb and Loesser and I, and a few others, are planning an expedition to Mercury to prospect for copper," Jonny was explaining. "In that ship you saw down at the spaceport. We\'ve devised a new metal-finder of the radiolocator type, with which we hope to be able to locate new copper deposits. That\'s the machine in the workshop.', '"We\'ve maintained a certain secrecy about it," he went on, "because naturally we don\'t want other prospectors stealing the idea of our new finder and beating us to it. And I\'m afraid Loesser thought you were spying on us. People here are always a little suspicious of strangers."', '"So I\'ve noticed," Carlin answered dryly. "This is the first world in the galaxy where I\'ve ever felt completely unwelcome."', '"Oh, I wouldn\'t say that," replied the other. "But put yourself in our place, Carlin. Figure how you would feel if you were an Earthman, your world starved for power because its copper was spent to establish a galactic civilization that now neglects it."', "Jonny's thin brown face was earnest, his blue eyes watching Carlin as though eager to convince him. Carlin shook his head.", '"I can see your problem in lacking copper," he said. "But the remedy for it is so simple. Nine-tenths of you should emigrate to other, better worlds as the Control Council advised."', 'Jonny smiled. "There you come up against the obstinacy of my people. We\'ve an older planetary tradition, a deeper, more ancient love for our world, than any other people in the galaxy."', '"I think you people live too much in the past," Carlin answered frankly. "But it\'s none of my business. Anyway, I hope your expedition brings home copper."', '"Thanks," Jonny said softly. "I think we have a good chance."', "Carlin went back to the veranda of the old house and sat there pondering. Something about Jonny's explanation had been vaguely unsatisfying.", 'To his trained eyes, the glimpse he had had of that towering machine had not suggested any metal-finding device. There had somehow been a suggestion in its half-glimpsed bulk of something quite different; something vaguely disturbing, almost menacing.', '"The devil, I must have knots in my subconscious to start getting premonitions like that," Carlin swore. "The poor devils are just secretive about their plans because everyone else here is that way."', 'He lounged boredly around the house during the hot, sleepy afternoon. There was no one to talk to, for the brothers stayed out in their workshop and Marn was out tending the big hydroponic tanks.', "He tinkered with the old video set in the living room but the only stations he could get were local Earth ones, and lectures on hydroponics and gossip about unknown people didn't interest him.", 'He finally gave up and stretched out on the veranda, staring sleepily down into the green cup of the valley and cursing the psychotherapist whose insane idea had sent him here to die of boredom. He dozed until he was awakened by the sputter of an arriving ato-truck.', 'It contained three lanky young men, tall Earthmen who went back to the workshop without stopping at the house. The other partners in the prospecting expedition, Carlin supposed sleepily.', 'Again he felt that queer sense of something threatening, that vague premonition that had clung to him ever since he glanced into the workshop. If only he could remember what that machine reminded him of.', 'Days passed and Carlin still could not remember that, though his disturbing doubt persisted. There was no chance of another look into the workshop for it was always locked except when Jonny and Harb and their half-dozen partners worked in it.', '"The trouble with me," Carlin told himself ironically, "is that I haven\'t anything else to occupy my mind on this blamed world."', "Yet Carlin's first repelled dislike of Earth had faded much by now. The crudities of existence, the lack of civilized conveniences, no longer bothered him so much. He had to admit that whether or not Earth-treatment was benefiting his twisted subconscious, this sleepy old planet was a fine place for a rest.", 'He spent his mornings idly rambling the twisting roads, his afternoons lounging on the cool, shady veranda of the old house, or helping Marn tend the hydroponic tanks. Or fishing with Gramp in the foaming brook below the ridge, while that oldster told interminable tales of the old days when he had followed space.', 'Neighbors, hydroponic farmers up and down the valley, dropped in at the Land house in the evenings. Carlin did not intrude, and gradually their first stiff suspicion of him abated and they talked freely before him. The talk always swung to the paramount consideration on this power-starved planet—the need for copper. It made Carlin feel a little guilty to remember how much of it was wasted on other worlds.', '"I have to drive down to the spaceport for Jonny, to get some instruments he left in the ship," Marn said to him after dinner one evening. "Do you want to go along?"', 'Carlin grinned. "I\'ve legged it so much lately that riding anywhere would be a change."', 'The old ato-truck swung down the twisting road in the blaring sunset. The heavens behind them were a glory of fusing colors as the red ball of Sol dipped majestically toward the horizon.', "Despite his appreciation of that wild splendor, Carlin felt a vague uneasiness. Why should the loveliness of the evening bring disturbing recollection of Jonny Land's puzzling machine into his mind?", '"You\'re getting to like it better here, aren\'t you?" asked Marn.', "She was usually so silent with him that Carlin glanced quickly at her profile as she drove. It struck him with surprise that she had a certain beauty. Her thick mop of ashen hair, and firm-chinned face, and small, competent hands grasping the wheel, were oddly attractive. It wasn't the fine-edged, shimmering beauty that Nila had, but it had appeal.", '"Yes, I must be getting more accustomed to it," he answered her question. "And it\'s not as provincial as I thought. Nearly every man you meet here has been to space some time or other."', '"Every Earth boy runs away to space sooner or later," she said, and smiled. "Following space is in our blood. And our planet\'s so poor now that it\'s the only way most of our men can make a living." She added, "Some of our men never come back. My father didn\'t. And my mother died, when he was lost."', "It was dusk when they reached the spaceport. As he walked with the girl along its edge toward her brothers' ship, she drew him aside toward a tall shaft that loomed up spectrally in the twilight.", '"This is where the first Earthman went away to space," she told him.', 'He looked at the deeply engraved legend on the pedestal of the soaring column. It was the Monument to the Space-Pioneers.', '"Gorham Johnson took off in his first flight from this very spot," Marn said.', 'Carlin strained his eyes in the dusk to read the roll of names and dates engraved on the pedestal.', 'Gorham Johnson, 1991 Mark Carew, 1998 Jan Wenzi, 2006 John North, 2012', 'Names of the men who long ago had first dared space, the men who had first followed a dream to the nearby planets that then had seemed so far, the men who had first hurtled starward and opened up the galaxy.', '"Lord, more than two thousand years ago," Carlin murmured. "Queer little ships they must have had."', 'His imagination was touched. This simple roll of names of men long dead somehow brought it all close to him for the first time.', 'Those old, pathetically flimsy ships, the enormous courage of those men to whom space was all one unknown abyss. He began to understand why tourists came from all the galaxy to see these mementoes.', '"They and their little ships started it all, the whole galactic civilization, the vast human empire," he said musingly.', 'Marn was looking up at the spire towering in the dusk.', '"People criticize us Earthmen for our pride. But this is why we\'re proud. We\'re the people who opened up the frontiers of the Universe."', 'Carlin nodded thoughtfully. "You\'ve a great heritage. But perhaps you remember it too well. This is the present, not the past."', '"You\'re like all the others, you think Earth\'s history is over," Marn said defiantly. "You\'ll find out differently. Earthmen will open up the last frontier of all—" She checked herself suddenly, and then said, crestfallen, "I\'m sorry. I didn\'t mean to quarrel."', "Carlin wanted to ask what she had meant, but Marn started on again through the deepening darkness toward her brother's ship.", 'He walked with her into the battered planet-cruiser and looked around curiously. It was a medium craft designed for a minimum crew, with oversize cyclotrons and propulsion-wave equipment, drive-plates fore and aft, and an unusually heavy set of heat-screen generators.', '"The Hot Side of Mercury is terrible," Marn said when she saw him glancing at the generators. "You need the heaviest heat-screens you can get to prospect there."', 'Amidships, Carlin noticed a big, empty round room or hold. There was nothing in it but a skeleton of girders designed to hold something over a sliding plate in the floor.', "He remembered Jonny's big machine in the workshop. It would fit into this frame. He would have liked to make further inspection but Marn had found the instruments she had come after.", 'As they emerged from the ship, a lean, uniformed figure in the dusk greeted them in a pleasant voice.', '"Hello, Marn. I saw you walking across the tarmac. How is Jonny coming with his plans?"', 'It was a young man in the gray uniform of Control Operations, the agency of law and order throughout the galaxy. He bowed to Carlin.', '"I\'m Ross Floring, Control Operations commander here. You\'re the Earth-treatment chap staying with the Lands? Glad to meet you."', 'Floring was not more than thirty, an alert, clean-cut, likable young man. He turned back to Marn.', '"How soon are Jonny and his friends planning to take off for Mercury?"', 'Marn looked uncomfortable. "I don\'t know, Ross. They have some more preparations to make, they say."', "Carlin somehow sensed a strain in the atmosphere. There was an earnestness in Floring's manner that was not accounted for by his words.", '"I like Jonny a lot, Marn," he said seriously. "You know that. I\'d hate to see him have trouble on this expedition."', 'Marn seemed to evade his meaning. "Jonny won\'t have any trouble. A trip to Mercury is nothing for Harb and him."', '"I sincerely hope he won\'t," Floring said quietly. "Copper isn\'t worth risking too much for. Tell him I said so, will you? And tell him I\'m coming up some day to talk with him."', 'Marn was obviously eager to get away. Carlin, puzzled, followed her.', '"I\'ll see you again, Mr. Carlin," Floring called after him pleasantly. "We can have a talk about home. Yes, I come from Canopus too."', "It wasn't until they were in the ato-truck driving homeward that Carlin realized he hadn't told Floring his name or origin. Why would Control Operations have taken the trouble to check up on that?", '"Floring seemed like a nice chap," he told Marn. The girl nodded, troubled.', '"He is—one of the best," she said. "And he likes Jonny. But he\'d forget everything else for his duty."', 'She was, obviously, thinking aloud rather than answering Carlin. He wondered again about that queer feeling of strain. It had sounded almost as though Floring were warning her.'], 'CHAPTER V': ['Desperate Play', 'The truck wheezed and groaned up the dark old road to the ridge. In the velvet black skies, the stars were chains of glittering light. Vega, Arcturus, Altair—they looked far away.', 'The house was dark when Marn stopped the truck behind it, though there were still lights out in the workshop. There was a solemn, buzzing hush about the starlit summer night.', '"I have to take these things back to Jonny," said the girl.', '"Marn, what are your brothers really planning?" Carlin asked her. "Does Floring know?"', 'She twisted uncomfortably. "Jonny told you all about their plans himself, didn\'t he?"', 'She was such a poor liar, she was so oddly appealing a figure in the starlight as she looked up at him with troubled white face, that sudden impulse made Carlin bend and kiss her.', 'Her small body was firm and warm in his hands and there was a breathlessness about her cool lips. But she did not move.', 'He looked down at her. "You don\'t mind, do you?" he asked.', '"No, I don\'t mind," Marn said, her voice toneless, "It\'s all right for a star-world visitor to have a little flirtation with an Earth girl before he goes away, isn\'t it?"', '"But it isn\'t that!" Carlin started to protest, and then stopped.', 'After all, what was it but that? What could it be but that?', '"It\'s all right, but please don\'t again," Marn said quietly. "Good night, Laird."', "He went into the house feeling depressed and thoughtful. He wished now that he hadn't had that impulse. Marn wasn't the sophisticated sort.", 'Lying in his bed and looking out the window at the distant spaceport beacons down in the valley, Carlin heard her come in and retire. Apparently Jonny and Harb were still working.', 'What were they working at really? Why had Floring been so grave in his veiled warning?', '"Oh, the devil, it\'s none of my business," Carlin yawned. "There isn\'t much in this little system for them to get into trouble about. Nothing but eight or nine small planets and one medium sun."', 'Carlin suddenly sat bolt upright in bed as his mind dwelt on that last thought.', '"The Sun? Good glory, that\'s what they\'re up to! It must be! Sun-mining!"', 'He was dismayed, horrified by the sudden flash of revelation. The disquieting mystery that had puzzled him since his first coming here suddenly shaped clearly as pieces fell together in his mind.', '"They wouldn\'t be so crazy as to try it, surely! Yet it all fits together—the heat-screens on their ship, the secrecy about it all. And that machine I saw could be a big magnetic dredge!"', 'Sun-mining! Most strictly forbidden of enterprises, banned by the Control Council for years since the first disastrous attempts at it had almost wrecked certain planetary systems.', "Visions of frightening possibilities crowded Carlin's mind, of a desperately reckless attempt unchaining catastrophe on the inner planets of this little system.", '"But Jonny Land wouldn\'t try it! He\'s a CE, he knows what would happen."', "Carlin could not convince himself. He remembered only too clearly Jonny's intense obsession with Earth's copper shortage, his quiet determination.", 'And Floring must suspect something of the truth! That was what had made the Control Officer give his grave hinted warning.', 'Carlin got up and feverishly dressed. He had to find out the truth, now, at once. If the Land brothers and their friends were really bent on such a mad enterprise, it would have to be stopped even if it meant his informing Control Operations.', '"If I could get one good look at the inside of that machine of theirs, I could soon tell whether it\'s really a magnetic dredge," he thought.', 'He went quietly down through the dark house and out into the starlight. Light and sounds of activity still came from the workshop.', "Carlin crept toward it. He hated this spying. But he had to know. He couldn't permit a crazy attempt to unloose disaster here.", 'The workshop was closed, and there were no windows. But as he stood irresolute, the big front doors opened and Loesser and two other young Earthmen came out, wearily mopping their brows.', '"We\'ll be back tomorrow, Jonny," Loesser called back into the building. "Ought to finish her up in a few days now."', 'The three strode wearily toward their ato-truck and drove away. The doors remained open for the moment.', 'Carlin stepped forward and from his vantage in the dark peered into the big lighted room. Jonny and Harb Land were putting back the metal cover on the central mechanism, before they too quit work.', "One glance at the interior of that machine was enough for Carlin's trained eyes. Those big magnetic-current coils, that massive beam-head, that battery of Markheim filters—he had been right, they spelled disaster.", "A small, hard object prodded Carlin's back and a voice throbbing with anger spoke in his ear.", '"This is an atom-pistol. Raise your hands. I don\'t want to harm you."', '"Marn!" he exclaimed, stunned.', '"Don\'t turn!" warned the girl. Her voice was choked with wrath. "I heard you get up and I followed you out here. You are a spy!"', '"Don\'t turn!" warned the girl. "I followed you here. You are a spy!"', "Carlin was so stunned with horror by his discovery of the brothers' catastrophic plans, that he reacted by sheer, desperate impulse to the weapon in his back. He swung around and grabbed for the atom-pistol.", 'It would have been suicidal, had another than Marn been holding the weapon. But Marn, as much a stranger as he to deadly violence, let her finger hesitate on the trigger too long. Perhaps she would not have fired in any case. Pondering it later, he was not sure.', '"Harb! Jonny!"', "The two brothers came running out from the rear of the lighted workshop, Harb's craggy face dark and deadly as he saw them.", 'Carlin jumped back, leveled the weapon he had just taken from the girl.', "Jonny's voice rang command. The lame youngster's thin brown face was set, but he had not lost calm.", '"Harb, stop!"', 'The thing froze into a queer sort of tableau as Harb Land pulled up and stood there, his giant figure quivering with wrath, his big fists clenched as he glared at Carlin.', '"I told you," Harb said thickly over his shoulder to his brother. "I told you what would happen if we took him in."', 'Marn had run toward them, her face pale and stricken.', '"It\'s my fault, Jonny," she said despairingly. "I heard him come out and followed him, but let him take my gun instead of shooting."', '"Quiet, Marn," soothed Jonny. "It\'s going to be all right. Carlin just doesn\'t understand."', 'The lame youngster, in this taut moment of strain, was suddenly the biggest of them, the dominating personality here.', '"I understand, all right," Carlin said hotly. "I guessed it tonight, and one look at that magnetic dredge confirmed my guess." His voice crackled with the rising wrath he felt. "Going to Mercury prospecting, were you? You never had any such plan. You and your partners have been getting ready to attempt sun-mining."', '"Carlin, Earth\'s starved for power. You\'ve seen for yourself. To get the power that will revive our world, we\'ve got to have copper. And the copper in our planets was exhausted long ago. But there\'s still billions of tons of copper in our System, in one place. The Sun. It\'s there in hot gases, more copper than Earth and our sister-planets will need for millenniums to come. It\'s our only possible source of copper and we intend to tap it."', '"You and the others have brooded so long over your need for copper that you\'ve gone crazy!" Carlin said, his voice whipped with anger.', '"What\'s crazy about our using the copper of the Sun for our planet?" Jonny asked evenly.', '"You, a CE, ask me that?" cried Carlin. "You know as well as I do that sun-mining brings catastrophe! Oh, you can get close enough to the Sun in your ship, I know. You can suck up all the gaseous copper you want from it, with that magnetic dredge. But what happens on your Sun when you do it?', '"You know as well as I what would happen, what has always happened when it was tried. The suction creates a whirl in the solar surface, a tiny Sun-spot that grows and grows until it\'s grown into a terrific solar typhoon that pours disastrous increased heat and electric force onto its planets. You know it\'s happened every time Sun-mining was ever tried, and that that\'s why Control Council forbids Sun-mining."', 'Jonny Land nodded calmly. "I know all that. But suppose I\'ve found a way to do Sun-mining without starting Sun-spots?"', 'Disbelief hardened Carlin\'s voice. "You haven\'t. Nobody ever has. There just isn\'t any way—suck out gases from any point on the Sun and you lower pressure at that point, and lowered pressure automatically starts a whirl."', '"Carlin, I have found such a way! I tell you, with it we can suck unlimited copper from the Sun without creating one tiny Sun-spot!"', 'Laird Carlin stared. "You\'re telling me that, because you know I\'m going to report your plans to Control Operations."', '"You wouldn\'t do that!" cried Marn, incredulously.', 'Carlin nodded firmly. "I don\'t want to but I\'ve got to. I can\'t let a bunch of crazy men bring on a disaster that might scorch life itself off your inner planets."', "Jonny Land's thin face flared irritable emotion as he limped forward unheeding of the gun in Carlin's hand.", '"Carlin, man, be reasonable! Why do you suppose I had you come here and live with us? It was because you\'re a CE and I\'ll need another trained engineer\'s help in operating this thing. And do you suppose I ever thought I could get your help unless I could convince you I\'ve found the way to safe Sun-mining? I can convince you, Carlin!"', "Carlin felt the conviction in Jonny's voice. What the crippled young man said did logically explain something otherwise puzzling—why they had taken him into their home when their work was so secret.", 'He remembered now that it was not until Jonny Land had learned he was a CE, on his first arrival on Earth, that the young Earthman had shown interest and offered him lodgings.', '"All I ask," Jonny was saying earnestly, "is that you give me a chance to explain our plans to you. I know I can convince you that we can mine the Sun without the slightest danger of disaster."', '"If that\'s so," Carlin demanded skeptically, "why didn\'t you convince the Control Council of that, and get permission for Sun-mining instead of trying to do all this in secret?"', '"Carlin, I did try to convince the Council," Jonny Land declared. "I made one petition to them after another, giving them full details of my plan. But Council isn\'t composed of engineers. And the popular prejudice against Sun-mining, due to those past disasters, is so strong that Council refused us permission to make the attempt."', '"That\'s why Ross Floring and the others down at Control Operations watch my brothers so closely, Laird," Marn added quickly. "They know about our petitions, and Floring suspects that Jonny is going to try this thing anyway."', 'It all fitted together logically, Carlin had to admit. Yet he still stood irresolute, the atom-gun in his hand.', '"Here\'s a proposition, Carlin," said Jonny. "I\'ll explain every detail of our plan to you in the morning. If you don\'t admit then that the plan\'s completely without danger of disaster, I\'ll let you go and tell everything to Floring. I give you my word on it."', 'Carlin looked at him doubtfully. "Jonny, you\'d break your word as cheerfully as your neck to carry out your purpose for Earth."', 'Jonny Land grinned crookedly. "That\'s true. But on the other hand, I\'m still hoping for your help in this project. That\'s why I want to convince you, and that\'s the best guarantee I can give you."', 'Carlin shrugged, but he slowly lowered the weapon.', '"I can tell you right now that I\'ll have no part in any such illegal venture," he said flatly. "But I\'m willing to hear your explanation."', '"Well," Jonny said, with a tired sigh, "we\'ve had enough dramatics for one evening. Harb, lock up the workshop and we\'ll all turn in for tonight."', 'Carlin looked a little awkwardly at Marn as he handed her back the atom-pistol.', '"I\'m sorry if I appear ungrateful for your hospitality," he told her. "It\'s just that I can\'t stand by and do nothing if a crazy attempt threatens to bring on catastrophe."', '"I know," Marn said soberly, and there was no hostility in her face. "But you\'ll find out that Jonny knows what he\'s doing."', 'Out of the darkness behind them spoke a shrill voice that made Laird Carlin swing around in astonishment.', '"Well, I\'m blamed glad you people quit arguin\' for tonight, anyway. It\'s time all decent folks was in bed."', 'Gramp Land stood back there in the dark where he had apparently been standing for some time. There was a grin on his withered face as he lowered the heavy atom-gun he had been holding.', '"Sure got tired holdin\' this thing aimed at your back, Mr. Carlin," he chuckled.'], 'CHAPTER VI': ['"You Owe a Chance to Earth!"', 'Doubts assailed Carlin almost as soon as he retired. He could not sleep, the rest of that night.', 'Had he been childish to let Jonny persuade him into giving the plan a hearing? Jonny was sincere enough, but he was a fanatic on this one subject of securing power for Earth.', 'The recklessness of Earthmen was proverbial. These men, made desperate by long brooding over the poverty of their world, might think little of the danger of provoking solar catastrophe in their obsessed desire to secure copper.', "Carlin chilled. He remembered what had happened years ago at the star Mizar when Sun-mining had been attempted. The suck of magnetic dredges swiftly creating a whirl in the star's surface gases, a Sun-spot maelstrom that had expanded with disastrous swiftness. And then the engulfing of the mining ships in the sudden outpour of increased heat, the scorching of inner planets that wreaked ruin before the spots subsided.", "It had been the same later at Polaris, and at Delta Gemini. No wonder that such a popular wrath against Sun-mining had arisen that Control Council had strictly forbidden further attempts! Man's science, great as it was, was not yet great enough to dare tampering with stars.", 'Yet he could see, too, how these Earthmen would inevitably turn their thoughts to Sun-mining. There was not any copper left in their System except in one body—their Sun. And that had limitless amounts of the power-metal, in vaporized form. No wonder they had been led into the plan to tap the metal of their Sun.', 'Carlin dozed before daybreak, but woke with the sunrise and went down, to find the others already at breakfast. They greeted him with a word, all but Harb Land who maintained a stony, dangerous silence.', '"We\'ll go out and show you our work, as soon as you have breakfast," Jonny said quietly.', 'Gramp Land was the only one in good spirits. The old man twitted Carlin.', '"It\'s sure a good thing you got reasonable last night. I would have hated to blast you."', 'Marn smiled slightly. "You wouldn\'t have done it. You\'re too chicken-hearted even to kill a fly."', '"Ho, what are you talking about?" exclaimed Gramp indignantly. "When I was young, they called me the toughest Earthman in space."', 'Carlin walked silently out to the workshop with Harb and Jonny. The lame youngster opened the building, and then gestured toward the tall, cylindrical machine.', '"Take a look for yourself, first," he invited.', 'Carlin scanned the mechanism with trained eyes. Magnetic dredges were a little out of his line, yet the principle of the mechanism was clear enough.', '"You understand the basic idea of Sun-mining?" Jonny was saying. "A ship approaches the photosphere or visible surface of the Sun as closely as possible, protected by heavy heat-screens from the radiation. The magnetic dredge is then turned on. The dredge generates a high-powered magnetic field concentrated into a beam. That beam drives down into the swirling super-hot gases of the solar surface.', '"Those gases consist of dozens of metals and other elements in vaporized form—iron, copper, sodium, calcium and so on, all mixed together. The beam sucks a column of those solar gases up to the ship. For its magnetic pull powerfully attracts the iron vapor in the mixture, and so the whole mixture is rapidly sucked upward."', 'He pointed to the massive flared nozzles in the downward projector-face of the great machine.', '"The gases are sucked in there, through Markheim filters which can be set to screen out the atoms of any desired element. The copper gases are screened out, solidified by cooling, and stored. The other gases go on through the filters."', 'Carlin nodded curtly. "And those unwanted gases are ejected into space, and more of the solar mixture continuously drawn up, and so on until your ship is filled with copper. Yes, it\'s the same scheme that was used by the Mizar and Polaris Sun-miners. And it will have exactly the same result! Sucking gases out of any point in the solar surface will lower pressure at that point. And lowered pressure at any point of the photosphere instantly and inevitably starts a whirl of gases, a growing maelstrom or Sun-spot!"', 'Jonny Land shook his head. "Carlin, you\'re jumping to conclusions. This dredge does not simply eject its unwanted gases into space like former designs. Take a look at that beam-head more closely."', 'Carlin looked. And he was puzzled, after a brief inspection of the curious concentric construction of the beam-head.', '"I don\'t get it. It looks like you have two circular beam-heads, one inside the other."', '"That," said Jonny, "is the secret of my scheme. Lowered pressure in the solar surface at the point of suction creates a whirl, a Sun-spot. But suppose we can suck up gases without lowering pressure?"', 'Carlin stared. "How?"', '"The two beam-heads," reminded the lame youngster eagerly. "The inner one is the one that beams down a positive magnetic pull to suck up solar vapors. The outer one is designed to use a simultaneous negative magnetism to shoot the unwanted vapors back down into the Sun."', 'The whole meaning of the explanation flashed over Carlin, and the possibilities of it dawned across his brain.', 'He said nothing, but crawled under the towering dredge and for minutes inspected inside and outside of the beam-head, feed-tubes and cut-offs. He finally came back out to them.', '"Well?" challenged Jonny Land.', 'Carlin bit his lip. "I\'ve got to admit your scheme looks practical enough. You should be able to suck up gases without any Sun-spotting effect, by using that continuous kickback. But—"', '"But what?" demanded Harb Land, frowning.', 'Carlin shook his head. "Blast it, I can\'t see why the Council would turn down your petition if this is as workable as it seems."', 'Jonny shrugged. "I told you why. Control Council contains the finest statesmen in the galaxy. Statesmen, not engineers. They admitted their experts\' reports on this showed it theoretically workable. But they said it was too dangerous to take a chance on theory when it comes to tampering with suns. We don\'t need copper that badly, they said."', 'His fists clenched in sudden passion. "We don\'t need copper! The galaxy as a whole doesn\'t need it, they meant. And what does it matter if one little world called Earth is fading and dying for lack of the copper it squandered to open up the galaxy? What does it matter, except to Earthmen?"', 'It was the first time that Carlin had ever seen Jonny Land give way to emotion. The superhuman strain that drove and dominated this lame, thin youngster for a moment flared hot and anguished on his face. Then his narrow shoulders sagged. He stood looking at the towering dredge with brooding eyes, before turning to Carlin.', '"Carlin," he said then, "there\'s only one way to prove to the Council this way of Sun-mining is safe—and that\'s by doing it! That\'s what we\'re going to do. We\'re going to the Sun and come back with a shipload of copper. They\'ll see then that it\'s wholly safe. They\'ll have to give permission then. And a fleet of ships equipped with dredges can suck enough copper from the Sun to give Earth all the power it needs hereafter.', '"You\'ve seen the dredge and you know our plans. You\'ve seen enough of Earth to know how much our success would mean to this world. Carlin, do you still want to tell Floring about this?"', '"You couldn\'t!" exclaimed Harb Land harshly. "You couldn\'t destroy all the hope that\'s left for our world\'s people. You—all you star-world people—you owe this chance to Earth!"', "Carlin stood there, torn by conflicting feelings. Strong among them was his intense admiration as an engineer for the ingenuity and daring of Jonny Land's solution to the problem.", 'But there were other things to consider. There was the duty he and every citizen had to support the Control Council. That support was what kept galactic civilization going. Yet these Earthmen, this little band fighting so fiercely for their ancient, worn world would flout it.', '"Jonny!" came Marn\'s sharp cry from outside. "Jonny!"', '"Something\'s wrong!" Jonny exclaimed, limping hastily forward.', 'They hurried out into the sunlight. Marn was running toward them and at the same moment they heard the drumming of an approaching ato-car.', '"It\'s Ross Floring coming here!" Marn panted. "I recognized his car coming up the hill!"', '"He\'s only coming up here to look around. He suspects what we\'re up to, but he can\'t be sure. Don\'t show any excitement."', 'Harb gestured fiercely toward Carlin. "But if he says anything, Floring will know."', 'A pleasant voice hailed them. Ross Floring, lean in his gray uniform, drove up behind the house and climbed out of his ato-car.', '"Hello, folks," he greeted. "Thought I\'d come up and see you. Jonny, I haven\'t seen you for weeks. Every time you come down to the spaceport, you spend all your time buried in that ship."', 'Jonny smiled. "It\'s keeping us pretty busy, getting ready."', "Laird Carlin sensed genuine liking between the Control Operations officer and the lame young engineer. Yet there was unspoken tension too. It showed behind Jonny's cool smile and Floring's pleasant eyes.", 'Floring was looking past them, through the open doors of the workshop at the towering magnetic dredge.', '"Is that your new metal-finding dingus, Jonny? The thing you\'re going to use to locate copper on Mercury?"', 'He stepped toward it. Harb Land made a violent movement forward, but a flat look from his brother stopped him.', '"Yes, that\'s it," Jonny said. "Want to look it over, Ross?"', 'Floring stood, cocking his head at the towering machine. He laughed at the question.', '"Jonny, you know I\'m no engineer. A thing like this is beyond me." He turned toward Carlin. "But Mr. Carlin, you\'re a CE. What do you think of this new metal-finding device of Jonny\'s?"', "Breathless silence held the group for a moment. Floring's face was unmoved, pleasant, but his purpose was obvious now. Knowing that Carlin had come to Earth merely as an Earth-treatment case, he was counting on Carlin's unbiased truthfulness.", 'Carlin felt their eyes on him. Now was the time, he knew, to play the part of a good galactic citizen and inform Floring just what was going on. It was his duty to do it.', "But he couldn't! He couldn't betray the last desperate hope of a gallant old planet's people in their struggle against destiny! He had known he couldn't, from the time Floring had first appeared. He spoke as casually as he could.", '"Yes, I\'ve looked it over. It\'s one of the most ingenious metal-finders I\'ve ever seen."', 'Carlin felt a queer relief that was almost happiness, as he spoke. For he knew now that he could never have obstructed these people in their brave, desperate struggle to revive their planet.', 'But Ross Floring looked astounded. A little blank frown of surprise came into his face and he stared steadily at Carlin.', '"Then you approve of Jonny\'s plans?" he said quietly, "But, of course, I might have known that he\'d convince you."', "There was double meaning to the Control officer's words, clear to all of them. Yet they all ignored it.", "Floring was temporarily defeated. He couldn't take action without expert opinion that the machine before him was for Sun-mining. He had expected such an opinion from Carlin, and had been disappointed.", 'But he was not completely frustrated. Carlin found out now how thorough and resourceful was this pleasant young officer.', '"It would be a shame, Jonny," Floring remarked casually, "if you should run into disaster on this trip and the design of your new apparatus be lost. A metal-finder like this is too valuable to lose."', 'They were momentarily puzzled by the comment. But in the next moment, Floring showed what he had in mind. He drew from his jacket pocket a tiny tri-dimen camera, stepped close to the towering dredge, and before anyone could prevent it had snapped a half-dozen pictures of its interior mechanism.', 'Harb Land started forward with a smothered oath. But it was too late. Floring was already pocketing the camera.', '"I\'ll keep these films," he said calmly. "If your machine should ever be lost, the design of it will be preserved this way."', '"You can\'t keep those films!" Harb Land exclaimed angrily. "You\'ve no right!"', '"You surely don\'t think I would steal the design from you?" Floring said, with a look of surprise.', '"It isn\'t that," Harb protested. "But—"', '"But what?" the officer asked calmly.', 'Harb was silent, his craggy face a mixture of emotions as he looked appealingly at Jonny.', "Carlin understood Floring's cleverness. They could not protest the films without giving the real reason for their protest, and that they could not do.", '"It\'s all right for him to keep those pictures, Harb," Jonny said quietly.', 'Floring turned, bidding a pleasant farewell.', '"I\'ll be seeing you again soon," he promised.'], 'CHAPTER VII': ['Last Frontier', "As soon as Floring's ato-car had purred away, the little group stood in the sunlight outside the workshop, in stricken silence.", 'Carlin put into words what was in all their minds.', '"Jonny, you know why he took those pictures! He\'ll telephoto them to Canopus headquarters to be examined by engineer experts, and they\'ll send back word that the machine is a magnetic dredge for Sun-mining!"', 'Jonny nodded. "Yes, of course. Floring has suspected our plans all along, and now he\'s going to make sure."', '"And when word comes back from Canopus, he\'ll seize our dredge and ship to stop our expedition!" groaned Harb.', '"I know that," Jonny Land said, as his blue eyes swept them. "But it will take fourteen or fifteen hours before he gets that report back. Before that time ends, we\'ve got to be on our way to the Sun!"', 'Laird Carlin felt a shock of astonishment, but before he could comment, Jonny was speaking swiftly on.', '"It\'s our only chance now—to get away before Floring receives the proof that will authorize him to stop us! The dredge here is almost finished. If we can install it in the \'Phoenix\' and take off tonight, we\'ll have our chance to prove to the galaxy that Sun-mining can be safe."', '"Install the dredge tonight?" cried Harb Land. The gangling giant\'s face was sick with anxiety. "Jonny, we can\'t do it! Not that soon."', '"We\'ve got to!" Jonny\'s voice cut like a steel rapier. "Harb, you go get Loesser and Vito and the other boys. Have them bring the big truck with them. If we work hard enough, we should be able to have the dredge ready to roll by dark. Once we get it into the \'Phoenix\', we can take off and complete installation in space."', '"You can\'t do it," groaned his brother. "You know you figured on taking a week yet for that installation."', 'Carlin stepped forward. He had long ago reached his decision. He had reached it in that moment when he had answered Floring.', '"I\'m a CE, you know," he reminded. "I can help a lot in that installation."', "Marn stared at him, amazement and dawning gladness in her eyes. And Harb Land's tortured face turned haggardly on Carlin.", '"You\'d do that? You\'d help us? By heaven, if you would, we might make it!"', "Jonny's brilliant blue eyes bored Carlin's face.", '"Carlin, I was hoping for this. I knew from the first I\'d need another engineer\'s help in installing and operating the dredge. I brought you home because I was hoping I could enlist your aid before we started on the expedition. But all the same, I\'ve got to warn you. We\'re directly bucking a Control Council order. You can lose your certificate and go to Rigel prison, even if our plan succeeds. And if it doesn\'t succeed, it may mean perishing with us. And after all, Earth isn\'t your world."', '"Who the devil is doing anything for Earth?" Carlin retorted. "This old planet of yours means nothing to me either way."', '"Laird, are you so sure of that?" Marn asked him, her eyes very bright.', '"Do we have to get emotional?" Carlin asked roughly. "I\'m an engineer, and this is the biggest engineering experiment to be tried for centuries. Don\'t you think I want to be in on it?" He added crushingly, "And as for my getting mixed up in the blame, I\'m already blasted well mixed in it. When I denied to Floring that this was a magnetic dredge, I implicated myself right there in the whole business. I\'ve got to make it succeed, now."', 'Harb Land was already running toward his truck. Jonny shot sharp orders at his sister.', '"Marn, I want you and Gramp to watch the road this afternoon. Floring might come back. Carlin, you and I haven\'t a moment to lose."', 'Carlin strode after the limping youngster into the workshop, and Jonny there rapidly explained what remained to be done.', '"The kickback feed-pipes to the beam-head have to be hooked up, the cooling coils to solidify the copper are not yet in place, and the whole dredge has to be fastened in its frame so it\'ll be ready to swing aboard the truck tonight."', 'Carlin was appalled by the amount of work that remained, for two pairs of hands. But Jonny added an encouraging qualification.', '"Loesser and Harb and the others can help in the ato-welding and cable work if we set it up for them. They\'re all veteran spacemen and know how to handle ordinary tools."', "Carlin plunged into the work with Jonny. But as they toiled to set up the coils and feed-pipes of the massive mechanism, an inward aghastness at what he was doing oppressed Carlin's mind.", "Why was he doing it, breaking Control law and endangering his certificate and even his liberty? Why under heaven should he be sharing the risks of these men for a planet he hadn't even seen until a few weeks ago?", '"I must still be star-sick, unstable," he thought dismally. "Or I\'d never have got mixed up in this mad business. Sun-mining!"', "Blind reaction was dominating him. Curse it, he wasn't the type to join Quixotic forlorn hopes. He was Laird Carlin, sober, hard-working engineer, who ought right now to be far across the galaxy at the job to which he belonged.", "And all the time Carlin's mind spun miserably to this whirl of self-reproach and foreboding, he was working with Jonny at topmost speed, squeezing into the frame of the great dredge where the lame youngster could not go, fastening Veer-clamps, hooking self-sealing leads to the flat Markheim filters.", 'The sound of ato-trucks rocked the noon air, and Harb Land came running heavily into the workshop.', '"I got the others—Loesser\'s bringing in the big truck now," panted Harb. "What do you want us to do, Jonny?"', "Loesser, and Vito, and the other four young Earthmen who came hastening after Harb were dominated by excitement. Loesser's broad red face was shining with emotion as he came up to Carlin.", '"I want to apologize. I never thought any star-world stranger would come in with us and help us."', '"Save it, and get the welders on those rear feed-pipes," Carlin retorted. "Get in here—I\'ll show you."', 'Through the hot afternoon hours, the hiss of ato-welders and reek of fusing metal stifled the workshop.', 'Dripping with perspiration, stiff from cramped postures, Carlin worked on inside the great dredge.', "And all those hours, in rhythm with the welders' hiss and the clang of wrenches, his thoughts beat a mocking tempo through his brain.", '"All this, for no reason! For somebody else\'s world, a world that ought to have been evacuated long ago! Even if it succeeds, you win nothing. And if it fails, the Sun licks you all up like midges."', 'Yet he labored blindly on. It might be crazy, but what he had started, he would finish.', 'It was work against an inexorable time limit that rapidly was approaching. As the shadows lengthened, as the sun went down, they still had not finished.', 'Jonny Land limped unsteadily to turn on the workshop lights. His face was a gray mask of fatigue and sweat as he turned to the others.', '"Two more hours," he said huskily. "We can\'t take more, if we\'re to get the dredge into the \'Phoenix\' and take off before midnight."', 'Those two hours, afterward, seemed weeks in length to Carlin. And the mocking devil in his brain kept taunting, "It\'s no business of yours, you know!"', '"That\'s near enough!" Jonny\'s hoarse voice finally declared. "We can hook up those last cables on the way. All the work that require heavy tools is done—and we daren\'t take more time."', 'They were, all of them, drunk with fatigue, staggering with the furious drive of twelve hours of unbroken toil. Blackened by welder flare, glistening with sweat, they looked to Carlin like a crew of devils.', "Jonny's driving energy remained unconquerable.", '"Marn," he ordered, "back the big truck in here. Harb, you and Carlin rig the hoist."', 'The big, flat-bodied ato-truck backed ponderously into the workshop and they swung the massive magnetic dredge carefully aboard. Loesser and the others then hastily chained it to the bed of the truck.', 'Jonny limped toward the cab. "All right, we\'re starting. Harb, you drive. No, Marn—you\'re not going to the spaceport with us."', 'Marn, face white and eyes big with fear, saw the gleam of the atom-pistol that Harb was thrusting into his pocket.', '"Oh, Jonny, not that, no matter what happens!"', 'Jonny\'s blue eyes flashed arctic light. "That, or anything, now," he rasped. "You know what this means to our people, Marn."', 'Then his face softened, and he patted her arm.', 'Tears streaked her cheeks as she kissed and clung to him, and then to Harb.', 'Carlin was climbing heavily onto the truck when he felt her touch on his arm.', '"You too, Laird," she whispered, quivering lips blindly pressing his cheek. "All of you must come back."', '"Get on!" cried Harb Land, and then the truck went into gear.', 'Carlin jumped for the cab, and under the starry night they were rolling at increasing speed down the twisting road toward the valley.', "And suddenly all the nightmare mocking in Carlin's brain was gone and there was only the rush of sweet air against his face, and the splash of the lamps ahead, and the jolt and rumble of the big machine as they raced down toward the spaceport's distant beacons.", "Earth air and Earth smells in Carlin's nostrils, sleepy Earth sounds in his ears; the shine of the old spaceport's beacons, and the soaring loom of the distant tower that marked the spot where a man of long ago had first dared space. This world, this little Earth, was worth risking death for, even for a stranger from far stars!", "He knew he was a little crazy, he still had a corner of his mind that told him all this was mere intoxication of emotion which was sweeping away reason. But the mocking devil in Carlin's mind was gone, and he was one in mind and purpose with his companions, now.", '"It\'s like getting out of prison to get started!"', '"We\'re not off Earth yet!" warned Jonny. "Cut the lights and drive around to the north end of the spaceport, Harb. Ease the truck to the \'Phoenix\' as quietly as you can." A little later he warned, "Slower, slower. Keep to the edge of the tarmac."', 'Lightless, its motors a mere low rumble, the big truck crept around the dark edge of the spaceport toward the "Phoenix." The little planet-ship took black shape in the darkness, a low, torpedo bulk brooding beneath the stars. Harb backed the truck toward its side, as they jumped out of the cab.', 'Light flashed on them from a hand-krypton in the door of the "Phoenix!" A lean, uniformed figure stood there, gun in hand, looking at them.', '"I thought you would be coming," said Ross Floring quietly. "Jonny, I\'m sorry about this."', 'Carlin was as frozen as his companions, by the disastrous overturn of their attempt at secrecy. Floring stepped out of the ship.', '"I\'ve been looking through your ship while I waited," he said. "You have triple as much heat-screen coverage as you\'d need for the Hot Side of Mercury. You were going to the Sun."', '"You can\'t prove it, Ross," Jonny said levelly. "You\'ve no proof."', '"I\'ve enough to prohibit this ship from clearing Earth until investigation," Floring replied. "A certain report will reach me from Canopus by morning. Then we\'ll see."', "Carlin saw it then, saw the dark giant figure of Harb Land stealing around the truck and looming up behind Floring. He glimpsed the gleam of Harb's raised atom-pistol.", "Then Harb struck. The butt of the weapon came down on Floring's head and the officer crumpled limply to the tarmac.", '"See if anyone else is in the ship!" Jonny said swiftly. "Loesser, watch the Control station!"', 'Then he bent with Carlin over the unconscious man.', '"We\'ll have to take him with us," Jonny said. "If we leave him here he\'d soon be found, then the Control cruisers would be after us."', 'A few weeks before, Laird Carlin would have been aghast at seeing a semi-sacred officer of Control Operations struck down. With what spirit of reckless defiance of law had his companions infected him? He marveled at himself as he coolly picked up the limp figure.', '"Tie him into one of the chairs in the pilot room," Jonny was saying.', 'Harb came plunging out of the ship. "Nobody else aboard. He came over here alone."', 'By the time Carlin had the unconscious man secured in the pilot room, Harb and the others had slid open the big hatch in the side of the "Phoenix." Hastily, fumbling in darkness, they ran out the ship hoist and hooked onto the big magnetic dredge.', 'Then, with infinite labor, they swung the massive mechanism into the hold amidships. Mere short flashes of hand lamps had to suffice to guide the beam-head of the dredge down into the round keel opening.', '"Fasten half the frame bolts—they\'ll hold till we get into space," panted Jonny.', 'Carlin skinned his knuckles in the dark, fumbling with bolts and wrench. Every instant he expected to hear an alarm from Loesser that Control officers were coming.', '"That\'ll have to hold," said the sweating Jonny. "Run the truck off the tarmac. Harb, make ready for take-off!"'], 'CHAPTER VIII': ['Solar Struggle', 'Oxygenators started throbbing, doors clanged, as the others tumbled aboard. Harb Land, smeared with dirt and oil, his shock of hair wild, climbed into the pilot seat and expertly touched controls.', '"Generators coming on!" sang Loesser\'s breathless voice from the interphone, as the low, deep hum began.', '"Stasis on," said Harb rapidly, his fingers busy. The blue cushion of force was around them as Carlin slumped drunkenly into a seat. "Zero, two and five acceleration schedule. Here we go!"', 'And the "Phoenix" swept up with a rush from the spaceport, the propulsion-waves streaming from its drive-plates hurling it out and upward into the star-sown sky, the spaceport lamps and the southward blinking lights of New York falling swiftly away.', '"Authorization!" yelped a startled voice from the universal communic on the panel. "Give authorization for take-off!"', '"Authorization already given," Harb Land rapped back, then cut the communic. He laughed. "That\'ll puzzle them a while."', 'Crazy, reckless, suicidal, to Carlin seemed the way that Harb was taking them out from Earth. The atmosphere of the planet had no sooner started a shrill, rising scream around them than it fell and faded as they came out of the envelope of air.', "Luna burst up out of the eastern heavens like a great globe of dull gold against the stars. And then Carlin's eyes were smitten by the flare and glare of the brilliant disk of Sol, of the Sun.", 'And then the "Phoenix" lined out and was plunging headlong through the void at a speed that Carlin knew was flatly illegal to use inside any System, a rush toward that distant Sun flare.', '"Cut down, cut down!" cried Jonny to his brother. "Any more speed and you\'ll not be able to decelerate in time to orbit around the Sun."', 'Harb Land turned a wild, dirty face aflame with emotion. "By heaven, we\'re on our way at last! We\'ll show them now that Earthmen can still blaze a space-trail nobody else has dared!"', "Jonny Land's voice lashed them, his thin face dripping and determined.", '"You\'re all of you blowing your tops with excitement. This hasn\'t even started yet. Look at what we\'re heading for!"', 'Carlin heard the others fall silent and himself felt a chill of awe as he looked ahead at the giant fire orb toward which the "Phoenix" was plunging.', '"We\'ll be orbiting before we have the dredge set up, unless we hurry," Jonny prodded. "Come on, help me with it."', 'The big magnetic dredge had to be bolted into place, the coils and pipes had to be hooked to their connections inside the ship, the cables to the generators, the cooling coils to the compressor, the outlets of the Markheim filters to the bunkers astern.', 'Thrumming, creaking, shivering in every strut to the blind thrust of power that was hurling it on, the "Phoenix" rocked and shook about them as Carlin labored with Jonny and two of the other men to make those last connections. The cramped space in the hold around the dredge was hot, stifling, for the oxygenators couldn\'t keep the air there pure.', '"All ready!" Jonny called finally, after eternal-seeming hours of toil. "And none too soon. We\'re getting there fast. Harb has put out most of the heat-screens."', 'Through the windows, the ship seemed enveloped by a halo of dim light, the force-screens that repelled radiations of heat.', 'But when Carlin stumbled with Jonny into the pilot room, they were half blinded even through the screens by the fierce, blazing glare from ahead.', 'Half the sky ahead was Sun, a gigantic abyss of roaring flame that crushed the mind by its magnitude. All directions of space seemed canceled, and they were falling, falling, into an inferno of fire.', 'Harb turned a sweating face. "We\'ll cut off to orbit in less than an hour," he informed.', 'Ross Floring spoke from the chair in which he was tied, and in which he had come back into consciousness.', '"Jonny, I\'ve been waiting for you! Harb wouldn\'t listen to me. You\'ve got to turn back!"', 'Jonny shook his head. "No use, Ross, I know you\'re only doing your duty. And I\'m sorry to drag you into this danger. But we\'re not stopping now."', '"But you\'ll never get there!" Floring exclaimed. "Control cruisers must already be after you. They\'ll have found out where I am by now."', '"Empty threats!" Harb jeered. "They can\'t know where he is."', '"Jonny, look at my badge!" cried Floring. "See the tiny radio bulb in the back of it? It\'s a \'finder\' by which any Control officer can be located at any distance. When I didn\'t report back, they\'d use it to spot me out here."', '"If that\'s true," said Jonny Land, his thin face suddenly haggard, "they\'ll be after us by now. Harb, cut the communic back in!"', 'Harb obeyed. Roar of static from the gigantic orb ahead was a dull background to the sharp voice that came from the instrument.', '"Control Operations squadron four hundred thirty-three nine calling \'Phoenix!\' Last warning! We are overhauling you and will shell you unless you turn and surrender."', 'Startled, Harb Land jabbed a button and twisted the knob of the visor-screen. The far-seeing eye quartered space behind them, and then the black space scene held steady. There against the stars came a little pattern of four tiny triangles of light. Triangles—galaxy-wide sign of Control.', '"By heaven, they actually have come after us!" cried Harb. "Jonny, they\'re only minutes behind us and pulling up fast!"', '"We broadside as soon as we range you unless you turn now," warned the steely voice from the communic.', 'Laird Carlin, only a few weeks before, would no more have dreamed of disobeying a Control Operations command than he would have of picking stars from the sky. Galaxy citizens were trained to revere the great organization that had made the Universe a place of law and order.', 'But the ancient independence of these men of Earth was strong in him now. They had already risked so much, had incurred certain penalty even if they now surrendered.', '"Keep going!" Carlin exclaimed. "They can\'t follow us once you start orbiting close to the Sun\'s photosphere. No ordinary Control cruiser has heavy enough heat-screens to follow us into that!"', '"By Jupiter, it\'s so!" exclaimed Harb, faint hope lighting his face. "But I daren\'t crowd on more speed now. I\'ve got to start decelerating if we\'re to orbit correctly."', '"Decelerate by plan," Jonny said grimly. "They may not range us in time. We\'ll soon know."', 'The "Phoenix," flying at a tangent toward the gigantic sphere of the Sun, was aiming to swing into an orbit around Sol as close as possible to its photosphere or gaseous surface.', "It had to be so. No ship would ever have power enough to go that close to the Sun's colossal pull and hold its position by its own energy. To get that close and to stay that close to Sol without being drawn in to it, a ship had to go into an orbit around it like a tiny satellite.", 'The air in the "Phoenix" was already stifling hot. Jonny switched in another of the heat-screens, and the dim halo around the flying ship deepened.', "Harb's fingers were flashing over the controls, decelerating, steering the ship in a closing spiral toward the Sun.", '"Carlin, talk them out of this madness!" cried Ross Floring, aghast. "The cruisers will be broadsiding us in moments."', 'Carlin paid no attention. His eyes were on the visor-screen where the four cruisers now loomed big as they came closer.', 'Then it came. Silent, deadly, four blinding gouts of flame burst near the "Phoenix." Four salvos of atomic shells whose wave of force rocked the plunging ship. Loesser came tumbling into the pilot room, red face glistening.', '"They\'ll bracket us next salvo or two!" he yelled. "What\'s our chance?"', '"Turn on heat-screens Six and Seven!" roared Harb Land, without looking around. "I\'m going into orbit now!"', '"It\'s too soon!" Jonny cried warning. "It\'s—"', "Carlin saw that Harb hadn't even heard. The giant was recklessly cutting the elements of their plotted course, depending on their own power to pull into orbit in time.", 'The heat-screens, all they had, were on full now. Another salvo burst to spaceward of them. Carlin knew the men behind realized Floring was aboard. But Control Operations would sacrifice any men to prevent the Sun-mining that always before had meant disastrous solar disturbances.', '"Great blazing stars!" breathed Loesser, staring. "Look at that!"', 'Forgotten, the deadly shells that were groping for them. For now the "Phoenix" was deep in the awesome corona of the star and was curving in closer through heat that was over two thousand degrees.', "Carlin's mind shook to the fearful spectacle that was the firmament. Not he, nor any other living man, had ever come so close to a star. They were entering a region of such violent energies that all laws of space and time here seemed cancelled.", 'Blinding, eye-dazing even through the strong protective filter of the heat-screens, the brilliance of Sol stunned them. They looked on a vast, raging ocean of flaming gases, a sea of vaporized metallic and non-metallic elements that was like a cosmic furnace.', 'Even through the heat-screens, the radiance heated the air in the ship scorchingly. But now the visor-screen showed that the Control cruisers were falling back and disappearing from sight behind.', 'Blinding, eye-dazing even through the filter of the heat-screens, the brilliance of Sol stunned them.', '"They couldn\'t follow us this close to the photosphere!" Harb cried exultantly. "We\'ve shaken them and we\'re almost in orbit."', '"You can\'t orbit the Sun!" Floring pleaded. "And even if you could, the cruisers will lay to outside the heat and range you by locator and fire till they destroy us! Put about!"', 'The man Vito, choking and gasping for breath, came into the pilot room from the engine rooms astern.', '"Heat-screens won\'t take another dyne! If we go closer, we\'re done for."', '"We\'re orbiting now," Jonny said huskily. "Wait!"', 'Harb Land was engaged in the most difficult operation of spacemanship, bringing a ship into exact balanced orbit around a celestial body.', 'Most difficult, even when the body was a planet. Impossible, nearly, when the body was a Titanic star!', "Carlin saw the giant's face a frozen mask as he centered his dial needles, fed force with infinite delicacy, guided, changed—and changed again.", 'Harb reached and slammed open a switch. The hum of propulsion waves died. The "Phoenix" was without driving power. And the needle of the gravi-gauges remained constant, the ship\'s path around the Sun was unvarying.', '"We\'ve orbited!" Harb Land\'s voice was a hoarse, exhausted sound.', 'Carlin wanted to shout, "By heaven, there are no spacemen in the galaxy except Earthmen—none!"', 'The "Phoenix" was circling the Sun, deep in the corona and reversing layer and close to the photosphere or light-emitting surface which was the vague boundary of the star itself.', 'Their sensation was that of men suspended over a Universe of raging flame and force. The mind shook to the impact of it. They were here where no men, no life, had ever been intended to be. They were violating the sanctity of a star.', '"Now—the dredge," Jonny said hoarsely. "We\'ve not power enough to force the heat-screens like this for long. Come on, Carlin."', 'Carlin stumbled back with him into the stifling hold. The men around the towering magnetic dredge were like sooty devils staring with wild eyes.', 'The metal was so hot its touch made him cry out as he closed the circuit of the generators with the ato-turbines. The rotors began their whine, building up a magnetic field.', 'The whole ship suddenly shook and quivered. Harb came plunging back into the hold.', '"Those Control Cruisers are starting to salvo us by radiolocator!"', '"We only need a little time," panted Jonny Land. "The cooler coils, Carlin!"', "Carlin felt like a man in a dream as he sweated with Jonny to get the magnetic dredge started. The field was building steadily, and the great nozzles of the beam-head had been lowered below the keel. Jonny's brilliant eyes clung to the panel of gauges, and finally he opened the field-switch.", '"Now!"', 'They crowded around the view-plate in the keel, peering half-blindly down against the glare of the raging Sun-sea below. The dredge was projecting a powerful, concentrated magnetic field down into that ocean of flaming gas like a sucking straw. But for moments they saw nothing. Time that seemed endless went by. Then—', '"Here she comes!" yelled Loesser.', 'A column of flaming vapor was shooting up from the fiery ocean below. Compared to the gigantic mass of Sol, it was the merest filament, the flimsiest thread of fire.', 'But it was rushing up and up toward the hovering "Phoenix," a finger of fiery vaporized elements drawn irresistibly up along the beam of magnetism to the ship.', 'Another salvo of shells went off in space somewhere close by and rocked the ship with its wave of force. But next instant came a heavier impact, as the fiery column of gas reached the nozzles below the ship.', "They heard a deafening roar. That up-sucked stream of vaporized elements was being drawn through the heat-proof nozzles and intakes, through the Markheim filters that screened out its copper atoms, and was then being shot downward again by the kickback's negative field.", '"The kickback\'s working!" Jonny Land yelled. "If the effect of it is what we calculated, we\'ve done it!"'], 'CHAPTER IX': ['An Earthman Comes Home', 'For the moment, none of them paid any attention to the fact that precious copper was solidifying in the cooler coils into granules of metal that were being blown into the bunkers. The real test was what their beam of magnetic force was doing to the surface of the Sun.', "Did it seem incredible, as it almost did to Carlin, that such a fragile finger of force could in the least disturb the mighty orb below? He knew better. He knew the unnaturally delicate balance of a star's surface, which a slight change of pressure artificially induced could stir into a whirl that would expand in giant Sun-spots. If that happened, it would mean chaos.", '"No sign of a whirl yet," Jonny breathed, peering down through black glare-proof lenses. "No sign at all."', 'There was no moment of crisis, no clean-cut moment of triumph. There was just the time speeding by, the flow of copper into the ship, and the constant reports of Jonny—"No whirl forming yet."', "Salvos shook the ship as the Control cruisers far outside the sun glare fired more and more accurately. But they went unheeded. Success or failure of the most audacious engineering exploit in the galaxy's history hinged upon Jonny's muttered reports.", '"No whirl yet."', 'Jonny Land finally raised his head, looked at them as they stood with wild surmise on their faces.', '"We\'ve done it," he said, almost unbelievingly. "We\'ve nearly filled the bunkers with copper and there\'s no whirl down there, no disturbance to grow into a spot. We\'ve made Sun-mining possible."', "Tears were running down Loesser's face. Harb Land looked dazed. But Jonny walked across the hold to the wall through which the cooler coils fed into the bunkers. He peered through a quartz view-plate.", 'They looked with him. The bunker rooms were heaped high with shining red granules. Copper, virgin-pure, blown into the rooms and already almost filling them. Copper milked from the Sun!', '"Copper for Earth!" whispered Jonny, his thin face blazing now. "Power, and new life, for the old planet!"', 'The "Phoenix" rocked wildly and metal screeched rendingly as they were flung from their feet by a salvo that had finally bracketed the ship.', '"The feed-pipes!" screeched Loesser, scrambling to his feet beside Carlin.', "Carlin saw. The ship's walls had held, but the shock had snapped strained cables and cooler coils. Two intake tubes were giving way, white-hot copper vapor forcing out through cracks in them.", '"Veer-clamps on those two pipes!" yelled Jonny. "If they give, everything goes!"', 'Knowledge of what it meant if the pipes gave way, if super-heated metallic vapor blew out into the hold, flung Carlin in a crazy rush for the Veer-clamps and wrenches.', 'He got a clamp around one of the pipes, and the man Vito started spinning shut the bolts that would hold the fracture tightly. He swung round toward the other pipe.', '"Clamp!" yelled Jonny Land, in a cry that was like a hoarse howl of agony.', "Carlin's blood left his heart as he glimpsed the most horrible and heroic sight he had ever beheld. The other strained tube had been about to blow open, and Jonny Land had flung his arms around it and was holding it together by agonized effort while the white-hot vapor sprayed his body.", 'Harb Land wildly snatched his brother away as Carlin flung the big clamp around the pipe and convulsively spun its bolts shut.', 'He staggered around then. Harb was bending over his brother.', '"Jonny! Jonny!"', "Jonny's whole chest and neck were blackened and blasted. His face was a ghastly, sooted mask as his eyes looked up at them.", 'Another salvo went off close by, and again the "Phoenix" rocked wildly.', '"Cut the dredge!" Carlin cried. "We\'ve proved the process is successful, and we can\'t stay here now or your brother will die!"', '"Control cruisers from \'Phoenix!\' We\'re putting out to surrender. Be ready to give injured man medical treatment."', '"Break out of your orbit at once and we\'ll contact you for surrender by locator when you\'re outside the corona," came the sharp, fast answer.', 'The generators of the "Phoenix" started roaring their shrillest note as Harb Land frantically flung power into the drive-plates. Beneath the thrust of its propulsion vibrations the battered ship began to move, to fight its way out of the gigantic pull of Sol, breaking slowly out in a tangent off its orbit.', 'Carlin, Loesser, all of them in the hold, were bending over Jonny Land when Floring, released by Harb, came back. The officer looked down and then shook his head somberly.', '"No chance," he said. "He won\'t even last until we reach the cruisers."', 'Jonny was lying, unhearing, fighting for breath, looking up at them without seeing them, his sooted face a writhing mask. Carlin felt tears sting his eyes, and saw everything through a blur.', '"Jonny, we did it—you did it!" Loesser was choking. "Made Sun-mining possible! Why, soon now there\'ll be scores of ships, new, big ships, coming here and getting all the copper Earth needs!"', 'He was, Carlin knew, trying to reach home to the dimming mind with that reassurance, that assurance that the dying man had not given away life in vain.', "It didn't reach Jonny Land. He wasn't Jonny Land any longer, he was just a living creature dying in pain, and he couldn't feel or know anything but pain. And then the pain went, and life went with it, and his face was a lax, empty mask that had no meaning for them.", "Carlin felt dull, tired, drained of emotion. He had just seen the only hero he had ever known die, but a hero's death was just death, just mortal pang and final release.", 'He went forward to the pilot room.', '"Jonny\'s dead," he said to Harb Land.', 'Harb\'s shoulders sagged, but he did not turn as he guided the "Phoenix" on spaceward to where the grim Control cruisers waited.', 'Control Court here in New York was only a small room in the building by the spaceport. There were no officials in it except the three middle-aged judges who sat behind a small table and prepared to pass sentence on Laird Carlin and his seven comrades.', 'There were no lawyers, no oratory, no jurymen. They were not needed. The government psychologists who had quietly questioned the accused men during their four days in prison had submitted the factual hypnosis records which were complete and incontrovertible evidence.', 'The chief judge, the man in the middle, quietly read the decision as Carlin and the others faced him.', '"This court is placed in a peculiarly difficult position in assessing your offense. On the one hand, you men deliberately broke a Control Council regulation and defied its officers. On the other hand, your action has proved the practicability of a process of Sun-mining which will be of incalculable value to this and every other System in the galaxy.', '"To forgive your offense because the ultimate result was good would be to set a fatal precedent. It would establish the principle that illegal means do not matter if end-purposes are good. We cannot permit such a precedent to be established. Therefore, regretfully, this court must pass the prescribed punishment for your offense."', 'Carlin could not deny the crystalline logic. He had known from the first that this must be the issue, and he was too tired to care.', '"You are sentenced to two years imprisonment in Rigel Prison and also to the loss of your spacemen\'s licenses or Cosmic Engineer\'s certificate, whichever you hold. Such sentence is obligatory in this case." He added quickly, "It is, however, within our discretion to suspend the prison term and to limit cancellation of your certificates to one year from date. Such is the sentence of this court."', 'Loesser drew a gusty breath of relief. "For a minute, I thought it was Rigel for us sure enough!"', 'The chief judge had risen. "Speaking personally," he added quietly, "we would like to congratulate you men upon a great achievement."', 'Ross Floring came to their side.', '"A year\'s suspension isn\'t long," he said, and Carlin nodded wearily.', "When, with Harb Land's giant figure leading them, they emerged from the building into the sunlight, a roar that deafened them came from the waiting crowd outside. The people of Earth, at least, had no need to temper their gratitude.", 'Harb was grimly silent as he pushed through the crowd toward Marn and old Gramp Land. Carlin found himself buffeted by eager hands, assailed by joyful faces and voices, as he followed.', 'A grizzled, excited man clapped his shoulder. "We Earthmen showed \'em we could still conquer space, didn\'t we?"', "We Earthmen? Somehow, for the first time in all these days, Carlin's dulled mind felt a stir of pride as though at an accolade.", "He didn't like to meet Marn's pale face. But she spoke steadily.", '"It\'s all right, Laird, about Jonny. Women of Earth for two thousand years have seen their men go out into space—and not all come back."', 'Floring had followed them. "I want you to see something," he said.', 'He led the way toward the towering Monument of the Space-Pioneers. Carlin looked at the roll of names. Then his eyes suddenly blurred as he saw that, for the first time in several centuries, a new name had been added to the bottom of that great roll.', 'JON LAND', "Marn's eyes were shining. And her giant brother looked long, with haggard face somehow comforted. But old Gramp Land turned sadly away.", '"A name on a stone is poor exchange for my boy," he muttered. "I\'m gettin\' old."', 'That evening, in the old house up on the ridge, they were subdued and silent at dinner. The table was too big, and they looked around too often as if listening for a familiar limping step and a cheerful voice.', 'Carlin was doubly oppressed because of the thing that he had not yet told them. He hated, somehow, to break the news.', '"There\'s something they found out when they made our psycho-records for the trial," he said finally. "Mine showed that I had no instability of coordination, no star-sickness any longer."', '"You mean, you\'re cured?" said Harb, surprised. "Why, that\'s fine. I never thought of it, but you made the trip Sunward all right, so I should have known."', '"The psychos say," Carlin told them, "that some people out in the galaxy now and then approximate much closer to the original Earth stock than the average. Such people respond rapidly to Earth-treatment. I\'m one of them, it seems." He added uncomfortably, "I can go back home to Canopus now, though I\'ll have to work at a desk job for a year. The only thing is that there\'s a ship for Canopus tonight, and there won\'t be another for weeks."', '"You\'re not going tonight?" exclaimed Harb. "Not as soon as that?"', 'Carlin felt a little heartsick. "I wish I didn\'t have to, so soon. But there\'s nothing for me to do here now that I\'m all okay."', '"I\'ll drive you down to the spaceport."', '"I think I\'d rather walk down," Carlin said slowly. "I don\'t know why, but I would. It\'s not far and I sent my bags on down."', '"Then I\'ll walk a little of the way with you," said Marn.', 'Twilight had changed into soft summer darkness by the time Carlin had exchanged a last old-fashioned hand grip with Harb and Gramp Land, and started down the road with Marn.', 'She went only around the first turn of the old road with him, and then stopped.', '"Good-by, Marn," he said, but she only averted her face.', 'Carlin hesitated, then turned and walked on. Luna was lifting its shining shield in the east, and the silver summer silence lay over everything, hardly broken by the stir of branches and the low buzz of insects. The night was warm and still.', "He had a lump in his throat and he tried to laugh at himself because he had it. A man couldn't let illogical emotions overrule his reason. This crazy, heroic old planet Earth and its people—he would never forget them, but he had to return to his own life and work, he had to go home.", "Laird Carlin suddenly stopped. He knew, abruptly, why dull oppression had gnawed his mind all day. It wasn't because he was going home. It was because he was leaving home. He was leaving the only place where his spirit had ever found something it had always lacked, a peace, an ancient certitude, a kinship that had grown and grown.", 'Carlin turned and strode rapidly back up the road. Not until he was almost upon her did he perceive that Marn Land was still standing in the silvered road where he had left her.', '"I was waiting for you," she said simply. "I knew you wouldn\'t go."', 'His hands grasped her shoulders as he spoke in a rush.', '"Marn, I couldn\'t! I thought of Canopus, I thought of friends there and a girl who likes me and the garden cities I used to love, and it was all unreal, I\'m tied somehow to this queer old planet, to Jonny and Harb and all of the others, and to you!"', 'She came into his arms quietly. "I know. There\'s been more than one like you, more than one who came to Earth and found he somehow couldn\'t leave. This old world is in the blood of our race, Laird." She looked up. "A year\'s not long. We\'ll need you here to replace Jonny, to supervise the Sun-mining. And I need you. I always will."', 'Carlin held her closely, all tiredness and doubts gone now, strangely content. He looked up at the summer stars and thought of worlds out there, but it was all far away, far away.', 'And Earth was close, its ancient quiet night enfolding him. Soft wind stirred leafing branches in the moonlight, and the road wound up white and sure toward the old house, and out of the vastness of time and space, an Earthman had come home.']})



```python
import pandas as pd
forgotten_world  = pd.DataFrame.from_dict(chapter_dict, orient='index') 
forgotten_world
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>77</th>
      <th>78</th>
      <th>79</th>
      <th>80</th>
      <th>81</th>
      <th>82</th>
      <th>83</th>
      <th>84</th>
      <th>85</th>
      <th>86</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CHAPTER I</th>
      <td>Stranger from the Stars</td>
      <td>Carlin was the only one of the four hundred pa...</td>
      <td>He was bored with the vessel and everyone aboa...</td>
      <td>A blond girl from Altair Four came tripping al...</td>
      <td>The blonde from Altair Four favored the tall d...</td>
      <td>"Oh, Mr, Carlin, the annunciators just said th...</td>
      <td>"Just what is thrilling about it?" Carlin aske...</td>
      <td>The girl was a little dumfounded. "Why, I mean...</td>
      <td>She prattled on, voicing all the appropriate c...</td>
      <td>"Just think, all of us in this ship came from ...</td>
      <td>...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>CHAPTER II</th>
      <td>Ancient Town</td>
      <td>Carlin looked with a jaundiced eye on the scen...</td>
      <td>This ancient town called New York was like a m...</td>
      <td>"It's like one of the bird-people's lofts on P...</td>
      <td>Old? Yes. Pitifully old, like a withered belda...</td>
      <td>The spaceport, some distance northward amid lo...</td>
      <td>The "Larkoom" landed softly. Carlin waited wea...</td>
      <td>But for a moment, he was startled by the air h...</td>
      <td>He looked around uncertainly. The tourists wer...</td>
      <td>The psychotherapist had told him, "Live as nea...</td>
      <td>...</td>
      <td>Marn uttered an apologetic exclamation. "Oh, I...</td>
      <td>She led upstairs. There was no grav-lift, just...</td>
      <td>It was clean, of course, spotlessly so. But it...</td>
      <td>Yet the girl made no apologies for it, seemed ...</td>
      <td>"We'll bring your bags up after dinner," she s...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>CHAPTER III</th>
      <td>Old Planet</td>
      <td>When Marn had gone, Carlin lay down wearily on...</td>
      <td>But it wasn't the voyage so much as this world...</td>
      <td>The sound of an angry voice came up dimly thro...</td>
      <td>"—if Control Operations finds out what we're d...</td>
      <td>There was a murmur of lower voices, and then t...</td>
      <td>What were these Earthmen doing that they were ...</td>
      <td>When Carlin went down to dinner, he expected o...</td>
      <td>Carlin stared dismayedly at the food set befor...</td>
      <td>He ate what he could, which was little. His we...</td>
      <td>...</td>
      <td>Carlin recognized the broad red face, angry ey...</td>
      <td>"What are you doing here?" Loesser demanded ha...</td>
      <td>Carlin was bewildered by his vehemence. "Why, ...</td>
      <td>"I thought so!" blazed Loesser, his eyes ragin...</td>
      <td>He snatched an object from his jacket pocket. ...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>CHAPTER IV</th>
      <td>Mystery Machine</td>
      <td>Laird Carlin was child of a galactic civilizat...</td>
      <td>The atom-pistol in Loesser's hand and the obvi...</td>
      <td>"Why, what's the matter?" he began, puzzled an...</td>
      <td>He knew later how near he had been to death. A...</td>
      <td>"Loesser, put that gun down!" snapped Jonny.</td>
      <td>Loesser turned violently. "This fellow was spy...</td>
      <td>Harb Land's craggy face darkened ominously.</td>
      <td>"I warned you what might happen," he said hars...</td>
      <td>"Is this man crazy?" Laird Carlin demanded bew...</td>
      <td>...</td>
      <td>"He is—one of the best," she said. "And he lik...</td>
      <td>She was, obviously, thinking aloud rather than...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>CHAPTER V</th>
      <td>Desperate Play</td>
      <td>The truck wheezed and groaned up the dark old ...</td>
      <td>The house was dark when Marn stopped the truck...</td>
      <td>"I have to take these things back to Jonny," s...</td>
      <td>"Marn, what are your brothers really planning?...</td>
      <td>She twisted uncomfortably. "Jonny told you all...</td>
      <td>She was such a poor liar, she was so oddly app...</td>
      <td>Her small body was firm and warm in his hands ...</td>
      <td>He looked down at her. "You don't mind, do you...</td>
      <td>"No, I don't mind," Marn said, her voice tonel...</td>
      <td>...</td>
      <td>Carlin shrugged, but he slowly lowered the wea...</td>
      <td>"I can tell you right now that I'll have no pa...</td>
      <td>"Well," Jonny said, with a tired sigh, "we've ...</td>
      <td>Carlin looked a little awkwardly at Marn as he...</td>
      <td>"I'm sorry if I appear ungrateful for your hos...</td>
      <td>"I know," Marn said soberly, and there was no ...</td>
      <td>Out of the darkness behind them spoke a shrill...</td>
      <td>"Well, I'm blamed glad you people quit arguin'...</td>
      <td>Gramp Land stood back there in the dark where ...</td>
      <td>"Sure got tired holdin' this thing aimed at yo...</td>
    </tr>
    <tr>
      <th>CHAPTER VI</th>
      <td>"You Owe a Chance to Earth!"</td>
      <td>Doubts assailed Carlin almost as soon as he re...</td>
      <td>Had he been childish to let Jonny persuade him...</td>
      <td>The recklessness of Earthmen was proverbial. T...</td>
      <td>Carlin chilled. He remembered what had happene...</td>
      <td>It had been the same later at Polaris, and at ...</td>
      <td>Yet he could see, too, how these Earthmen woul...</td>
      <td>Carlin dozed before daybreak, but woke with th...</td>
      <td>"We'll go out and show you our work, as soon a...</td>
      <td>Gramp Land was the only one in good spirits. T...</td>
      <td>...</td>
      <td>"It's all right for him to keep those pictures...</td>
      <td>Floring turned, bidding a pleasant farewell.</td>
      <td>"I'll be seeing you again soon," he promised.</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>CHAPTER VII</th>
      <td>Last Frontier</td>
      <td>As soon as Floring's ato-car had purred away, ...</td>
      <td>Carlin put into words what was in all their mi...</td>
      <td>"Jonny, you know why he took those pictures! H...</td>
      <td>Jonny nodded. "Yes, of course. Floring has sus...</td>
      <td>"And when word comes back from Canopus, he'll ...</td>
      <td>"I know that," Jonny Land said, as his blue ey...</td>
      <td>Laird Carlin felt a shock of astonishment, but...</td>
      <td>"It's our only chance now—to get away before F...</td>
      <td>"Install the dredge tonight?" cried Harb Land....</td>
      <td>...</td>
      <td>"We'll have to take him with us," Jonny said. ...</td>
      <td>A few weeks before, Laird Carlin would have be...</td>
      <td>"Tie him into one of the chairs in the pilot r...</td>
      <td>Harb came plunging out of the ship. "Nobody el...</td>
      <td>By the time Carlin had the unconscious man sec...</td>
      <td>Then, with infinite labor, they swung the mass...</td>
      <td>"Fasten half the frame bolts—they'll hold till...</td>
      <td>Carlin skinned his knuckles in the dark, fumbl...</td>
      <td>"That'll have to hold," said the sweating Jonn...</td>
      <td>None</td>
    </tr>
    <tr>
      <th>CHAPTER VIII</th>
      <td>Solar Struggle</td>
      <td>Oxygenators started throbbing, doors clanged, ...</td>
      <td>"Generators coming on!" sang Loesser's breathl...</td>
      <td>"Stasis on," said Harb rapidly, his fingers bu...</td>
      <td>And the "Phoenix" swept up with a rush from th...</td>
      <td>"Authorization!" yelped a startled voice from ...</td>
      <td>"Authorization already given," Harb Land rappe...</td>
      <td>Crazy, reckless, suicidal, to Carlin seemed th...</td>
      <td>Luna burst up out of the eastern heavens like ...</td>
      <td>And then the "Phoenix" lined out and was plung...</td>
      <td>...</td>
      <td>Carlin felt like a man in a dream as he sweate...</td>
      <td>"Now!"</td>
      <td>They crowded around the view-plate in the keel...</td>
      <td>"Here she comes!" yelled Loesser.</td>
      <td>A column of flaming vapor was shooting up from...</td>
      <td>But it was rushing up and up toward the hoveri...</td>
      <td>Another salvo of shells went off in space some...</td>
      <td>They heard a deafening roar. That up-sucked st...</td>
      <td>"The kickback's working!" Jonny Land yelled. "...</td>
      <td>None</td>
    </tr>
    <tr>
      <th>CHAPTER IX</th>
      <td>An Earthman Comes Home</td>
      <td>For the moment, none of them paid any attentio...</td>
      <td>Did it seem incredible, as it almost did to Ca...</td>
      <td>"No sign of a whirl yet," Jonny breathed, peer...</td>
      <td>There was no moment of crisis, no clean-cut mo...</td>
      <td>Salvos shook the ship as the Control cruisers ...</td>
      <td>"No whirl yet."</td>
      <td>Jonny Land finally raised his head, looked at ...</td>
      <td>"We've done it," he said, almost unbelievingly...</td>
      <td>Tears were running down Loesser's face. Harb L...</td>
      <td>...</td>
      <td>Carlin turned and strode rapidly back up the r...</td>
      <td>"I was waiting for you," she said simply. "I k...</td>
      <td>His hands grasped her shoulders as he spoke in...</td>
      <td>"Marn, I couldn't! I thought of Canopus, I tho...</td>
      <td>She came into his arms quietly. "I know. There...</td>
      <td>Carlin held her closely, all tiredness and dou...</td>
      <td>And Earth was close, its ancient quiet night e...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 87 columns</p>
</div>




```python
forgotten_world = forgotten_world.reset_index()
forgotten_world
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
      <th>index</th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>...</th>
      <th>77</th>
      <th>78</th>
      <th>79</th>
      <th>80</th>
      <th>81</th>
      <th>82</th>
      <th>83</th>
      <th>84</th>
      <th>85</th>
      <th>86</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CHAPTER I</td>
      <td>Stranger from the Stars</td>
      <td>Carlin was the only one of the four hundred pa...</td>
      <td>He was bored with the vessel and everyone aboa...</td>
      <td>A blond girl from Altair Four came tripping al...</td>
      <td>The blonde from Altair Four favored the tall d...</td>
      <td>"Oh, Mr, Carlin, the annunciators just said th...</td>
      <td>"Just what is thrilling about it?" Carlin aske...</td>
      <td>The girl was a little dumfounded. "Why, I mean...</td>
      <td>She prattled on, voicing all the appropriate c...</td>
      <td>...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CHAPTER II</td>
      <td>Ancient Town</td>
      <td>Carlin looked with a jaundiced eye on the scen...</td>
      <td>This ancient town called New York was like a m...</td>
      <td>"It's like one of the bird-people's lofts on P...</td>
      <td>Old? Yes. Pitifully old, like a withered belda...</td>
      <td>The spaceport, some distance northward amid lo...</td>
      <td>The "Larkoom" landed softly. Carlin waited wea...</td>
      <td>But for a moment, he was startled by the air h...</td>
      <td>He looked around uncertainly. The tourists wer...</td>
      <td>...</td>
      <td>Marn uttered an apologetic exclamation. "Oh, I...</td>
      <td>She led upstairs. There was no grav-lift, just...</td>
      <td>It was clean, of course, spotlessly so. But it...</td>
      <td>Yet the girl made no apologies for it, seemed ...</td>
      <td>"We'll bring your bags up after dinner," she s...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CHAPTER III</td>
      <td>Old Planet</td>
      <td>When Marn had gone, Carlin lay down wearily on...</td>
      <td>But it wasn't the voyage so much as this world...</td>
      <td>The sound of an angry voice came up dimly thro...</td>
      <td>"—if Control Operations finds out what we're d...</td>
      <td>There was a murmur of lower voices, and then t...</td>
      <td>What were these Earthmen doing that they were ...</td>
      <td>When Carlin went down to dinner, he expected o...</td>
      <td>Carlin stared dismayedly at the food set befor...</td>
      <td>...</td>
      <td>Carlin recognized the broad red face, angry ey...</td>
      <td>"What are you doing here?" Loesser demanded ha...</td>
      <td>Carlin was bewildered by his vehemence. "Why, ...</td>
      <td>"I thought so!" blazed Loesser, his eyes ragin...</td>
      <td>He snatched an object from his jacket pocket. ...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CHAPTER IV</td>
      <td>Mystery Machine</td>
      <td>Laird Carlin was child of a galactic civilizat...</td>
      <td>The atom-pistol in Loesser's hand and the obvi...</td>
      <td>"Why, what's the matter?" he began, puzzled an...</td>
      <td>He knew later how near he had been to death. A...</td>
      <td>"Loesser, put that gun down!" snapped Jonny.</td>
      <td>Loesser turned violently. "This fellow was spy...</td>
      <td>Harb Land's craggy face darkened ominously.</td>
      <td>"I warned you what might happen," he said hars...</td>
      <td>...</td>
      <td>"He is—one of the best," she said. "And he lik...</td>
      <td>She was, obviously, thinking aloud rather than...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CHAPTER V</td>
      <td>Desperate Play</td>
      <td>The truck wheezed and groaned up the dark old ...</td>
      <td>The house was dark when Marn stopped the truck...</td>
      <td>"I have to take these things back to Jonny," s...</td>
      <td>"Marn, what are your brothers really planning?...</td>
      <td>She twisted uncomfortably. "Jonny told you all...</td>
      <td>She was such a poor liar, she was so oddly app...</td>
      <td>Her small body was firm and warm in his hands ...</td>
      <td>He looked down at her. "You don't mind, do you...</td>
      <td>...</td>
      <td>Carlin shrugged, but he slowly lowered the wea...</td>
      <td>"I can tell you right now that I'll have no pa...</td>
      <td>"Well," Jonny said, with a tired sigh, "we've ...</td>
      <td>Carlin looked a little awkwardly at Marn as he...</td>
      <td>"I'm sorry if I appear ungrateful for your hos...</td>
      <td>"I know," Marn said soberly, and there was no ...</td>
      <td>Out of the darkness behind them spoke a shrill...</td>
      <td>"Well, I'm blamed glad you people quit arguin'...</td>
      <td>Gramp Land stood back there in the dark where ...</td>
      <td>"Sure got tired holdin' this thing aimed at yo...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>CHAPTER VI</td>
      <td>"You Owe a Chance to Earth!"</td>
      <td>Doubts assailed Carlin almost as soon as he re...</td>
      <td>Had he been childish to let Jonny persuade him...</td>
      <td>The recklessness of Earthmen was proverbial. T...</td>
      <td>Carlin chilled. He remembered what had happene...</td>
      <td>It had been the same later at Polaris, and at ...</td>
      <td>Yet he could see, too, how these Earthmen woul...</td>
      <td>Carlin dozed before daybreak, but woke with th...</td>
      <td>"We'll go out and show you our work, as soon a...</td>
      <td>...</td>
      <td>"It's all right for him to keep those pictures...</td>
      <td>Floring turned, bidding a pleasant farewell.</td>
      <td>"I'll be seeing you again soon," he promised.</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>6</th>
      <td>CHAPTER VII</td>
      <td>Last Frontier</td>
      <td>As soon as Floring's ato-car had purred away, ...</td>
      <td>Carlin put into words what was in all their mi...</td>
      <td>"Jonny, you know why he took those pictures! H...</td>
      <td>Jonny nodded. "Yes, of course. Floring has sus...</td>
      <td>"And when word comes back from Canopus, he'll ...</td>
      <td>"I know that," Jonny Land said, as his blue ey...</td>
      <td>Laird Carlin felt a shock of astonishment, but...</td>
      <td>"It's our only chance now—to get away before F...</td>
      <td>...</td>
      <td>"We'll have to take him with us," Jonny said. ...</td>
      <td>A few weeks before, Laird Carlin would have be...</td>
      <td>"Tie him into one of the chairs in the pilot r...</td>
      <td>Harb came plunging out of the ship. "Nobody el...</td>
      <td>By the time Carlin had the unconscious man sec...</td>
      <td>Then, with infinite labor, they swung the mass...</td>
      <td>"Fasten half the frame bolts—they'll hold till...</td>
      <td>Carlin skinned his knuckles in the dark, fumbl...</td>
      <td>"That'll have to hold," said the sweating Jonn...</td>
      <td>None</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CHAPTER VIII</td>
      <td>Solar Struggle</td>
      <td>Oxygenators started throbbing, doors clanged, ...</td>
      <td>"Generators coming on!" sang Loesser's breathl...</td>
      <td>"Stasis on," said Harb rapidly, his fingers bu...</td>
      <td>And the "Phoenix" swept up with a rush from th...</td>
      <td>"Authorization!" yelped a startled voice from ...</td>
      <td>"Authorization already given," Harb Land rappe...</td>
      <td>Crazy, reckless, suicidal, to Carlin seemed th...</td>
      <td>Luna burst up out of the eastern heavens like ...</td>
      <td>...</td>
      <td>Carlin felt like a man in a dream as he sweate...</td>
      <td>"Now!"</td>
      <td>They crowded around the view-plate in the keel...</td>
      <td>"Here she comes!" yelled Loesser.</td>
      <td>A column of flaming vapor was shooting up from...</td>
      <td>But it was rushing up and up toward the hoveri...</td>
      <td>Another salvo of shells went off in space some...</td>
      <td>They heard a deafening roar. That up-sucked st...</td>
      <td>"The kickback's working!" Jonny Land yelled. "...</td>
      <td>None</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CHAPTER IX</td>
      <td>An Earthman Comes Home</td>
      <td>For the moment, none of them paid any attentio...</td>
      <td>Did it seem incredible, as it almost did to Ca...</td>
      <td>"No sign of a whirl yet," Jonny breathed, peer...</td>
      <td>There was no moment of crisis, no clean-cut mo...</td>
      <td>Salvos shook the ship as the Control cruisers ...</td>
      <td>"No whirl yet."</td>
      <td>Jonny Land finally raised his head, looked at ...</td>
      <td>"We've done it," he said, almost unbelievingly...</td>
      <td>...</td>
      <td>Carlin turned and strode rapidly back up the r...</td>
      <td>"I was waiting for you," she said simply. "I k...</td>
      <td>His hands grasped her shoulders as he spoke in...</td>
      <td>"Marn, I couldn't! I thought of Canopus, I tho...</td>
      <td>She came into his arms quietly. "I know. There...</td>
      <td>Carlin held her closely, all tiredness and dou...</td>
      <td>And Earth was close, its ancient quiet night e...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 88 columns</p>
</div>




```python
forgotten_world = forgotten_world.rename(columns={'index':'chapter', 0:'text'}) # the rename method takes a dictionary
forgotten_world
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
      <th>chapter</th>
      <th>text</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>...</th>
      <th>77</th>
      <th>78</th>
      <th>79</th>
      <th>80</th>
      <th>81</th>
      <th>82</th>
      <th>83</th>
      <th>84</th>
      <th>85</th>
      <th>86</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CHAPTER I</td>
      <td>Stranger from the Stars</td>
      <td>Carlin was the only one of the four hundred pa...</td>
      <td>He was bored with the vessel and everyone aboa...</td>
      <td>A blond girl from Altair Four came tripping al...</td>
      <td>The blonde from Altair Four favored the tall d...</td>
      <td>"Oh, Mr, Carlin, the annunciators just said th...</td>
      <td>"Just what is thrilling about it?" Carlin aske...</td>
      <td>The girl was a little dumfounded. "Why, I mean...</td>
      <td>She prattled on, voicing all the appropriate c...</td>
      <td>...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CHAPTER II</td>
      <td>Ancient Town</td>
      <td>Carlin looked with a jaundiced eye on the scen...</td>
      <td>This ancient town called New York was like a m...</td>
      <td>"It's like one of the bird-people's lofts on P...</td>
      <td>Old? Yes. Pitifully old, like a withered belda...</td>
      <td>The spaceport, some distance northward amid lo...</td>
      <td>The "Larkoom" landed softly. Carlin waited wea...</td>
      <td>But for a moment, he was startled by the air h...</td>
      <td>He looked around uncertainly. The tourists wer...</td>
      <td>...</td>
      <td>Marn uttered an apologetic exclamation. "Oh, I...</td>
      <td>She led upstairs. There was no grav-lift, just...</td>
      <td>It was clean, of course, spotlessly so. But it...</td>
      <td>Yet the girl made no apologies for it, seemed ...</td>
      <td>"We'll bring your bags up after dinner," she s...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CHAPTER III</td>
      <td>Old Planet</td>
      <td>When Marn had gone, Carlin lay down wearily on...</td>
      <td>But it wasn't the voyage so much as this world...</td>
      <td>The sound of an angry voice came up dimly thro...</td>
      <td>"—if Control Operations finds out what we're d...</td>
      <td>There was a murmur of lower voices, and then t...</td>
      <td>What were these Earthmen doing that they were ...</td>
      <td>When Carlin went down to dinner, he expected o...</td>
      <td>Carlin stared dismayedly at the food set befor...</td>
      <td>...</td>
      <td>Carlin recognized the broad red face, angry ey...</td>
      <td>"What are you doing here?" Loesser demanded ha...</td>
      <td>Carlin was bewildered by his vehemence. "Why, ...</td>
      <td>"I thought so!" blazed Loesser, his eyes ragin...</td>
      <td>He snatched an object from his jacket pocket. ...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CHAPTER IV</td>
      <td>Mystery Machine</td>
      <td>Laird Carlin was child of a galactic civilizat...</td>
      <td>The atom-pistol in Loesser's hand and the obvi...</td>
      <td>"Why, what's the matter?" he began, puzzled an...</td>
      <td>He knew later how near he had been to death. A...</td>
      <td>"Loesser, put that gun down!" snapped Jonny.</td>
      <td>Loesser turned violently. "This fellow was spy...</td>
      <td>Harb Land's craggy face darkened ominously.</td>
      <td>"I warned you what might happen," he said hars...</td>
      <td>...</td>
      <td>"He is—one of the best," she said. "And he lik...</td>
      <td>She was, obviously, thinking aloud rather than...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CHAPTER V</td>
      <td>Desperate Play</td>
      <td>The truck wheezed and groaned up the dark old ...</td>
      <td>The house was dark when Marn stopped the truck...</td>
      <td>"I have to take these things back to Jonny," s...</td>
      <td>"Marn, what are your brothers really planning?...</td>
      <td>She twisted uncomfortably. "Jonny told you all...</td>
      <td>She was such a poor liar, she was so oddly app...</td>
      <td>Her small body was firm and warm in his hands ...</td>
      <td>He looked down at her. "You don't mind, do you...</td>
      <td>...</td>
      <td>Carlin shrugged, but he slowly lowered the wea...</td>
      <td>"I can tell you right now that I'll have no pa...</td>
      <td>"Well," Jonny said, with a tired sigh, "we've ...</td>
      <td>Carlin looked a little awkwardly at Marn as he...</td>
      <td>"I'm sorry if I appear ungrateful for your hos...</td>
      <td>"I know," Marn said soberly, and there was no ...</td>
      <td>Out of the darkness behind them spoke a shrill...</td>
      <td>"Well, I'm blamed glad you people quit arguin'...</td>
      <td>Gramp Land stood back there in the dark where ...</td>
      <td>"Sure got tired holdin' this thing aimed at yo...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>CHAPTER VI</td>
      <td>"You Owe a Chance to Earth!"</td>
      <td>Doubts assailed Carlin almost as soon as he re...</td>
      <td>Had he been childish to let Jonny persuade him...</td>
      <td>The recklessness of Earthmen was proverbial. T...</td>
      <td>Carlin chilled. He remembered what had happene...</td>
      <td>It had been the same later at Polaris, and at ...</td>
      <td>Yet he could see, too, how these Earthmen woul...</td>
      <td>Carlin dozed before daybreak, but woke with th...</td>
      <td>"We'll go out and show you our work, as soon a...</td>
      <td>...</td>
      <td>"It's all right for him to keep those pictures...</td>
      <td>Floring turned, bidding a pleasant farewell.</td>
      <td>"I'll be seeing you again soon," he promised.</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>6</th>
      <td>CHAPTER VII</td>
      <td>Last Frontier</td>
      <td>As soon as Floring's ato-car had purred away, ...</td>
      <td>Carlin put into words what was in all their mi...</td>
      <td>"Jonny, you know why he took those pictures! H...</td>
      <td>Jonny nodded. "Yes, of course. Floring has sus...</td>
      <td>"And when word comes back from Canopus, he'll ...</td>
      <td>"I know that," Jonny Land said, as his blue ey...</td>
      <td>Laird Carlin felt a shock of astonishment, but...</td>
      <td>"It's our only chance now—to get away before F...</td>
      <td>...</td>
      <td>"We'll have to take him with us," Jonny said. ...</td>
      <td>A few weeks before, Laird Carlin would have be...</td>
      <td>"Tie him into one of the chairs in the pilot r...</td>
      <td>Harb came plunging out of the ship. "Nobody el...</td>
      <td>By the time Carlin had the unconscious man sec...</td>
      <td>Then, with infinite labor, they swung the mass...</td>
      <td>"Fasten half the frame bolts—they'll hold till...</td>
      <td>Carlin skinned his knuckles in the dark, fumbl...</td>
      <td>"That'll have to hold," said the sweating Jonn...</td>
      <td>None</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CHAPTER VIII</td>
      <td>Solar Struggle</td>
      <td>Oxygenators started throbbing, doors clanged, ...</td>
      <td>"Generators coming on!" sang Loesser's breathl...</td>
      <td>"Stasis on," said Harb rapidly, his fingers bu...</td>
      <td>And the "Phoenix" swept up with a rush from th...</td>
      <td>"Authorization!" yelped a startled voice from ...</td>
      <td>"Authorization already given," Harb Land rappe...</td>
      <td>Crazy, reckless, suicidal, to Carlin seemed th...</td>
      <td>Luna burst up out of the eastern heavens like ...</td>
      <td>...</td>
      <td>Carlin felt like a man in a dream as he sweate...</td>
      <td>"Now!"</td>
      <td>They crowded around the view-plate in the keel...</td>
      <td>"Here she comes!" yelled Loesser.</td>
      <td>A column of flaming vapor was shooting up from...</td>
      <td>But it was rushing up and up toward the hoveri...</td>
      <td>Another salvo of shells went off in space some...</td>
      <td>They heard a deafening roar. That up-sucked st...</td>
      <td>"The kickback's working!" Jonny Land yelled. "...</td>
      <td>None</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CHAPTER IX</td>
      <td>An Earthman Comes Home</td>
      <td>For the moment, none of them paid any attentio...</td>
      <td>Did it seem incredible, as it almost did to Ca...</td>
      <td>"No sign of a whirl yet," Jonny breathed, peer...</td>
      <td>There was no moment of crisis, no clean-cut mo...</td>
      <td>Salvos shook the ship as the Control cruisers ...</td>
      <td>"No whirl yet."</td>
      <td>Jonny Land finally raised his head, looked at ...</td>
      <td>"We've done it," he said, almost unbelievingly...</td>
      <td>...</td>
      <td>Carlin turned and strode rapidly back up the r...</td>
      <td>"I was waiting for you," she said simply. "I k...</td>
      <td>His hands grasped her shoulders as he spoke in...</td>
      <td>"Marn, I couldn't! I thought of Canopus, I tho...</td>
      <td>She came into his arms quietly. "I know. There...</td>
      <td>Carlin held her closely, all tiredness and dou...</td>
      <td>And Earth was close, its ancient quiet night e...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 88 columns</p>
</div>




```python
forgotten_world.to_csv('Forgotten_World.csv',index=False)
```


```python

```


```python

```


```python

```