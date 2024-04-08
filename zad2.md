# Zadanie 1

- A - rodzeństwo
- B - kuzynostwo
- C - swatowie
- D - x jest przybranym dzieckiem y
- E - przyrodnie rodzeństwo
- F - szwagier/szwagierka
- G - x jest wujkiem/ciocią y

# Zadanie 2

rodzic(antoni, rafal).  
rodzic(antoni, maria).  
rodzic(antoni, marek).  
rodzic(wieslawa, rafal).  
rodzic(magdalena, maria).  
rodzic(wieslawa, marek).  
rodzic(marek, maciek).  
rodzic(eugeniusz, piotr).  
rodzic(wieslaw, lukasz).  
rodzic(lukasz, maja).  
rodzic(lukasz, oliwia).  
rodzic(maja, oskar).  
rodzic(maja, monika).  
rodzic(pawel, oskar).  
rodzic(oliwia, krystian).  
rodzic(aleksander, krystian).  
rodzic(tomasz, monika).  
rodzic(oskar, ela).  

mezczyzna(antoni).  
mezczyzna(rafal).  
mezczyzna(eugeniusz).  
mezczyzna(piotr).  
mezczyzna(wieslaw).  
mezczyzna(lukasz).  
mezczyzna(oskar).  
mezczyzna(tomasz).  
mezczyzna(marek).  
mezczyzna(krystian).  
mezczyzna(pawel).  
mezczyzna(aleksander).  
mezczyzna(maciek).  

osoba(X) :- rodzic(X, _).  
osoba(X) :- rodzic(_, X).  

kobieta(X) :- osoba(X), \+ mezczyzna(X).  
ojciec(X, Y) :- mezczyzna(X), rodzic(X, Y).  
matka(X, Y) :- kobieta(X), rodzic(X, Y).  
corka(X, Y) :- kobieta(X), rodzic(Y, X).  
brat_rodzony(X, Y) :- mezczyzna(X), ojciec(O, X), ojciec(O, Y), matka(M, X), matka(M, Y), X \= Y.  
brat_przyrodni(X, Y) :- mezczyzna(X), rodzic(Z, X), rodzic(Z, Y), \+ brat_rodzony(X, Y), X \= Y.  
kuzyn(X, Y) :- mezczyzna(X), rodzic(Z, X), rodzic(W, Y), rodzic(R, Z), rodzic(R, W), X \= Y.  
dziadek_od_ojca(X, Y) :- ojciec(X, Z), mezczyzna(Z), rodzic(Z, Y).  
dziadek_od_matki(X, Y) :- ojciec(X, Z), kobieta(Z), rodzic(Z, Y).  
dziadek(X, Y) :- ojciec(X, Z), rodzic(Z, Y).  
babcia(X, Y) :- matka(X, Z), rodzic(Z, Y).  
wnuczka(X, Y) :- rodzic(Y, Z), rodzic(Z, X), kobieta(X).  
przodek_do2pokolenia(X, Y) :- rodzic(X, Z), rodzic(Z, Y).  
przodek_do3pokolenia(X, Y) :- rodzic(X, Z), przodek_do2pokolenia(Z, Y).  
