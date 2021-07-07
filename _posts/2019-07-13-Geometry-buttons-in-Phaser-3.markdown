---
layout: post
title: "Geometry buttons in Phaser 3"
date: 2019-07-13 00:36:34
categories: development
---
Given the constants
```
    const BUTTON_WIDTH: number = 80;
    const BUTTON_HEIGHT: number = 20;
    const TEXT_FONT = {
        fontFamily: "Ubuntu Mono",
    };
```
Create an instance of `GameObjects.Rectangle` and some descriptive text if you prefer. 

```
    var btn_rect: Phaser.GameObjects.Rectangle = this.add
        .rectangle(20 + BUTTON_WIDTH/2, 20 + BUTTON_HEIGHT/2, 80, 20, 0xff0000, 1);
    var btn_text: Phaser.GameObjects.Text = this.add
        .text(btn_rect.getTopLeft().x+20, btn_rect.getTopLeft().y, 'Repair', TEXT_FONT);
```
Then create some event handlers from the output of the `setInteractive` function.

```
    var btn_handler = btn_rect.setInteractive();

    btn_handler.on(Phaser.Input.Events.POINTER_OVER, function() {
        btn_rect.setAlpha(0.8);
    });

    btn_handler.on(Phaser.Input.Events.POINTER_OUT, function() {
        btn_rect.setAlpha(1);
    });

    btn_handler.on(Phaser.Input.Events.POINTER_DOWN, function() {
        // even less alpha for when the button is ACTUALLY being clicked
        btn_rect.setAlpha(0.6);
    });

    btn_handler.on(Phaser.Input.Events.POINTER_UP, function() {
        btn_rect.setAlpha(0.8);
        repairs++; // or whatever you want your button to do
    });
```

For bonus points, wrap it in a class/function of its own.
