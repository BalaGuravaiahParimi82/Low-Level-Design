### SOLID Design Principles

- S -- Single Responsible Principle(SRP)
- O -- Open/Closed Principle(OCP)
- L -- Liskow Substitution Principle
- I -- Interface Seggregation Principle(ISP)
- D -- dependency Inversion Principle. 


#### Single Responsibility Principle(SRP) :

A class should have single Reason to Change.

A class which is not following SRP is below.

- has a logic to calculate price(logic might change in future) 
- has a logic to print invoice(logic might change in future)
- has a logic to save data to db(logic might change in future)

For multiple reasons you are making changes in single class which is not recomended. we need to change class only for a single reason/purpose.

Making changes in Invoice class each and every time for multiple reasons like while changing price logic, while making printing invoice changes, which making db chnages.

- - single --> Multiple

##### Marker.java
```java
package com.demo.S;

public class Marker {
	
	String name;
	String colour;
	int year;
	int price;
	
	public Marker(String name, String colour, int year, int price)
	{
		this.name = name;
		this.colour = colour;
		this.year = year;
		this.price = price;
	}
}

```
##### Invoice.java
```java
package com.demo.S;

public class InVoice {
	
	private Marker marker;
	private int quantity;
	
	public InVoice(Marker marker, int quantity)
	{
		this.marker = marker;
		this.quantity = quantity;
	}
	
	public int calculateTotal()
	{
		int price = marker.price * this.quantity;
		return price;
	}
	
	public void printInvoice()
	{
		// Print the Invoice
	}
	
	public void saveToDB()
	{
		// Save the data into DB
	}
}
 ```


 Here is the code which has single reason for each class.

##### InvoiceDAO.java
 ```java

 package com.demo.S;

public class InVoiceDAO {
	
	InVoice inVoice;
	
	public InVoiceDAO(InVoice inVoice)
	{
		this.inVoice = inVoice;
	}
	
	public void saveToDB()
	{
		// Save into the DB
	}

}

```
##### InvoicePrinter.java
```java
package com.demo.S;

public class InVoicePrinter {
	
	private InVoice inVoice;
	
	public InVoicePrinter(InVoice inVoice)
	{
		this.inVoice = inVoice;
	}	
}
```

From the above code we don't need to touch InVoice frequently.

- Take Invoice Object and make print it seperately.
- Take InVoice Object and Make DB Changes sepeartely.
- In Invoice Class Itself Make changes for calculating logic.

- - single -> single

- Simply, In Spring Boot purspective we have Controller, Business, Data Layer seperately which is a Layered architecture.





