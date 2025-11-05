package oopsexp8og;

import java.util.Scanner;

class WordTask implements Runnable {
    private final String paragraph;
    WordTask(String paragraph) { this.paragraph = paragraph; }

    public void run() {
        String[] words = paragraph.trim().split("\\s+");
        for (String w : words) {
            System.out.println("[word]  " + w);
            try { Thread.sleep(2000); } catch (InterruptedException ignored) {}
        }
    }
}

class VowelTask implements Runnable {
    private final String paragraph;
    VowelTask(String paragraph) { this.paragraph = paragraph; }

    public void run() {
        String vowels = "aeiouAEIOU";
        for (char c : paragraph.toCharArray()) {
            if (vowels.indexOf(c) >= 0) {
                System.out.println("[vowel] " + c);
                try { Thread.sleep(2000); } catch (InterruptedException ignored) {}
            }
        }
    }
}

public class RunnableDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter paragraph:");
        String para = sc.nextLine();

        Thread word = new Thread(new WordTask(para), "word");
        Thread vowel = new Thread(new VowelTask(para), "vowel");

        word.start();
        vowel.start();
    }
}



Question 2:
package oopsexp8og;

import java.util.*;

class EvenTask implements Runnable {
    int arr[];
    EvenTask(int arr[]){ this.arr = arr; }

    public void run(){
        for(int x : arr){
            if(x % 2 == 0){
                System.out.println("[even] " + x);
                try{ Thread.sleep(2000); }catch(Exception e){}
            }
        }
    }
}

class OddTask implements Runnable {
    int arr[];
    OddTask(int arr[]){ this.arr = arr; }

    public void run(){
        for(int x : arr){
            if(x % 2 != 0){
                System.out.println("[odd]  " + x);
                try{ Thread.sleep(2000); }catch(Exception e){}
            }
        }
    }
}

public class ThreadArrayDemo {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int arr[] = new int[10];

        System.out.println("Enter 10 numbers:");
        for(int i=0;i<10;i++){
            arr[i] = sc.nextInt();
        }

        Thread even = new Thread(new EvenTask(arr), "even");
        Thread odd  = new Thread(new OddTask(arr), "odd");

        even.start();
        odd.start();
    }
}

Question 3:
package oopsexp8og;

import java.util.*;

class TableTask implements Runnable {
    int n;
    TableTask(int n){ this.n = n; }

    public void run(){
        for(int i=1;i<=10;i++){
            System.out.println("[table] " + n + " x " + i + " = " + (n*i));
            try{ Thread.sleep(2000);}catch(Exception e){}
        }
    }
}

class DivisorTask implements Runnable {
    int n;
    DivisorTask(int n){ this.n = n; }

    public void run(){
        for(int i=1;i<=n;i++){
            if(n % i == 0){
                System.out.println("[divisor] " + i);
                try{ Thread.sleep(2000);}catch(Exception e){}
            }
        }
    }
}

public class ThreadNumberDemo {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number: ");
        int num = sc.nextInt();

        Thread t1 = new Thread(new TableTask(num),"table");
        Thread t2 = new Thread(new DivisorTask(num),"divisor");

        t1.start();
        t2.start();
    }
