using System;
using System.Windows.Forms;

namespace GuessTheNumberGame
{
    public partial class MainForm : Form
    {
        private int targetNumber;
        private bool gameActive;

        public MainForm()
        {
            InitializeComponent();
            InitializeGame();
        }

        private void InitializeGame()
        {
            Random random = new Random();
            targetNumber = random.Next(1, 1001);
            gameActive = true;

            labelPrompt.Text = "I have a number between 1 and 1000--can you guess my number?";
            labelResult.Text = "";
            textBoxGuess.Text = "";
            textBoxGuess.Enabled = true;

            this.BackColor = SystemColors.Control;
        }

        private void CheckGuess(int guess)
        {
            int difference = Math.Abs(guess - targetNumber);

            if (difference == 0)
            {
                MessageBox.Show("Correct!");
                this.BackColor = System.Drawing.Color.Green;
                textBoxGuess.Enabled = false;
                gameActive = false;
            }
            else
            {
                labelResult.Text = (difference <= 10) ? "Warmer" : "Colder";
                this.BackColor = (guess < targetNumber) ? System.Drawing.Color.Blue : System.Drawing.Color.Red;
            }
        }

        private void buttonSubmitGuess_Click(object sender, EventArgs e)
        {
            if (gameActive && int.TryParse(textBoxGuess.Text, out int guess) && guess >= 1 && guess <= 1000)
            {
                CheckGuess(guess);
            }
            else
            {
                MessageBox.Show("Please enter a valid number between 1 and 1000.");
            }
        }

        private void buttonPlayAgain_Click(object sender, EventArgs e)
        {
            InitializeGame();
        }
    }
}
