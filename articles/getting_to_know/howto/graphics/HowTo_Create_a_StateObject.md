---
title: How to create a State Object
description: Demonstrates how to create a state object using any of the state object classes.
requireMSLicense: true
---

## Overview

In this example, we will demonstrate how to create a state object using any of the state object classes: [BlendState](xref:Microsoft.Xna.Framework.Graphics.BlendState), [DepthStencilState](xref:Microsoft.Xna.Framework.Graphics.DepthStencilState), [RasterizerState](xref:Microsoft.Xna.Framework.Graphics.RasterizerState), or [SamplerState](xref:Microsoft.Xna.Framework.Graphics.SamplerState).

## To create a state object

1. Declare three state object variables as fields in your game.

    This example declares three rasterizer state objects and uses them to change the culling state.

    ```csharp
    RasterizerState rsCullNone;
    ```

2. Create a customizable state object.

    Create a state object from the [RasterizerState](xref:Microsoft.Xna.Framework.Graphics.RasterizerState) class and initialize it by explicitly setting the cull mode.

    ```csharp
    rsCullNone = new RasterizerState();
    rsCullNone.CullMode = CullMode.None;
    rsCullNone.FillMode = FillMode.WireFrame;
    rsCullNone.MultiSampleAntiAlias = false;
    ```

3. Respond to the user pressing the A key on a gamepad to change the culling mode.

    The application starts with culling turned off; toggle between culling modes by pushing the A key on a gamepad. Unlike a customizable state object, use a built-in state object to create an object with a set of predefined state.

    ```csharp
    if (GamePad.GetState(PlayerIndex.One).Buttons.A == ButtonState.Pressed)
    {
        changeState = true;
    }
    
    if ((changeState) && (GamePad.GetState(PlayerIndex.One).Buttons.A == ButtonState.Released))
    {
        if (GraphicsDevice.RasterizerState.CullMode == CullMode.None)
        {
            GraphicsDevice.RasterizerState = RasterizerState.CullCounterClockwise;
        }
        else if (GraphicsDevice.RasterizerState.CullMode == CullMode.CullCounterClockwiseFace)
        {
            GraphicsDevice.RasterizerState = RasterizerState.CullClockwise;
        }
        else if (GraphicsDevice.RasterizerState.CullMode == CullMode.CullClockwiseFace)
        {
            GraphicsDevice.RasterizerState = rsCullNone;
        }
    
        changeState = false;
    }
    ```

Try this technique with the [HowTo Create a BasicEffect](./HowTo_Create_a_BasicEffect.md) sample and see what kinds of effects the above functionality applies.
