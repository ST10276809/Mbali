# Mbali T. Mtsweni ST10276089

Content Editor or IDE:
Open a content editor or an coordinates advancement environment (IDE) such as Visual Studio, Visual Studio Code, or JetBrains Rider.
Duplicate Code:
Duplicate the given code into a modern record inside your content editor or IDE. Spare the record with a .cs expansion, for illustration, RecipeProgram.cs.
Compile:
Since this can be a C# program, you wish to compile it some time recently running. On the off chance that you're utilizing an IDE like Visual Studio or JetBrains Rider, basically press the build or compile button. On the off chance that you're employing a content editor or command-line interface, you'll compile utilizing the C# compiler (csc). Open a command incite or terminal, explore to the catalog containing your .cs record, and run.
Run: After successfully compiling, you can run the program. If you're using an IDE, you can run it directly from the IDE. If you compiled using the command-line interface, run the executable by entering its name.
Interact: Once the program starts running, follow the on-screen instructions. You can choose options from the menu by entering the corresponding number and then providing any additional input as requested (e.g., recipe name, ingredient details, etc.).
Exit: To exit the program, choose option 5 from the menu.

        Recipe Book ingredients code of Part One

using System.Collections.Generic;
using System.Text.RegularExpressions;

namespace BookOfRecipes
{
    class Program
    {
        static Dictionary<string, List<Ingredient>> recipes = new Dictionary<string, List<Ingredient>>();
        static List<string> steps = new List<string>();

        static void Main(string[] args)
        {
            bool exit = false;

            while (!exit)
            {
                Console.WriteLine("\nWelcome to the Book Of Recipes");//The program starts with displaying a welcome message and a menu of options for the user.
                Console.WriteLine("1) Insert a new recipe");//Users may add a new recipe
                Console.WriteLine("2) View the recipe");//Option to view the recipe
                Console.WriteLine("3) The scale of the recipe");//User can enter the measurents
                Console.WriteLine("4) Reset the quantity of the ingredient");//User can start the ingredients over
                Console.WriteLine("5) Exit");
                string choice = Console.ReadLine();

                switch (choice)
                {
                    case "1":
                        EnterNewRecipe();//Prompts the user to input the name of the recipe. 
                        break;
                    case "2":
                        ViewRecipe();//Asks the user to view the recipe
                        break;
                    case "3":
                        RecipeScale();//Asks the user to enter the name of the recipe they want to scale
                        break;
                    case "4":
                        ResetIngredientQuantity();//Placeholder message indicates that the functionality to reset ingredient quantities is not fully implemented
                        break;
                    case "5":
                        exit = true;
                        break;
                    default:
                        Console.WriteLine("Incorrect input. Please try again.");
                        break;
                }
            }
        }

        static void EnterNewRecipe()
        {
            List<Ingredient> ingredients = new List<Ingredient>();//A new class for Ingredients

            Console.Write("Enter the name of the recipe: ");
            string recipeName = Console.ReadLine();

            Console.Write("Enter the number of ingredients: ");
            int ingredientCount = Convert.ToInt32(Console.ReadLine());

            for (int i = 0; i < ingredientCount; i++)
            {
                Console.WriteLine($"\nIngredient {i + 1}:");
                Console.Write("Name: ");
                string name = Console.ReadLine();

                Console.Write("Quantity (for example, '2 cups'): ");
                string quantity = Console.ReadLine();

                ingredients.Add(new Ingredient(name, quantity));
            }
            recipes.Add(recipeName, ingredients);

            Console.Write("\nEnter the number of steps: ");
            int stepCount = Convert.ToInt32(Console.ReadLine());

            for (int i = 0; i < stepCount; i++)
            {
                Console.WriteLine($"\nStep {i + 1}");
                Console.Write("Description: ");
                string description = Console.ReadLine();
                steps.Add(description);
            }
        }

        static void ViewRecipe()
        {
            Console.Write("Enter the name of the recipe: ");
            string recipeName = Console.ReadLine();

            if (!recipes.ContainsKey(recipeName))
            {
                Console.WriteLine("Recipe not found.");
                return;
            }

            Console.WriteLine($"\nRecipe: {recipeName}");
            Console.WriteLine("\nIngredients:");
            foreach (var ingredient in recipes[recipeName])
            {
                Console.WriteLine($"- {ingredient.Quantity} of {ingredient.Name}");
            }

            Console.WriteLine("\nSteps:");
            for (int i = 0; i < steps.Count; i++)
            {
                Console.WriteLine($"{i + 1}, {steps[i]}");
            }
        }

        static void RecipeScale()
        {
            Console.Write("Enter the name of the recipe: ");
            string recipeName = Console.ReadLine();

            if (!recipes.ContainsKey(recipeName))
            {
                Console.WriteLine("Recipe not found.");
                return;
            }

            Console.WriteLine("\nChoose a scaling factor - 0.5 (half), 2 (double), 3 (triple): ");
            double scaleFactor = Convert.ToDouble(Console.ReadLine());

            foreach (var ingredient in recipes[recipeName])
            {
                ingredient.ScaleQuantity(scaleFactor);
            }

            Console.WriteLine("The ingredients have been scaled!");
        }

        static void ResetIngredientQuantity()
        {
            // Implementation to reset ingredient quantities
            Console.WriteLine("Resetting ingredient quantities...");
        }

        class Ingredient
        {
            public string Name { get; private set; }
            private string originalQuantity;
            public string Quantity { get; private set; }

            public Ingredient(string name, string quantity)
            {
                Name = name;
                Quantity = originalQuantity = quantity;
            }

            public void ScaleQuantity(double scaleFactor)
            {

                string[] parts = Quantity.Split(' ');
                if (parts.Length != 2)
                {
                    Console.WriteLine("Invalid quantity format.");
                    return;
                }

                double amount;
                if (!double.TryParse(parts[0], out amount))
                {
                    Console.WriteLine("Invalid quantity format.");
                    return;
                }

                string unit = parts[1];
                amount *= scaleFactor;
                Quantity = $"{amount} {unit}";
            }

            public void ResetQuantity()
            {
                Quantity = originalQuantity;
            }
        }
    }
}
