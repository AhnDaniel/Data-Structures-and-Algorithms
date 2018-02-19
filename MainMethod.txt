/*
 * Main function. Outputs a menu function that allows user
 * to navigate between 5 options:
 * print, insert, remove, clear, search
 */

import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		
		System.out.println("This program allows the user to input values into a sorted linked list.");
		
		int choice;
		MyList list = new MyList();
		
		do{
			menu();													// calls menu function unless program is terminated
			Scanner input = new Scanner(System.in);
			
			while(!input.hasNextInt()){								// error check; input must be an int value
				System.out.println("\nInvalid input. Enter a number corresponding to the option you wish to choose:\n");
				menu();
				input = new Scanner(System.in);
			}
			choice = input.nextInt();
			
			switch(choice){
			case 1:
				list.print();
				System.out.println("\n");
				break;
			case 2:
				double num = verifyInput(1);
				list.add(num);
				break;
			case 3:
				double num2 = verifyInput(2);
				list.remove(num2);
				break;
			case 4:
				list.clear();
				break;
			case 5:
				double val = verifyInput(3);
				list.search(list.getSize(), val);
				break;
			case 6:
				choice = 6;
				break;
			default:
				System.out.println("Invalid option. Program will now terminate.");
				choice = 6;
			}
			
		}while(choice != 6);
		
		System.out.println("\nThe program has been terminated.");		// when user wishes to exit program
	}
	
	/*
	 * This method is simply to bring up the menu function again, instead of having to display it in main every time.
	 */
	public static void menu(){				// menu function
		
		System.out.print("Please enter the number corresponding to the option you wish to choose:\n\n"
				+ "Entering a value greater than 6 or less than 1 will automatically terminate the program.\n\n"
				+ "1.	Print the elements of the list\n"
				+ "2.	Insert an element\n"
				+ "3.	Remove an element\n"
				+ "4.	Empty the list\n"
				+ "5.	Search the list\n"
				+ "6.	Exit\n\n");
		
	}
	
	/*
	 * This method checks to see if the user enters a valid input when inserting/deleting/searching for an element. Valid input is 
	 * either:
	 * an integer value or decimal value because the program will convert all numbers to floating point decimals. This is why
	 * the return type is double. I made it like this so that it would be a lot easier to group numbers such as 2 and 2.0 to 
	 * be equivalent when comparing, because they would both become 2.0, and therefore comparison becomes simple.
	 */
	
	public static double verifyInput(int i){							// 'i' represents either insertion or deletion
		if(i == 1){														// insertion
			System.out.print("You have chosen to add an element.\n"
				+ "What number would you like to insert into the list?   ");
			Scanner input = new Scanner(System.in);
			double num = 0;
			
			while(!input.hasNextInt() && !input.hasNextFloat()){		// if the input is not an integer or decimal value
				System.out.println("You have entered an invalid number for insertion.\n"
						+ "Please enter either an integer or decimal value.   ");
				
				input = new Scanner(System.in);
			}
			
			String inpt = input.next();
			num = Double.parseDouble(inpt);
			
			return num;
		}
		else if(i == 2){												// deletion
			System.out.print("You have chosen to remove an element.\n"
					+ "What number would you like to remove from the list?   ");
				Scanner input = new Scanner(System.in);
				double num = 0;
				
				while(!input.hasNextInt() && !input.hasNextFloat()){		// if the input is not an integer or decimal value
					System.out.println("You have entered an invalid number for deletion.\n"
							+ "Please enter either an integer or decimal value.   ");
					
					input = new Scanner(System.in);
				}
				
				String inpt = input.next();
				num = Double.parseDouble(inpt);
				
				return num;
		}
		else{														// searching
			System.out.print("What value would you like to search for in the list?   ");
				Scanner input = new Scanner(System.in);
				double num = 0;
				
				while(!input.hasNextInt() && !input.hasNextFloat()){		// if the input is not an integer or decimal value
					System.out.println("You have entered an invalid number for searching.\n"
							+ "Please enter either an integer or decimal value.   ");
					
					input = new Scanner(System.in);
				}
				
				String inpt = input.next();
				num = Double.parseDouble(inpt);
				
				return num;
		}
	}
}
