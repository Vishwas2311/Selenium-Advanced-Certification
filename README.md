# Selenium-Advanced-Certification
//this is for Selenium Advanced certification 



package lambdatest;

import java.util.Iterator;
import java.util.List;
import java.util.Set;

import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;

public class Assignment {
public static void main(String[] args) throws InterruptedException {
	
	System.setProperty("webdriver.chrome.driver","V:\\chromedriver_win32\\chromedriver.exe");
	WebDriver driver=new ChromeDriver();
	driver.manage().window().maximize();
	driver.get("https://www.lambdatest.com/");
	
	WebDriverWait explicit= new WebDriverWait(driver, 10);
	List<WebElement> wait = explicit.until(ExpectedConditions.visibilityOfAllElementsLocatedBy(By.xpath("//a[.='See All Integrations']")));
	String Url=wait.get(0).getAttribute("href");
	System.out.println(Url);
	
	
	JavascriptExecutor java =(JavascriptExecutor)driver;
	java.executeScript("window.scrollBy(0,4000)");
	
	driver.findElement(By.xpath("//a[.='See All Integrations']")).sendKeys(Keys.CONTROL,Keys.ENTER);
	
	Set<String> windows=driver.getWindowHandles();
	Iterator <String> it= windows.iterator();
	String parent=it.next();
	String child =it.next();
	driver.switchTo().window(child);
	String newwindow = driver.getCurrentUrl();
	
	Assert.assertEquals(Url, newwindow);
	
	
	JavascriptExecutor scroll=(JavascriptExecutor)driver;
	scroll.executeScript("window.scrollBy(0,6000)");
	
	List<WebElement> Actual=driver.findElements(By.xpath("//div/div[4]/a"));
          Actual.get(2).click();
          String lambda=driver.getTitle();
          
          
    String Expected="Running Automation Tests Using TestingWhiz LambdaTest | LambdaTest";
	Assert.assertEquals(Expected, lambda);
	driver.close();
	
	driver.switchTo().window(parent);
	
	int count=0;
	while(it.hasNext()) {
		
		int url=  Integer.parseInt(it.next());
		count=count+url;
	}
	System.out.println(count);
	
	driver.navigate().to("https://www.lambdatest.com/blog/");
	Thread.sleep(1000);
	driver.findElement(By.xpath("//a[text()='Community'] [1]")).click();
	String currenturl=driver.getCurrentUrl();
	
	String Expected1 ="https://community.lambdatest.com/";
	
	Assert.assertEquals(currenturl, Expected1);
	
	driver.close();
	
}
}



