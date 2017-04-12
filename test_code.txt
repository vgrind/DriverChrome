package test_test.pp.test;

import org.apache.commons.io.FileUtils;
import org.openqa.selenium.By;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

import java.io.File;
import java.io.IOException;

public class FirstTest {

    private WebDriver driver;

    @BeforeClass
    public void setUp() {
        driver = new ChromeDriver();
    }

    @Test // Marking this method as part of the test
    public void testLoginPass() throws InterruptedException, IOException {

        driver.get("http://the-internet.herokuapp.com/");
        driver.findElement(By.xpath("/html/body/div[2]/div/ul/li[18]/a")).click();
        // Find the text input element by its id and type "tomsmith"
        driver.findElement(By.id("username")).sendKeys("tomsmith");
        // Find the text input element by its id and type "SuperSecretPassword!"
        driver.findElement(By.id("password")).sendKeys("SuperSecretPassword!");
        // Click Login button
        driver.findElement(By.className("radius")).click();
        File scrFileAfter=((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
        FileUtils.copyFile(scrFileAfter, new File("c:\\test\\screenshotafter.png"));
    }

    @AfterClass
    public void quitDriver(){
        driver.quit();
    }

    }
