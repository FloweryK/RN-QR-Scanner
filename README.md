# How to Install

### react-native-camera 설치

https://react-native-camera.github.io/react-native-camera/docs/installation

※ QR scan을 위해서는 react-native-camera에서 MLKit 추가 설정을 해줘야 하므로, 꼼꼼히 읽을 것



<br/>

# How to Use

### `RNCamera` 사용법

다음과 같이 컴포넌트로 사용할 수 있다.

```react
let camera;

<RNCamera
	ref={ref => (camera = ref)}
	style={{
		width: 200,
		height: 400,
	}}
	type={RNCamera.Constants.Type.back}
	captureAudio={false}
/>
```

※ `camera`는 실제 `RNCamera`에서 사진을 찍을 때 사용한다. 위 코드에서는 영향이 없다. 



<br/>

### Barcodes 기능 사용법

`RNCamera`의 `onGoogleVisionBarcodesDetected`를 사용한다.

```react
const BarcodeDetected = ({barcodes}) => {
    barcodes.forEach(barcode => console.warn(barcode.data));
  };

<RNCamera ...
	onGoogleVisionBarcodesDetected={BarcodeDetected}
/>

// result
// WARN: "안녕하세요! QR코드입니다!"
```



<br/>

### 기능 관찰

- `onGoogleVisionBarcodeDetected`가 뱉는 전체 데이터는 아래와 같다.

  ```json
  [
  	{
  		"bounds": 
  			{
  				"origin": {"x": 127.31481481481481, "y": 48.28571644425392}, 
  				"size": {"height": 109.71429061889648, "width": 169.44444444444446}
  			}, 
  			"data": "안녕하세요! QR코드입니다!", 
  			"dataRaw": "안녕하세요! QR코드입니다!", 
  			"format": "QR_CODE", 
  			"type": "TEXT"
  		}
  ]
  ```


- 바코드가 감지되지 않은 IDLE 상태에서는 1초에 2프레임, 한 번 감지되면 초당 20~30프레임씩 읽다가, 다시 감지되지 않으면 IDLE 상태로 돌아간다.
- `RNCamera`는 각 preview 프레임을 제공하지 않는다. 따라서 preview 프레임에 processing을 하고싶다면 native를 사용해야한다.

<br/>



### 이슈

- `RNCamera` 컴포넌트가 container에 제대로 들어가지 않고 튀어나오는 문제가 있다.
  (관련 이슈: https://github.com/react-native-camera/react-native-camera/issues/1902)



<br/>

<br/>

### 기타

온라인 qr 코드 생성기: https://ko.online-qrcode-generator.com/

