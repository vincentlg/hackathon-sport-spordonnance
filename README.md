# hackathon-sport-spordonnance
Code du project Spordonnance - Hackathon sport

# Le consortium
3 noeuds validateurs maintenus par 3 mutuelles.
Implémentaiton:geth - Consensus:POA - Host:GCloud Tool:[hackathon-sport.rockside.io](https://hackathon-sport.rockside.io
![img consortium](https://github.com/vincentlg/hackathon-sport-spordonnance/blob/master/consortium.png)

# Les acteurs
Patricia - Médecin
0x2c68bfBc6F2274E7011Cd4AB8D5c0e69B2341309

Axelle - Patient ALD
0xbeEd6fd5407D63f178D39c21c1BC9A770bE9BfF4

Paul - Club sportif
0xDB1D171Ee83802ff5D48841EB96C63Ba4b94E8c9

Bob - Financeur
0xb189a2D8E7e88EbDC51B25869d5e491118D7B593

# Le Smart Contract
Déployé sur le consortium: 0x52436444ede8c4d18e585a6b3ab55727b5540d5e

```javascript
pragma solidity >=0.4.22 <0.6.0;

contract Spordonnance {

    mapping (address => bool) public eligiblePatient;
    mapping (address => bool) public workoutByPatient;
    mapping (address => address) public sportHallByPatient;
    mapping (address => mapping (address => bool)) public paidWorkout;

    event LogWorkoutHappen(address patient, address sportHall);

    function isEligible(address patient) public onlyDoctor {
        eligiblePatient[patient] = true;
    }
    
    function selectSportHall(address sportHall) public onlyPatient {
        require(eligiblePatient[msg.sender]);
        sportHallByPatient[msg.sender] = sportHall;
    }
    
    function validPatientWorkout(address patient) public onlySportHall {
        require(sportHallByPatient[patient] == msg.sender);
        workoutByPatient[patient] = true;
        
    }
    
    function notifyWorkoutIsPaid(address patient, address sportHall) public onlyhealthInsurance {
        paidWorkout[patient][sportHall] = true;
    }
    
    modifier onlyDoctor() {
        _;
    }
    modifier onlyPatient() {
        _;
    }
    modifier onlySportHall() {
        _;
    }
    modifier onlyhealthInsurance() {
        _;
    }
}
```

# L'application
Web3 & Metamask : Permet de démontrer 4 transactions sur le smart contract.









