# SalesManagement

create database SalesDB;

create table Items 
(
	ItemID int primary key identity,
	ItemName varchar(50),
	ItemPrice decimal(10,2)
);

create table Inventory 
(
	InvID int primary key identity,
	ItemID int foreign key references Items,
	InvDate datetime,
	BegInv int,
	ItemOut int,
	ItemRemaining int
);

create table Sales
(
	SalesID int primary key identity,
	SalesDate datetime,
);

create table SalesDetails
(
	SaleDID int primary key identity,
	InvID int foreign key references Inventory,
	SalesID int foreign key references Sales,
	SalesQty int
);
/////////////////////////////////////////////////////////////////////////////////////////////////////
insert into Items
values
('Apple', 10),
('Banana', 12),
('Carrots', 12),
('Durian', 50),
('Eggplant', 15);

select * from Items;

insert into Inventory
values
(1, '4-6-2025', 100, 0, 100),
(2, '4-6-2025', 100, 0, 100),
(3, '4-6-2025', 100, 0, 100),
(4, '4-6-2025', 100, 0, 100),
(5, '4-6-2025', 100, 0, 100);

select * from Inventory;

insert into Sales
values
('4-6-2025'),
('4-6-2025'),
('4-6-2025'),
('4-6-2025'),
('4-6-2025');

select * from Sales;

insert into SalesDetails
values
(1, 1, 10),
(2, 2, 20),
(3, 3, 30),
(4, 4, 40),
(5, 5, 50);

select * from SalesDetails;
////////////////////////////////////////////////////////////////////////////////////////////////////
create view viewSales as
select i.ItemName as [Name], s.SalesDate, sd.SalesQty from Items i
inner join Inventory inv on inv.ItemID = i.ItemID
inner join SalesDetails sd on sd.InvID = inv.InvID
inner join Sales s on s.SalesID = sd.SalesID

select * from viewSales;

////////////////////////////////////////////////////////////////////////////////////////////////////
(localdb)\MSSQLLocalDB

Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=SalesDB;Integrated Security=True


SalesDBConnectionString

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace SalesManagement
{
    public partial class Form1 : Form
    {
        protected override CreateParams CreateParams
        {
            get
            {
                CreateParams handleParams = base.CreateParams;
                handleParams.ExStyle |= 0x02000000;
                return handleParams;
            }
        }
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            // TODO: This line of code loads data into the 'salesDbDataSet.Items' table. You can move, or remove it, as needed.
            this.itemsTableAdapter.Fill(this.salesDbDataSet.Items);
            this.WindowState = FormWindowState.Maximized;

            int listBoxWidth = this.ClientSize.Width / 4 - 75;
            int listBoxHeight = this.ClientSize.Height - 200;

            //Table
            dataGridView1.Size = new Size(this.ClientSize.Width - 440, this.ClientSize.Height - 25);

            //Listbox
            listBox1.Size = new Size(listBoxWidth, listBoxHeight);
            listBox1.Location = new Point(1500, 7);

            //Textbox
            textBox1.Size = new Size(listBoxWidth, this.ClientSize.Height - 975);
            textBox1.Location = new Point(1500, 850);

            //textBox2.Size = new Size(listBoxWidth, this.ClientSize.Height - 975);  
            //textBox2.Location = new Point(1500, 930);

            //Button
            button1.Size = new Size(100, 50);
            button1.Location = new Point(1550, 930);
            button2.Size = new Size(100, 50);
            button2.Location = new Point(1750, 930);

        }

        private void panel1_Paint(object sender, PaintEventArgs e)
        {

        }

        private void dataGridView1_CellContentClick(object sender, DataGridViewCellEventArgs e)
        {

        }

        private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
        {

        }

        
    }
}
