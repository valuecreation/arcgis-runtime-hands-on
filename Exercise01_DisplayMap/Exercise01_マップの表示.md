# マップの表示

## MainWindow.xaml

```xml
<Window x:Class="Exercise01_DisplayMap.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:esri="http://schemas.esri.com/arcgis/runtime/2013"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:Exercise01_DisplayMap"
        mc:Ignorable="d"
        Title="MainWindow" Height="350" Width="525">
    <Grid>
        <esri:MapView x:Name="MyMapView"/>
    </Grid>
</Window>
```

## MainWindow.xaml

```cs
using System;
using System.Windows;

using Esri.ArcGISRuntime.Mapping;

/**
 * Exercise01_DisplayMap
 * 
 * //TODO
 * MapViewに背景地図を追加する
 * 
 * */
namespace Exercise01_DisplayMap
{
    /// <summary>
    /// MainWindow.xaml の相互作用ロジック
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();

            /**
             * MapViewに背景地図を追加する
             * **/

            // xamlにXML 名前空間参照の追加し、MapView(MyMapView)を定義する->MainWindow.xaml

            // Mapオブジェクトを作成する
            Map mMyMap = new Map();

            // 呼び出すサービスを定義する（ArcGISTiledLayer）
            var serviceUri = new Uri("http://services.arcgisonline.com/arcgis/rest/services/World_Topo_Map/MapServer");

            // サービスからレイヤーオブジェクトを作成する
            ArcGISTiledLayer imageLayer = new ArcGISTiledLayer(serviceUri);

            // Mapオブジェクトのベースマップにaddする
            mMyMap.Basemap.BaseLayers.Add(imageLayer);

            // Map をMapViewにセットする
            MyMapView.Map = mMyMap;

            // 応用：BaseMapクラスからの呼び出し:ArcGIS Onlineの様々な背景地図が呼び出し可能
            // mMyMap = new Map(Esri.ArcGISRuntime.Mapping.Basemap.CreateOceans());
            // MyMapView.Map = mMyMap;

        }
    }
}
```
