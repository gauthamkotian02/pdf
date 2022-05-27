# pdf
.netusing System;
namespace Exercises
{
class PersonalDetails
{
 string name;
 int age;
 string gender;
 public PersonalDetails(string name, int age, string gender)
 {
 this.name = name;
 this.age = age;
 this.gender = gender;
 }
 public virtual void Display()
 {
 Console.WriteLine("\n..........PERSONAL DETAILS..........\n");
 Console.WriteLine("Name :" + name);
 Console.WriteLine("Age :" + age);
 Console.WriteLine("Gender :" + gender);
 }
}
class CourseDetails : PersonalDetails
{
 int regNo;
 string course;
 int semester;
 public CourseDetails(string name, int age, string gender, int regNo, string course, int 
semester) : base(name, age, gender)
 {
 this.regNo = regNo;
 this.course = course;
 this.semester = semester;
 }
 public override void Display()
 {
 base.Display();
 Console.WriteLine("\n..........COURSE DETAILS..........\n");
15
 Console.WriteLine("Register Number :" + regNo);
 Console.WriteLine("Course :" + course);
 Console.WriteLine("Semester :" + semester);
 }
}
class MarksDetails : CourseDetails
{
 int[] marks = new int[5];
 int total;
 float average;
 string grade;
 int flagFail;
 public MarksDetails(String name, int age, string gender, int regNo, string course, int 
semester, int[] marks) : base(name, age, gender, regNo, course, semester)
 {
 total = 0;
 
 for (int i = 0; i < 5; i++)
 {
 this.marks[i] = marks[i];
 total += marks[i];
 if (marks[i] < 35)
 {
 flagFail = 1;
 }
 }
 Calculate();
 }
 private void Calculate()
 {
 average = total / 5;
 if (flagFail == 1 || average < 40)
 grade = "Fail";
 else if (average >= 70)
 grade = "Distinction";
 else if (average >= 60)
 grade = "First Class";
 else if (average >= 50)
 grade = "Second Class";
 else
16
 grade = "Pass Class";
 }
 public override void Display()
 {
 base.Display();
 Console.WriteLine("\n..........MARKS DETAILS..........\n");
 Console.Write("Marks in 5 subjects:");
 for (int i = 0; i < 5; i++)
 Console.Write(marks[i] + " ");
 Console.WriteLine();
 Console.WriteLine("Total :" + total);
 Console.WriteLine("Average :" + average);
 Console.WriteLine("Grade :" + grade);
 }
 }
 class MultiLevel
 {
 public static void Main(string[] args)
 {
 MarksDetails Student1 = new MarksDetails("Abjhijith", 22, "Male", 20190001, 
"MCA", 5, new int[] { 77, 80, 98, 95, 90 });
 Student1.Display();
 }
 }
}
<BR>
  using System;
using System.Diagnostics;
namespace Exercises
{
class BenchmarkAllocation
{
 const int _max = 100000;
 static void Main(string[] args)
 {
 var Arr2D = new int[100, 100];
 var ArrJagged = new int[100][];
 for(int i=0;i<100;i++)
 {
 ArrJagged[i] = new int[100];
 }
 var Stopwatch2D = Stopwatch.StartNew();
 
 for (int i = 0; i < _max; i++)
 {
 for (int j = 0; j < 100; j++)
 {
 for (int k = 0; k < 100; k++)
 {
 Arr2D[j, k] = k;
 }
 }
 }
 Stopwatch2D.Stop();
 var StopwatchJagged = Stopwatch.StartNew();
 
 for (int i = 0; i < _max; i++)
 {
 for (int j = 0; j < 100; j++)
 {
 for (int k = 0; k < 100; k++)
 {
 ArrJagged[j][k] = k;
 }
 }
26
 }
 StopwatchJagged.Stop();
 Console.Write("\nTime taken for allocation in case of 2D array:");
 Console.WriteLine(Stopwatch2D.Elapsed.TotalMilliseconds+"milliseconds");
 Console.Write("\nTime taken for allocation in case of Jagged array:");
 Console.WriteLine(StopwatchJagged.Elapsed.TotalMilliseconds + "milliseconds");
 }
}
}
                         
 <BR>
  using System;
using System.IO;
namespace Exercises
{
class FileRead
{
 public static void Main()
 {
 string fileName;
 
 while(true)
 {
 Console.WriteLine("\n--------MENU--------\n");
 Console.WriteLine("\n1.Create a File");
 Console.WriteLine("\n2.Existence of the File");
 Console.WriteLine("\n3.Read the content of the File");
 Console.WriteLine("\n4.Exit");
 Console.Write("\nEnter your choice:");
 int ch = int.Parse(Console.ReadLine());
 switch(ch)
 {
 case 1:
 Console.Write("\nEnter the file name to create:");
 fileName = Console.ReadLine();
 Console.Write("\nWrite the content of the file:\n");
 string r= Console.ReadLine();
 using (StreamWriter fileStr = File.CreateText(fileName))
 {
 fileStr.WriteLine(r);
 }
 Console.WriteLine("File is created");
 break;
 case 2:
 Console.Write("\nEnter the file name:");
 fileName = Console.ReadLine();
 if(File.Exists(fileName))
 {
 Console.WriteLine("File exists...");
30
 }
 else
 {
 Console.WriteLine("File does not exist in the current directory!");
 }
 break;
 case 3:
 Console.Write("Enter the file name to read the contents:\n");
 fileName = Console.ReadLine();
 if (File.Exists(fileName))
 {
 using (StreamReader sr = File.OpenText(fileName))
{
 string s= " ";
Console.WriteLine("Here is the content of the file:");
while((s = sr.ReadLine()) != null)
{
 Console.WriteLine(s);
 }
 Console.WriteLine(" ");
 }
 }
 else
 {
 Console.WriteLine("File does not exists");
 }
 break;
 case 4:
 Console.WriteLine("\nExisting....");
 return;
 default:
 Console.WriteLine("\nInvalid choice");
 break;
 }
 }
 }
}
}
<BR>
  using System;
namespace Exercises
{
class Fraction : IComparable
{
 int z, n;
 public Fraction(int z, int n)
 {
 this.z = z;
 this.n = n;
 }
 public static Fraction operator +(Fraction a, Fraction b)
 {
 return new Fraction(a.z * b.n + a.n * b.z, a.n * b.n);
 }
 public static Fraction operator *(Fraction a, Fraction b)
 {
 return new Fraction(a.z * b.z, a.n * b.n);
 }
 public int CompareTo(object obj)
 {
 Fraction f = (Fraction)obj;
 if ((float)z / n < (float)f.z / f.n)
 return -1;
 else if ((float)z / n > (float)f.z / f.n)
 return 1;
 else
 return 0;
 }
 public override string ToString()
 {
 return z + "/" + n;
 }
}
class ICompInterface
{
 public static void Main()
 {
 Fraction[] a =
36
 {
 new Fraction(5,2),
 new Fraction(29,6),
 new Fraction(4,5),
 new Fraction(10,8),
 new Fraction(34,7),
 };
 Array.Sort(a);
 Console.WriteLine("Implementing the IComparable Interface in " + "Displaying 
Fractions:");
 
 foreach (Fraction f in a)
 {
 Console.WriteLine(f + " ");
 }
 Console.WriteLine();
 Console.ReadLine();
 }
}
}
  <br>
  using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
namespace program1
{
public partial class Form1 : Form
{
 public Form1()
 {
 InitializeComponent();
 }
 private void button1_Click(object sender, EventArgs e)
 {
 label1.Text = NumtoWord(long.Parse(textBox1.Text));
 }
 public string NumtoWord(long number)
 {
 string word = "";
 if(number==0)
 {
 return "Zero";
 }
 if(number<0)
 {
 return "Minus" + Math.Abs(number);
 }
 if(number/10000000>0)
 {
 word += NumtoWord(number / 10000000) + "Crore";
 number %= 10000000;
 }
 if(number/100000>0)
42
 {
 word += NumtoWord(number / 100000) + "Lakhs";
 number %= 100000;
 }
 if (number / 1000 > 0)
 {
 word += NumtoWord(number / 1000) + "Thousand";
 number %= 1000;
 }
 if (number / 100 > 0)
 {
 word += NumtoWord(number / 100) + "Hundred";
 number %= 100;
 }
 if(number>0)
 {
 string[] units = new string[] { "Zero", "One", "Two", "Three", "Four", "Five", "Six", 
"Seven", "Eight", "Nine", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", 
"Seventeen", "Eighteen", "Nineteen" };
 string[] Tens = new string[] { "Zero", "Ten", "Twenty", "Thirty", "Fourty", "Fifty", 
"Sixty", "Seventy", "Eighty", "Ninety" };
 if(number<20)
 {
 word += units[number];
 }
 else
 {
 word += Tens[number / 10];
 if(number%10>0)
 {
 word += units[number % 10];
 }
 }
 }
 return word;
 }
}
}
<br>
  using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
namespace program5 {
public partial class Form1 : Form
{
 public Form1()
 {
 InitializeComponent();
 timer1.Start();
 }
 private void Form1_Load(object sender, EventArgs e)
 {
 System.Timers.Timer timer = new System.Timers.Timer();
 timer.Interval = 1000;
 timer.Elapsed += Timer_Elapsed;
 timer.Start();
 }
 private void Timer_Elapsed(object sender, System.Timers.ElapsedEventArgs e)
 {
 circularProgressBar1.Invoke((MethodInvoker)delegate
 {
 circularProgressBar1.Text = DateTime.Now.ToString("hh:mm:ss");
 circularProgressBar1.SubscriptText = DateTime.Now.ToString("tt");//AM or PM
 });
 }
}
}
<br>
  using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
namespace program6._1
{
public partial class Form1 : Form
{
 static Random r = new Random();
 int value;
 int guessnum;
 int win = 10;
 int guess = 1;
 Button button1;
 TextBox textBox1;
 RichTextBox richTextBox1;
 RichTextBox richTextBox2;
 Label label1;
 Label label2;
 Label label3;
 Label label4;
 public Form1()
 {
 InitializeComponent();
 value = r.Next(100);
 this.Controls.Clear();
 this.BackColor = Color.SkyBlue;
 this.AutoSize = true;
 this.Padding = new Padding(16);
 label1 = new Label();
 label1.Text = "Pick a number between 1 to 100";
 label1.Bounds = new Rectangle(10, 20, 340, 40);
 label1.Font = new Font("Arial", 16);
 textBox1 = new TextBox();
 textBox1.Bounds = new Rectangle(20, 50, 120, 80);
 textBox1.Font = new Font("Arial", 24);
52
 button1 = new Button();
 button1.Text = "Check your Guess";
 button1.Bounds = new Rectangle(160, 50, 120, 40);
 button1.BackColor = Color.LightGray;
 button1.Click += new EventHandler(button1_Click);
 label2 = new Label();
 label2.Text = "Low Guess";
 label2.Bounds = new Rectangle(20, 150, 160, 40);
 label2.Font = new Font("Arial", 18);
 richTextBox1 = new RichTextBox();
 richTextBox1.Bounds = new Rectangle(20, 190, 160, 300);
 richTextBox1.Font = new Font("Arial", 16);
 label3 = new Label();
 label3.Text = "High Guess";
 label3.Bounds = new Rectangle(180, 150, 160, 40);
 label3.Font = new Font("Arial", 18);
 richTextBox2 = new RichTextBox();
 richTextBox2.Bounds = new Rectangle(180, 190, 160, 300);
 richTextBox2.Font = new Font("Arial", 16);
 label4 = new Label();
 label4.Bounds = new Rectangle(20, 100, 340, 40);
 label4.Font = new Font("Arial", 16);
 this.Controls.Add(label1);
 this.Controls.Add(textBox1);
 this.Controls.Add(button1);
 this.Controls.Add(label4);
 this.Controls.Add(label2);
 this.Controls.Add(label3);
 this.Controls.Add(richTextBox1);
 this.Controls.Add(richTextBox2);
 }
 private void button1_Click(object sender, EventArgs e)
 {
 if (textBox1.Text == "")
 {
 return;
 }
 guessnum = Convert.ToInt32(textBox1.Text);
 textBox1.Text = String.Empty;
53
 if (win >= 0)
 {
 if (guessnum == value)
 {
 MessageBox.Show("You have guessed the number!\nThe number was" + 
value);
 InitializeComponent();
 }
 else if (guessnum < value)
 {
 richTextBox1.Text += guessnum + "\n";
 MessageBox.Show("Wrong Guess and number of guesses left are" + (10 -
guess));
 }
 else if (guessnum > value)
 {
 richTextBox2.Text += guessnum + "\n";
 MessageBox.Show("Wrong Guess and number of guesses left are" + (10 -
guess));
 }
 guess++;
 win--;
 }
 if (guess == 11)
 {
 MessageBox.Show("You loose ,Correct Guess is" + value);
 }
 }
}
}
<br>
  using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
namespace program7
{
public partial class Form1 : Form
{
 private string fileName;
 private RichTextBox txtContent;
 private ToolBar toolBar;
 public Form1()
 {
 fileName = null;
 initializeComponents();
 }
 void initializeComponents()
 {
 this.Text = "My notepad";
 this.MinimumSize = new Size(600, 450);
 this.FormClosing += new FormClosingEventHandler(NotepadClosing);
 this.MaximizeBox = true;
 toolBar = new ToolBar();
 toolBar.Font = new Font("Arial", 16);
 toolBar.Padding = new Padding(4);
 toolBar.ButtonClick += new ToolBarButtonClickEventHandler(toolBarClicked);
 ToolBarButton toolBarButton1 = new ToolBarButton();
 ToolBarButton toolBarButton2 = new ToolBarButton();
 ToolBarButton toolBarButton3 = new ToolBarButton();
 toolBarButton1.Text = "New";
 toolBarButton2.Text = "Open";
 toolBarButton3.Text = "Save";
 toolBar.Buttons.Add(toolBarButton1);
 toolBar.Buttons.Add(toolBarButton2);
 toolBar.Buttons.Add(toolBarButton3);
56
 txtContent = new RichTextBox();
 txtContent.Size = this.ClientSize;
 txtContent.Height -= toolBar.Height;
 txtContent.Top = toolBar.Height;
 txtContent.Anchor = AnchorStyles.Left | AnchorStyles.Right | AnchorStyles.Top | 
AnchorStyles.Bottom;
 txtContent.Font = new Font("Arial", 16);
 txtContent.AcceptsTab = true;
 txtContent.Padding = new Padding(8);
 this.Controls.Add(toolBar);
 this.Controls.Add(txtContent);
 }
 private void toolBarClicked(object sender, ToolBarButtonClickEventArgs e)
 {
 saveFile();
 switch(toolBar.Buttons.IndexOf(e.Button))
 {
 case 0:
 this.Text += "My notepad";
 txtContent.Text = string.Empty;
 fileName = null;
 break;
 case 1:
 OpenFileDialog openDlg = new OpenFileDialog();
 if (DialogResult.OK == openDlg.ShowDialog())
 {
 fileName = openDlg.FileName;
txtContent.LoadFile(fileName);
this.Text = "My notepad" + fileName;
 }
 break;
 }
 }
 void saveFile()
 {
 if (fileName == null)
 {
 SaveFileDialog saveDlg = new SaveFileDialog();
 if (DialogResult.OK == saveDlg.ShowDialog())
 {
 fileName = saveDlg.FileName;
 this.Text += " " + fileName;
 }
 }
 else
 {
 txtContent.SaveFile(fileName, RichTextBoxStreamType.RichText);
57
 }
 }
 private void NotepadClosing(object sender,FormClosingEventArgs e)
 {
 saveFile();
}
/*static void Main(string[] args)using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
namespace moneyconvertion
{
 public partial class Form1 : Form
 {
 public Form1()
 {
 InitializeComponent();
 }
 private void button1_Click(object sender, EventArgs e)
 {
 {
 label4.Visible = true;
 if (textBox1.Text == "")
 {
 label4.Text = "Enter the amount";
 }
 else
 {
 Double convertedamt = Convert.ToDouble(textBox1.Text);
if (comboBox1.SelectedItem== "INR" && comboBox2.SelectedItem 
== "USD")
 {
 Double a = convertedamt / 74;
label4.Text = a + "$";
 }
else if (comboBox1.SelectedItem == "INR" && 
comboBox2.SelectedItem == "SAR")
 {
 Double a = convertedamt / 17;
 label4.Text = a + "SAR";
 }
else if (comboBox1.SelectedItem== "INR" && 
comboBox2.SelectedItem == "EUR")
 {
67
 Double a = convertedamt / 11;
label4.Text = a + "EUR";
 }
else
{
 label4.Text = "Please Enter the conversion code";
 }
 }
 }
 }
 private void button2_Click(object sender, EventArgs e)
 {
 textBox1.Text = "";
 label4.Text = "";
 
 }
 }
}
  <br>
  
{
 Application.Run(new Form1());
}*/
private void Form1_Load(object sender, EventArgs e)
{
}
}
}
  <br>
  
