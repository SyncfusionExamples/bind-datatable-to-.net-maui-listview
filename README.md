**[View document in Syncfusion .NET MAUI Knowledge Base](https://www.syncfusion.com/kb/13128/how-to-bind-data-from-the-datatable-to-net-maui-listview-sflistview)**

## Sample

```xaml
<ListView:SfListView x:Name="listView" ItemsSource="{Binding ContactsInfo}" ItemSize="70">
    <ListView:SfListView.ItemTemplate>
        <DataTemplate>
            <Grid x:Name="grid" RowSpacing="0">
                <Grid.RowDefinitions>
                    <RowDefinition Height="*" />
                    <RowDefinition Height="1" />
                </Grid.RowDefinitions>
                <Grid RowSpacing="0">
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition Width="70" />
                        <ColumnDefinition Width="*" />
                        <ColumnDefinition Width="Auto" />
                    </Grid.ColumnDefinitions>
                    <Label Text="{Binding ItemArray[0]}" LineBreakMode="NoWrap" FontSize="16" TextColor="#474747" VerticalOptions="CenterAndExpand" Padding="10,0,0,0"/>
                    <Grid Grid.Column="1" RowSpacing="1" VerticalOptions="Center">
                        <Grid.RowDefinitions>
                            <RowDefinition Height="*" />
                            <RowDefinition Height="*" />
                        </Grid.RowDefinitions>
                        <Label LineBreakMode="NoWrap" TextColor="#474747" Text="{Binding ItemArray[1]}" VerticalOptions="CenterAndExpand"/>
                        <Label Grid.Row="1" Grid.Column="0" TextColor="#474747" LineBreakMode="NoWrap" Text="{Binding ItemArray[3]}" FontSize="12" VerticalOptions="StartAndExpand"/>
                    </Grid>
                    <Label LineBreakMode="NoWrap" TextColor="#474747" Text="{Binding ItemArray[2]}" FontSize="10" Grid.Row="0" Grid.Column="2" Padding="0,10,10,0" HorizontalOptions="End" VerticalOptions="Start"/>
                </Grid>
                <StackLayout Grid.Row="1" BackgroundColor="#E4E4E4" HeightRequest="1"/>
            </Grid>
        </DataTemplate>
    </ListView:SfListView.ItemTemplate>
</ListView:SfListView>

ViewModel.cs:

public ObservableCollection<object> ContactsInfo { get; set; }

public ContactsViewModel()
{
    GenerateInfo();
}

private void GenerateInfo()
{
    Random random = new Random();
    
    ContactsInfo = new ObservableCollection<object>();

    DataTable dt = new DataTable("Contacts");
    dt.Columns.Add("ContactID", typeof(Int32));
    dt.Columns.Add("ContactName", typeof(string));
    dt.Columns.Add("ContactType", typeof(string));
    dt.Columns.Add("ContactNumber", typeof(string));

    for (int i = 0; i < CustomerNames.Count(); i++)
    {
        dt.Rows.Add(i + 1, CustomerNames[i], contactType[random.Next(0, 5)], random.Next(100, 400).ToString() + "-" + random.Next(500, 800).ToString() + "-" + random.Next(1000, 2000).ToString());
    }

    for (int i = 0; i < dt.Rows.Count; i++)
    {
        ContactsInfo.Add(dt.Rows[i]);
    }
}
```