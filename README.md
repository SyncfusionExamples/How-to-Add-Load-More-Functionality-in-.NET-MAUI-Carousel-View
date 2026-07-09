# How-to-Add-Load-More-Functionality-in-.NET-MAUI-Carousel-View

This section explains how to add Load More functionality in the .NET MAUI Carousel View using the SfCarousel control. The AllowLoadMore property enables loading additional items when the user reaches the end of the carousel, and the LoadMoreItemsCount property specifies the number of items to be loaded.

## XAML

Define the SfCarousel control and enable the load more functionality by setting AllowLoadMore to True and specifying the number of items to load using LoadMoreItemsCount.
```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:carousel="clr-namespace:Syncfusion.Maui.Carousel;assembly=Syncfusion.Maui.Carousel"
             xmlns:local="clr-namespace:Sample"
             x:Class="Sample.MainPage"
             Title="LoadMore">

    <ContentPage.BindingContext>
        <local:CarouselViewModel/>
    </ContentPage.BindingContext>

    <ContentPage.Content>
        <carousel:SfCarousel x:Name="carousel"
                             ItemsSource="{Binding ImageCollection}"
                             AllowLoadMore="True"
                             LoadMoreItemsCount="2"
                             ViewMode="Linear">

            <carousel:SfCarousel.ItemTemplate>
                <DataTemplate>
                    <Image Source="{Binding Image}"
                           Aspect="AspectFit"/>
                </DataTemplate>
            </carousel:SfCarousel.ItemTemplate>

        </carousel:SfCarousel>
    </ContentPage.Content>

</ContentPage>
```

## C#

Create a view model that contains the image collection and bind it to the carousel. The carousel loads additional items based on the value specified in the LoadMoreItemsCount property.
```csharp
using System.ComponentModel;

namespace Sample
{
    public partial class MainPage : ContentPage
    {
        public MainPage()
        {
            InitializeComponent();
        }
    }

    // Model
    public class CarouselModel
    {
        public CarouselModel(string imageString)
        {
            Image = imageString;
        }

        private string _image;

        public string Image
        {
            get { return _image; }
            set { _image = value; }
        }
    }

    // ViewModel
    public class CarouselViewModel : INotifyPropertyChanged
    {
        public CarouselViewModel()
        {
            ImageCollection.Add(new CarouselModel("image1.png"));
            ImageCollection.Add(new CarouselModel("image2.png"));
            ImageCollection.Add(new CarouselModel("image3.png"));
            ImageCollection.Add(new CarouselModel("image4.png"));
            ImageCollection.Add(new CarouselModel("image5.png"));
        }

        private List<CarouselModel> imageCollection = new List<CarouselModel>();

        public List<CarouselModel> ImageCollection
        {
            get { return imageCollection; }
            set
            {
                imageCollection = value;
                OnPropertyChanged(nameof(ImageCollection));
            }
        }

        public event PropertyChangedEventHandler? PropertyChanged;

        public void OnPropertyChanged(string property)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(property));
        }
    }
}
```