# How use Xamarin.Forms ListView in SfNavigationDrawer (SfListView)

You can layout [SfListView](https://help.syncfusion.com/xamarin/listview/overview?) in [SfNavigationDrawer](https://help.syncfusion.com/xamarin/navigation-drawer/overview?) in Xamarin.Forms.

You can also refer the following article.

https://www.syncfusion.com/kb/11396/how-use-xamarin-forms-listview-in-sfnavigationdrawer-sflistview

**XAML**

Setting ListView as [DrawerContentView](https://help.syncfusion.com/cr/xamarin/Syncfusion.SfNavigationDrawer.XForms~Syncfusion.SfNavigationDrawer.XForms.SfNavigationDrawer~DrawerContentView.html?) in NavigationDrawer.
``` xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ListViewXamarin"
             xmlns:navigationdrawer="clr-namespace:Syncfusion.SfNavigationDrawer.XForms;assembly=Syncfusion.SfNavigationDrawer.XForms"
             xmlns:syncfusion="clr-namespace:Syncfusion.ListView.XForms;assembly=Syncfusion.SfListView.XForms"
             x:Class="ListViewXamarin.MainPage">
 
    <ContentPage.BindingContext>
        <local:ContactsViewModel/>
    </ContentPage.BindingContext>
 
    <ContentPage.Content>
        <navigationdrawer:SfNavigationDrawer x:Name="navigationDrawer" DrawerFooterHeight="0" DrawerHeaderHeight="0" IsOpen="{Binding IsOpen}" Position="{Binding Position}">
 
            <navigationdrawer:SfNavigationDrawer.ContentView>
                <StackLayout BackgroundColor="White">
                    <Button BackgroundColor="LightGray" Text="Show ListView" WidthRequest="150" HeightRequest="50" HorizontalOptions="Center" VerticalOptions="Center" Command="{Binding ShowListView}" />
                </StackLayout>
            </navigationdrawer:SfNavigationDrawer.ContentView>
 
            <navigationdrawer:SfNavigationDrawer.DrawerContentView>
                <ContentView>
                    <Grid>
                        <syncfusion:SfListView x:Name="listView" ItemSpacing="1" AutoFitMode="DynamicHeight" ItemsSource="{Binding contactsinfo}" BackgroundColor="White">
                            <syncfusion:SfListView.HeaderTemplate>
                                <DataTemplate>
                                    <Grid>
                                        <Label HeightRequest="50" Text="ListView Items" HorizontalTextAlignment="Center" VerticalTextAlignment="Center" BackgroundColor="DarkCyan"/>
                                    </Grid>
                                </DataTemplate>
                            </syncfusion:SfListView.HeaderTemplate>
                            <syncfusion:SfListView.ItemTemplate >
                                <DataTemplate>
                                    ...
                                </DataTemplate>
                            </syncfusion:SfListView.ItemTemplate>
                        </syncfusion:SfListView>
                    </Grid>
                </ContentView>
            </navigationdrawer:SfNavigationDrawer.DrawerContentView>
 
        </navigationdrawer:SfNavigationDrawer>
    </ContentPage.Content>
</ContentPage>
```

**C#**

Changing ListView position in **ViewModel** command
``` c#
namespace ListViewXamarin
{
    public class ContactsViewModel : INotifyPropertyChanged
    {
        private bool _isOpen;
        private Position _position;
 
        int flag = 0;
        public Position Position
        {
            get => _position;
            set
            {
                _position = value;
                OnPropertyChanged("Position");
            }
        }
        public bool IsOpen
        {
            get => _isOpen;
            set
            {
                _isOpen = value;
                OnPropertyChanged("IsOpen");
            }
        }
        public Command ShowListView { get; set; }
 
        public ContactsViewModel()
        {
            ShowListView = new Command(OnShowListView);
        }
 
        private void OnShowListView(object obj)
        {
            if (flag > 3)
                flag %= 4;
            switch (flag)
            {
                case 0:
                    Position = Position.Left;
                    break;
                case 1:
                    Position = Position.Bottom;
                    break;
                case 2:
                    Position = Position.Right;
                    break;
                case 3:
                    Position = Position.Top;
                    break;
                default:
                    break;
            }
            IsOpen = true;
            flag++;
        }
        public event PropertyChangedEventHandler PropertyChanged;
 
        public void OnPropertyChanged(string name)
        {
            if (this.PropertyChanged != null)
                this.PropertyChanged(this, new PropertyChangedEventArgs(name));
        }
    }
}
```
**Output**

![ListViewInNavigationdrawer](https://github.com/SyncfusionExamples/listview-in-navigationdrawer-xamarin/blob/master/ScreenShots/ListviewInNavigationdrawer.gif)
