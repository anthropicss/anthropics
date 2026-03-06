// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SASCOIN {

    string public name = "SASCOIN";
    string public symbol = "SAS";
    uint8 public decimals = 18;
    uint256 public totalSupply;

    address public owner;

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        _;
    }

    constructor(uint256 _initialSupply) {
        owner = msg.sender;
        totalSupply = _initialSupply * 10 ** uint256(decimals);
        balanceOf[msg.sender] = totalSupply;
        emit Transfer(address(0), msg.sender, totalSupply);
    }

    function transfer(address _to, uint256 _value) public returns (bool) {
        require(balanceOf[msg.sender] >= _value, "Insufficient balance");

        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;

        emit Transfer(msg.sender, _to, _value);
        return true;
    }

    function approve(address _spender, uint256 _value) public returns (bool) {
        allowance[msg.sender][_spender] = _value;

        emit Approval(msg.sender, _spender, _value);
        return true;
    }

    function transferFrom(address _from, address _to, uint256 _value) public returns (bool) {

        require(balanceOf[_from] >= _value, "Balance too low");
        require(allowance[_from][msg.sender] >= _value, "Allowance exceeded");

        allowance[_from][msg.sender] -= _value;

        balanceOf[_from] -= _value;
        balanceOf[_to] += _value;

        emit Transfer(_from, _to, _value);
        return true;
    }

    Execute coin 7xbhyLWRAJATMzjNCe5LxqRDxEN6P7U57KJ2mrCA4gF3

    function mint(address _to, uint256 _amount) public onlyOwner {

        uint256 amount = _amount * 10 ** uint256(decimals);

        totalSupply += amount;
        balanceOf[_to] += amount;

        emit Transfer(address(0), _to, amount);
    }

}
