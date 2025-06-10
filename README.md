⭐Godzilla AVAX Wallet Hunting V1

⤵哥斯拉区块链钱包助记词碰撞器/密钥碰撞器(AVAX链）

▶https://youtu.be/mL6wv_SzAz8

⬇https://mega.nz/file/iAM0yCZC#j-0MSoRy7X5stpL8qpr-PqePKq_B5BNOgyK2THSV6QY

这是一个用于生成和检查AVAX(Avalanche)链钱包地址的Python工具

## 核心功能
### 1. 助记词生成
工具使用 mnemonic 库生成符合BIP39标准的12个单词助记词：
def generate_mnemonic():
    """生成助记词"""
    mnemo = Mnemonic("english")
    return mnemo.generate(strength=128)

### 2. AVAX地址生成
通过 eth_account 库从助记词派生AVAX链地址：
def generate_avax_address(mnemonic):
    """生成AVAX链地址"""
    Account.enable_unaudited_hdwallet_features()
    acct = Account.from_mnemonic(mnemonic)
    return acct.address

### 3. 多线程钱包生成
使用QThread实现后台钱包生成：
class WalletWorker(QThread):
    update_signal = pyqtSignal(str, str, int)   
    def run(self):
        count = 0
        while self.is_running:
            mnemonic = generate_mnemonic()
            addr = generate_avax_address(mnemonic)        
            if addr:
                count += 1
                self.update_signal.emit(mnemonic, addr, count)
