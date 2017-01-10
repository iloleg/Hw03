Примеры кода
Пример 1
До 
var _FolderLabelPrinter = ConfigurationManager.AppSettings["LabelPrintelFileLocation"];
var _LabelLocationPrinterFile = ConfigurationManager.AppSettings["LabelLocationName"];
var LocationLabelFile = @"" + _FolderLabelPrinter + @"\" + _LabelLocationPrinterFile;
            try
            {
                var doc = new DocumentClass();
                if (doc.Open(LocationLabelFile))
                {
                   
                    doc.GetObject("BarCodeLocation").Text = Convert.ToString(ItemLocationComboBox.Text);
                    doc.GetObject("Location").Text = Convert.ToString(ItemLocationComboBox.Text);
                    doc.StartPrint("", PrintOptionConstants.bpoDefault);
                    doc.PrintOut(1, PrintOptionConstants.bpoDefault);
                    doc.EndPrint();
                    doc.Close();



                }
                


После 

try
            {
                if (new DocumentClass().Open(@"" + ConfigurationManager.AppSettings["LabelPrintelFileLocation"] + @"\" + ConfigurationManager.AppSettings["LabelLocationName"]))
                {
                    
                    new DocumentClass().GetObject("BarCodeLocation").Text = Convert.ToString(this.ItemLocationComboBox.Text);
                    new DocumentClass().GetObject("Location").Text = Convert.ToString(this.ItemLocationComboBox.Text);
                    new DocumentClass().StartPrint("", PrintOptionConstants.bpoDefault);
                    new DocumentClass().PrintOut(1, PrintOptionConstants.bpoDefault);
                    new DocumentClass().EndPrint();
                    new DocumentClass().Close();



                }

Пример 2
До 

public static string ImageToByte(FileStream fs)
            {
                var imgBytes = new byte[fs.Length];
                fs.Read(imgBytes, 0, Convert.ToInt32(fs.Length));
                var encodeData = Convert.ToBase64String(imgBytes, Base64FormattingOptions.InsertLineBreaks);

                return encodeData;
            }

После 
public static string ImageToByte(FileStream fs)
            {
                fs.Read(new byte[fs.Length], 0, Convert.ToInt32(fs.Length));

                return Convert.ToBase64String(new byte[fs.Length], Base64FormattingOptions.InsertLineBreaks);
            }

Пример 3
До 

public static ImageSource ByteToImage(byte[] imageData)
            {
                var biImg = new BitmapImage();
                var ms = new MemoryStream(imageData);
                biImg.BeginInit();
                biImg.StreamSource = ms;
                biImg.EndInit();

                var imgSrc = biImg as ImageSource;

                return imgSrc;
            }

После 

public static ImageSource ByteToImage(byte[] imageData)
            {
                new BitmapImage().BeginInit();
                new BitmapImage().StreamSource = new MemoryStream(imageData);
                new BitmapImage().EndInit();

                var imageSource = new BitmapImage() as ImageSource;

                return imageSource;
            }






Группы данных
Проблема
У нас есть фрагмент кода, который можно сгруппировать.

void PrintOwing() 
{
  PrintBanner();

  //print details
  Console.WriteLine("name: " + name);
  Console.WriteLine("amount: " + GetOutstanding());
}

Решение!
метод вместо
void PrintOwing()
{
  PrintBanner();
  PrintDetails(GetOutstanding());
}

void PrintDetails(double outstanding)
{
  Console.WriteLine("name: " + name);
  Console.WriteLine("amount: " + outstanding);
}

Одержимость элементарными типами

Проблема
У нас  есть массив, в котором хранятся разнотипные данные.
string[] row = new string[2];
row[0] = "Liverpool";
row[1] = "15";
Решение
Performance row = new Performance();
row.SetName("Liverpool");
row.SetWins("15");


Длинный список параметров

Проблема
Мы получаем несколько значений из объекта, а затем передаем их в метод как параметры.
int low = DaysTempRange().GetLow();
int high = DaysTempRange().GetHigh();
bool withinPlan = plan.WithinRange(low, high);
Решение
Вместо этого передаем весь объект.
bool withinPlan = plan.WithinRange(DaysTempRange());


