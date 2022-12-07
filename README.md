# class
#include <iostream>

using namespace std;

class Critter {
public:
  int count = 0;
  Critter(int hunger = 0, int boredom = 0); // constructor prototype
  void Talk();
  void Eat(int food = 4);
  void Play(int fun = 4);
  void GetValues() const;
  void medical();

private:
  int m_Hunger;
  int m_Boredom;

  int GetMood() const;
  void PassTime(int time = 1);
};

Critter::Critter(int hunger, int boredom)
    : // constructor definition
      m_Hunger(hunger), m_Boredom(boredom) {}

inline int Critter::GetMood() const { return (m_Hunger + m_Boredom); }

void Critter::PassTime(int time) {
  m_Hunger += time;
  m_Boredom += time;
}

void Critter::Talk() {
  cout << "I'm a critter and I feel ";

  int mood = GetMood();
  if (mood > 15) {
    cout << "despair";
    //空腹度と暇度を足して１５より上なら絶望する。
  } else if (mood > 13) {
    cout << "mad.\n";
  } else if (mood > 10) {
    cout << "frustrated.\n";
  } else if (mood > 5) {
    cout << "okay.\n";
  } else {
    cout << "happy.\n";
  }

  cout << "I am ";

  if (m_Hunger > 10) {
    cout << "extremely";
  } else if (m_Hunger > 5) {
    cout << "very";
  } else {
    cout << "not";
  }

  cout << " hungry.\n";

  cout << "I am ";

  if (m_Boredom > 10) {
    cout << "extremely";
  } else if (m_Boredom > 5) {
    cout << "very";
  } else {
    cout << "not";
  }
  cout << " bored.\n";

  PassTime();
}

void Critter::Eat(int food) {
  cout << "Brruppp.\n";
  m_Hunger -= food;
  if (m_Hunger < 0) {
    m_Hunger = 0;
  }

  PassTime();
}

void Critter::Play(int fun) {
  cout << "Wheee!\n";

  m_Boredom -= fun;
  if (m_Boredom < 0) {
    m_Boredom = 0;
  }

  PassTime();
}

void Critter::GetValues() const {
  cout << "Hunger Lvl: " << m_Hunger << endl;
  cout << "Boredom Lvl: " << m_Boredom << endl;
}
void Critter::medical() {
  if (count == 0) {
    m_Hunger = 0;
    m_Boredom = 0;
    count = 1;
    cout << "got the best";
    // medical関数を追加してm_Hunger
    //とm_Boredomの値を０にする。
    //１回しか使えないようにif文を使う。
  } else {
    cout << "I can't go to the hospital anymore";
  }
}

int main() {
  Critter crit;
  crit.Talk();

  int choice;
  do {
    cout << "\nCritter Caretaker\n\n";
    cout << "0 - Quit\n";
    cout << "1 - Listen to your critter\n";
    cout << "2 - Feed your critter\n";
    cout << "3 - Play with your critter\n";
    cout << "4 - List values of hunger and boredom\n\n";
    cout << "5 _ Go hospital\n";

    cout << "Choice: ";
    cin >> choice;

    switch (choice) {
    case 0:
      cout << "Good-bye.\n";
      break;
    case 1:
      crit.Talk();
      break;
    case 2:
      crit.Eat();
      break;
    case 3:
      crit.Play();
      break;
    case 4:
      crit.GetValues();
      break;
    case 5:
      crit.medical();
      break;
    default:
      cout << "\nSorry, but " << choice << " isn't a valid choice.\n";
    }
  } while (choice != 0);

  return 0;
}
