DOKUMENTACE PRO SKYMINE RESOUCEPACK

-------------------------------------------------------------------------------------------------------------------------------

Struktura RP, je následující, v ASSETS jsou pojmenované složky, třídící RP na různé kategorie

nová kategorie lze přidat přes přidání následujícího řádku do assets/Minecraft/atlases do blocks.json a item.json


        {"type": "directory", "source": "<název_adresáře>",   "prefix": "<název_adresáře>/"},

pro přidání nového itemu se určí kategorie, přidá se to do ní, následně se v assets/Minecraft/items podle typu itemu co se přidává 

pokud jde o figurku/čepici, tak se to přidává do carved_pumpkin.json, pokud jde o item/jídlo přidává se to na structure_block.json

nový item se přidává ve formátu


      {"when": "<ID_itemu>",		"model": {"type": "model","model": "<název_adresáře>:<cesta_modelu>"}},


(případně pokud je model v podsložce tak to je ve formátu <složka_v_models/název_modelu.json>)


model bude mít cestu k textuře ve formátu

"<název_adresáře>:<cesta_k_textuře>"

-------------------------------------------------------------------------------------------------------------------------------

itemy se givují následujícím způsobem

pouze samotný otexturovaný item:
give @p minecraft:<structure_block/carved_pumpkin>[minecraft:custom_model_data={strings:["<ID_itemu>"]}]



givování jídla:

/give @p structure_block[food={nutrition:2,saturation:1},consumable={consume_seconds:1},max_stack_size=128,custom_model_data={strings:["hranolky"]}]

vysvětlení komponentů:

consumable={consume_seconds:1} //// jak dlouho se budou jíst, default 1.6(sec)
food={nutrition:2,saturation:1} //// nutrition jsou kusy masa, 1 = 0.5 paličky, saturation = saturace, taky 1 = 0.5 saturace
max_stack_size=99 //// do kolika se budou stackovat itemy, rozshah 1 - 99
custom_model_data={strings:["hranolky"]} //// slovo v [" "] uršuje model itemu

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

givogání zbraní:
give @p structure_block[attribute_modifiers=[{type:attack_damage,amount:10,slot:mainhand,id:"dmg",operation:add_value},{type:attack_speed,amount:-2,slot:mainhand,id:"speed",operation:add_value}],custom_model_data={strings:["banhammer"]}]

vysvětlení komponentů:

attribute_modifiers=[{type:attack_damage,amount:10,slot:mainhand,id:"dmg",operation:add_value},{type:attack_speed,amount:-2,slot:mainhand,id:"speed",operation:add_value}]

//// atribute modifiers jsou kinda složitý, přes ně jde nastavit hromadu věcí, víc atributů se dává do stejný závorky, 
každý segment vypadá:
attribute_modifiers=[] základní segment
[{atribut_1},{atribut_2}]

{type:<typ_atributu>,amount:<množství_v_int>,slot:<naztev_slotu>,operation:<typ_operace>}


<typ_atributu> /// věci jako attack_damage (velikost dmg), attack_speed (-3 je kinda jako sekera, -2 je rychlejší než meč), a mnohem víc atributů který jde najít na webu

<množství_v_int> /// síla atributu, jde sem napsat jakýkoliv celý číslo, stránka tvrdí 0-30


<naztev_slotu>  /// kdy se bude atribut dít, např, mainhand pro vybavený v ruce, offhand pro secondary slot, armor kdekoliv na armor slotu, nebo specifikovanej armor slot jako head, chest, legs, feet

id je naprosto random jméno, idk k čemu to je, myslim že tim jde sdílet stejnej mezi několika itemy najednou, ale nejsem si jistej

<typ_operace> /// add_value/add_multiplied_base/add_multiplied_total může být jedna z těhlech, jedna jen přidá value, druhá násobí base value, třetí se stackuje s existujícíma effektama, jako např speed potion + třetí bude rychlejší než speed + 2.


///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

givování itemu se jménem a lorem:

give @p structure_block[lore=[[{"text":"LORE","italic":false,"color":"dark_red"}]],item_name=[{"text":"Název","italic":false}],rarity=uncommon]

vysvětlení komponentů:

lore=[[{"text":"LORE","italic":false,"color":"dark_red"}]] //// nastaví barvu lore, pro více řádků lze udělat:
lore=[[{"text":"LORE","bold":true,"italic":false,"color":"dark_red"}],["dwadwadwa"]]

každý [{}] je jeden řádek, který může mít vlastní nastavení, italic je default, proto se musí vypnout, pokud chcem normální, nebo upravený font
"text":"LORE" //// věci v "" značí text co je napsaný na řádku
"color":"dark_red" //// nastaví mc přednastavený barvy
"color":"#c03939" //// umožní jakoukoliv hex barvu

item_name=[{"text":"Název","italic":false,"color":"dark_gray"}] //// jméno itemu

rarity=uncommon //// pokud nenastavíme barvu itemu, tak můžem použít mc default barvy itemu, jako 
- common pro normální itemy, 
- uncommon pro žlutý jako music disc, 
- rare pro modrý text jako ench knížka,
- epic pro fialový jako command block

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

!!! POTŘEBUJE DATAPACK POKUD CHCEM CUSTOM SONGY!!!

givování MUSIC DISCŮ:

/give @p minecraft:structure_block[jukebox_playable="minecraft:pigstep",custom_model_data={strings:["music_disc_ava"]}]


jukebox_playable="minecraft:pigstep" //// pokud nemáme datapack, tak sem můžem dát vanilla hudbu, nebo dokonce i zvuky

pokud máme datapack, tak v něm nastavíme délku songy, titulky atd, a tady na to referencujem přes cestu, myslim že minecraft:<custom songa>, protože tak to je nsatavený, ale not sure


