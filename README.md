# Ceny nabíjení elektromobilů

**Aplikace: https://comsator.github.io/ACDC/**

Webová aplikace, která ukazuje ceny AC a DC nabíjení u PRE, ČEZ, E.ON, innogy, Ionity, Tesly a Shell Recharge. Běží samostatně na GitHub Pages a na iPhonu ji lze přidat na plochu jako aplikaci.

## Soubory

| Soubor | K čemu je |
|---|---|
| `index.html` | celá aplikace (vzhled i logika) |
| `ceny.json` | ceníky; jediný soubor, který se při změně cen upravuje |
| `manifest.webmanifest`, `icon-*.png`, `apple-touch-icon.png` | název a ikona aplikace na ploše |
| `sw.js` | offline režim: bez připojení ukáže naposledy stažené ceny |
| `.nojekyll` | říká GitHubu, ať soubory zveřejní beze změn |

## Zveřejnění na GitHub Pages

1. Na github.com založte nový **veřejný** repozitář, například `ceny-nabijeni` (GitHub Pages jsou u bezplatného účtu dostupné jen pro veřejné repozitáře).
2. V repozitáři zvolte **Add file → Upload files**, přetáhněte všechny soubory z této složky a potvrďte **Commit changes**. Soubor `.nojekyll` začíná tečkou a ve Finderu nebo Průzkumníku může být skrytý; pokud ho nenahrajete, aplikace funguje i bez něj.
3. Otevřete **Settings → Pages**, v části *Build and deployment* nastavte *Source: Deploy from a branch*, větev `main`, složku `/ (root)` a uložte.
4. Za minutu až dvě je aplikace na adrese https://comsator.github.io/ACDC/.

## Přidání na plochu iPhonu

1. Adresu otevřete v **Safari**.
2. Klepněte na **Sdílet** a zvolte **Přidat na plochu**.
3. Aplikace se pak otevírá na celou obrazovku pod ikonou s bleskem.

## Aktualizace cen

Aplikace si při každém otevření (a pak každých 30 minut) stáhne `ceny.json`. Stačí tedy upravit tento soubor v repozitáři, aplikaci není třeba znovu instalovat.

- Ceny jsou v Kč/kWh včetně DPH.
- `updatedAt` a `verifiedAt` jsou data ve tvaru `RRRR-MM-DD`.
- Každý provozovatel má seznam `tariffs`; tarif má `tier` (`adhoc` = bez registrace, `free` = registrace bez paušálu, `paid` = s paušálem), `fee` (paušál v Kč) a `rates`.
- Sazba (`rates`) má `kind` (`AC` nebo `DC`), u DC pásmo výkonu `minKw`/`maxKw`, cenu `p`, případně horní mez `pMax`, příznak `from` (cena „od“) a časová okna `tod` pro denní a noční sazbu (`from`/`to` jsou hodiny českého času).
- Kde cena není známá, je místo `p` text v poli `na`.

Rozhodující je vždy cena v aplikaci provozovatele nebo na stojanu.
