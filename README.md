# Token---DIO-e-Binance---Blockchain-Developer-with-Solidity-

Para o projeto de criação do token nos padrões ERC20, utilizei como base o passo a passo do <https://ethereum.org/pt/developers/tutorials/erc20-annotated-code/#functions-that-modify-token-information/> junto aos conhecimentos adquiridos no bootcamp. 


![image](https://github.com/user-attachments/assets/2d9e8c9f-17bf-488d-8eac-e83459dd17e5)


```

// SPDX-License-Identifier: MIT
// OpenZeppelin Contracts v4.4.0 (utils/Context.sol)

pragma solidity ^0.8.20;


import "@openzeppelin/contracts/utils/Context.sol";
import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
import "@openzeppelin/contracts/utils/math/SafeMath.sol";

contract Money is Context, IERC20 {

    
    using SafeMath for uint256;
    mapping (address => uint256) private _balances;
    mapping (address => mapping (address => uint256)) private _allowances;
    uint256 private _totalSupply;
    string private _name;
    string private _symbol;
    uint8 private _decimals;


    constructor ()  {
        _name = "Money";
        _symbol = "MONEY";
        _decimals = 18;
         _totalSupply = 10000 * (10 ** uint256(_decimals));
        _mint(msg.sender, _totalSupply);
    }

    function name() public view returns (string memory) {
        return _name;
    }

    function symbol() public view returns (string memory) {
        return _symbol;
    }


    function decimals() public view returns (uint8) {
        return _decimals;
    }


    function totalSupply() public view override returns (uint256) {
        return _totalSupply;
    }


    function balanceOf(address account) public view override returns (uint256) {
        return _balances[account];
    }


    function transfer(address recipient, uint256 amount) public virtual override returns (bool) {

        _transfer(_msgSender(), recipient, amount);
        return true;
    }

    function allowance(address owner, address spender) public view virtual override returns (uint256) {
        return _allowances[owner][spender];
    }

    function approve(address spender, uint256 amount) public virtual override returns (bool) {

        _approve(_msgSender(), spender, amount);
        return true;
    }


    function transferFrom(address sender, address recipient, uint256 amount) public virtual override returns (bool) {
        _transfer(sender, recipient, amount);

        _approve(sender, _msgSender(), _allowances[sender][_msgSender()].sub(amount,
             "ERC20: transfer amount exceeds allowance"));
        return true;
    }


    function increaseAllowance(address spender, uint256 addedValue) public virtual returns (bool) {
        _approve(_msgSender(), spender, _allowances[_msgSender()][spender].add(addedValue));
        return true;
    }


    function decreaseAllowance(address spender, uint256 subtractedValue) public virtual returns (bool) {
        _approve(_msgSender(), spender, _allowances[_msgSender()][spender].sub(subtractedValue,
                "ERC20: decreased allowance below zero"));
        return true;
    }

    function _transfer(address sender, address recipient, uint256 amount) internal virtual {

        require(sender != address(0), "ERC20: transfer from the zero address");
        require(recipient != address(0), "ERC20: transfer to the zero address");
        _beforeTokenTransfer(sender, recipient, amount);
        _balances[sender] = _balances[sender].sub(amount, "ERC20: transfer amount exceeds balance");
        _balances[recipient] = _balances[recipient].add(amount);
        emit Transfer(sender, recipient, amount);

    }
    

    function _approve(address owner, address spender, uint256 amount) internal virtual {
        require(owner != address(0), "ERC20: approve from the zero address");
        require(spender != address(0), "ERC20: approve to the zero address");

        _allowances[owner][spender] = amount;
                emit Approval(owner, spender, amount);
    }


    function _mint(address account, uint256 amount) internal virtual {
        require(account != address(0), "ERC20: mint to the zero address");
        _beforeTokenTransfer(address(0), account, amount);
        _totalSupply = _totalSupply.add(amount);
        _balances[account] = _balances[account].add(amount);
        emit Transfer(address(0), account, amount);
    }

    function _burn(address account, uint256 amount) internal virtual {
        require(account != address(0), "ERC20: burn from the zero address");

        _beforeTokenTransfer(account, address(0), amount);

        _balances[account] = _balances[account].sub(amount, "ERC20: burn amount exceeds balance");
        _totalSupply = _totalSupply.sub(amount);
        emit Transfer(account, address(0), amount);
    }

    function mint(address account, uint256 amount) public {
    _mint(account, amount);}
 
    function _beforeTokenTransfer(address from, address to, uint256 amount) internal virtual { }
}



```

Terminal do Remix após a conclusão: 

![image](https://github.com/user-attachments/assets/1683d6e2-ae5a-4f2b-b3b4-48cb46e6c583)



![image](https://github.com/user-attachments/assets/3ac72c75-9176-4f76-ae83-1f590b491742)


Exemplo de funções implementadas ao token: 

![image](https://github.com/user-attachments/assets/6a113e5b-3562-46ca-b1a9-8981e2ca7a34)


![image](https://github.com/user-attachments/assets/a0d7ba3b-802f-4d5a-ab51-699a79d10552)


![image](https://github.com/user-attachments/assets/ee9626b4-bf51-48a6-b8ac-43ef8e93cef0)

Como resultado, o token Money foi criado
:)
