# ToggleSlider
A nice C# toggle-slider (apple-esc) as a Style property for a .NET CheckBox 

# Usage

- Add the following to your App.xml

```
<!-- Slider Textbox -->
        
        <!-- Sets colours for different states -->
        <SolidColorBrush x:Key="OptionMark.MouseOver.Background" Color="#FFF3F9FF"/>
        <SolidColorBrush x:Key="OptionMark.MouseOver.Border" Color="#FF5593FF"/>
        <SolidColorBrush x:Key="OptionMark.Disabled.Background" Color="#FFE6E6E6"/>
        <SolidColorBrush x:Key="OptionMark.Disabled.Border" Color="#FFBCBCBC"/>
        <SolidColorBrush x:Key="OptionMark.Pressed.Background" Color="#FFD9ECFF"/>
        <SolidColorBrush x:Key="OptionMark.Pressed.Border" Color="#FF3C77DD"/>
        <SolidColorBrush x:Key="Background" Color="#FF008000"/>

        <Style x:Key="SliderTemplate" TargetType="{x:Type CheckBox}">
            <!-- Sets initial colours on creation -->
            <Setter Property="FocusVisualStyle" Value="{StaticResource FocusVisual}"/>
            <Setter Property="Background" Value="{StaticResource Background}"/>
            <Setter Property="BorderBrush" Value="{StaticResource OptionMark.Static.Border}"/>
            <Setter Property="Foreground" Value="{DynamicResource {x:Static SystemColors.ControlTextBrushKey}}"/>
            <Setter Property="BorderThickness" Value="1"/>
            <Setter Property="HorizontalAlignment" Value="Right" />

            <Setter Property="Template">
                <Setter.Value>
                    <!-- Sets XAML for actual controls -->
                    <ControlTemplate TargetType="{x:Type CheckBox}">
                        <Grid x:Name="templateRoot" Background="Transparent" SnapsToDevicePixels="True">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="Auto"/>
                                <ColumnDefinition Width="*"/>
                            </Grid.ColumnDefinitions>
                            
                            <!-- Actual Slider -->
                            <Grid>
                                <Border Name="RefreshBackground" CornerRadius="10" Width="40" Height="20" Background="{TemplateBinding Background}"/>
                                <Border Name="RefreshCircle" CornerRadius="10" Width="20" Height="20" Background="White" HorizontalAlignment="{TemplateBinding HorizontalAlignment}"/>
                            </Grid>

                        </Grid>
                        <ControlTemplate.Triggers>
                            <!-- Hover Colours -->
                            <Trigger Property="IsMouseOver" Value="true">
                                <Setter Property="Background" TargetName="RefreshCircle" Value="#e0e0e0"/>
                            </Trigger>
                            <!-- Disabled Colours -->
                            <Trigger Property="IsEnabled" Value="false">
                                <Setter Property="Background" TargetName="RefreshCircle" Value="#e0e0e0" />
                            </Trigger>
                            <!-- Pressed Colours -->
                            <Trigger Property="IsPressed" Value="true">
                                <Setter Property="Background" TargetName="RefreshCircle" Value="#bdbdbd"/>
                            </Trigger>
                            <!-- Setters for checked and unchecked states -->
                            <Trigger Property="IsChecked" Value="true">
                                <Setter Property="HorizontalAlignment" TargetName="RefreshCircle" Value="Right" />
                                <Setter Property="Background" TargetName="RefreshBackground" Value="#FF008000" />
                            </Trigger>
                            <Trigger Property="IsChecked" Value="{x:Null}">
                                <Setter Property="HorizontalAlignment" TargetName="RefreshCircle" Value="Left" />
                                <Setter Property="Background" TargetName="RefreshBackground" Value="#FF0000" />
                            </Trigger>
                            <Trigger Property="IsChecked" Value="false">
                                <Setter Property="HorizontalAlignment" TargetName="RefreshCircle" Value="Left" />
                                <Setter Property="Background" TargetName="RefreshBackground" Value="#FF0000" />
                            </Trigger>
                        </ControlTemplate.Triggers>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
```
- In your page XML, add a new CheckBox element and add the attribute;
```
<CheckBox Style="{DynamicSource SliderTemplate}" />
```

For your reference, by default the dimensions of the slider are 20*40px. It does not have any scaling capabilities, but you can adjust the size of the elements to your liking in the code you added to your App.XML. To keep a similar look I recommend you;
- maintain diameters equal to overall height and 
- width equal to twice the height/diameter
