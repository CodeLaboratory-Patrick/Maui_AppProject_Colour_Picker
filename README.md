# Color Picker Application

This guide provides a detailed explanation of the Color Picker application built with .NET MAUI. It allows users to select RGB values using sliders and also generate random colors. The user can also copy the generated color's HEX value to the clipboard. The UI is designed in XAML, while the behavior and logic are implemented in C#. Let's break down the components, including XAML and C# code, with the relevant screenshots for better understanding.

## MainPage.xaml Overview

The `MainPage.xaml` file describes the user interface, including sliders for selecting RGB values and buttons for random color generation and copying the color value. Here's a breakdown of the main elements:

- **Color Resources**: There are three color resources defined - Primary, Secondary, and Tertiary, which are used for styling the sliders and UI elements.
  ```xml
  <Color x:Key="Primary">#ab3527</Color>
  <Color x:Key="Secondary">#775752</Color>
  <Color x:Key="Tertiary">#705c2e</Color>
  ```
- **UI Elements**: The page uses a `Grid` container with a `Frame` in which a vertical stack layout (`VerticalStackLayout`) is used to align the color picker controls vertically.
- **RGB Sliders**: The `Slider` controls are used to let users pick Red, Green, and Blue values. Each slider has event handlers (`ValueChanged`) that will adjust the displayed color accordingly.
  ```xml
  <Slider x:Name="sldRed" ThumbColor="{StaticResource Primary}" ... ValueChanged="Slider_ValueChanged"/>
  ```
- **Hex Value Display**: There is a label that shows the color's HEX value. A button (`ImageButton`) next to it allows users to copy this value to the clipboard.
- **Random Color Button**: A button that lets users generate a random color.

## MainPage.xaml.cs Overview

The `MainPage.xaml.cs` file contains the logic for handling user interactions with the sliders, buttons, and other UI elements.

- **Field Variables**: The class has `isRandom` and `hexValue` variables to manage state.
- **Slider Interaction (****`Slider_ValueChanged`****)**: Whenever the slider value changes, it invokes this method to create an RGB color from the current slider values and sets it as the background.
  ```csharp
  private void Slider_ValueChanged(object sender, ValueChangedEventArgs e)
  {
      if (!isRandom)
      {
          var red = sldRed.Value;
          var green = sldGreen.Value;
          var blue = sldBlue.Value;
          Color color = Color.FromRgb(red, green, blue);
          SetColor(color);
      }
  }
  ```
- **Random Color Generation (****`btnRandom_clicked`****)**: This event handler generates a random color using `Random.Next(0, 256)` for each RGB component and sets it as the background color.
  ```csharp
  private void btnRandom_clicked(object sender, EventArgs e)
  {
      isRandom = true;
      var random = new Random();
      var color = Color.FromRgb(
          random.Next(0, 256),
          random.Next(0, 256),
          random.Next(0, 256));
      SetColor(color);
      sldRed.Value = color.Red;
      sldGreen.Value = color.Green;
      sldBlue.Value = color.Blue;
      isRandom = false;
  }
  ```
- **Copy to Clipboard (****`ImageButton_Clicked`****)**: When the copy button is pressed, the color HEX value is copied to the clipboard, and a toast message is displayed to indicate the action.
  ```csharp
  private async void ImageButton_Clicked(object sender, EventArgs e)
  {
      await Clipboard.SetTextAsync(hexValue);
      var toast = Toast.Make("Color copied",
          CommunityToolkit.Maui.Core.ToastDuration.Short, 12);
      await toast.Show();
  }
  ```

## Screenshots and UI Flow

Here are the three main screenshots showing the UI of the Color Picker:

1. **Basic UI Layout**:
<img width="426" alt="기본화면" src="https://github.com/user-attachments/assets/1625bf54-c9f7-4438-a784-0f5e90ca6c25">


   - The initial state of the application with RGB sliders at their default values.


2. **Random Color Generation**:
<img width="426" alt="랜덤 컬러 생성" src="https://github.com/user-attachments/assets/ef37e59b-fcf7-4774-90c9-05538820c961">


   - Shows the UI after clicking on "Generate Random Colour" button. The background and button colors change to the generated color.


3. **Copy Color to Clipboard**:
<img width="426" alt="컬러 값 복사" src="https://github.com/user-attachments/assets/a1b089ec-cd4e-47ad-882f-b05b13878e00">

   
   - Demonstrates copying the generated color value to the clipboard, displaying the toast notification.


## Summary

This Color Picker application allows users to manually select RGB values or generate random colors. The UI is built using XAML with thoughtful styling for an intuitive experience, while the interaction logic is implemented in C#. It effectively uses the MAUI framework to handle UI events, randomization, and clipboard interactions.

### Key Features:

- RGB value sliders for direct color picking.
- Button for generating random colors.
- Copying HEX value of the selected color to the clipboard.

