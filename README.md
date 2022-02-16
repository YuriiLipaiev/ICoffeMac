# ICoffeMac

#include <iostream>

enum class TypeError
{
	Error_NoError = 0,
	Error_NoCoffee = 1,
	Error_NoWater = 2,
	Error_NoSugar = 3,
	Error_NoMilk = 4
	

};

class ICoffeeMachine {
public:
	virtual ~ICoffeeMachine() {}
	virtual bool MakeAmericano(bool make) = 0;
	virtual bool MakeLatte(bool make) = 0;

};

class ICoffeeMachineRecipe {
public:
	virtual ~ICoffeeMachineRecipe() {}
	virtual bool SetAmericanoRecipe(uint32_t coffee, uint32_t water, uint32_t sugar, uint32_t milk) = 0;
	virtual bool SetLatteRecipe(uint32_t coffee, uint32_t water, uint32_t sugar, uint32_t milk) = 0;
};

class CoffeeMachine : public ICoffeeMachine, public ICoffeeMachineRecipe {
public:
	CoffeeMachine(uint32_t coffee, uint32_t water, uint32_t sugar, uint32_t milk):
		m_CoffeMachineCoffee(coffee),
		m_CoffeMachineWater(water),
		m_CoffeMachineSugar(sugar),
		m_CoffeMachineMilk(milk)
		
	{}

	~CoffeeMachine() {}

	void getErrCoffeMachineCoffee() const {

		if (m_CoffeMachineCoffee == 0 || m_CoffeMachineCoffee < 50) {

			throw m_errCoffe;
		}

	}

	void getErrCoffeMachineWater() const {

		if (m_CoffeMachineWater == 0 || m_CoffeMachineWater < 70) {

			throw m_errWater;
		}
	}

	void getErrCoffeMachineSugar() const {

		if (m_CoffeMachineSugar == 0 || m_CoffeMachineSugar < 20) {

			throw m_errSugar;
		}
	}

	void getErrCoffeMachineMilk() const {

		if (m_CoffeMachineMilk == 0 || m_CoffeMachineMilk < 160) {

			throw m_errMilk;
		}

	}
	
	bool SetAmericanoRecipe(uint32_t coffee, uint32_t water, uint32_t sugar, uint32_t milk) override
	{
		if ((m_CoffeMachineCoffee != 0 && m_CoffeMachineCoffee > 50) && (m_CoffeMachineWater != 0 && m_CoffeMachineWater > 100) && (m_CoffeMachineSugar != 0 && m_CoffeMachineSugar > 20) && (m_CoffeMachineMilk != 0)) {
			if ((coffee == 70) && (water == 120) && (sugar == 20 || sugar == 0) && (milk == 0)) {

				m_CoffeMachineCoffee = m_CoffeMachineCoffee - coffee;
				m_CoffeMachineWater = m_CoffeMachineWater - water;
				m_CoffeMachineSugar = m_CoffeMachineSugar - sugar;
				m_CoffeMachineMilk = m_CoffeMachineMilk - milk;

				return true;

			}

			else
			{
				return false;

			}
		}
		else
		{
			std::cout << "Status: One of the ingredients is missing!" << std::endl;
			return false;
		}

	}

	bool MakeAmericano(bool make) override
	{
		if (make) {

			std::cout << "Status: Your coffe Americano is ready!" << std::endl;
			return true;
		}

		else
		{
			std::cout << "Status: Components don't match the recipe, coffe americano,\n or ingredient is missing!" << std::endl;
			return false;
		}

	}

	bool SetLatteRecipe(uint32_t coffee, uint32_t water, uint32_t sugar, uint32_t milk) override
	{
		if ((m_CoffeMachineCoffee != 0 && m_CoffeMachineCoffee > 50) && (m_CoffeMachineWater != 0 && m_CoffeMachineWater > 100) && (m_CoffeMachineSugar != 0 && m_CoffeMachineSugar > 20) && (m_CoffeMachineMilk != 0) && m_CoffeMachineMilk > 160) {
			if ((coffee == 50) && (water == 70) && (sugar == 20 || sugar == 0) && (milk == 160)) {

				m_CoffeMachineCoffee = m_CoffeMachineCoffee - coffee;
				m_CoffeMachineWater = m_CoffeMachineWater - water;
				m_CoffeMachineSugar = m_CoffeMachineSugar - sugar;
				m_CoffeMachineMilk = m_CoffeMachineMilk - milk;

				return true;
			}

			else
			{
				return false;
			}
		}

		else
		{
			std::cout << "Status: One of the ingredients is missing!" << std::endl;

			return false;
		}

	}

	bool MakeLatte(bool make) override
	{
		if (make) {

			std::cout << "Status: Your coffe Latte is ready!" << std::endl;
			return true;
		}

		else
		{
			std::cout << "Status: Components don't match the recipe, coffee Latte,\n or ingredient is missing!" << std::endl;
			return false;
		}

	}

	void getCoffeeIngredients() {

		std::cout << "Coffe: " << m_CoffeMachineCoffee << std::endl;
		std::cout << "Water: " << m_CoffeMachineWater << std::endl;
		std::cout << "Sugar: " << m_CoffeMachineSugar << std::endl;
		std::cout << "Milk: " << m_CoffeMachineMilk << std::endl;
	}

private:

	uint32_t m_CoffeMachineWater = 0;
	uint32_t m_CoffeMachineSugar = 0;
	uint32_t m_CoffeMachineMilk = 0;
	uint32_t m_CoffeMachineCoffee = 0;
	
	TypeError m_errCoffe = TypeError::Error_NoCoffee;
	TypeError m_errWater = TypeError::Error_NoWater;
	TypeError m_errSugar = TypeError::Error_NoSugar;
	TypeError m_errMilk = TypeError::Error_NoMilk;
	
};


int main()
{ 
	std::cout << "<< Coffee Machine is make Americano and Latte. >>\n"
		"Error codes :\n"
		"Error_NoCoffee = 1,\n"
		"Error_NoWater = 2,\n"
		"Error_NoSugar = 3,\n"
		"Error_NoMilk = 4\n";
	
	CoffeeMachine cm(400, 400, 400, 400); //load inredients 
		
	std::cout << std::endl;
	std::cout << "Ingredients loaded: " << std::endl; 
	cm.getCoffeeIngredients(); //showing how much ingredients loaded.
	std::cout << std::endl;
	 //exception catch block
		try
		{
			cm.getErrCoffeMachineCoffee();
			cm.getErrCoffeMachineWater();
			cm.getErrCoffeMachineSugar();
			cm.getErrCoffeMachineMilk();
		}

		catch (const TypeError& err)
		{
			std::cout << "Ahtung! Ahtung! Code error: " << (int)err  << std::endl;
		}
	// Americano coffee recipe
	std::cout << std::endl;
	std::cout << "A cup of Americano coffee contains: Coffee: 70g, Water: 120g, Sugar: 20g or 0g, Milk: 0g." << std::endl;
	cm.MakeAmericano(cm.SetAmericanoRecipe(70, 120, 20, 0)); // first arg: coofee, second arg: water,third arg: sugar, fourth arg: milk 	                                                       
	std::cout << std::endl;

	// Latte coffee recipe
	std::cout << "A cup of Latte coffee contains: Coffee: 50g, Water: 70g, Sugar: 20g or 0g, Milk: 160g." << std::endl;
	cm.MakeLatte(cm.SetLatteRecipe(50, 70, 20, 160));  // first arg: coofee, second arg: water, third arg: sugar, fourth arg: milk 
	std::cout << std::endl;
	
	std::cout << "A cup of Latte coffee contains: Coffee: 50g, Water: 70g, Sugar: 20g or 0g, Milk: 160g." << std::endl;
	cm.MakeLatte(cm.SetLatteRecipe(50, 70, 20, 160));  // first arg: coofee, second arg: water, third arg: sugar, fourth arg: milk 
	std::cout << std::endl;


	

	std::cout << "Remaining ingredients: " << std::endl; //showing how much ingredients remaining.
	cm.getCoffeeIngredients();


		return 0;
}
