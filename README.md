# Blockchain-bank-KYC-part1




pragma solidity ^0.5.0;

///contract is a keyword 

/// @title bacnk KYC with delegation.
contract bank_KYC {
    
    struct Customer {
        string userName;   
        string data;  
        address bank;
    }
    
    struct Bank {
        string name;
        address ethAddress;
        string regNumber;
    }

    mapping(string => Customer) customers;

    mapping(address => Bank) banks;

    
	///add function to add a customer 
    function addCustomer(string memory _userName, string memory _customerData) public {
        require(customers[_userName].bank == address(0), "Customer is already present");
        customers[_userName].userName = _userName;
        customers[_userName].data = _customerData;
        customers[_userName].bank = msg.sender;
    }
   ///update function to update a customer  details  
    function modifyCustomer(string memory _userName, string memory _newcustomerData) public {
        require(customers[_userName].bank != address(0), "No data found  related to  input Customer in  database");
        customers[_userName].data = _newcustomerData;
    }    
    
///remove function to remove a customer   
    function removeCustomer(string memory _Name) public{
        require(customers[_Name].bank != address(0), "This customer is not present in the database");
        delete customers[_Name];
        
    }
	
	
	 ///view function  to see the details 
    function viewCustomer(string memory _userName) public view returns (string memory, string memory, address) {
        require(customers[_userName].bank != address(0), "No data found related to inpuut Customer name");
        return (customers[_userName].userName, customers[_userName].data, customers[_userName].bank);
    }
   
    
}
