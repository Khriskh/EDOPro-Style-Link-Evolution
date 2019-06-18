## User Manual

### Keyboard shortcuts:
* ESC: Minimize the window.
* A: Holding down this button will let the system stop at every timing.
* S: Holding down this button will let the system skip every timing.
* R: Fix the font error.
* F1~F4: Show the cards in your grave, banished zone, extra deck, xyz materials.
* F5~F8: Show the cards in your opponent's grave, banished zone, extra deck, xyz materials.

### Colour in card list:
#### Background: 
* White = your card, Grey = your opponent's card  

#### Text: 
Cards in deck, extra deck and banished zone: 
* Black = face-up, Blue = face-down

Xyz materials:
* Black = default, Blue = the owner of the Xyz Material is different from its controller

### Sequence:
* Main Monster Zone: 0~4, starting from the left hand side.
* Extra Monster Zone: 5~6, starting from the left hand side.
* Spell & Trap Zone: 0~4, starting from the left hand side.
* Field Zone: 5
* Pendulum Zone: 0~1, starting from the left hand side (when used with LOCATION_PZONE).
* separated pendulum zones: 6~7
* joined with szone: 0, 4
* joined with szone + speed duel: 1, 3
* The others: 0~n, starting from the bottom.

### Deck edit page:
* All numeric textboxes: They support >, =, <, >=, <= signs.
* Card name: Search card names and texts by default, $foo will only search foo in card names, and @foo will search cards of "foo" archetype(due to translation, card name contains "foo" does not mean that card is "foo" card).

### Command-line options:
* -e foo.cdb:
Load foo.cdb as external database. Multi parameters are supported.
* -efoo.cdb:
Load foo.cdb as the extra database. (depreciated)
* -n Player:
Enter `Player` as nickname.
* -h 127.0.0.1:
Enter `127.0.0.1` to host ip textbox.
* -p 7911:
Enter `7911` to host port textbox.
* -w 123456:
Enter `123456` to host password textbox.
* -k:
Do not exit ygopro automatically when returning from any mode opened by one of the following parameters.
* -j:
Automatic join host. Use the host info in system.conf or provided by `-h` `-p` etc.
* -d [filename]:
Automatic open deck edit mode. If `filename` is presented, the file will opened. Files with full path are supported. If the file is in correct folder of ygopro, you can use filename instead. The same below.
* -r [filename]:
Automatic open replay mode and open `filename` .
* -s [filename]:
Automatic open single mode and open `filename` .


### Directories:
* pics: .jpg card images(177*254).
* pics\thumbnail: .jpg thumbnail images(44*64).
* script: .lua script files.
* textures: Other image files.
* deck: .ydk deck files.
* replay: .yrp and .yrpX replay files.
* expansions: extra databases, pics, pics\thumbnail, script, strings.conf
