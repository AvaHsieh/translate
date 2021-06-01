 Chapter 1. Web technologies and HTTP 第一章、網路科技與 HTTP 協定
This chapter covers
• How a web page is loaded by the browser
• What HTTP is and how it evolved up to HTTP/1.1 • The basics of HTTPS
• Basic HTTP tools
本章節涵蓋內容:
• 網頁是如何被瀏覽器載入的
• 什麼是 HTTP， 以及 HTTP 是如何從 1.1 進化成 2.0
• HTTPS 協定的基礎
• 基礎的 HTTP 工具
This chapter gives you background on how the web works today and explains some key concepts necessary for the rest of this book to make sense; then it introduces HTTP and the history of the previous versions. I expect many of the readers of this book to be at least somewhat familiar with a lot of what is discussed in this first chapter, but I encourage you not to skip it; use this chapter as an opportunity to refresh yourself on the basics. 本章節介紹了現代網路的背景知識，並解釋要讀懂這本書後面內容所需要的重要觀念。此外
還介紹 HTTP 的歷史和過去的版本。雖然我預期許多正在閱讀這本書的讀者對這一章的多數 內容有大概的認識，但我還是建議不要跳過本章節，用來複習回顧基本的概念。
1.1. How the web works 1.1. 網路如何運作
The internet has become an integral part of everyday life. Shopping, banking, communication, and entertainment all depend on the internet, and with the growth of the Internet of Things (IoT), more and more devices are being put online, where they can be accessed remotely. This access is made possible by several technologies, including Hypertext Transfer Protocol (HTTP), which is a key method of requesting access to remote web applications and resources. Although most people understand how to use a web browser to surf the internet, few truly understand how this technology works, why HTTP is a core part of the web, or why the next version (HTTP/2) is causing such excitement in the web community.

 網際網路已成為日常生活不可或缺的一部分。購物、銀行、通訊和娛樂皆仰賴網路，物聯網 普及和越來越多的電子器材有聯網的功能，讓使用者得以遠端操作。這些得以實現歸功於許 多技術，包括超文件傳輸協定(HTTP)，是讓使用者得以使用及取得遠端網路應用程式和資源 的關鍵技術之一。 儘管大多數人都會使用瀏覽器上網，但非常少人真正懂得底層的科技如 何運作、HTTP 為何是網路的核心，以及為何下一個版本(即 HTTP/2)讓網路社群如此引頸期 盼的原因。
1.1.1. The internet versus the World Wide Web
1.1.1. 網際網路(Internet) 全球資訊網路(World Wide Web)的差別 
For many people, the internet and the World Wide Web are synonymous, but it’s important to differentiate between the two terms.
對許多人而言，Internet 和 World Wide Web 是同義詞，但其實區分兩者的差別非常重要。
The internet is a collection of public computers linked through the shared use of the Internet Protocol (IP) to route messages. It’s made up of many services, including the World Wide Web, email, file sharing, and internet telephony. The World Wide Web (or the web), therefore, is but one part of the internet, though it’s the most visible part, and as people often look at email through web-mail front ends (such as Gmail, Hotmail, and Yahoo!), some of them use the web interchangeably with the internet. 網際網路(Internet)指的是整個透過網際網路協定(IP)傳遞訊息的公共電腦集體。由許多服務
所組成，包括全球資訊網路(World Wide Web)、電子郵件、檔案分享，以及網際網路電話。 全球資訊網路(World Wide Web)是屬於網際網路的一部分，同時也是最引人注意的服務。許 多人透過網站介面閱覽電子郵件(比如 Gmail、Hotmail、和雅虎)。部分人將 web 和 internet 兩字交替使用。
HTTP is how web browsers request web pages. It was one of the three main technologies defined by Tim Berners-Lee when he invented the web, along with unique identifiers for resources (which is where Uniform Resource Locators, or URLs, came from) and Hypertext Markup Language (HTML). Other parts of the internet have their own protocols and standards to define how they work and how their underlying messages are routed through the internet (such as email with SMTP, IMAP, and POP). When examining HTTP, you’re dealing primarily with the World Wide Web. This line is getting more blurred, however, as services built on top of HTTP, even without a traditional web front end, mean that defining the web itself is trickier and trickier! These services (known by acronyms such as REST or SOAP) can be used by web pages and non-web pages (such as mobile apps) alike. The IoT simply represents devices that expose services that other devices

 (computers, mobile apps, and even other IoT devices) can interact with, often through HTTP calls. As a result, you can use HTTP to send a message to a lamp to turn it on or off from a mobile phone app, for example.
HTTP 是瀏覽器請求網頁的方式，與統一資源定位符(也就是 URL 網址)和超文件標示語言
(HTML)同為全球資訊網路之父 Tim Berners-Lee 發明的三大技術之一。網際網路的其他服 務各自有專屬的協定和標準，規範使用的方式和訊息如何透過路由器傳遞(像電子郵件有 SMTP、IMAP 和 POP等協定)。當檢視 HTTP 時，您絕大多數的時間都在處理全球資訊網 路。網際網路和全球資訊網路的差異越來越小。然而，只要網路服務使用 HTTP 協定，即便 沒有傳統的網頁介面，仍屬於全球資訊網路，這代表如何定義網路變得越來越棘手。使用者 可透過網路，或是其他的方式(如手機 APP)使用這些服務(以縮寫 REST 和 SOAP 為人所 知)。物聯網這個詞代表任何提供服務讓其他裝置(如電腦、手機 APP ，甚至其他的物聯網裝 置)得與之聯繫的裝置，通常是透過 HTTP 請求。因此，透過 HTTP，您可以藉由手機 APP 傳遞訊息開啟和關閉一盞燈的電源。
Although the internet is made up of myriad services, a lot of them are being used proportionally less and less while use of the web continues to grow. Those of us who recall the internet in the earliest days recall acronyms such as BBS and IRC that are practically gone today, replaced by web forums, social media websites, and chat applications. 即使網際網路是由無數種服務組成，其中許多應用的使用率正按比例逐漸減少，反之網路的
需求卻持續成長。經歷過網路剛起步的時期的人可能還記得 BBS 和 IRC這些縮寫，如今這 些服務已不復存在，取而代之的是網路論壇、社群網站及線上聊天應用程式。
 
All this means that although the term World Wide Web was often incorrectly used interchangeably with the internet, the continued rise of the web—or at least of HTTP, which was created for it—may mean that soon, that understanding may not be as far from the truth as it once was. 這些都說明了即便全球資訊網路這個詞常被誤用為網際網路，但隨著網路服務，或者至少
是 HTTP—這個專為 Web 量身打造的協定的興起，意謂著不久的將來，將全球資訊網路看 成網際網路本身也不像過去那般偏離現實了。
