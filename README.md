# Of-mice-and-men C#

For every digit that the user guessed correctly in the correct place, 
there is going to be a “mouse”. 
For every digit the you correctly in the wrong place is a “man”
Every time you will makes a guess, 
you will see how many “mice” and “men” they have.



    using System;
    using System.Collections.Generic;
    using System.ComponentModel;
    using System.Data;
    using System.Drawing;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;
    
    namespace Of_mice_and_men
    {
        public partial class Form1 : Form
        {
            private List<char> Random4digit;
    
            public Form1()
            {
                InitializeComponent();
                random4digits();
    
            }
    
            private void random4digits()
            {
                Random random = new Random();
                int digits = random.Next(1000, 10000);
                Random4digit = digits.ToString().ToList(); 
            }
    
            private void Check_btn_Click(object sender, EventArgs e)
            {
                Win_label.Text = "";
    
                string userguess = textBox1.Text;
                if (userguess.Length != 4)
                {
                    Win_label.Text = "Please enter a valid 4-digit number.";
                    return;
                }
    
                List<char> guessingnumbers = userguess.ToList();
    
                
                int mice = 0; //correct position
                int men = 0;  //wrong position
    
                List<char> wrongtarget = new List<char>();
                List<char> wrong_guess = new List<char>();
    
                for (int i = 0; i < 4; i++)
                {
                    if (guessingnumbers[i] == Random4digit[i])
                    {
                        mice++;
                    }
                    else
                    {
    
                        wrongtarget.Add(Random4digit[i]);//add the digits to unmatched lists
                        wrong_guess.Add(guessingnumbers[i]);
                    }
                }
    
                foreach (char digit in wrong_guess) //chechs if there are any digits that are not in the right places but correct
                {
                    if (wrongtarget.Contains(digit))
                    {
                        men++;
                        wrongtarget.Remove(digit); 
                    }
                }
    
                if (mice == 1) { label1.Text = "Mouse: " + mice + ", Men: " + men; }//display the result 
                else { label1.Text = "Mice: " + mice + ", Men: " + men; }//display the result 
    
    
                if (mice == 4)//if the user has guessed the correct number
                {
                    Win_label.Text = "Congratulations! You've guessed the correct number!";
                    Check_btn.Enabled = false;
                }
            }
    
            private void label1_Click(object sender, EventArgs e)
            {
    
            }
    
            private void textBox1_KeyPress(object sender, KeyPressEventArgs e)
            {
                if (!char.IsDigit(e.KeyChar) && !char.IsControl(e.KeyChar))
                {
                    e.Handled = true; // Block the character if it's not a digit
                }
            }
        }
    }
