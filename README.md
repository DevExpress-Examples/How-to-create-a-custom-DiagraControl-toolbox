# How to create a custom DiagraControl toolbox

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
