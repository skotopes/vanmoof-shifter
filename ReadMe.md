# About

Simple issues with vanmoof s3 e-shifter are pretty much covered by other people. This repo is focusing on MCU part of it. Replacing, reflashing and etc...

# Intro

Main culprit is MindMotion MM32F031F6U6 (https://www.mindmotion.com.cn/en/products/mm32mcu/mm32f/mm32f_others/mm32f031xxq/)

What's wrong with it:
- Quite obscure and obsolete component even by Chinese standards
- You may find some stock on aliexpress, but no trusted suppliers
- Official vendor tools don't support it (Don't let website fool you)
- There is MM32F0140 series which may provide pin2pin compatibility, but no guarantee that firmware will run on it

On the bright side:
- It is cortex-m0
- It got SWD
- There is a Segger support by the Vendor (J-Link and J-Flash works perfectly)
- No protection

How it may fail:

- Sometimes it just die
- GPIO/UART port damage

# Requirements

So you found that something wrong with your MCU, and you want to replace it.
You will need following:

- Windows PC
- Segger supported hardware (J-Link or any other thing that can be converted into j-link)
- J-Link software installed
- J-Link pack from Recommended Software section in https://www.mindmotion.com.cn/en/products/mm32mcu/mm32f/mm32f_others/mm32f031xxq/ installed

# Pinout for connection

The only thing that we need is MCU debug connector.

```
 ~ MCU side ~
 -----------
| 5 | 3 | 1 |
| 6 | 4 | 2 |
 -----------
 ~ shaft ~
```

| Pin  | Signal | Destination |
|-------|-----|------------|
| 1 | Reset | |
| 2 | Vdd    | Provide Vdd from j-link or external power supply |
| 3 | SWDIO | Connect to J-Link SWDIO|
| 4 | NC    | |
| 5 | SWCLK | Connect to J-Link SWCLK |
| 6 | GND   | Connect to J-Link GND |


Vdd can be anything from 3.3V to 5V, but your J-Link must be able to work with it. 3.3V is a safe choice.

# Programming firmware

Quite straight forward process:
- Open J-Flash
- Create new project, select MM32F031F6U6, if it's not there then make sure that you have J-Link pack from Mind Motion installed
- Menu -> Target -> Connect. If it fails then check your wiring and MCU.
- Menu -> File -> Open Data file choose firmware
- Menu -> Target -> Manual Programming -> Program and Verify

If successful you'll get working shifter, if not - well, princess was in another castle.

I'll put firmware I extracted from dead shifter. It may or may not work. Please create pull request if you'll find working one. 
