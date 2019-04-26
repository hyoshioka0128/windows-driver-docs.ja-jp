---
title: USB ビデオ クラス 1.5 仕様に対する Microsoft の拡張機能
description: により、標準形式で適切に定義されたフレーム メタデータを実行する機能だけでなく、新しいコントロール USB ビデオ クラス 1.5 仕様に対する Microsoft 拡張機能について説明します。
ms.date: 04/03/2019
ms.localizationpriority: medium
ms.custom: rs5, 19H1
ms.openlocfilehash: 8a88e66f7f7d8fe90bd55bfdbc783b17c659a693
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338494"
---
# <a name="microsoft-extensions-to-usb-video-class-15-specification"></a>USB ビデオ クラス 1.5 仕様に対する Microsoft の拡張機能

## <a name="1-overview"></a>1 の概要

### <a name="11-summary"></a>1.1 の概要

Microsoft の拡張機能、 [USB ビデオ クラス仕様](https://go.microsoft.com/fwlink/p/?linkid=2085170)新しいコントロールと同様、標準形式で適切に定義されたフレーム メタデータを実行する機能を有効にします。

### <a name="12-architecture-decisions"></a>1.2 アーキテクチャの決定

USB ビデオ クラス (UVC) フレームのメタデータのサポートは、アイソクロナスと一括エンドポイントはできます。 ただし、一括のエンドポイントの場合、メタデータのサイズになります 240 バイトに制限されています (原因という事実にビデオ フレームのすべてのデータは、1 つのビデオ フレームのパケットで一括エンドポイントに転送される)。

UVC メタデータのサポートには、ベースのペイロードの周囲に利用可能なだけになります。

UVC メタデータのサポートは、Media Foundation (MF) キャプチャ パイプラインを通じてしか利用できませんになります。

UVC メタデータは、オプトインになります。 メタデータのサポートが必要なすべての IHV と OEM は、カスタムの INF ファイルをこれに有効にする必要があります。

UVC メタデータは、メモリを割り当てられているシステムのみをサポートします。 VRAM DX サーフェスはサポートされません。

## <a name="2-architectural-overview"></a>2 つのアーキテクチャの概要

### <a name="21-description"></a>2.1 の説明

#### <a name="221-capability-discovery-through-inf"></a>2.2.1 INF を通じて機能の検出

##### <a name="2211-still-image-capture--method-2"></a>2.2.1.1 イメージのキャプチャはまだ – 方法 2

いくつか既存の UVC デバイスではの 2.4.2.4 (イメージのキャプチャも) のセクションで説明した方法 2 をサポートしていませんが、 *UVC 1.5 クラス specification.pdf*でダウンロードできますが、 [USB ビデオ クラス仕様](https://go.microsoft.com/fwlink/p/?linkid=2085170)web サイトです。

Windows 10 バージョン 1607 および以前のバージョンをデバイス UVC 1.5 仕様ごとのサポートを提供する場合でもメソッドの 2 の場所をキャプチャ パイプラインが利用できませんでした。

Windows 10 version 1703 では、このメソッドを利用するデバイスは、カメラのドライバーの INF ファイルをカスタムを使用する必要がありますがカスタム INF メソッド 2 静止イメージのキャプチャを有効にするのには、特定のハードウェアに必要)。

注:カメラのドライバーは、Windows USBVIDEO に基づくことができます。SYS またはカスタム ドライバー バイナリに基づくことができます。

カスタム UVC ドライバーまたは受信トレイ UVC のドライバーのいずれかに基づいて、カスタムの INF ファイルには、次の AddReg エントリを含める必要があります。

**EnableDependentStillPinCapture**:REG_DWORD:(有効) 0x1 0x0 (無効)

このエントリが有効 (0x1) に設定されている場合、キャプチャ パイプラインはまだイメージのキャプチャ (ファームウェアも UVC 1.5 の仕様で指定されたメソッドの 2 のサポートをアドバタイズを想定) の方法 2 を活用します。

カスタムの INF セクションの例のとおりようになります

```INF
[USBVideo.NT.Interfaces]
AddInterface=%KSCATEGORY_CAPTURE%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER_EXT%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO_CAMERA%,GLOBAL,USBVideo.Interface

[USBVideo.Interface]
AddReg=USBVideo.Interface.AddReg

[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,,EnableDependentStillPinCapture,0x00010001,0x00000001
```

#### <a name="222-extension-unit-controls"></a>2.2.2 拡張ユニット コントロール

Microsoft の拡張機能、 **USB ビデオ クラス仕様**新しいコントロールを有効にする (Microsoft XU と呼ばれる) GUID MS_CAMERA_CONTROL_XU で識別される、拡張機能単位で行われます。

```cpp
// {0F3F95DC-2632-4C4E-92C9-A04782F43BC8}
DEFINE_GUID(MS_CAMERA_CONTROL_XU,
    0xf3f95dc, 0x2632, 0x4c4e, 0x92, 0xc9, 0xa0, 0x47, 0x82, 0xf4, 0x3b, 0xc8);
```

デバイスのファームウェアによって実装される Microsoft XU には、次のセクションで定義されている新しいコントロールを格納します。 次の要求の定義は、そのコントロールのオーバーライドの定義を明示的に指定されていない場合に、これらすべてのコントロールに適用されます。 参照してください**UVC 1.5 クラス specification.pdf** D3、D4、GET_INFO などの定義についてはします。

GET_INFO 要求は、(つまり D3 と D4 のビットを 0 に設定されます)、自動更新と非同期の機能を使用しないコントロールがレポートされます。

GET_LEN 要求はレポートのこのコントロールのペイロードの最大長 (**wLength**)。

GET_RES 要求の解決 (ステップ サイズ) に報告されます**qwValue/dwValue**します。 その他のすべてのフィールドは、0 に設定する必要があります。

GET_MIN 要求のサポートされる最小値をレポートは**qwValue/dwValue**します。 その他のすべてのフィールドは、0 に設定する必要があります。

GET_MAX 要求の最大のサポートされている値をレポートは**qwValue/dwValue**します。 さらに、サポートされているすべてのフラグを 1 に設定するものと**bmControlFlags**します。 その他のすべてのフィールドは、0 に設定する必要があります。

GET_DEF および GET_CUR 要求は、既定値とそれぞれのフィールドの現在の設定をレポートは**qwValue/dwValue**と**bmControlFlags**します。 その他のすべてのフィールドは、0 に設定する必要があります。

SET_CUR 要求は、すべてのフィールドを設定した後、ホストによって発行されます。

次の表は、Microsoft XU の制御セレクターをそれぞれの値とのビット位置には、 *bmControls*拡張機能単位の記述子フィールド。

![拡張機能ユニット コントロール](images/uvc-1-15-01.png)

##### <a name="2221-cancelable-asynchronous-controls"></a>2.2.2.1 キャンセル可能な非同期コントロール

非同期のキャンセル可能なコントロールは、自動更新機能を活用することでは、ここに定義されます。

GET_INFO 要求は、このようなコントロールを自動更新コントロール (たとえば、ビットを 1 に設定するものと D3) としてではない非同期のコントロール (たとえば、ビットを 0 に設定するものと D4) を報告する必要があります。

このようなコントロールの新しい値を設定する SET_CUR 要求を発行できます (、SET_CUR(NORMAL) 要求の**bmOperationFlags:D0**ビットが 0 に設定) 以前 SET_CUR(NORMAL) 要求をキャンセルまたは (、SET_CUR(CANCEL) 要求、 **bmOperationFlags:D0**ビットが 1 に設定されます)。 要求を受信した (ただし、ハードウェアの構成または要求された新しい設定に収束されていない) すぐに、デバイスによって SET_CUR 要求が完了します。 SET_CUR(NORMAL) 要求ごとに、デバイスは SET_CUR(CANCEL) 要求が到着するとします。 または、新しい設定が適用されたときに発生したこのコントロールの対応するコントロールの変更割り込みを生成しますこの割り込みが到着するまでは、進行中のある SET_CUR(NORMAL) 要求と見なされます。 SET_CUR(NORMAL) 要求が進行中の場合は、この特定のコントロールに対する追加の SET_CUR(NORMAL) 要求は、エラーが発生します。 SET_CUR(CANCEL) 要求は常に成功する必要があります。 Nothing をキャンセルする場合、デバイスだけは何も行いません。

コントロールの変更の割り込みのペイロード ビットを有する**bmOperationFlags:D0** SET_CUR(NORMAL) によって指定される設定が適用されている場合は 0 に設定 (つまり収束が発生しました)、set _ により、設定が適用されていない場合は、1 に設定(つまり収束まだ発生していない) SET_CUR(NORMAL) 要求後に付属している CUR(CANCEL) 要求。

##### <a name="2222-focus-control"></a>2.2.2.2 フォーカス コントロール

このコントロールは、カメラのフォーカス設定を指定する、ホスト ソフトウェアを使用できます。 これは、すべてのビデオ ストリーミング、ビデオ コントロールのインターフェイスに関連付けられているインターフェイスのすべてのエンドポイントに影響を与えるグローバル コントロールです。

![フォーカスを移動](images/uvc-1-15-02.png)

このコントロールはキャンセル可能な非同期コントロール (セクション 2.2.2.1 GET_INFO 要求の要件と SET_CUR 要求の機能の動作を参照) として機能します。

GET_MAX 要件:このコントロールは D0、D1、D2、D8 および D18 で bits サポートをアドバタイズ**bmControlFlags**します。

GET_DEF 要件:既定の**bmControlFlags**は D0 および D18 1 に設定して**dwValue**を 0 に設定します。

フィールドの GET_CUR/SET_CUR 要求の場合、次の制限が適用されます**bmControlFlags**:

- D0、D1 と D8 のビット単位の間でビットが 1 つのみを設定できます。設定されている、いずれも有効な D2 のビットが設定されているかどうかです。

- D16、D17、D18、D19 および D20、間でビットが 1 つのみを設定できます。設定されている、いずれも無効です。

- D1 は、すべての他のビット現在定義されている (D0、D2、D8、D16、D17、D18、D19 および D20) と互換性がありません。

- D2 は、D1 と D8 と互換性がありません。

D0 が設定されていない場合は、D2 を D16、D17、D18、D19 D20 と互換性がありません。

##### <a name="2223-exposure-control"></a>2.2.2.3 露出コントロール

このコントロールは、カメラの危険度の設定を指定する、ホスト ソフトウェアを使用できます。 これは、すべてのビデオ ストリーミング、ビデオ コントロールのインターフェイスに関連付けられているインターフェイスのすべてのエンドポイントに影響を与えるグローバル コントロールです。

![露出コントロール](images/uvc-1-15-03.png)

非同期コントロール (つまりビットを 1 に設定するものと D4) としてではない AutoUpdate コントロール (つまり D3 ビットを 0 に設定する必要があります)、GET_INFO 要求はこのコントロールをレポートものとします。

GET_MAX 要件:このコントロールは D0、D1 と D2 にビットのサポートをアドバタイズ**bmControlFlags**します。

GET_DEF 要件:既定の**bmControlFlags**は D0 1 に設定して**qwValue**を 0 に設定します。

フィールドの GET_CUR/SET_CUR 要求の場合、次の制限が適用されます**bmControlFlags**:

- D0、D1 と D2 のビット単位の間では、少なくとも 1 つのビットを設定するものとします。

- D1 は、D0 と D2 と互換性がありません。

##### <a name="2224-ev-compensation-control"></a>2.2.2.4 EV 補正コントロール

このコントロールは、カメラの EV 補正設定を指定する、ホスト ソフトウェアを使用できます。 これは、すべてのビデオ ストリーミング、ビデオ コントロールのインターフェイスに関連付けられているインターフェイスのすべてのエンドポイントに影響を与えるグローバル コントロールです。

![EV 補正コントロール](images/uvc-1-15-04.png)

非同期コントロール (つまりビットを 1 に設定するものと D4) としてではない AutoUpdate コントロール (つまり D3 ビットを 0 に設定する必要があります)、GET_INFO 要求はこのコントロールをレポートものとします。

GET_RES 要求はすべてのサポートされている解像度 (ステップ サイズ) に対応するビットを設定してレポートの**bmControlFlags**します。 その他のすべてのフィールドは、0 に設定する必要があります。

最小値と最大サポートされている値を報告するものと GET_MIN および GET_MAX 要求**dwValue**します。 ビット D4 ものであるし、ビットのみに設定されます (手順 1 のサイズを示す) **bmControlFlags**します。 その他のすべてのフィールドは、0 に設定する必要があります。

1 ビットのみを D0、D1、D2、D3 と D4 の間でビット フィールドを設定および GET_DEF、GET_CUR、SET_CUR 要求セクション 2.2.2.1 内の定義に従いますが、1 つ含まれていては**bmControlFlags**します。 さらに、GET_DEF 要求が含まれていては**dwValue**を 0 に設定します。

##### <a name="2225-white-balance-control"></a>2.2.2.5 ホワイト バランス コントロール

このコントロールは、カメラのホワイト バランス設定を指定する、ホスト ソフトウェアを使用できます。 これは、すべてのビデオ ストリーミング、ビデオ コントロールのインターフェイスに関連付けられているインターフェイスのすべてのエンドポイントに影響を与えるグローバル コントロールです。

![ホワイト バランス コントロール](images/uvc-1-15-05.png)

非同期コントロール (つまりビットを 1 に設定するものと D4) としてではない AutoUpdate コントロール (つまり D3 ビットを 0 に設定する必要があります)、GET_INFO 要求はこのコントロールをレポートものとします。

GET_RES、GET_MIN、GET_MAX 要求は次のセクション 2.2.2.1 内の定義が含まれていては**dwValueFormat**を 1 に設定します。

GET_MAX 要件:このコントロールは D0、D1 と D2 にビットのサポートをアドバタイズ**bmControlFlags**します。

GET_DEF 要件:既定の**bmControlFlags**は D0 1 に設定して**dwValueFormat および dwValue**を 0 に設定します。

フィールドの GET_CUR/SET_CUR 要求の場合、次の制限が適用されます**bmControlFlags**:

- D0、D1 と D2 のビット単位の間では、少なくとも 1 つのビットを設定するものとします。

- D1 は、D0 と D2 と互換性がありません。

##### <a name="2226-iso-control"></a>2.2.2.6 ISO コントロール

このコントロールは、カメラのイメージのキャプチャもの ISO フィルム速度の設定を指定する、ホスト ソフトウェアを使用できます。 このコントロールは、指定したビデオ/静止エンドポイント (つまり、ビデオ コントロールのインターフェイスに関連付けられているすべてのビデオ ストリーミング インターフェイス上のすべての動画または静止エンドポイントのサブセット) に適用のみ。 まだキャプチャ メソッドの 1 が使用されている場合、このコントロールはビデオ エンドポイントでサポートする必要があります。 方法 2 またはもキャプチャするための方法 3 を使用する場合、このコントロールはまだエンドポイントでサポートする必要があります。

![ISO コントロール](images/uvc-1-15-06.png)

非同期コントロール (つまりビットを 1 に設定するものと D4) としてではない AutoUpdate コントロール (つまり D3 ビットを 0 に設定する必要があります)、GET_INFO 要求はこのコントロールをレポートものとします。

GET_RES、GET_MIN、GET_MAX、GET_DEF、GET_CUR 要求セクション 2.2.2.1 内の定義に従います。 また、これらの要求の出力として一覧はすべて、D0 のいずれかの可能なエンドポイントのみ (Auto モード) または D52 (手動モード) つまりエンドポイントが D0 または D52 のいずれかの可能な場合には表示を取得します。それ以外の場合、これは取得は表示されません。

##### <a name="2227-face-authentication-control"></a>2.2.2.7 顔認証の制御

このコントロールは、カメラが顔認証に使用されるストリーミングのモードをサポートするかどうかを指定する、ホスト ソフトウェアを使用できます。 カメラが顔認証をサポートする必要がある場合にのみ、このコントロールをサポートする必要があります。

このコントロールでは、インすらストラクチャ Red (IR) のデータを生成できるし、は、指定したビデオ エンドポイント (つまり、ビデオ コントロールのインターフェイスに関連付けられているすべてのビデオ ストリーミング インターフェイス上のすべてのビデオのエンドポイントのサブセット) にのみ適用するカメラに適用されるだけです。

![顔認証の制御](images/uvc-1-15-07.png)

GET_RES および GET_MIN 要求とレポート フィールド**bNumEntries** 0 に設定され、追加のフィールドがあるためありません。

GET_MAX 要求では、ビットを 1 に設定、 **bmControlFlags**フィールドは、そのエンドポイントに対応するモードがサポートされていることを示します。 GET_MAX 要求の出力は、すべての一覧を表示し、D1 または D2 (つまり場合 D1 または D2 のいずれかのエンドポイントは、それ以外の一覧を取得、取得にないは) のいずれかの可能な唯一のエンドポイント。 また、エンドポイントに提供するありません D1 と D2 の両方に対応します。 エンドポイントの (つまり外部顔認証の目的) 汎用的に動作が予想される場合、D0 は (D1 と D2) だけでなくそのエンドポイントの 1 に設定する必要があります。

GET_DEF の/GET_CUR/SET_CUR 要求、ビットが 1 に設定は、そのエンドポイントに対応するモードが選択されていることを示します。 これらの要求では、1 つ、1 ビットのみ (D0、D1 と D2) 間で特定のエンドポイントに設定するものとします。 D0 は、そのエンドポイントでは、既定で 1 に設定する必要があります (つまり外部顔認証の目的)、汎用的に動作する場合、エンドポイント (つまり実装固有の) 既定の選択肢が返す GET_DEF 要求が必要です。それ以外の場合、D1 または D2 (ただし両方ではなく) 必要があります設定を 1 に既定では。 GET_DEF/GET_CUR 要求の出力は GET_MAX 要求出力に含まれるすべてのエンドポイントに関する情報を含める必要がありますただし、SET_CUR 要求は GET_MAX 要求の出力に含まれるエンドポイントのサブセットのみを含めることがあります。

##### <a name="2228-camera-extrinsics-control"></a>2.2.2.8 カメラ Extrinsics コントロール

このコントロールは、カメラ extrinsics データは、ビデオ コントロールのインターフェイスに関連付けられているビデオのストリーミング インターフェイス上のエンドポイントを取得する、ホスト ソフトウェアを使用できます。 各エンドポイントのために取得したデータは、属性 (IMFDeviceTransform::GetOutputStreamAttributes 呼び出しを使用して取得した)、対応するストリームの属性ストアで MFStreamExtension_CameraExtrinsics として表示されます。

![カメラ extrinsics コントロール](images/uvc-1-15-08.png)

GET_RES、GET_MIN、GET_MAX、GET_CUR 要求とレポート フィールド**bNumEntries** 0 に設定され、追加のフィールドがあるためありません。

GET_DEF 要求には、extrinsics 情報が使用可能なすべてのエンドポイントが一覧表示されます。

##### <a name="2229-camera-intrinsics-control"></a>2.2.2.9 カメラの組み込みコントロール

このコントロールは、カメラの組み込みデータは、ビデオ コントロールのインターフェイスに関連付けられているビデオのストリーミング インターフェイス上のエンドポイントを取得する、ホスト ソフトウェアを使用できます。 各エンドポイントのために取得したデータは、属性 (IMFDeviceTransform::GetOutputStreamAttributes 呼び出しを使用して取得した)、対応するストリームの属性ストアで MFStreamExtension_PinholeCameraIntrinsics として表示されます。

![カメラの組み込みコントロール](images/uvc-1-15-09.png)

GET_RES、GET_MIN、GET_MAX、GET_CUR 要求とレポート フィールド**bNumEntries** 0 に設定され、追加のフィールドがあるためありません。

GET_DEF 要求には、使用可能な組み込みの情報が含まれるすべてのエンドポイントは一覧表示します。

##### <a name="22210-metadata-control"></a>2.2.2.10 メタデータ コントロール

このコントロールは、クエリを実行し、カメラによって生成されるメタデータを制御するには、ホスト ソフトウェアを使用できます。 これは、すべてのビデオ ストリーミング、ビデオ コントロールのインターフェイスに関連付けられているインターフェイスのすべてのエンドポイントに影響を与えるグローバル コントロールです。 このコントロールにマップ[ **KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA** ](ksproperty-cameracontrol-extended-metadata.md)カメラ ドライバー。

![コントロールのメタデータ](images/uvc-1-15-metadata-control.png)

SET_CUR 要求は、ファームウェアによってサポートされている場合、次の処理が適用されます。

- GET_MIN、GET_DEF 要求はフィールド dwValue を 0 に設定をレポートする必要があります。
- GET_RES 要求は、GET_MAX 要求によって報告された同じ値であるフィールド dwValue を報告する必要があります。
- 0 に設定する dwValue に SET_CUR 要求が受信されると、カメラはすべてのメタデータを作成できません。 DwValue GET_MAX 要求によって報告された同じ値に設定と SET_CUR 要求が受信されると、カメラは、メタデータを生成できるし、このようなメタデータのサイズは、任意のフレームの dwValue を超えることはできません。

SET_CUR 要求が、ファームウェアによってサポートされていない場合、次の処理が適用されます。

- GET_MIN、GET_DEF 要求には、フィールド dwValue に GET_MAX 要求によって報告された値が同じであるものと報告します。
- GET_RES 要求では、フィールド dwValue を 0 に設定を報告します。
- カメラがメタデータを生成し、このようなメタデータの合計サイズは、任意のフレームの dwValue - GET_MAX 要求によって報告された –、時間、UsbVideoHeader メタデータ ペイロードのサイズ以下の 1024 バイトを超えることはできません。  
- UsbVideoHeader メタデータのペイロードは、sizeof(KSCAMERA_METADATA_ITEMHEADER) + sizeof(KSTREAM_UVC_METADATA) または 24 バイトです。
生成されたメタデータは、2.2.3 セクションで説明されている Microsoft 標準形式のメタデータに準拠しているものとします。

##### <a name="22211-ir-torch-control"></a>2.2.2.11 IR Torch コントロール

このコントロールは、IR LED ハードウェア レポートの範囲を制御でき、制御する機能を提供するための柔軟な手段を提供します。  これは、すべてのビデオ ストリーミング、カメラに接続されている IR への lamp の電源を調整することによって、ビデオ コントロールのインターフェイスに関連付けられているインターフェイスのすべてのエンドポイントに影響を与えるグローバル コントロールです。 このコントロールにマップ[ **KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE** ](ksproperty-cameracontrol-extended-irtorchmode.md)カメラ ドライバー。

![IR Torch コントロール](images/uvc-1-15-irtorch-control.png)

次の処理が適用されます。

- GET_LEN 要求は、8 の値を報告する必要があります。
- GET_INFO 要求では、3 を報告します。  この値は、同期 GET_CUR と SET_CUR をサポートするコントロールを示します。
- GET_MIN 要求は、0 および dwValue に最低限の電力を示す値を設定する設定フィールドの寸法を報告する必要があります。  0 の電源レベルは OFF である可能性がありますが、動作可能な最小電力レベルは、0 にコールする必要はありません。
- GET_RES 要求は、0 および dwValue のセットに設定するフィールドの寸法をレポートは、GET_MAX(dwValue) – 以下の数値を GET_MIN(dwValue) などその GET_MAX(dwValue) – GET_MIN(dwValue) は、この値で均等に分割します。  dwValue には、ゼロ (0) をできない可能性があります。
- GET_MAX 要求は、このコントロールの機能を識別するために、D [0-2] のビットを設定で設定フィールドの寸法を報告する必要があります。  寸法は、D0 セット、OFF がサポートされている、他の少なくとも 1 つのビット設定が必要になることを示す、アクティブな状態をサポートしているビットがする必要があります。  dwValue は、通常の電源を示す値を設定する必要があります。
- GET_DEF 要求は、ストリーミングを開始する前に、システムがでなければなりません、既定のモードに設定フィールドの寸法を報告する必要があります。  寸法は、(ON) 2 または 4 (繰り返し) に設定する必要があります。  dwValue は、FaceAuth コントロールに通常使用電力レベルに設定する必要があります。  dwValue は、製造元によって定義されます。
- GET_CUR 要求にはレポート フィールド寸法の現在の操作モードに設定および dwValue の現在の照明に設定を指定します。
- SET_CUR 要求が受信されると、IR Torch は要求された動作モードを使用して prorate 輝度に、照明を設定します。

IR トーチを出力する必要があります、 [ **MF_CAPTURE_METADATA_FRAME_ILLUMINATION** ](standardized-extended-controls-.md)のすべてのフレームの属性。  デバイス MFT またはを含めることによってこれを提供できます、 **MetadataId_FrameIllumination**カメラからのメタデータのペイロード内の属性。  2.2.3.4.4 セクションを参照してください。  

このメタデータの唯一の目的は、フレームが点灯しているかどうかどうかを示すです。  これは、同じメタデータが必要な[ **KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE** ](ksproperty-cameracontrol-extended-faceauth-mode.md) DDI、 **MSXU_FACE_AUTHENTICATION_CONTROL**セクションで定義されています。2.2.2.7 します。  

#### <a name="223-metadata"></a>2.2.3 メタデータ

フレームのメタデータの標準形式のデザインは、Windows 10 から UVC カスタム メタデータのデザインに基づいています。 Windows 10 では、UVC のカスタム メタデータをサポート、カメラのドライバーをカスタム INF を使用して (注: カメラのドライバーは、Windows USBVIDEO に基づくことができます。SYS がカスタム INF はを介してメタデータを特定のハードウェアに必要) です。 場合`MetadataBufferSizeInKB<PinIndex>`レジストリ エントリが存在し、0 以外の場合、その pin でのカスタム メタデータはサポートされてし、値がメタデータに使用するバッファー サイズを示します。 `<PinIndex>`フィールドをピン留めするビデオのインデックスの 0 から始まるインデックスを示します。

Windows 10 バージョン 1703、カメラのドライバーは、次 AddReg エントリを含めることによって Microsoft 標準形式のメタデータのサポートを通知できます。

`StandardFormatMetadata<PinIndex>` :REG_DWORD:0x0 (NotSupported) 0x1 (サポート)

このレジストリ キーは DevProxy によって読み取られ、KSSTREAM_METADATA_INFO 構造の Flags フィールドで KSSTREAM_METADATA_INFO_FLAG_STANDARDFORMAT フラグを設定して、メタデータが標準の形式である UVC ドライバーに通知します。

##### <a name="2231-microsoft-standard-format-metadata"></a>2.2.3.1 Microsoft の標準形式のメタデータ

Microsoft の標準形式のメタデータは、次の構造体の 1 つまたは複数のインスタンスを示します。

![標準の形式のメタデータ](images/extension-standard-format-metadata.png)

```cpp
typedef struct tagKSCAMERA_METADATA_ITEMHEADER {
    ULONG MetadataId;
    ULONG Size; // Size of this header + metadata payload following
} KSCAMERA_METADATA_ITEMHEADER, *PKSCAMERA_METADATA_ITEMHEADER;
```

MetadataId フィールドは明確に定義された識別子とカスタムの識別子を含む次の列挙型の定義から識別子 (識別子 > = MetadataId_Custom_Start)。

```cpp
typedef enum {
    MetadataId_Standard_Start = 1,
    MetadataId_PhotoConfirmation = MetadataId_Standard_Start,
    MetadataId_UsbVideoHeader,
    MetadataId_CaptureStats,
    MetadataId_CameraExtrinsics,
    MetadataId_CameraIntrinsics,
    MetadataId_FrameIllumination,
    MetadataId_Standard_End = MetadataId_FrameIllumination,
    MetadataId_Custom_Start = 0x80000000,
} KSCAMERA_MetadataId;
```

サイズのフィールドは、sizeof(KSCAMERA_METADATA_ITEMHEADER) + sizeof(Metadata Payload) に設定されます。

##### <a name="2232-firmware-generated-standard-format-metadata-from-usb-video-frame-packets"></a>2.2.3.2 USB ビデオ フレーム パケットからの標準フォーマットのファームウェアによって生成されたメタデータ

UVC 経由でフレーム ベースのビデオの転送中にビデオのフレームは、一連のパケットに packetized、先頭に UVC ペイロード ヘッダー。 各 UVC ペイロード ヘッダーは、USB ビデオ クラス ドライバー フレーム ベースのペイロードの仕様によって定義されます。

**ペイロードのヘッダー**

フレーム ベースの形式のペイロード ヘッダー形式の説明を次に示します。

![ペイロードのヘッダー](images/uvc-1-15-10.png)

**HLE (ヘッダーの長さ) フィールド**

ヘッダーの長さのフィールドをヘッダーの長さを指定します (バイト単位)。

**ビット フィールドのヘッダー フィールド**

*FID:フレームの識別子*

- このビットを使用して、各フレームの開始境界で切り替えますは、フレームの残りの部分で、一定のままです。

*EOF:フレームの終了*

- このビットは、ビデオ フレームの終了を示します、フレームに属している、前回のビデオ サンプルで設定されます。 このビットを使用して、フレーム転送の完了の待機時間を短縮するよう最適化でありは省略可能です。

*PTS:プレゼンテーション タイムスタンプ*

- このビット設定、PTS フィールドの存在を示します。

*SCR の場合:ソースのクロックの参照*

- このビット設定、SCR のフィールドの存在を示します。

*RES:予約されています。*

- 0 に設定します。

*STI:静止画像*

- このビット セットは、静止画像に属するものとしてビデオ サンプルを識別します。

*エラーします。エラー ビット*

- このビット設定、デバイスのストリーミングではエラーを示します。

*EOH:ヘッダーの終わり*

- このビット設定、BFH フィールドの末尾を示します。

*PTS:プレゼンテーション タイムスタンプ、サイズ:4 バイトで、値:数*

- PTS フィールドでは、BFH [0] フィールドで PTS ビットが設定されている場合があります。 ヘッダーを表示セクション 2.4.3.3"ビデオとまだイメージ ペイロード"で、*ビデオ デバイスの USB デバイス クラス定義*仕様。

*SCR の場合:ソースの時計の参照、サイズ:6 バイトは、値:数*

- SCR フィールドでは、BFH [0] フィールドに、SCR のビットが設定されている場合があります。 2.4.3.3 を参照してください*ビデオとイメージのペイロード ヘッダーも*で、*ビデオ デバイスの USB デバイス クラス定義*仕様。

既存の UVC ドライバー HLE フィールドは、12 バイト (PTS/SCR 存在) を 2 バイト (ありません PTS/SCR 存在) または最大のいずれかに固定されます。 ただし、サイズのバイトのフィールドでは、中、HLE フィールドは最大 255 バイト ヘッダー データの可能性がありますを指定できます。 ときにペイロード ヘッダーの最初の 12 バイトがビデオに固有の標準メタデータとして選択し、追加のデータの次のフレーム場合両方 PTS/SCR は、設定されており、HLE を超える 12 バイト、INF エントリ`StandardFormatMetadata<PinIndex>`設定されます。

フレーム (ファームウェアによって生成される) 標準形式のメタデータは、そのフレームを表すビデオ フレームのパケット内に見つかった部分的な blob を連結することによって取得されます。

![メタデータのフレームのパケット](images/extension-metadata-frame-packets.png)

##### <a name="2233-metadata-buffer-provided-to-user-mode-component"></a>2.2.3.3 ユーザー モード コンポーネントに提供されるメタデータ バッファー

ユーザー モード コンポーネントに提供されるメタデータのバッファーになります (UVC ドライバーによって生成された) UVC タイムスタンプの後にファームウェアによって生成されたメタデータ項目メタデータ項目と、次のようにレイアウトは。

![メタデータのバッファー](images/extension-metadata-buffer.png)

##### <a name="2234-metadata-format-for-standard-metadata-identifiers"></a>2.2.3.4 標準のメタデータの識別子のメタデータ形式

ファームウェアには、識別子に対応するメタデータを生成するかどうかを選択できます。 ファームウェアを識別子に対応するメタデータを生成する場合は、その識別子のメタデータがファームウェアによって出力されるすべてのフレームに存在する必要があります。

###### <a name="22341-metadataidcapturestats"></a>2.2.3.4.1 MetadataId_CaptureStats

この識別子に対するメタデータの形式は、次の構造によって定義されます。

```cpp
typedef struct tagKSCAMERA_METADATA_CAPTURESTATS {
    KSCAMERA_METADATA_ITEMHEADER Header;
    ULONG Flags;
    ULONG Reserved;
    ULONGLONG ExposureTime;
    ULONGLONG ExposureCompensationFlags;
    LONG ExposureCompensationValue;
    ULONG IsoSpeed;
    ULONG FocusState;
    ULONG LensPosition; // a.k.a Focus
    ULONG WhiteBalance;
    ULONG Flash;
    ULONG FlashPower;
    ULONG ZoomFactor;
    ULONGLONG SceneMode;
    ULONGLONG SensorFramerate;
} KSCAMERA_METADATA_CAPTURESTATS, *PKSCAMERA_METADATA_CAPTURESTATS;
```

**フラグ**フィールドがいっぱいになるし、有効なデータ、構造体の後で、フィールドのどれを示します。 Flags フィールドには、フレーム間ものと変わりません。 現時点では、次のフラグが定義されています。

```cpp
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_EXPOSURETIME            0x00000001
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_EXPOSURECOMPENSATION    0x00000002
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_ISOSPEED                0x00000004
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_FOCUSSTATE              0x00000008
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_LENSPOSITION            0x00000010
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_WHITEBALANCE            0x00000020
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_FLASH                   0x00000040
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_FLASHPOWER              0x00000080
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_ZOOMFACTOR              0x00000100
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_SCENEMODE               0x00000200
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_SENSORFRAMERATE         0x00000400
```

**占有**フィールドが将来に予約されており、0 に設定する必要があります。

**ExposureTime**フィールドには、フレームをキャプチャしたとき、センサーに適用される、100 ナノ秒の露出時間が含まれています。 これ対応する MF サンプル MF_CAPTURE_METADATA_EXPOSURE_TIME 属性として表示されます。

**ExposureCompensationFlags**フィールドには、EV (正確にフラグを設定するものと KSCAMERA_EXTENDEDPROP_EVCOMP_XXX 手順の 1 つ) 補正手順は EV 報酬値を伝達するために使用します。 **ExposureCompensationValue**フィールドには、フレームをキャプチャしたとき、センサーに適用される手順の単位で EV 報酬値が含まれています。 これら対応する MF サンプル MF_CAPTURE_METADATA_EXPOSURE_COMPENSATION 属性として表示されます。

**IsoSpeed**フィールドに、フレームをキャプチャしたときに、センサーを適用する ISO の速度値が含まれています。 これは単位です。 これ対応する MF サンプル MF_CAPTURE_METADATA_ISO_SPEED 属性として表示されます。

**FocusState**フィールドには KSCAMERA_EXTENDEDPROP_FOCUSSTATE 列挙型で定義されている値のいずれかを実行する現在のフォーカス状態が含まれています。 これ対応する MF サンプル MF_CAPTURE_METADATA_FOCUSSTATE 属性として表示されます。

**LensPosition**単位は、フレームがキャプチャされたときにフィールドに論理レンズの位置が含まれます。 これは、GET 呼び出しで KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUS から照会できる値と同じです。 これ対応する MF サンプル MF_CAPTURE_METADATA_LENS_POSITION 属性として表示されます。

**ホワイト バランス**ケルビンで値をフレームをキャプチャしたときに、センサーに適用するホワイト バランスがフィールドに含まれています。 これ対応する MF サンプル MF_CAPTURE_METADATA_WHITEBALANCE 属性として表示されます。

**Flash**フィールドには、オフ、フレームをキャプチャしたときに、1 は、flash および 0 の意味 flash でブール値が含まれています。 これ対応する MF サンプル MF_CAPTURE_METADATA_FLASH 属性として表示されます。

**FlashPower**フィールドには、範囲内の値は、キャプチャされたフレームに適用されるフラッシュの電源の [0, 100]。 ドライバーが調整可能な power flash をサポートしていない場合、このフィールドを省略する必要があります。 これ対応する MF サンプル MF_CAPTURE_METADATA_FLASH_POWER 属性として表示されます。

**ZoomFactor**フィールドには、キャプチャされたフレームに適用される Q16 形式でズーム値が含まれています。 これ対応する MF サンプル MF_CAPTURE_METADATA_ZOOMFACTOR 属性として表示されます。

**SceneMode**フィールドには、64 ビット KSCAMERA_EXTENDEDPROP_SCENEMODE_XXX フラグは、キャプチャされたフレームに適用される、シーンのモードが含まれています。 これ対応する MF サンプル MF_CAPTURE_METADATA_SCENE_MODE 属性として表示されます。

**SensorFramerate**フィールドは、フレームをキャプチャしたら、上部の 32 ビットで分子の値との下位 32 ビットの分母の値で構成されるヘルツ センサーの測定値のレートを格納します。 これ対応する MF サンプル MF_CAPTURE_METADATA_SENSORFRAMERATE 属性として表示されます。

###### <a name="22342-metadataidcameraextrinsics"></a>2.2.3.4.2 MetadataId_CameraExtrinsics

この識別子に対するメタデータの形式では、バイト配列のペイロードを続けて標準 KSCAMERA_METADATA_ITEMHEADER 必要があります。 ペイロードに揃える必要があります、 [MFCameraExtrinsics](https://msdn.microsoft.com/library/windows/desktop/mt740392)構造とそれに続く 0 個以上[MFCameraExtrinsic_CalibratedTransform](https://msdn.microsoft.com/library/windows/desktop/mt740393)構造体。 使用されていないすべてのバイトのペイロードの最後に行う必要があるし、0 に設定して、ペイロードは 8 バイトでアラインにあります。

###### <a name="22343-metadataidcameraintrinsics"></a>2.2.3.4.3 MetadataId_CameraIntrinsics

この識別子に対するメタデータの形式では、バイト配列のペイロードを続けて標準 KSCAMERA_METADATA_ITEMHEADER 必要があります。 ペイロードに揃える必要があります、 [MFPinholeCameraIntrinsics](https://msdn.microsoft.com/library/windows/desktop/mt740396)構造体。 使用されていないすべてのバイトのペイロードの最後に行う必要があるし、0 に設定して、ペイロードは 8 バイトでアラインにあります。

###### <a name="22344-metadataidframeillumination"></a>2.2.3.4.4 MetadataId_FrameIllumination

この識別子に対するメタデータの形式は、次の構造によって定義されます。

```cpp
typedef struct tagKSCAMERA_METADATA_FRAMEILLUMINATION {
    KSCAMERA_METADATA_ITEMHEADER Header;
    ULONG Flags;
    ULONG Reserved;
} KSCAMERA_METADATA_FRAMEILLUMINATION, *PKSCAMERA_METADATA_FRAMEILLUMINATION;
```

**フラグ**フィールドは、キャプチャされたフレームに関する情報を示します。 現時点では、次のフラグが定義されています。

```cpp
#define KSCAMERA_METADATA_FRAMEILLUMINATION_FLAG_ON 0x00000001
```

照明が存在していたときに、フレームをキャプチャした場合、フラグ KSCAMERA_METADATA_FRAMEILLUMINATION_FLAG_ON 設定するものとします。 それ以外の場合、このフラグは設定できません。

**占有**フィールドは将来使用するために予約されていると、0 に設定する必要があります。
