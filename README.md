# formularzewpf


WIDOK

<Window x:Class="formularze.Window1"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:formularze"
        mc:Ignorable="d"
        Title="Obliczenia dla keadratu" Height="450" Width="800">
    <Grid>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*"></ColumnDefinition>
            <ColumnDefinition Width="*"></ColumnDefinition>
            <ColumnDefinition Width="auto"></ColumnDefinition>
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
        </Grid.RowDefinitions>
        <TextBlock 
            Margin="10"
            FontSize="20">
            Bok kwadratu
        </TextBlock>
        <TextBlock 
            Margin="10"
            FontSize="20"
            Grid.Row="1">
            Pole kwadratu
        </TextBlock>
        <TextBlock 
            Margin="10"
            FontSize="20"
            Grid.Row="2">
            Obwód kwadratu
        </TextBlock>
        <TextBox
            Grid.Column="1"
            Margin="5"
            x:Name="bok_txt"
            
            TextChanged="bok_txt_TextChanged">
            
        </TextBox>
        <TextBlock
            x:Name="wynik_pole_txt"
            FontSize="20"
            Grid.Column="1"
            Grid.Row="1">
            
        </TextBlock>
        <TextBlock
            x:Name="wynik_obwod_txt"
            FontSize="20"
            Grid.Column="1"
            Grid.Row="2">

        </TextBlock>
        <Button Content="Oblicz"
                Grid.Row="6"
                Margin="20"
                Grid.ColumnSpan="2"
                Click="Button_Click">
            
        </Button>
        <Rectangle
            Width="{Binding ElementName=bok_txt, Path=Text}"
            Height="{Binding ElementName=bok_txt, Path=Text}"
            Fill="{Binding ElementName=kolorki, Path=Text}"
            Grid.Row="3">
            
        </Rectangle>
        <Rectangle
            Width="20"
            Height="20"
            Fill="Orange"
            Margin="2"
            Grid.Row="4"
            x:Name="kwadrat">
            
        </Rectangle>
        <ComboBox
            x:Name="kolorki"
            Grid.Column="1"
            Grid.Row="4"
            Margin="10"
            SelectedIndex="0">
            <ComboBoxItem>Red</ComboBoxItem>
            <ComboBoxItem>Green</ComboBoxItem>
            <ComboBoxItem>Blue</ComboBoxItem>
            <ComboBoxItem>Fuchsia</ComboBoxItem>
        </ComboBox>
        <CheckBox 
            Grid.Column="1"
            Grid.Row="5"
            IsChecked="True"
            Margin="20"
            x:Name="przezrocz_chbox">
            Przeźroczysty?
        </CheckBox>
        <StackPanel
            Grid.Column="1"
            Grid.Row="5">
            <RadioButton
                GroupName="widocznosc"
                x:Name="widoczny">
                Widoczny
            </RadioButton>
            <RadioButton
                GroupName="widocznosc"
                x:Name="niewidoczny"
                IsChecked="True">
                Niewidoczny
            </RadioButton>
            
            
        </StackPanel>
    </Grid>
</Window>





SKRYPT

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Shapes;

namespace formularze
{
    /// <summary>
    /// Logika interakcji dla klasy Window1.xaml
    /// </summary>
    public partial class Window1 : Window
    {
        public Window1()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            String wpisanyBok = bok_txt.Text;
            kwadrat.Fill = (SolidColorBrush)new BrushConverter().ConvertFromString(kolorki.Text);
            if(przezrocz_chbox.IsChecked == true)
            {
                kwadrat.Opacity = 0.5;
            }
            else
            {
                kwadrat.Opacity = 1;    
            }
            if(widoczny.IsChecked == true)
            {
                kwadrat.Visibility = Visibility.Visible; 
            }
            if(niewidoczny.IsChecked == true)
            {
                kwadrat.Visibility = Visibility.Visible;
            }
            double bok;
            MessageBox.Show("Wpisano: " + wpisanyBok, "Wartość wpisana",
                MessageBoxButton.OK, MessageBoxImage.Information);
            if(double.TryParse(wpisanyBok, out bok))
            {
                double pole = bok * bok;
                wynik_pole_txt.Text = pole.ToString();
                double obwod = 4 * bok;
                wynik_obwod_txt.Text = obwod.ToString();

                kwadrat.Width = bok;
                kwadrat.Height = bok;
            }
            else
            {
                MessageBox.Show("Musisz wpisać liczbę rzeczywistą");
                wynik_obwod_txt.Text = "";
                wynik_pole_txt.Text = "";
            }
        }

        private void bok_txt_TextChanged(object sender, TextChangedEventArgs e)
        {
            if(double.TryParse(bok_txt.Text, out double boczek))
            {
                kwadrat.Width = boczek * 2;
                kwadrat.Height = boczek * 2;
            }
        }
    }
}
