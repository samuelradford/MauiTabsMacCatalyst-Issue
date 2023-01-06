# MauiTabsMacCatalyst-Issue
To demonstrate an issue with .NET MAUI tabs on Mac Catalyst

When adding multiple `<ShellContent>` elements to a single `<Tab>` element in AppShell.xaml, certain parts of the shell content will be hidden under the `<TabBar>`.

Replication steps:

1) Create new .NET MAUI file
2) Delete the default AppShell.xml content and replace with the following:

```csharp
    <TabBar>
        <Tab Title="SingleContent">
            <ShellContent
                Title="Home"
                ContentTemplate="{DataTemplate local:MainPage}"
                Route="MainPage" />
        </Tab>
        <Tab Title="MultipleContent">
            <ShellContent
                Title="Home"
                ContentTemplate="{DataTemplate local:MainPage}"
                Route="MainPage" />
            <ShellContent
                Title="Home"
                ContentTemplate="{DataTemplate local:MainPage}"
                Route="MainPage" />
        </Tab>
    </TabBar>
```

3) Delete the default MainPage.xaml content and replace with the following:

```csharp
    <Grid RowDefinitions="Auto, *, *">
        <VerticalStackLayout>

            <Rectangle HorizontalOptions="FillAndExpand"
                       Fill="Black"
                       HeightRequest="5"
                       Margin="0, 10"/>

            <Label 
            Text="Welcome to .NET MAUI!"
            VerticalOptions="Center" 
            HorizontalOptions="Center" />

            <Button Text="Show Current Route" />

        </VerticalStackLayout>
    </Grid>
```

4) Delete default MainPage.xaml.cs code behind (as we don't need the click button behaviours).
5) Run the app

You will see that on the 'SingleContent' tab, you can see the content without any problem. But you will see on the 'MultipleContent' tab that some of the content is remove and/or hidden underneath the `<TabBar>`.

<kbd>
<img width="789" alt="Screenshot 2023-01-06 at 18 26 38" src="https://user-images.githubusercontent.com/19474685/211075502-48f92b57-e3df-4352-833d-a0c7cee8c5b3.png">
</kbd>

<kbd>
<img width="790" alt="Screenshot 2023-01-06 at 18 28 31" src="https://user-images.githubusercontent.com/19474685/211075467-f004cafb-37a1-4160-99b8-7de11078a832.png">
</kbd>
