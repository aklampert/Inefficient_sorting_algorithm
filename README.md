public class Sort2 {

	public static void main(String[] args){
	
	//The purpose of this code was for learning puproses strictly. It is too inefficient for any serious use
	//I had an idea I wanted to implement, regardless of it's inefficiencies
	//Forced me to get better at method writing and how to manipulate arrays
	//Note that for 100,000 elements in array, it took about 15 seconds for this algorithm to sort
	//Method descriptions yet to come
		int[] array = {93, 4, 18, 84, 96, 3, 3, 4, 12, 9, 78, 49, 101, 249, 15};

		for(int e : sort2lg(array)) System.out.print(e + " ");
	}	
	
	/*public static int[] sort2lg(int[] array){
    This commented out piece was another algorithm I was attempting. It is unbelievably ineffecient for arrays of LARGE length
		int[] sort = new int[array.length];
		int[] simArray = array;

		for(int i = 0; i<array.length; i++){
			if(simArray.length <=1) break;
			int x=findAllInstances(simArray, min(simArray));
			if(x>1){
				int j=0;
				for(j = 0; j<x; j++){
					sort[i+j] = min(simArray);
				}
				simArray = copyDecr(simArray, min(simArray));
				i+=j-1;
			} 
			else{
				sort[i] = min(simArray);
				simArray = copyDecr(simArray, min(simArray));
			}
		}
		
		sort[sort.length-1] = simArray[0];		
		return sort;
  	}
  	*/
  
  	//method that returns an array ordered from least to greatest
 	 public static int[] sort2lg(int[] array){
		int index;
		int temp;
		int count;
		
		for(int i=0; i < array.length; i++){
			
			int[] playArray = new int[array.length - i];
			
			for(int j = i; j < array.length; j++){
				playArray[j-i] = array[j];
			}
			
			if(i == array.length - 1) break;
			
			count = findAllInstances(array,min(playArray));
			if(count > 1){
				int[] temps = new int[count];
				int[] y = findAllIndexes(array,min(playArray));
				for(int j=0; j < count; j++){
					temps[j] = array[i+j];
					array[i+j] = min(playArray);
					array[y[j]] = temps[j];
					i = i+j;
				}
			}
			else{
				index = findIndex(array, min(playArray));
				temp = array[i];
				array[i] = min(playArray);
				array[index] = temp;
			}
		}
		return array;

	}
	
	/*public static int[] copyDecr(int[] array, int key){
		int[] newArray = new int[0];
		int k = 0;
		while(k<array.length){
			if(array[k]==key){
				k++;
				continue;
			}

			newArray = copyAdd(newArray,1);
			newArray[newArray.length-1] = array[k];
			k++;
		}
		return newArray;
	}
  	*/
  
 	 //method that returns an array of indexes corresponding to an element's appearance in an array
		public static int[] findAllIndexes(int[] array, int key){
			int[] indexes = new int[1];
			int count = findAllInstances(array, key);
			if(count > 1){
				indexes = copyAdd(indexes, count-1);
				int k = 0;
				int j = 0;
				while(k<array.length){
					if(array[k]==key){
						indexes[j] = k;
						j++;
					}
					k++;
				}
			}
			else{
				for(int i = 0; i<array.length; i++){
					if(array[i]==key) {
          					indexes[0] = i;
          					break;
        				}
				}
			}
			return indexes;
		}
	
  	//method that counts the amount of times an element appears in array
		public static int findAllInstances(int[] array, int key){
			int count = 0;
			for(int i = 0; i<array.length; i++){
				if(key==array[i]) count++;
			}
			return count;	
		}
	
  	//method that returns an array with length increase of given size
		public static int[] copyAdd(int[] array, int size){
			int[] newArray = new int[array.length+size];
    
    			if(size < 0) newArray = array;
    			else{
		  		for(int i = 0; i<array.length;i++){
			  		newArray[i] = array[i];
		  		}
				array=newArray;
    			}
			return array;
		}
	
 	 //method that returns the first index (or only index if no repeats) an specific element in an array
 	 //Returns -1 if the element is not in the array
 	 public static int findIndex(int[] array, int key){
		int index = -1;
		for(int i = 0; i < array.length; i++){
			if(array[i] == key){
				index = i;
				break;
			}
		}
		return index;
	}
  
  	//method that returns the minimum of an array
	public static int min(int[] array){
		int k=0;
		int min=min(array[0],array[1]);
		while(k < array.length ){
			if(k <= array.length - 3){
				int temp = min(min, array[k+2]);
				if(temp < min) min = temp;
			}
			else break;
			k++;
		}
		return min;
	}
	
	//method which returns the minimum of two given integers
  	public static int min(int a, int b){
		if(a>=b) return b;
		else return a;
	}
}

