# FirstProject
class Bank {
	public static void main(String[] args) {
		
		
		Customer kalle = new Customer("Kalle Anka", "9238890231");
		Account kallesAcc = kalle.getAccount();
		CreditCard kallesCard1 = new MasterCard("1234 5678 1234 5678", "MasterCard", kallesAcc);
		hampus.addCreditCard(kallesCard1);
		System.out.println(kalles);
		
		System.out.println("Account Amount " + kallesAcc.getAmount());
		kallesCard1.makePayment(100);
		System.out.println("Account Amount " + kallesAcc.getAmount());
		kallesAcc.addMoney(3000);
		System.out.println("Account Amount " + kallesAcc.getAmount());
		kallesCard1.makePayment(1300);
		System.out.println("Account Amount " + kallesAcc.getAmount());
	}
}
import java.math.BigInteger;
import java.util.Random;

public class Account {
	
	private long accountNumber;
	private double amount = 0;
	
	public double getAmount() {
		return amount;
	}
	public void addMoney(double money) {
		amount = amount + money;
	}
	public boolean withdrawMoney(double money) {
		if (amount < money) {
			System.out.println("There is not enough money");
			return false;
		}
		amount = amount - money;
		System.out.println("Payment successed");
		return true;
		
	}
	
	public Account() {
		BigInteger b = new BigInteger(256, new Random());
		accountNumber = Math.abs(b.longValue());
		System.out.println("Account: "+accountNumber);
	}
}
public class Customer {
	
	private String personalNumber;	
	private String name;
	private Account customerAccount = null;
	private CardList customerCards = null;
	
	public Customer(String pn, String name, Account account, CardList cardList) {
		personalNumber = pn;
		this.name = name;
		customerAccount = account;
		customerCards = cardList;
	}
	
	public Customer(String pn, String name) {
		personalNumber = pn;
		this.name = name;
		customerAccount = new Account();
	}
	
	public Account getAccount() {
		return customerAccount;
	}
	
	public void pritntCustomerInfo() {
		String details = String.format("Name : %s \n PN: %s", name, personalNumber);
		System.out.println();
		//TODO Print info on CreditCards and Account
	}
	
	public boolean addCreditCard(CreditCard card) {
		if (customerCards == null) {
			customerCards = new CardList();
			card.showCard();
		}
		return customerCards.add(card);
	} 
}
public class Visa extends CreditCard{
	
	public Visa (String n, String t, Account acc) {
		super(n, t, acc);
		
	}
	public boolean makePayment(double money) {
		System.out.println("Trying to make payment "+money);
		return customerAccount.withdrawMoney(0.98 * money);
	}
}
public class MasterCard extends CreditCard{
	
	public MasterCard(String n, String t, Account acc) {
		super(n, t, acc);
		
	}
	public boolean makePayment(double money) {
		System.out.println(money);
		return customerAccount.withdrawMoney(money);
	}
}
abstract public class CreditCard {
	
	public String number;
	public String type;
	public Account customerAccount;
	
	
	
	public void showCard(){
		System.out.println("Number: "+number);
		System.out.println("Type: "+type);
	}
	
	public CreditCard(String n, String t, Account acc) {
		number = n;
		type = t;
		customerAccount = acc;
		//TODO implement
	}
	public abstract boolean makePayment(double amount);
}
public class CardList { 
	private CreditCard[] thecards = new CreditCard[3];
	
	public boolean add(CreditCard c){
		int i = 1;
		boolean freeSlot = false;
		while (i < thecards.length && !freeSlot)
			if(thecards[i] == null){
				thecards[i]=c;
				freeSlot = true;
				}
			else {
				i++;
			}
		if (i < thecards.length) {
			System.out.println("Card(s) in wallet: "+i);
			return false;
		}
		    System.out.println("No space left for new cards");
		return true;
	}
	
	public void printCards() {
		for (int i=0; i < thecards.length; i++) {
			if (thecards[i] != null) {
				System.out.println("Card: ");
			}
		}
	}
}
