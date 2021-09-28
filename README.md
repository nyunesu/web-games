# How to make money with short web games

Hello! A bit of context, I'm Felipe (nyunesu), and I made a living in 2019 out of web games. Here I'll teach you how I did that and how you can do it to.



## What this isn't about

First of all, let me clarify what this isn't about:

- .io games
- ads
- multiplayer
- large games

Here I'll mention what I have experience with so I can guide you through the path I made, and hopefully that will be useful for you.



## Licensing

Licensing is selling the rights of a website to host your game, usually comes in form of a flat fee.

There are two types of licensing: exclusive and non-exclusive.

As the name says one allows you to sell and monetize your games with other websites while the other doesn't. Sometimes the exclusive licensing is referred to as Sponsorship.



## The right kind of games

There's no "right" or "wrong" in here, I'll provide the information I have and the way that I think you can benefit the most from it. Please don't take anything that I say for granted, try it and adapt in a way that will work better for you.

I've reached out to **Cool Math Games** and **Armor Games** and asked them directly about their interests.

### Expectations

- Be clear how to play
  *Write it in the e-mail or even inside the game -- This should be clear to the curator and also the player*
- Let them know if there are any strategies that will make the game more enjoyable
  *Also let them know before they play it*
- Shouldn't be too difficult in the first two minutes
  *It's okay to ramp up the difficulty later on, but at least at the start it shouldn't be too challenging*

### Specifics

One more time, this is just to maximize your revenue from the websites I will list, some of them might be look for some specifics while other doesn't care.  Those tips here are to maximize your reach among all available licensors out there.

- PC-First games
  *Think of your game controls for PC players before anything else, it's okay to port your controls to reach a mobile later, but they shouldn't be your primary target*
- Mid-Hardcore games
  *It doesn't mean that they don't have interest in soft core or hypercasual experiences, it's just that it's not their focus*
- Skill-based gameplay
  *Look for something that exercises the player's brain in some sort of level, strategic-thinking, hand-eye coordination, problem-solving and so on...*
- Uniqueness
  *Having a clone of a game there is already in their website won't get you anywhere. Make sure if your game has a commonly used mechanic, you have something that tell apart from the other games*
- Universe
  *Spend some time thinking about your game's universe, even if there are no text or dialog try to come up with an interesting looking character or setting. The players will fill in the blanks.*
- Ending
  *If your game has an end, make it rewarding or at least surprising, completing things is awesome, so congratulate the player for that.*
- SFW & Violence
  *Take it easy on the amount of violence, and also make sure you game stays SFW.*



## Pitching

**The first price you negotiate with a licensor will set your cost as a developer.**

This is true for you and for them. It'll be hard for them to lower it, as you can say you sold the other games for X and you want the same. It will also be hard for you to increase - unless the games are substantially different - since it's likely that they'll use the same argument with you.

When negotiating with Addicting Games for the first time, our conversation was similar to this:

```
Me: Hey, would be interested in this game for $900?
AG: Sorry, we only pay $300 for those type of games
Me: Oh, that's unfortunate, even if I lower it down to $700?
AG: I can raise the offer for you to $400
Me: $600?
AG: Let's me in the middle, $500!
Me: Deal!
```

I sent two extra emails for $200, sounds like a great deal to me. More than ever, this was the first negotiation, that means that all my other games were sold for $500, I sold them 4 games so that means I got $800 for 2 emails. That's how important your first negotiation is.

### How to Pitch

It's not that complicated, all you need is a clear description of your game, a web build that includes and the things mentioned above in **[Expectations]**.

Here's an example of how a first pitching email looks like:

```
To: person.or.company@company.com
Subject: Game Opportunity - [Game Name]

Hi [Person or Company],

I've made this new game called [Game Name] and I'd like to know if you'd be interested in bringing this to your platform.

It's a [Game Genere] in [Context] where you [Something unique about the game].

[--Embeded GIF--]

You can play it here:
[Web build URL]

I'd like to know if you'd interested in a [type of licensing you're looking for] deal.

(-- Optional START --)
I've estimated around $XXX for this game's non-exclusve license. 
(-- Optional END --)

Please let me know if that would be possible.

Best regards,
[Your Name]
```

If you prefer to hear their offer first, it's up to you. As long as you're not rude or demanding it's okay to offer the price you think it's fair (maybe a bit above) and then haggle for a bit. The worst answer you're going to get is that the price is too high or out of their budget.

You can also ask them afterwards if they would be interested in exclusivity or paying more for the game to be release in their website first, some sites do that.



## Piracy

It's pretty easy to pirate a game in the web, so you should at least take precautions of shady websites hosting your game without rights to do it.

All I can provide to you is a Unity script for anti piracy, since that's all I have, but I'm pretty sure you can find more out there.
You should not forget to import my "External.jslib" file from https://github.com/nyunesu/PNLib/blob/main/Plugins/External.jslib in your project in order to run my anti piracy script fine.

```cs
using System.Collections;
using System.Collections.Generic;
using System.Runtime.InteropServices;
using System.Text;
using System.Linq;
using UnityEngine;

public class AntiPiracy : MonoBehaviour
{
	[SerializeField]
	private string[] allowedHosts =
	{
		"itch.io",
		"newgrounds.com",
		"ungrounded.net",
		"kongregate.com",
		"konggames.com",
		"itch.zone",
		"v6p9d9t4.ssl.hwcdn.net",
		"file://",
		"localhost",
		"127.0.0.1",
	};

	private const string RedirectURL = "https://i.giphy.com/media/lgcUUCXgC8mEo/giphy.webp";

	private void Start()
	{
		if (!Application.isEditor)
			ValidateURL();
	}

	[DllImport("__Internal")]
	private static extern void ExternalEval(string str);

	private void ValidateURL()
	{
		ValidateURLWithJavaScript();

		if (IsValidURL(allowedHosts) == false)
			Redirect();
	}

	private static void Redirect()
	{
		Application.OpenURL(RedirectURL);
	}

	private static bool IsValidURL(IEnumerable<string> urls)
	{
		return urls.Any(url => Application.absoluteURL.ToLower().Contains(url));
	}

	private static string CompileHosts(IReadOnlyList<string> allowedUrLs)
	{
		StringBuilder urls = new StringBuilder();

		for (int i = 0; i < allowedUrLs.Count; i++)
		{
			urls.Append("(document.location.host.includes('");
			string url = allowedUrLs[i];

			if (url.IndexOf("http://", StringComparison.Ordinal) == 0)
				url = url.Substring(7);
			else if (url.IndexOf("https://", StringComparison.Ordinal) == 0)
				url = url.Substring(8);

			urls.Append(url);
			urls.Append("'))");

			if (i < (allowedUrLs.Count - 1))
				urls.Append(" && ");
		}

		return urls.ToString();
	}

	private void ValidateURLWithJavaScript()
	{
		StringBuilder javascriptTest = new StringBuilder();
		javascriptTest.Append("if (");
		javascriptTest.Append("(document.location.host != 'localhost') && (document.location.host != '')");

		if (allowedHosts.Length > 0)
			javascriptTest.Append(" && ");

		javascriptTest.Append(CompileHosts(allowedHosts));
		javascriptTest.Append("){ document.location='");
		javascriptTest.Append(RedirectURL);
		javascriptTest.Append("'; }");
		ExternalEval(javascriptTest.ToString());
	}
}
```



## Contacts & Info

Those are the most reliable websites for someone making games in Unity for PC. There should be more out there, but out of the 100+ e-mails I sent looking out for licensors for web games, those were the better I could find! 

|               | Cool Math Games              | Addicting Games            | Armor Games           |
| ------------- | ---------------------------- | -------------------------- | --------------------- |
| **@**         | afeigenbaum@coolmath.com     | btaveraclark@shockwave.com | mygame@armorgames.com |
| **Licensing** | $700                         | $500                       | $200 - $300           |
| **Work**      | API, Branding, Game Changes* | API, Branding              | Branding              |
| **Average**   | $635                         | $375                       | $280                  |

*\*Cool Math Games is the only website as far as I know that asks for game changes, although they're very reasonable with the changes and they're asked before you make the deal so you can evaluate if that's worth or not.*

The average is from a collective of gamedevs that also sell their games to web.
If you don't want to undersell your game is highly recommended that you don't sell it for a value below the average. Remember if your game has enough quality to be in their platforms you deserve to be paid (:


### Averages

**Duration**: ~2 weeks per game*

**Revenue**: 
~$1900 per game

- $700 (Cool Math Games)
- $250 (Armor Games)
- $500 (Addicting Games)
- $450 (Kongregate)*
- $30 (Ads in small websites)



\* *I don't like to give you time estimates since a game that takes a week for me might take more or less for you - It's better if you just play the game and check it for yourself the amount of effort that would take for you to make something of a similar quality*

\* *Kongregate no longer accepts new submissions or has it's monthly contests*



Sometimes is often possible to start your game in a competitive prize-based game jam, and if you do a good job you'll have some extras at the beginning as well!



## Games

The games that I used as reference to write this article:

[Deep Down](https://www.coolmathgames.com/0-deep-down)

[GENERATOR](https://www.coolmathgames.com/0-generator)

[Unnamed Chick Game](https://www.coolmathgames.com/0-unnamed-chick-game)

[Pumpking](https://www.coolmathgames.com/0-pumpking)



## Thanks

That's it guys, I hope this information can be useful for you.

If you have questions, feel free to reach me out
[@nyunesu](https://twitter.com/nyunesu) or [nyunesu@gmail.com](mailto:nyunesu@gmail.com)
