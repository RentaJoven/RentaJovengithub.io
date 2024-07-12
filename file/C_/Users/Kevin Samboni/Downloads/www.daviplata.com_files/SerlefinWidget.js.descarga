function SerlefinWidget(endpoint, clientToken, imgUrl, cssUrl, closeImgUrl, menuUrl) {
    if (imgUrl == null) imgUrl = "https://m.serlefin.com/SerlefinWidget/IMG/digit.png";
    if (cssUrl == null) cssUrl = "https://m.serlefin.com/SerlefinWidget/CSS/SerlefinWidget.css"
    if (closeImgUrl == null) closeImgUrl = "https://m.serlefin.com/SerlefinWidget/IMG/whiteX.png";
	if (menuUrl == null) menuUrl = "https://m.serlefin.com/SerlefinWidget/IMG/menu.png";
    this.endpoint = endpoint;
    this.clientToken = clientToken;
    /* Add CSS */
    var head = document.getElementsByTagName("head")[0];
    var link = document.createElement("link");
    link.rel = "stylesheet";
    link.type = "text/css";
    link.href = cssUrl;
    link.media = 'all';
    head.appendChild(link);


    /* Add widget componenets */
    this.mainDiv = document.createElement("div");
	
	
    this.frameDiv = document.createElement("div");
    this.frameDiv.style.display = "none";
	this.frameDiv.style.zIndex = "100000";
    this.frameDiv.classList.add("serlefinWidgetWindow");
    var chatHeader = document.createElement("div");
    chatHeader.classList.add("serlefinWidgetHeader");
	this.homeButton = document.createElement("img");
    this.homeButton.src = menuUrl;
    chatHeader.appendChild(this.homeButton);
	
    this.closeButton = document.createElement("img");
    this.closeButton.src = closeImgUrl;
    chatHeader.appendChild(this.closeButton);

	
    this.frameDiv.appendChild(chatHeader);
    this.frame = document.createElement("iframe");
    this.frame.src = endpoint;
    this.frameDiv.appendChild(this.frame);


    this.mainDiv.appendChild(this.frameDiv)

    this.buttonDiv = document.createElement("div");
    //this.buttonDiv.style.cssText = "float: right; text-align: right; padding-right: 1em";
    this.openButton = document.createElement("div");
    this.openButton.style.cssText = "position: fixed; right: 2em;top: 80vh;font-size: 1em;cursor: pointer;z-index: 1000000;";
    var img = document.createElement("img");
    img.src = imgUrl;
    img.classList.add("serlefinWidgetIcon");
    this.openButton.appendChild(img);
    this.buttonDiv.appendChild(this.openButton);
    //this.mainDiv.appendChild(this.buttonDiv);

    document.body.appendChild(this.mainDiv);
    var self = this;
    /* Obel/close functions */
    this.openWidget = function () {
        self.buttonDiv.style.display = "none";
        self.frameDiv.style.display = "block";
    };
    this.closeWidget = function () {
        self.buttonDiv.style.display = "block";
        self.frameDiv.style.display = "none";
    };
	this.goHome = function () {
        self.frame.src = endpoint;
    };

    this.openButton.addEventListener("click", this.openWidget);
    this.closeButton.addEventListener("click", this.closeWidget);
    this.homeButton.addEventListener("click", this.goHome);

    this.frameLoaded = false;
    var self = this;
    window.addEventListener("message", function (event) {
        if (event.data != null && event.data.SerlefinWidgetLoaded == true) {
            self.frameLoaded = true;
        }
    });
    this.setWidgetData = function (data) {
        if (self.frameLoaded)
            self.frame.contentWindow.postMessage(data, "*");
        else
            setTimeout(self.setWidgetData, 1000, data);
    };
}