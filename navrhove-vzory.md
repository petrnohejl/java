Návrhové vzory
==============


Zásady OOP
==========

**Rozhraní** je množina informací, které o sobě daná entita (třída, enum, interface, metoda) zveřejní. Touto informací může být signatura nebo kontrakt. Publikované rozhraní by mělo být nedotknutelné. Zastaralé entity se označují jako deprecated.

**Signatura** (hlavička, deklarace) je souhrn informací zpracovatelných překladačem. Signatura dat představuje název a typ. Signatura metody představuje název, typ návratové hodnoty, typy parametrů, výjimky a další atributy. Signatura datových typů (class, enum, interface) představuje název typu, název předka, implementovaných rozhraní a signatury všech jeho členů.

**Kontrakt** je souhrn pravidel, které je nutno dodržet, avšak nelze je zkontrolovat překladačem. Např. přípustné hodnoty parametrů metody. Kontrakt je deklarován v dokumentaci.

**Implementace** je souhrn informací, které se třída snaží maximálně utajit.

Programovat proti rozhraní
--------------------------

Proměnné nemají být deklarovány jako instance konkrétních tříd, ale jako instance nějakého datového typu, jenž není vázán na konkrétní implementaci - interface nebo abstraktní třída. Například `List<Product> list = new ArrayList<>();` a nikoliv `ArrayList<Product> list = new ArrayList<>();`. List je interface a ArrayList je třída.

Je vhodné vnější rozhraní programu (API) postavit na konstrukcích interface, protože umožní lépe skrýt implementaci.

Důsledné skrytí implementace
----------------------------

Spolupracující programy by neměly mít možnost zjistit/ovlivnit, jak objekt dělá, že umí to, co umí. Neměli bychom zveřejňovat pomocné metody.

Zapouzdření (encapsulation) a odpoutání částí kódu, které by se mohly měnit
---------------------------------------------------------------------------

Dobře zapouzdřený kód je možné odpoutat od zbytku kódu a měnit, aniž by to ovlivnilo funkčnost spolupracujících programů. Odpoutání kódu a odstranění přímých vazeb lze provést pomocí rozhraní.

Přednost skládání před dědičností
---------------------------------

Dědičnost nedovoluje zcela skrýt implementační detaily a narušuje tak správné zapouzdření. Ke správné implementaci potomka je často nutné znát informace o způsobu implementace předka.

Například třída `UniverzalniVystup`. Pokud bych definoval pro každý druh výstupu speciálního potomka dané třídy, měl bych svázané ruce, protože by potomci nemohly být v jiné dědické hierarchii - např. hierarchii proudů `OutputStream`. Pokud definuji výstupní objekt jako instanci nějakého rozhraní, mám volnější ruce, jak jeho třídu definovat.

Dědičnost se používá tehdy, jsou-li instance potomka speciálním druhem instancí předka. Liskov Substitution Principle: instance podtypu se musí dát použít všude, kde lze použít instanci nadtypu. Kde lze použít instanci předka, musí být možné použít i instanci potomka. Špatný příklad: obdelník je potomkem bodu. Body mohou tvořit i trojúhelník a substituce tedy nedává smysl.

Špatné použití dědičnosti: potomek dědí třídu jen proto, aby mohl zdědit část implementace předka. Špatný příklad: třída _Letadlo_ je potomkem třídy _Křídlo_. Pak nelze zařídit, aby bylo potomkem dvou křídel.

Soudržnost (cohesion)
---------------------

Každý balíček, třída, metoda by měly mít na starosti jen jeden hlavní úkol. Správně navržená třída by měla mít krátké metody. Krátké by měly být i definice tříd a počty tříd v balíčku.

Špatný příklad: třída _Obdélník_ v grafickém programu zajišťuje vykreslování tvaru a v jiném programu zajišťuje výpočty vlastností tvaru (obvod, obsah). Soudržnost obou programů je narušena, protože metody pro výpočet vlastností jsou závislé na změnách metod pro vykreslování.

Návrh řízený odpovědnostmi (responsibility-driven design)
---------------------------------------------------------

Jeden úkol by měla řešit pouze jedna entita. Při úpravách funkcionality je pak nutné upravit pouze danou entitu a není třeba zkoumat celý kód.

Minimální vzájemná provázanost (coupling)
-----------------------------------------

Je vhodné minimalizovat počet vazeb mezi entitami.

Vyhýbat se duplicitám v kódu
----------------------------

Duplicitní (zkopírovaný) kód může být náchylný k chybám. Vhodné je též používat pojmenované konstanty namísto literálů.

Nepodřizovat návrh snahám o maximální efektivitu
------------------------------------------------

Není vhodné optimalizovat kód předčasně. Průměrný program tráví 80% svého života ve 20% svého kódu. Optimalizace některých částí kódu může být zbytečná. Důležité je, aby šel program dobře modifikovat. Na detaily je vhodné se soustředit, až když je celek navržen a odladěn. Optimalizovat je vhodné až tehdy, kdy skutečně vím, která část programu je neefektivní.


Simple Factory Method
=====================

Definuje statickou metodu nahrazující konstruktor. Používá se tam, kde potřebujeme získat odkaz na objekt, ale přímé použití konstruktoru není z nejrůznějších příčin optimálním řešením.

Tento vzor se hodí, pokud potřebujeme vytváření nových instancí nějakým způsobem hlídat, nebo provádět akce, které nám nedovolí konstruktor. Tovární metoda může vytvořit novou instanci, nebo vrátit odkaz na již existující instanci.

Například třída _Integer_ ze standardní knihovny má předdefinované instance pro hodnoty -128 až 127. Pokud použiju konstruktor, vždy vytvořím novou instanci. Pokud vžak použiju tovární metodu `valueOf()`, získám pro malé hodnoty odkaz na již existující instanci. Je to rychlejší a šetřím paměť.

Charakteristika Simple Factory Method a rozdíly oproti konstruktoru:

- Statická metoda, která vrací instanci zadané třídy (včetně instancí potomků)
- Vytváří novou instanci, nebo vrací odkaz na již existující
- Může vracet instance různých typů (potomky)
- Větší svoboda v definici (volání přetížené verze konstruktoru musí být prvním příkazem těla konstruktoru)
- Metoda může mít libovolné jméno

Konvence pro názvy továrních metod: 

- getInstance
- valueOf
- getFooBar

```java
public abstract class Human
{
	private static int index = 0;

	public static Human getHuman()
	{
		switch(index++ % 3)
		{
			case 0: return new LazyHuman();
			case 1: return new BriskHuman();
			case 2: return new WorkoholicHuman();
			default: throw new RuntimeException("Invalid maximum");
		}
	}

	public abstract void wakeUp();
	public abstract void work();
	public abstract void sleep();

	private static class LazyHuman extends Human
	{
		public void wakeUp() { System.out.println("Waking up slowly"); }
		public void work() { System.out.println("Working slowly"); }
		public void sleep() { System.out.println("Sleeping deeply"); }
	}

	private static class BriskHuman extends Human
	{
		public void wakeUp() { System.out.println("Waking up briskly"); }
		public void work() { System.out.println("Working briskly"); }
		public void sleep() { System.out.println("Sleeping normally"); }
	}

	private static class WorkoholicHuman extends Human
	{
		public void wakeUp() { System.out.println("Waking up quickly"); }
		public void work() { System.out.println("Working a lot"); }
		public void sleep() { System.out.println("Sleeping shortly"); }
	}
}
```