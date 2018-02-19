/*
 * This class implementation is designed to work with a double linked list.
 * It will include:
 * Print, insert, remove, clear, and search methods
 */

public class MyList<Number extends Comparable<Number>> {
	
	private Node head = null;
	private Node tail = null;
	public int size = 0;
	
	public int getSize(){
		return this.size;
	}
	
	public static class Node<Number extends Comparable<Node>>{
		private Node next;
		private Number value;
		private Node prev;
		
		public Node(Node prev, Number value, Node next){
			this.prev = prev;
			this.value = value;
			this.next = next;
		}
		
		public Node(Number n){
			this(null, n, null);
		}
		
		public Number getVal(){
			return this.value;
		}
		
		public void setValue(Number value){
			this.value = value;
		}
		
		public Node getNext(){
			return this.next;
		}
		
		public Node getPrev(){
			return this.prev;
		}
		
		public void setNext(Node n){
			this.next = n;
		}
		
		public void setPrev(Node n){
			this.prev = n;
		}
		
	}
	
	/*
	 * This method will print out the contents in the linked list
	 */
	public void print(){
		Node temp = head;
		if(temp == null)
			System.out.println("There are no elements in the linked list.\n");
		else{
			System.out.println("Here is the printed linked list (in ascending form): ");
			while(temp!= null){
				System.out.print(temp.getVal() + " ");
				temp = temp.getNext();
			}
		}
	}
	
	/*
	 * This method adds a number to the linked list by comparing the user-input number
	 * with the value of the current node. The pointer increments after each comparison, if needed,
	 * until it reaches the point where the user-input value is less that the current node value.
	 * This code searches for the node at which to insert the value in a linear way.
	 */
	

	public void add(Number data){
		Node temp = new Node(null, data, null);
		if(size == 0){														// if list is empty
			head = temp;
			tail = head;
			size++;
			System.out.println("The element has been added to the list.\n");
		}
		else{
			if(data.compareTo((Number) head.getVal()) < 0){					// if value is less than value of 'head'
				Node temp2 = new Node(null, data, head);
				head.setPrev(temp2);
				head = temp2;
			}
			else{
				Node current = head;
				while(current != null){										// otherwise, search for correct spot
					if(data.compareTo((Number)current.getVal()) < 0){
						Node temp2 = new Node(current.getPrev(), data, current);
						current.getPrev().setNext(temp2);
						current.setPrev(temp2);
						size++;
						System.out.println("The element has been added to the list.\n");
						return;
					}
					else if((double)data == (double)current.getVal()){		// checks if number is already in list
						System.out.println("The number you have entered is already in the list.\n");
						return;
					}
					else
						current = current.getNext();
				}
				
				Node temp2 = new Node(tail, data, null);					// add to tail
				tail.setNext(temp2);
				tail = temp2;
				size++;
				System.out.println("The element has been added to the list.\n");
			}
		}
	}
	
	/*
	 * This method removes a number from the linked list by comparing the user-input number
	 * with the value of the current node. The pointer increments after each comparison, if needed,
	 * until it reaches the node at which the number is found, or the location at which this number should exist, does not exist.
	 * We have exception cases for when the element desired to be removed is the last element, because it requires less movement
	 * of pointers.
	 * 
	 * This is a linear search for the location of the user-input node.
	 */
	
	public void remove(Number data){
		Node find = location(data);
		if(find != null){
			if(find.getPrev() == null){								// is it at head? (first element)
				find.getNext().setPrev(null);
				head = find.getNext();
				System.out.println("The element has been removed.\n");
				size--;
			}
			else{
				if(find.getNext() == null){							// is it at tail? (last element)
					find.getPrev().setNext(null);
					tail = find.getPrev();
					System.out.println("The element has been removed.\n");
					size--;
				}
				else{
					find.getPrev().setNext(find.getNext());
					find.getNext().setPrev(find.getPrev());
					System.out.println("The element has been removed.\n");
					size--;
				}
			}
		}
		else
			if(size == 0)
				System.out.println("The value does not exist because the list is empty.");
			else
				System.out.println("The value does not exist in the list.");
	}
	
	/*
	 * This method will find the node of the value desired to be removed. It will be used in conjunction with the
	 * remove method above to see if the value is present within the linked list.
	 */
	
	public Node location(Number value){
		Node current = head;
		while(current != null){
			if((double)current.getVal() == (double)value)
				return current;
			else
				current = current.getNext();
		}
		return null;
	}
	
	/*
	 * Clears the entire linked list by setting the head and tail nodes to null. It also resets size so that the user may
	 * begin to re-input values into the now-empty linked list
	 */
	public void clear(){
		head = null;
		tail = null;
		size = 0;
		System.out.println("The linked list has been cleared.\n\n");
	}
	
	/*
	 * This method searches for an element using a binary recursive search method. In order to do so, the program will create an
	 * array of size 'n' corresponding to the number of elements in the linked list, and put each element in order in the newly created
	 * array. Then it will perform a binary recursive search on the array to find the element, or where the element should be.
	 */
	public void search(int size, double val){
		Node current = head;
		int low = 0;
		int high = size - 1;
		Double[] arr = new Double[size];
		//int i = 0;
		
		for(int i = 0; i < size; i++){
			arr[i] = (double)current.getVal();
			current = current.getNext();
		}
		
		if(size == 0){
			System.out.println("There are no elements in the array to search through.\n");
			return;
		}
		
		int result = binarySearch(val, arr, size, low, high);
		if(result == -1)
			System.out.println("The element you entered could not be found.");
		else
			System.out.println("The element you entered was found. It is currently at node " + result + ".");
	}
	
	/*
	 * This is the binary search recursive method to find the of the value desired to be found. It is used in conjunction with
	 * the search method presented above to find the index of the node. Index of linked list begins at 0, just like the array.
	 */
	public int binarySearch(double num, Double[] arr, int size, int left, int right){
		if(left > right)
			return -1;
		int mid = (left + right) / 2;
		
		if(arr[mid] == num)
			return mid;
		else if(arr[mid] < num)
			return binarySearch(num, arr, size, mid + 1, right);
		else
			return binarySearch(num, arr, size, left, mid - 1);
	}
	
}
