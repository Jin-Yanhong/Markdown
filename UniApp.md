# App 获取版本信息

```javascript
plus.runtime.getProperty(plus.runtime.appid, wgtinfo => {
    this.version = wgtinfo.versionCode;
});
```
