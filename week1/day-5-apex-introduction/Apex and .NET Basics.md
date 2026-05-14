## 1.Map .NET Concepts to the Lightning Platform

	public class AccountUtils {
	
		public static List<Account> accountsByState(String state){
		
			 List<Account> accList=[SELECT Id, Name FROM Account WHERE BillingState = :state];
			 
	    	 return accList;
			 
		}
		
	}

---

##  2.Understand Execution Context

## AccountTriggerHandler

	public class AccountTriggerHandler {
    
   		public static void CreateAccounts (List<Account> accList)
   
    	{
	         for(Account acc : accList)
	         {
	             if(acc.ShippingState!=acc.BillingState)
	             {
	                 acc.ShippingState = acc.BillingState;
	             }
	         }
    	}

	}

---

## AccountTrigger on Account

	trigger AccountTrigger on Account (before insert) 

	{

     	if (Trigger.isBefore && Trigger.isInsert) {
	 
			AccountTriggerHandler.CreateAccounts(Trigger.new);		
		}	
		
	}

---

## AccountTriggerTest

	@isTest
	
	public class AccountTriggerTest { 
	
	    @isTest static void TestCreate200Records(){ 
		
	        List<Account> accts = new List<Account>();

			
	        for(Integer i=0; i < 200; i++) {
			
	            Account acct = new Account(Name='Test Account ' + i, BillingState = 'CA');
				
	            accts.add(acct);
				
	        }
			
	        Test.startTest();
			
	        insert accts;
			
	        Test.stopTest();
			
	        System.assertEquals(200, [SELECT Count() FROM Account WHERE ShippingState = 'CA' ]);
			
	    }
		
	}
