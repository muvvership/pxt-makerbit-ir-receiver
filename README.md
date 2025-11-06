# **Interest Group Code \- IR Remote Extension**

This is a MakeCode extension for the common infrared (IR) remote control included in many Elegoo and Arduino starter kits.

It has been customized for the "Interest Group Code" project to provide simple, easy-to-use blocks for 4th-grade students.

## **Using the Extension**

This extension adds a new category to MakeCode called **"Interest Group Code"**.

### **connect IR receiver**

You must use this block in an on start block. It tells the micro:bit which pin your IR receiver is connected to (usually P0) and which remote you're using (NEC).

makerbit.connectIrReceiver(DigitalPin.P0, IrProtocol.NEC)

## **How to Assign Actions to Buttons (like CH or EQ)**

You have two great ways to make buttons do things.

### **Method 1: The Easy Way (Event Blocks)**

This is the simplest way and is perfect for most projects. Use the on IR button pressed block. You can drag as many of these as you want onto your screen.

This example shows how to make the EQ button show a "target" icon and the CH+ button show a "ghost" icon.

// Run this code when EQ is pressed  
makerbit.onIrButton(IrButton.Eq, IrButtonAction.Pressed, function () {  
    basic.showIcon(IconNames.Target)  
})

// Run this code when CH+ is pressed  
makerbit.onIrButton(IrButton.ChPlus, IrButtonAction.Pressed, function () {  
    basic.showIcon(IconNames.Ghost)  
})

// Run this code when number 1 is pressed  
makerbit.onIrButton(IrButton.Number\_1, IrButtonAction.Pressed, function () {  
    basic.showNumber(1)  
})

### **Method 2: The Advanced Way (IF Statements)**

This method is for more advanced projects, like making a remote-controlled car where you need to check buttons inside a forever loop.

For this, you use **two** blocks:

1. last button pressed (code): This block *gets* the raw number code of the last button that was pressed.  
2. code for button %button: This block *holds* the correct code for a button you choose from the dropdown.

You use them together in an if block to check if they are equal.

let last\_button\_code \= 0

basic.forever(function () {  
    // 1\. Get the code for the last button pressed  
    last\_button\_code \= makerbit.lastButtonPressed\_code\_()  
      
    // 2\. Check if it's the code for EQ  
    if (last\_button\_code \== makerbit.irButtonCode(IrButton.Eq)) {  
        basic.showIcon(IconNames.Target)  
      
    // 3\. Check if it's the code for CH+  
    } else if (last\_button\_code \== makerbit.irButtonCode(IrButton.ChPlus)) {  
        basic.showIcon(IconNames.Ghost)  
    }  
})

## **New Blocks for Your Project**

### **last number pressed**

This is a special block made just for your project\! It's a "getter" block that simply **returns the last number (0-9) that was pressed** on the remote.

It's perfect for projects where you want students to enter a code, select a level, or choose an answer.

let last\_number \= 0

basic.forever(function () {  
    // Get the number from the "backend"  
    last\_number \= makerbit.irLastNumberPressed()  
      
    // Show it on the screen  
    basic.showNumber(last\_number)  
})

## **License**

Licensed under the MIT License (MIT).
