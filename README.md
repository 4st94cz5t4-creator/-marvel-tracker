# -marvel-tracker
from openpyxl.utils import get_column_letter
from textwrap import dedent
items=[("X-Men: First Class",132),("X-Men Origins: Wolverine",107),("X-Men",104),("X2",134),("X-Men: The Last Stand",104),("The Wolverine",126),("X-Men: Days of Future Past",132),("X-Men: Apocalypse",144),("Dark Phoenix",114),("Logan",137),("Deadpool",108),("Deadpool 2",119),("Captain America: The First Avenger",124),("Agent Carter S1",320),("Agent Carter S2",420),("Captain Marvel",124),("Iron Man",126),("Iron Man 2",124),("The Incredible Hulk",112),("Thor",115),("The Avengers",143),("Iron Man 3",130),("Thor: The Dark World",112),("Captain America: The Winter Soldier",136),("Guardians of the Galaxy",121),("Guardians Vol. 2",136),("Avengers: Age of Ultron",141),("Ant-Man",117),("Captain America: Civil War",147),("Black Widow",134),("Black Panther",134),("Spider-Man: Homecoming",133),("Doctor Strange",115),("Thor: Ragnarok",130),("Ant-Man and the Wasp",118),("Avengers: Infinity War",149),("Avengers: Endgame",181),("Loki S1",280),("What If...? S1",290),("WandaVision",350),("The Falcon and the Winter Soldier",300),("Shang-Chi",132),("Eternals",157),("Spider-Man",121),("Spider-Man 2",127),("Spider-Man 3",139),("The Amazing Spider-Man",136),("The Amazing Spider-Man 2",142),("Spider-Man: Far From Home",129),("Spider-Man: No Way Home",148),("Hawkeye",300),("Moon Knight",290),("Ms. Marvel",270),("Doctor Strange in the Multiverse of Madness",126),("Thor: Love and Thunder",119),("She-Hulk",315),("Black Panther: Wakanda Forever",161),("Ant-Man and the Wasp: Quantumania",125),("Secret Invasion",260),("The Marvels",105),("Loki S2",300),("Echo",250),("Agatha All Along",320),("Deadpool & Wolverine",128),("Daredevil: Born Again S1",540),("Captain America: Brave New World",118),("Ironheart",270),("Thunderbolts*",126),("The Fantastic Four: First Steps",130)]
html=["<html><head><meta charset='utf-8'><title>Marvel Tracker</title></head><body><h1>Marvel Tracker</h1><div id='stats'></div><progress id='p' max='100' value='0' style='width:100%'></progress><hr>"]
for i,(n,m) in enumerate(items):
    html.append(f"<label><input type='checkbox' id='c{i}'> {n} ({m} min)</label><br>")
html.append("<script>const items=%s;"%str(items))
html.append(dedent("""
function upd(){
let seen=0,total=0,cnt=0;
items.forEach((x,i)=>{total+=x[1];let c=document.getElementById('c'+i);if(localStorage['m'+i]=='1'){c.checked=true;} c.onchange=()=>{localStorage['m'+i]=c.checked?'1':'0';upd();}; if(c.checked){seen+=x[1];cnt++;}});
let rem=total-seen;
document.getElementById('stats').innerHTML=`Set ${cnt}/${items.length}<br>Set: ${(seen/60).toFixed(1)} t<br>Mangler: ${(rem/60).toFixed(1)} t`;
document.getElementById('p').value=seen/total*100;
}
upd();
</script></body></html>"""))
path="/mnt/data/Marvel_Tracker_Pro.html"
open(path,"w",encoding="utf8").write("".join(html))
print(path)
