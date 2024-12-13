---
title: Mastodon
draft: false
tags: 
publish: true
---
**Mastodon** is the world's largest free, open-source, decentralized microblogging network.
It is a part of the larger, open source [[Fediverse]]. Messages posted using the software are known as "toots". A toot can be up to 500 characters long. 

Private toots are not encrypted or secure. The admin of your server can read _any_ toot posted on their server, as well as _any_ toot sent to a user on their server. This is a necessary security precaution.

Mastodon usernames take the form @_username_@_instance_. If you're mentioning someone on your own instance, you just have to type the first part; if you're on elekk.xyz, @noelle will get to me just like @noelle@elekk.xyz will. If you leave off the "@_instance_" Mastodon understands that you want to talk to the local user.

---
## Summary
###### How is it like Twitter?
You post relatively-short status updates, and you can see a streaming list of your friends' status updates. You can keep notifications (replies, boosts, favorites, and DMs) in a separate column.  Mastodon also supports hashtags, which are words prefixed by #, like "#gaming" or "#pineapple". You can click on a hashtag to search for other posts containing that tag.


###### How is it like email?
Each Mastodon instance is independent but networked, like email servers. If you sign up for an email account on gmail.com, you don't automatically have an account on hotmail.com or aol.com, but you can send and receive messages to and from users on hotmail.com and aol.com. Likewise, if you sign up for an account on mastodon.social, that doesn't make an account for you on every other instance, but you can talk to users from other instances and they can talk to you.

Keep in mind that in general, when talking about Mastodon, "instance" and "server" mean the same thing.


###### How is it not like either of those?
Mastodon has two additional timelines that you can view: the *Local* timeline and the *Federated* timeline. The Local timeline is every post with a public status posted by users on your instance, with the exception of replies. 

The Federated timeline is every post with a public status posted by any user that your instance knows about, even from other instances. Your instance knows about a remote user if at least one user on your instance has EVER followed them.


###### How do privacy settings work?
Under each post you'll see three icons: a camera, a globe or a padlock, and the letters "CW". Click on the globe or padlock to choose the privacy settings for your post.
- **Public** means that everyone can see your post.
- **Unlisted** means that everyone can see your post, but it won't appear on the public timelines - either Local or Federated. Anyone who follows you or views your profile can see the toot, though.
- **Followers-Only** means that only people who follow you and people mentioned in the post can see your post in their timelines or on your profile page. If someone who doesn't follow you views your profile, they won't see this post.
- **Private** means that only people who are mentioned in your post can see it in their timelines or on your profile page.
Keep in mind that some servers, which run software that's compatible with but not the same as Mastodon, will ignore these privacy settings if you send a message to their users, so be careful!


###### Differences between distributed and federated networks
Both kind of networks are decentralized. However, distribution goes further than federation. A federated network has multiple centers, whereas a distributed network has no center at all.


---
#### Resources
- [Mastodon instances](https://instances.social/list) - List of Mastodon instances.
- [unmung.com/mastoview](http://www.unmung.com/mastoview) - Preview the local or federated timeline of any instance.
- [Toot scheduler](https://scheduler.mastodon.tools/) - Schedule now, toot later.
- [Fediverse Explorer](https://fediverse.0qz.fun/) - Trending hashtags and popular toots, regenerated every hour.


#### Bots
- [feed2toot](https://gitlab.com/chaica/feed2toot) - Automatically parses RSS feeds, identifies new posts and posts them on Mastodon (Python).
- [hnbot](https://github.com/raymestalez/mastodon-hnbot) - Posts the Hacker News stories with 100+ points (Python).
- [@TrendingBot@mastodon.social](https://mastodon.social/@TrendingBot) - Shows you what's trending on Mastodon.
- If you make a bot that posts automatically, have it post using the [unlisted privacy setting](https://gist.github.com/joyeusenoelle/74f6e6c0f349651349a0df9ae4582969#how-do-privacy-settings-work). This avoids having your bot flagged as spam.


---

###### See Also:
- [[Fediverse]]

###### References:
- [An Increasingly Less Brief Guide to Mastodon by joyeusenoelle](https://github.com/joyeusenoelle/GuideToMastodon/)
- [Wikipedia entry for Mastodon](https://en.wikipedia.org/wiki/Mastodon_(software))
