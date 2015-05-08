# FirstProject
class Bank {
	public static void main(String[] args) {
		
		
		Customer hampus = new Customer("Hampus Svens", "9238890231");
		Account hampusAcc = hampus.getAccount();
		CreditCard hampusCard1 = new MasterCard("1234 5678 1234 5678", "MasterCard", hampusAcc);
		hampus.addCreditCard(hampusCard1);
		System.out.println(hampus);
		
		System.out.println("Account Amount " + hampusAcc.getAmount());
		hampusCard1.makePayment(100);
		System.out.println("Account Amount " + hampusAcc.getAmount());
		hampusAcc.addMoney(3000);
		System.out.println("Account Amount " + hampusAcc.getAmount());
		hampusCard1.makePayment(1300);
		System.out.println("Account Amount " + hampusAcc.getAmount());
	}
}
