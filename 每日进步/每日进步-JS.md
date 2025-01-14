### 1. 立即执行函数和拓展运算符的综合用法
通过立即执行函数和拓展运算符，可以有效的简化操作方法。

背景：获取列表的请求参数 systemFields 的处理，当有搜索条件的时候，如 searchValue ，可能需要单独处理一下。

但是通过立即执行函数，把请求参数的逻辑聚拢在一起了，然后在将结果解构出来，如果没有搜索值的话，systemFields数组就不添加新的内容，如果有搜索值的话，就将返回的数组对象解构出来变成对象插入到 systemFields的数组里面去。


代码如下：
```js
let reqParams ={
 current: 1,
 size: 20,
 sort: [{  field: "createTime",  mode: this.sortMode}],
 systemFields: [ 
{ field: 'isNegative', value: [0], type: "text", method: "in"},
...(()=> {
    if(!this.searchValue) return []
    return [{ field: 'keyword', value: [this.searchValue], type: "text", method: "in"}]
 })(),
            
}
```


### 2. 事件委托模式
通过事件委托模式，优化通过循环监听事件消耗性能的bug

![[Pasted image 20241127230821.png|672]]![[Pasted image 20241127230827.png]]


### 3. 知识之间的关联：
对标
人事物理
四问学习法：我应该如何使用？
如何为我所用
滑梯理论：里面的how?



### 4. 事件流重复推送的优化
联网配置连接WiFi的情况下，会重复的推送事件，其中事件有失败和成功的，当前的处理使用定时器和队列的方式有问题。应该在成功之后，就停止处理事件。
![[Pasted image 20241128181911.png|672]]

### 5. 提前返回逻辑优化
```js
 const handleDeviceStatusResponse = (requestBTDeviceStatusRes) => {
          if (isResultValid) {
            return
          }

          if (requestBTDeviceStatusRes && requestBTDeviceStatusRes.success) {
            if(requestBTDeviceStatusRes.data && requestBTDeviceStatusRes.data.response) {
              if(requestBTDeviceStatusRes.data.response.Station === 'disconnect Wi-Fi now') {
                console.error('WIFI 连接断开了', requestBTDeviceStatusRes.data.response.Station)
                isResultValid = false
                return
              }

              if(requestBTDeviceStatusRes.data.response.Station === 'connect Wi-Fi now') {
                console.error('WIFI 连接成功', requestBTDeviceStatusRes.data.response.Station)
                this.sendCustomDataToDevice()
                isResultValid = true
                return
              } else {
                this.$u.toast('配网失败，请检查WiFi密码或者蓝牙已断开，再次尝试！')
                this.loading = false
                isResultValid = true
                return
              }
            }
          }
 
        }
```


```js

    const handleDeviceStatusResponse = (requestBTDeviceStatusRes) => {
          if (isResultValid) {
            return
          }
					
				 if (!requestBTDeviceStatusRes || !requestBTDeviceStatusRes.success) {
							return;  // 如果请求结果无效，直接返回
					}
					const response = requestBTDeviceStatusRes.data?.response;
					
					 if (!response || !response.Station) {
							console.error('设备状态响应无效', requestBTDeviceStatusRes);
							return;
					}
					
					const stationStatus = response.Station;

					
					 // 处理WiFi断开
						if (stationStatus === 'disconnect Wi-Fi now') {
								isResultValid = false;
								// this.loading = false;
								console.error('WiFi密码错误或设备无法连接到WiFi，等待重试', stationStatus);
								return;
														
						}
						
						 // 处理WiFi连接成功
						if (stationStatus === 'connect Wi-Fi now') {
								console.log('获取设备状态：WIFI 连接成功', stationStatus);
								this.sendCustomDataToDevice();  // 发送自定义数据
								isResultValid = true;
								
								return;
						}
						
						// 其他情况，处理配网失败
						this.$u.toast('配网失败，请检查WiFi密码或者蓝牙已断开，再次尝试！');
						this.loading = false;
						isResultValid = true;
						console.error('配网失败，未知错误');
 
        }

```