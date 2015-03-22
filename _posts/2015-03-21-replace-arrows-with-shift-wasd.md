---
layout: post
title: Replace the arrow-keys movement with shift+w|a|s|d
---

I moved to a mechanical keyboard and want to stop using the arrow keys in favor of the Shift+W (A,S,D) key combination. Here's the story of how I made that happen.

After borrowing a mechanical keyboard from a colleague I decided to buy one for myself.
I decided on the CoolerMaster TK Stealth. This is not too expensive but very durable and has gotten great reviews. The TK Stealth has a regular layout with a numpad section and arrow keys.

The one I borrowed was a compact keyboard without arrow keys.
Instead of the arrow keys it used FN+A key for left. FN+W for up. And so on.
WASD is what most gamers are used to for movement.

The reason why I want to use the WASD keys for movement is so that my fingers stay on the `home-row`.
This should speed up the number of keystrokes while also making typing feel much easier. Less strain on the fingers.

## Challenge accepted

To remap keys and key-combinations in OSX Yosemite there's one tool I know of that works very good.
And that's
<a href="https://pqrs.org/osx/karabiner/" target="_blank"> Karabiner</a>.
What I want to achieve is the same behaviour as the arrow-keys in every application. I decided on the left shift key because it's located near WASD. It's easy to press Shift with your pinky and WASD with your other fingers.

## Remapping keys on OSX Yosemite

Karabiner does not have this feature built in so we need to roll our own. Fortunately Karabiner allows us to write into a private.xml file with custom configurations. After some experimenting I came to this solution

```xml
<?xml version="1.0"?>
<root>
  <item>
    <name>Allow Shift+WASD keys to behave like arrow keys</name>
    <identifier>private.allow_esc_with_arrow_keys</identifier>
    <autogen>__KeyToKey__ KeyCode::W , ModifierFlag::SHIFT_L, KeyCode::CURSOR_UP | ModifierFlag::NONE</autogen>
    <autogen>__KeyToKey__ KeyCode::A , ModifierFlag::SHIFT_L, KeyCode::CURSOR_LEFT | ModifierFlag::NONE</autogen>
    <autogen>__KeyToKey__ KeyCode::S , ModifierFlag::SHIFT_L, KeyCode::CURSOR_DOWN | ModifierFlag::NONE</autogen>
    <autogen>__KeyToKey__ KeyCode::D , ModifierFlag::SHIFT_L, KeyCode::CURSOR_RIGHT | ModifierFlag::NONE</autogen>
  </item>
</root>

```

The 'code' is pretty straightforward. If you want to dig into the internals more take a look at github:
<a href="https://github.com/tekezo/Karabiner" target="_blank">tekezo/Karabiner</a>
I found this 
<a href="https://github.com/tekezo/Karabiner/blob/a13a11bb3c60401b7023958bf6d5205db4a30eb1/src/core/server/Resources/include/checkbox/custom_shortcuts.xml" target="_blank">page</a>
very helpful.

## Putting it all together
Find the private.xml which lives in ```/Users/<username>/Library/Application Support/Karabiner``` and copy the code above into this file. Start Karabiner and press the option `Reload XML`. Now search `allow` and select the option. Now you can use Left Shift + W (or A, S, D) to simulate the arrow keys. :)


Hope you enjoyed this post. :smile:
