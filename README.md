<!-- default badges list -->
![](https://img.shields.io/endpoint?url=https://codecentral.devexpress.com/api/v1/VersionRange/190767639/21.1.5%2B)
[![](https://img.shields.io/badge/Open_in_DevExpress_Support_Center-FF7200?style=flat-square&logo=DevExpress&logoColor=white)](https://supportcenter.devexpress.com/ticket/details/T828680)
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
<!-- default badges end -->
# How to create a custom DiagramControl toolbox

To create a custom toolbox using a standard ListBox, populate ListBox with the collection of diagram item tools: 
```cs
ShapeListBox.ItemsSource = BasicShapes.Stencil.Tools;
```
Aftehr that, attach **DiagramToolBehavior** to items in ListBox using ItemContainerStyle:

```xaml
<ListBox.ItemContainerStyle>
    <Style TargetType="ListBoxItem">
        <Setter Property="FocusVisualStyle" Value="{x:Null}"/>
        <Setter Property="dxmvvm:Interaction.BehaviorsTemplate">
            <Setter.Value>
                <DataTemplate>
                    <ContentControl>
                        <dxdiag:DiagramToolBehavior DiagramTool="{Binding}" Diagram="{Binding RelativeSource={RelativeSource AncestorType=ListBox}, Path=Tag}" />
                    </ContentControl>
                </DataTemplate>
            </Setter.Value>
        </Setter>
    </Style>
</ListBox.ItemContainerStyle>
```
DiagramToolBehavior will automatically enable the Drag&Drop feature for items in ListBox.

Then, add the ShapeToolboxPreview element to ListBox's ItemTemplate to visualize shapes:
```xaml
<ListBox.ItemTemplate>
    <DataTemplate>
        <dxdiag:ShapeToolboxPreview IsCompact="True"  ViewMode="IconsOnly" Diagram="{Binding ElementName=diagram}" ItemTool="{Binding}" Theme="{Binding ElementName=diagram, Path=Theme}" UniformMargin="3"/>
    </DataTemplate>
</ListBox.ItemTemplate>
```
