# Patron Proxy
http://www.newthinktank.com/2012/10/proxy-design-pattern-tutorial/


```plantuml
@startuml
class ATMMachine implements GetATMData, ATMState
class ATMProxy implements GetATMData, ATMState

 interface ATMState {
	+insertCard(): void 
	+ejectCard(): void 
	+insertPin(int pinEntered): void 
	+requestCash(int cashToWithdraw): void 
	
}
 interface GetATMData {
   getATMState(): ATMState
   setState(ATMState): void
   getCashInMachine(): int
}

class TestATMMachine {
  +main(final String[] args) : void
}
TestATMMachine *-- ATMMachine
TestATMMachine *-- ATMProxy
ATMProxy *-- ATMMachine
ATMMachine *-- "*" ATMState

	class HasCard implements ATMState
  
	class NoCard implements ATMState
	class HasPin implements ATMState
  class NoCash implements ATMState

note bottom of HasCard: public void insercard(ATMMachine machine) {\n machine.setState(new HasPin())\n} 
note left of ATMMachine: public void insertCard(){\n getATMState().insertCard()\n}

note right of ATMProxy: public void insertCard(){\n machine.insertCard()\n}
@enduml
```