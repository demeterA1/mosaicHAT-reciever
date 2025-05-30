1. Aby člověk mohl používat OSNMA, bude muset nejprve získat [PublicKey](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/nastaven%C3%AD_mosaicHAT/OSNMA/OSNMA_PublicKey_20240115100000_newPKID_1.crt) a [MerkleTree](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/nastaven%C3%AD_mosaicHAT/OSNMA/OSNMA_MerkleTree_20240115100000_newPKID_1.xml)\
aby jste získali merkle tree otevřete MerkleTree soubor a najděte TreeNode j4 a v něm x_ji to si zkopírujte a uložte

![How-to-apply-the-latest-GNSS-anti-spoofing-on-your-Septentrio14](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/pictures/How-to-apply-the-latest-GNSS-anti-spoofing-on-your-Septentrio14.jpg)

aby jste získali public key budete si muset stáhnout [OpenSSL Light](https://slproweb.com/products/Win32OpenSSL.html), aby jste z toho dostali potřebné data. v SSL napište a nezapomnějte změnit jméno soubor\
"openssl x509 -in "C:\Users\User\Downloads\OSNMA_PublicKey_20240115100000_newPKID_1.crt" -pubkey -noout -out key.pub"\
a teď stačí napsat "type key.pub" aby jste dostali Public key\
![publickey](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/pictures/publickey.jpg)


!!musíte vymazat CRLF (carriage return and line feed), který tam je navíc. Jinak vám to nepůjde!!
![extraline](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/pictures/extraline.jpg)

3. připojte mosaicHAT k počítači a otevřete [Septentrio](http://192.168.3.1/) stránky
nejprve zkontrolujte jestli máte správný firmware (4.14.4)\
[video jak to udělat](https://www.youtube.com/watch?v=bp8kNbzMl_c)
5. klikněte na GNSS -> OSNMA

6. OSNMA Configuration bude loose a NTP Client Configuration
 je OFF

7. klikněte na Advanced settings a zkopírujte tam Public Key a Merkle Tree, který jste si zkopírovali

8. klikněte OK

   ![septentrio](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/pictures/septentrio.jpg)

potrvá to pár minut než OSNMA naběhne

celý návod [here](https://www.ardusimple.com/how-to-apply-the-latest-gnss-anti-spoofing-on-your-septentrio-receiver/)
