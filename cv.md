Евгений Соловьёв
@YounChgao
Хочу быть полезным, найдя работу которая мне подойдёт. Хочу узнавать новое в понятной форме.
С++, С#, Java, 1C, learning JS.

private void Selection()
{
    WorkWithDataBase.ReadDataBase(out вузы, out факультеты, out формыОбучения);
    подходящиеФакультеты = факультеты.Where(p => p.PassingSchore <= res).ToList();

    подходящиеВузы = вузы.Where(v => v.ID_F.Intersect(подходящиеФакультеты.Select(f => f.ID_F)).Any()).ToList();
    foreach (ВУЗ вуз in подходящиеВузы)
    {
        TextBlock textBlock = new TextBlock()
        {
            TextWrapping = TextWrapping.Wrap,
            FontSize = 18
        };
        textBlock.Text = $"\n{вуз.Nazvanie}\nДата основания: {вуз.Data.Year}\nДиректор: {вуз.Director}\nАдрес: {вуз.Adress}\nВЕБ-сайт: {вуз.WebSite}\nE-mail: {вуз.Email}";
        STACKPANEL.Children.Add(textBlock);

        List<Факультет> факультетыВуза = подходящиеФакультеты.Where(p => вуз.ID_F.Contains(p.ID_F)).ToList();
        var query = факультетыВуза.Join(формыОбучения, f => f.ID_FO, f2 => f2.ID_FO, (f, f2) => new { Nazvanie = f.Nazvanie, PassingSchore = f.PassingSchore, FONazvanie = f2.Nazvanie });

        DataGrid grid = new DataGrid
        {
            AutoGenerateColumns = false,
            IsReadOnly = true,
            CanUserAddRows = false
        };
        DataGridTemplateColumn column1 = new DataGridTemplateColumn
        {
            Header = "Факультет",
            Width = new DataGridLength(500)
        };
        column1.CellTemplate = new DataTemplate();
        FrameworkElementFactory factory1 = new FrameworkElementFactory(typeof(TextBlock));
        factory1.SetBinding(TextBlock.TextProperty, new Binding("Nazvanie"));
        factory1.SetValue(TextBlock.TextWrappingProperty, TextWrapping.Wrap);
        column1.CellTemplate.VisualTree = factory1;

        DataGridTextColumn column2 = new DataGridTextColumn
        {
            Header = "Проходной балл",
            Binding = new Binding("PassingSchore")
        };
        DataGridTextColumn column3 = new DataGridTextColumn
        {
            Header = "Форма обучения",
            Binding = new Binding("FONazvanie")
        };
        grid.Columns.Add(column1);
        grid.Columns.Add(column2);
        grid.Columns.Add(column3);
        grid.ItemsSource = query;
        STACKPANEL.Children.Add(grid);
    }
    FIO.Content = $"{fio}. Проходной балл: {res}";
}

Опыта работы нет.
2-4 курс ПОИТ.
A2-B1
