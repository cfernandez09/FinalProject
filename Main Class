/*
 * Done by Caitlin Fernandez and Anna Sedlackova
 * Takes a string input and outputs anagrams that match the 1000 most common words in the English Dictionary.
 */

import java.util.Scanner;
import java.io.*;

public class FinalProject {

 /**
  * All fields for the class.
  */
 private static long startArrayInsert;
 private static long endArrayInsert;
 private static long startHashInsert;
 private static long endHashInsert;
 private static long startArraySearch;
 private static long endArraySearch;
 private static long startHashSearch;
 private static long endHashSearch;

 private static int tableSize = 1997; // Size of the hash table.
 private static int numWords = 0; // Stores number of words in the hash table.
 private static String[][] table = new String[tableSize][2];
 private static String fileName = "Dictionary.txt"; // Name of the file storing the dictionary.
 private static String[][] dictionary = new String[1000][2];
 private static String ln = null; // Line of the text editor.
 

 

 /**
  * DICTIONARY Converts a text file Dictionary.txt into an array of strings.
  */

 private static void toDictionary() {
  
   try {
   FileReader filereader = new FileReader(fileName);
   FileReader filereader2 = new FileReader(fileName);
   BufferedReader bufferedReader = new BufferedReader(filereader);
   BufferedReader bufferedReader2 = new BufferedReader(filereader2);
   int i = 0;

   startArrayInsert = System.currentTimeMillis();
   while ((ln = bufferedReader.readLine()) != null) {
    dictionary[i][0] = ln;
    i++;
   }
   endArrayInsert = System.currentTimeMillis();

   startHashInsert = System.currentTimeMillis();
   while ((ln = bufferedReader2.readLine()) != null) {
    insertIntoHashMap(ln);
    i++;
   }
   endHashInsert = System.currentTimeMillis();

   bufferedReader.close();
   bufferedReader2.close();
  } catch (FileNotFoundException ex) {
   System.out.println("Unable to open file '" + fileName + "'");
  } catch (IOException ex) {
   System.out.println("Error reading file '" + fileName + "'");
  }

 }

 /**
  * DATA STRUCTURE : Simple array
  * 
  * @param word
  * @return whether or not is the string contained within the dictionary
  */

 private static boolean searchArray(String word) {
  for (int i = 0; i < dictionary.length; i++) {
   if (dictionary[i][0] != null && word.compareTo(dictionary[i][0]) == 0 && dictionary[i][1] == null) {
     dictionary[i][1] = "printed";
     System.out.println(word);
     return true;
   }
  }
  return false;
 }

 /**
  * DATA STRUCTURE: Hash table
  * 
  * @param s
  * @return hashKey where input string is positioned
  */

 public static int insertIntoHashMap(String s) {
  int tempValue = 0;
  int j = 1;
  for (int i = 0; i < s.length(); i++)
   tempValue = tempValue + (s.charAt(i) - 'a');
  int hashKey = tempValue % tableSize;
  while (table[hashKey][0] != null) {
   hashKey = tempValue % tableSize + j;
   if (hashKey >= tableSize)
    hashKey = hashKey - tableSize;
   j++;
  }

  table[hashKey][0] = s;
  numWords++;
  return hashKey;
 }

 /**
  * DATA STRUCTURE: Hash table
  * 
  * @param s
  * @return returns where input string is positioned
  */
 public static int getHashKey(String s) { // Same as method above except it
            // does not place it into the
            // hash table.
  int tempValue = 0;
  for (int i = 0; i < s.length(); i++)
   tempValue = tempValue + (s.charAt(i) - 'a');
  int hashKey = tempValue % tableSize;
  return hashKey;
 }

 /**
  * DATA STRUCTURE: Hash table
  * 
  * @return number of words in the hash table
  */
 public int numberOfWords() {
  return numWords;
 }

 /**
  * DATA STRUCTURE: Hash table
  * 
  * @param myWord
  * @return searches for the match in the hash map
  */
 public static String searchHashMap(String myWord) {
  // compute the hash value of the given word
  int hashKey = getHashKey(myWord);
  int i = 0;
  while (i < tableSize && table[hashKey][0] != null && myWord.compareTo(table[hashKey][0]) != 0) {
   if (hashKey >= tableSize) {
    hashKey -= tableSize;
   }
   hashKey++;
   i++;
  }

  if (table[hashKey][0] != null && myWord.compareTo(table[hashKey][0]) == 0 && table[hashKey][1] == null) {
    table[hashKey][1] = "printed";
    System.out.println(table[hashKey][0]);
    return table[hashKey][0];
  } else
   return null;
 }

 /**
  * SCRAMBLE ALGORITHM FOR ARRAY
  * 
  * @param s
  */
 public static void findMatchesArray(String s) {
  startArraySearch = System.currentTimeMillis();
  findMatchesArray("", s);
  endArraySearch = System.currentTimeMillis();
 }
 
 /**
  * SCRAMBLE ALGORITHM FOR HASHTABLE
  * 
  * @param s
  */
 public static void findMatchesHash(String s) {
  startHashSearch = System.currentTimeMillis();
  findMatchesHash("", s);
  endHashSearch = System.currentTimeMillis();
 }

 /**
  * SCRAMBLE ALGORITHM FOR ARRAY
  * 
  * @param prefix
  * @param s
  */
 private static void findMatchesArray(String prefix, String s) {
  searchArray(prefix);
  if (s.length() != 0) {
   for (int i = 0; i < s.length(); i++) {
    findMatchesArray(prefix + s.charAt(i), s.substring(0, i) + s.substring(i + 1, s.length()));
   }
  }
 }
 
 /**
  * SCRAMBLE ALGORITHM FOR HASH TABLE
  * 
  * @param prefix
  * @param s
  */
 private static void findMatchesHash(String prefix, String s) {
  searchHashMap(prefix);
  if (s.length() != 0) {
   for (int i = 0; i < s.length(); i++) {
    findMatchesHash(prefix + s.charAt(i), s.substring(0, i) + s.substring(i + 1, s.length()));
   }
  }
 }

 /**
  * MAIN METHOD
  * 
  * @param args
  */
 public static void main(String[] args) {

  // Prompts user for a string to scramble
  Scanner scan = new Scanner(System.in);
  System.out.println("Enter your letters as a string without spaces in it: ");
  String s = scan.next();
  scan.close();

  // reads the dictionary
  FinalProject.toDictionary();

  // calls findMatches for prompted string by user
  System.out.println();
  System.out.println("Matches for array: ");
  FinalProject.findMatchesArray(s);
  System.out.println();
  System.out.println("Matches for hash table: ");
  FinalProject.findMatchesHash(s);

  System.out.println();
  // time for insertion for array
  System.out.println("Time for insertion for array: " + (endArrayInsert - startArrayInsert) + "ms");
  // time for insertion for hash table
  System.out.println("Time for insertion for hash table: " + (endHashInsert - startHashInsert) + "ms");
  // time for search for array
  System.out.println("Time for search for array: " + (endArraySearch - startArraySearch) + "ms");
  // time for search for hash table
  System.out.println("Time for search for hash table: " + (endHashSearch - startHashSearch) + "ms");
 }
}
