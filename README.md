<div>
    <center><h1>Selenium + Go</h1></center>
</div>
<div>
    <ol>
        <li>Скачать драйвер для браузера <a href="https://chromedriver.chromium.org/downloads" target="_blank">https://chromedriver.chromium.org/downloads</a></li>
        <li>Установить библиоту в свой проект через go mod <a href="https://github.com/tebeka/selenium" target="_blank">https://github.com/tebeka/selenium</a></li>
    <ol>
</div>

```Go
package main

import (
	"github.com/tebeka/selenium"
	"github.com/tebeka/selenium/chrome"
)

func main() {
	// Run Chrome browser
	service, err := selenium.NewChromeDriverService("./chromedriver", 4444)
	if err != nil {
		panic(err)
	}
	defer service.Stop()

	caps := selenium.Capabilities{}
	caps.AddChrome(chrome.Capabilities{Args: []string{
		"window-size=1920x1080",
		"--no-sandbox",
		"--disable-dev-shm-usage",
		"disable-gpu",
		// "--headless",  // comment out this line to see the browser
	}})

	driver, err := selenium.NewRemote(caps, "")
	if err != nil {
		panic(err)
	}

	driver.Get("https://www.google.com")
}
```

<div>
    <p>Заметка: На линуксе не работают драйверы с браузерами которые были установлены через изалурованную систему FlatPack, Snap</p>
</div>