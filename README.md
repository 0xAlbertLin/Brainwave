# Brainwave
For Self-Study Project  

基礎為兩塊Arduino  

藍芽有接收和發送兩邊的訊號  
藍芽接收腦波儀的資訊  
藍芽發送訊號控制Arduino  

WIFI連接至路由器  
將Arduino配置與GoogleSheet綁定  
即可讓使用者在使用腦波儀控制Arduino時，將腦波資訊即時上傳至GoogleSheet  
用其內建套建即可製作出可視化波型圖  

因發現訊號WIFI與藍芽無法共同使用  
原因可能為:  
1.Arduino的電路設計 藍芽及WIFI是走同一個通道  
2.藍芽及WIFI和馬達同時使用瞬間電流過大，導致訊號斷線  

因此使用穩流的電路板及更大的供電系統12V，而供電系統藍芽及WiFi各自獨立。  

但是斷線還是會發生若依循開機順序先將藍芽連線至腦波儀  
再將WIFI與路由器連線則可避免斷線發生  

但若開機這麼繁瑣並不適用於產品  

研究契機:發現有學校和醫院使用遊玩遊戲的方式來觀察過動症小朋友的腦波狀態，並訓練其專注度。  
而在自己有限資源中，也嘗試使用燒錄程式至晶片，  
由於時間限制及屢屢失敗，再交件期限內使用自己較熟悉的Arduino的方法解決。  
雖然發現訊號斷線的問題，最後使用兩個Ardiuino及兩個供電系統來穩定，  
分別各自處理藍芽訊號與WiFi的問題，在使兩者Arduino進行溝通上傳訊號至GoogleSheet中。  
