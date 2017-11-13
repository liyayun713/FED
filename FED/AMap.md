# 高德地图API
```js
// 加载地图，调用浏览器定位服务
var map = new AMap.Map('container', {
  resizeEnable: true,
  zoom: 10,   // 地图缩放比例
});
// 添加标记
var marker = new AMap.Marker({  // 加点
  map: map,
  zIndex: 101,
});
// 输入提示
var auto = new AMap.Autocomplete({
  input: 'tipinput',
});
// 搜索
var placeSearch = new AMap.PlaceSearch({
  map: map,
});
// 点击输入提示搜索
AMap.event.addListener(auto, 'select', select);
function select (e) {
  placeSearch.setCity(e.poi.adcode);
  placeSearch.search(e.poi.name);  // 关键字查询查询
}

// 监听点击搜索的结果
AMap.event.addListener(placeSearch, 'markerClick', searchConfirm);
function searchConfirm (result) {
  var lng = result.data.location.lng;
  var lat = result.data.location.lat;
  updateMarker(lng, lat);
  updateLnglat(lng, lat);
  clearAddressInfo();
  regeocoder(lng, lat);
}

// 点击搜索按钮
this.searchFn = function searchKeyWord (keyWord) {
  if (keyWord !== null) {
    placeSearch.search(keyWord);
  }
};
// 自动定位
map.plugin('AMap.Geolocation', function () {
  var geolocation = new AMap.Geolocation({
    enableHighAccuracy: true,             // 是否使用高精度定位，默认:true
    timeout: 10000,                       // 超过10秒后停止定位，默认：无穷大
    buttonOffset: new AMap.Pixel(10, 20), // 定位按钮与设置的停靠位置的偏移量，默认：Pixel(10, 20)
    zoomToAccuracy: true,                 // 定位成功后调整地图视野范围使定位位置及精度范围视野内可见，默认：false
    buttonPosition: 'RB',
    showCircle: false,
  });
  geolocation.options.markerOptions.bubble = true;
  map.addControl(geolocation);
  geolocation.getCurrentPosition();
  AMap.event.addListener(geolocation, 'complete', onComplete);// 返回定位信息
  AMap.event.addListener(geolocation, 'error', onError);      // 返回定位出错信息
});
if (location.href.indexOf('&guide=1') !== -1) {
  map.setStatus({scrollWheel: false});
}
var timeoutID = null;
// 为地图注册click事件获取鼠标点击出的经纬度坐标
map.on('click', function (e) {
  clearTimeout(timeoutID);
  timeoutID = window.setTimeout(function () {
    var lng = e.lnglat.getLng();
    var lat = e.lnglat.getLat();
    updateMarker(lng, lat);
    updateLnglat(lng, lat);
    clearAddressInfo();
    regeocoder(lng, lat);
  }, 200);
});
// 双击事件不做处理
map.on('dblclick', function () {
  clearTimeout(timeoutID);
});
// 更新标记
function updateMarker (lng, lat) {
  var newPositon = [];
  newPositon.push(lng);
  newPositon.push(lat);
  if (map.getZoom() > 16) {
    map.setCenter(newPositon);
  } else {
    map.setZoomAndCenter(16, newPositon);
  }
  marker.setPosition(newPositon);
  marker.setAnimation('AMAP_ANIMATION_DROP');
}

this.updateMarkFn = updateMarker;
// 更新经纬度
function updateLnglat (lng, lat) {
  self.loc.lng = lng;
  self.loc.lat = lat;
}

// 清空地址信息
function clearAddressInfo () {
  self.loc.formattedAddress = '';
  self.loc.basicAddress = '';
  self.loc.address = '';
  self.loc.province = '';
  self.loc.city = '';
  self.loc.county = '';
  self.loc.township = '';
  self.loc.house = '';
}

// 更新地址信息
function updateAddressInfo (data) {
  var adr = data.addressComponent;
  var formatAddress = data.formattedAddress;
  var basicAddress = adr.province + adr.city + (!adr.district ? adr.township : adr.district);
  self.loc.basicAddress = basicAddress;
  self.loc.address = formatAddress.substr(basicAddress.length, formatAddress.length);
  self.loc.formattedAddress = data.formattedAddress;
  var adcode = adr.adcode;
  self.loc.province = adcode.substr(0, 2) + '0000';
  self.loc.city = adcode.substr(0, 4) + '00';
  self.loc.township = adr.township;
  // 针对东莞中山没有区县进行转换
  self.loc.county = ((self.loc.city === '442000' || self.loc.city === '441900') && !adr.district) ? self.transformCode(self.loc.city, self.loc.township) : adcode;
  self.conferCode(self.loc.city, self.loc.county);
  checkAddress();
}

// 解析定位结果
function onComplete (data) {
  if (!self.loc.lat || self.autoGetLocation) {
    updateLnglat(data.position.getLng(), data.position.getLat());
    updateAddressInfo(data);
  } else if (self.autoGetLocation) {
    self.autoGetLocation;
  }
  // 已经定位过一次
  self.autoGetLocation = true;
  updateMarker(self.loc.lng, self.loc.lat);
}

// 解析定位错误信息
function onError (data) {
  if (!self.showFlag) return;
  Toast({
    message: '自动定位失败，请手动搜索',
    duration: 1500,
  });
}

// 逆地理编码
function regeocoder (lng, lat) {
  var lnglatXY = [];
  lnglatXY.push(lng);
  lnglatXY.push(lat);
  var geocoder = new AMap.Geocoder({
    radius: 1000,
    extensions: 'all',
  });
  geocoder.getAddress(lnglatXY, function (status, result) {
    if (status === 'complete' && result.info === 'OK') {
      updateAddressInfo(result.regeocode);
    }
  });
}
```
