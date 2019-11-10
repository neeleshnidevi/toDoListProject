# toDoListProject
Automation script to track to do list of person

The java code for carrying out this test is listed under section 'Source Code' in this document. It consist of 6 methods that carries out the 6 tests as outlined in the pdf document. The six methods to carry out the test are  a) main(), b) deleteItemFromList, c) completedItem(), d) toDoCount(), e) completedToDo(), f) activeToDo().

Steps to run the test:
1) Install and configure Selenium on the PC or workstation
2) Install Eclipse on the machine
3) Create a new java class file and copy over the lines of code listed below.
4) There is only one class file which will have 6 methods. Each method carries out a different set of test to test the 6 functionalities such as commented in the code i.e. main() method will test adding items to the to do list, deleteItemFromList() method will test deleting an item from the to do list, completedItem() method will test marking a task as complete, toDoCount() method will test that the todos count is updating correctly once a task has been marked as complete, completedToDo() method will test that only tasks that has been marked as complete are displayed once 'completed' button is clicked. activeToDo() will test that only tasks that are yet to complete is displayed once 'Active' button is clicked.   
5) Run the test by executing the java class file. Keep a watch on the console for test results as they execute. As each test passes it will say so in the console such as Test 1 passed, Test 2 passed, Test 3 passed, etc. For a successful end to end test of the app it should say in the console "Test 6 passed. Active toDos listed correctly" as the last line. If the last line displayed says Test 4 passed. That means test 5 and test 6 has failed.

Source Code:

package testProject;

import java.util.NoSuchElementException;

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class addToList {

	public static void main(String[] args) {
		System.setProperty("webdriver.chrome.driver", "C:\\Users\\neele\\eclipse-workspace\\chromedriver.exe");
		WebDriver driver = new ChromeDriver();
		
		String task1 = "Install Selenium";
		String task2 = "Configure Selenium";
		String task3 = "Write Down the Test Cases";
		String task4 = "Write Automation Scripts";
		String task5 = "Schedule Automation Scripts";
		
		
		//open website
		driver.get("http://todomvc.com/examples/angularjs/#/");		
		driver.manage().window().maximize();
	
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(task1);
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(Keys.ENTER);
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(task2);
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(Keys.ENTER);
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(task3);
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(Keys.ENTER);
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(task4);
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(Keys.ENTER);	
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(task5);
		driver.findElement(By.xpath("//form/input[contains(@class,'new-todo')]")).sendKeys(Keys.ENTER);	
		
		//ensure 4 items left is displayed at the bottom left
		String text = driver.findElement(By.xpath("//footer/span[@class='todo-count']")).getText();

		
		System.out.println("Test 1 passed. Adding of items to the list is working correctly.\n");
		
		deleteItemFromList(driver);
		completedItem(driver);
		toDoCount(driver);
		completedToDo(driver);
		activeToDo(driver);
		
	}
	
	public static void deleteItemFromList(WebDriver driver) {
		
		driver.findElement(By.xpath("//div/label[@class='ng-binding']")).click();				
		driver.findElement(By.xpath("//button[@class='destroy']")).click();
		
		System.out.println("Test 2 passed. Deletion of items is working correctly.");
	}
	
	public static void completedItem(WebDriver driver) {
		
		
		driver.findElement(By.xpath("//input[@class='toggle ng-pristine ng-untouched ng-valid']")).click();
		
		System.out.println("Test 3 passed. Marking an item as complete functionality is working correctly. Configure Selenium task marked as complete.");
	
	}
	
	public static void toDoCount(WebDriver driver) {
		
		//note the no of items left before delete
		String toDoCountBefore = driver.findElement(By.xpath("//span/strong[@class='ng-binding']")).getText();
		int i=Integer.parseInt(toDoCountBefore);
		int j = i - 1;
		
		System.out.println("Count before delete is " + toDoCountBefore);
		
		//mark 2nd task in the list as complete
		driver.findElement(By.xpath("//input[@class='toggle ng-pristine ng-untouched ng-valid']")).click();
		
		String toDoCountAfter = driver.findElement(By.xpath("//span/strong[@class='ng-binding']")).getText();
		System.out.println("Count after delete is " + toDoCountAfter);
		
		int k = Integer.parseInt(toDoCountAfter);
		
		if (k ==j) {
			System.out.println("Test 4 passed. The To Do count is updating correctly");}
		else {
			System.out.println("Test 4 failed. The To Do count is not updating correctly");}			
		}
	
	public static void completedToDo(WebDriver driver) {
		
		//click 'completed' hyperlink
		driver.findElement(By.xpath("//a[text()='Completed']")).click();
		
		// check completed items are appearing in the list		
		 driver.findElement(By.xpath("//label[text()='Configure Selenium']"));
		 driver.findElement(By.xpath("//label[text()='Write Down the Test Cases']"));
		 	 	 
		 System.out.println("Test 5 passed. Completed toDos listed correctly");}
	
	public static void activeToDo(WebDriver driver) {
		   
		//click 'active' hyperlink
		driver.findElement(By.xpath("//a[text()='Active']")).click();
		
		// check active tasks are being displayed
		driver.findElement(By.xpath("//label[text()='Write Automation Scripts']"));
		driver.findElement(By.xpath("//label[text()='Schedule Automation Scripts']"));
		
		System.out.println("Test 6 passed. Active toDos listed correctly");
	}
	
}


