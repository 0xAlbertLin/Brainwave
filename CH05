using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.IO.Ports;
using System.Threading;
using ThinkGearNET;

namespace ch05
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {
            label1.Text = "序列埠:";
            bool nul = true;
            string[] ports = SerialPort.GetPortNames();
            
            foreach (string s in ports)
            {
                nul = false;
                label1.Text += s + " ";
            }
            if (nul)
            {
                label1.Text += "無";
                label2.Text += "無可用的序列埠(COMPort)";
                button2.Enabled = false; //button2 被禁止使用
            }
            else
                button2.Enabled = true; //被允許使用
        }

        private void button2_Click(object sender, EventArgs e)
        {
            System.IO.Ports.SerialPort sp;
            label2.Text = "線路狀態:";
            int ok = 0;
            string[] ports = SerialPort.GetPortNames();
            string ExMeg = "";
            string ExPorts = "";
            foreach(string s in ports)
            {
                try
                {
                    sp = new System.IO.Ports.SerialPort(s);
                    sp.Open();
                    Thread.Sleep(100);
                    if (sp.CtsHolding)
                    {
                        ok = 1;
                        sp.Close();
                        break;
                    }
                    else
                    {
                        ExPorts = s;
                        ok = 2;
                    }
                    sp.Close();
                    }
                catch(Exception ex)
                {
                    ExMeg = ex.Message;
                    ok = 3;
                }
             }
            switch (ok)
            {
                case 1:
                    label2.Text += ExPorts + "已連線";
                    break;
                case 2:
                    label2.Text += "未連線";
                    break;
                case 3:
                    label2.Text += "例外狀況!" + ExMeg + ",請重新啟動腦波儀";
                    break;
            
            }
        }

        private void button2_MouseDown(object sender,MouseEventArgs e)
        {
            label2.Text = "線路狀態:";
        }

        private void button3_Click(object sender, EventArgs e)
        {
            ThinkGearWrapper _thinkGearWrapper = new ThinkGearWrapper();

            label3.Text = "腦波儀連線狀態:";
            if(button3.Text == "Connect")
            {
                int len = label2.Text.IndexOf("已") - label2.Text.IndexOf("C");

                string blueport;

                blueport = label2.Text.Substring(5, len);
                
                if(_thinkGearWrapper.Connect(blueport,57600,true))
                {
                    label3.Text += "連接腦波儀成功!";
                    button1.Enabled = false;
                    button2.Enabled = false;
                    button3.Text = "Disconnect";

                    //當連線成功時訂閱事件
                    _thinkGearWrapper.ThinkGearChanged += _thinkGearWrapper_ThinkGearChang;
                }
            else
                {
                    label3.Text += "無法連接腦波儀!";
                }

            }
            else
            {
                button1.Enabled = true;
                button2.Enabled = true;

                _thinkGearWrapper.ThinkGearChanged -= _thinkGearWrapper_ThinkGearChang;

                button3.Text = "Connect";
                _thinkGearWrapper.Disconnect();
                label3.Text += "腦波儀連線中斷";
            }
            
        }

        void _thinkGearWrapper_ThinkGearChang(object sender,ThinkGearChangedEventArgs e)
        {
            Console.WriteLine("雜訊:" + e.ThinkGearState.PoorSignal);
            Console.WriteLine("專注:" + e.ThinkGearState.Attention);
            Console.WriteLine("放鬆:" + e.ThinkGearState.Meditation);
            Thread.Sleep(960);
        }

        _thinkGearWrapper_ThinkGearChang(object sender, ThinkGearChangedEventArgs e)
        {
            label4.Text = "雜訊:" + e.ThinkGearState.PoorSignal;
            label5.Text = "專注:" + e.ThinkGearState.Attention;
            label6.Text = "放鬆:" + e.ThinkGearState.Meditation;
            Thread.Sleep(960);
        }

    }
}


