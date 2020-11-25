![](https://github.com/dounine/standalone-chrome-ssl/workflows/Publish%20Docker%20image/badge.svg) ![](https://img.shields.io/github/license/dounine/standalone-chrome-ssl)

# standalone-chrome-ssl

## Introduction
The selenium/standalone-chrome version does not support ssl blocking by default, and this version is supported.

## Useage
docker pull
```
docker pull dounine/standalone-chrome:1.0
```
docker run
```
docker run -d -p 4444:4444 --shm-size 2g dounine/standalone-chrome:1.0
```
## Code
scala
```
val proxy = new BrowserMobProxyServer()
proxy.start(0)
proxy.enableHarCaptureTypes(CaptureType.REQUEST_CONTENT)
val seleniumProxy = ClientUtil.createSeleniumProxy(proxy)
val filter: RequestFilter = new RequestFilter {
  override def filterRequest(httpRequest: HttpRequest, httpMessageContents: HttpMessageContents, httpMessageInfo: HttpMessageInfo): HttpResponse = {
    try {
      val body: String = httpMessageContents.getTextContents
      println(body)
    } catch {
      case exception: Exception =>
    }
    null
  }
}
proxy.addRequestFilter(filter)
val dc: DesiredCapabilities = DesiredCapabilities.chrome()
dc.setCapability(CapabilityType.PROXY, seleniumProxy)
val driver: RemoteWebDriver = new RemoteWebDriver(new URL("http://localhost:4444/wd/hub"), dc)
driver.manage().window().maximize()
driver.get("https://github.com/dounine/standalone-chrome-debug-ssl")
driver.quit()
```
