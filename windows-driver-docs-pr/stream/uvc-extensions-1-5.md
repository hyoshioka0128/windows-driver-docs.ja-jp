---
title: USB ビデオ クラス 1.5 仕様に対する Microsoft の拡張機能
description: 新しいコントロールと、適切に定義されたフレームメタデータを標準形式で実行する機能を有効にする、USB Video Class 1.5 仕様の Microsoft の拡張機能について説明します。
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.custom: rs5, 19H1
ms.openlocfilehash: c4c3cc05b84a44ad6c07fd474008266fdd26b32a
ms.sourcegitcommit: baf3075858705d4c78d4ea4b0869bf6291bcb823
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2020
ms.locfileid: "85112142"
---
# <a name="microsoft-extensions-to-usb-video-class-15-specification"></a>USB ビデオ クラス 1.5 仕様に対する Microsoft の拡張機能

## <a name="1-overview"></a>1概要

### <a name="11-summary"></a>1.1 概要

[USB ビデオクラス仕様](https://www.usb.org/document-library/video-class-v15-document-set)に対する Microsoft の拡張機能により、新しいコントロールだけでなく、適切に定義されたフレームメタデータを標準形式で実行する機能が有効になります。

### <a name="12-architecture-decisions"></a>1.2 アーキテクチャの決定

USB Video Class (UVC) フレームメタデータのサポートは、ISOCH と一括エンドポイントで使用できます。 ただし、一括エンドポイントの場合、メタデータのサイズは240バイトに制限されます (すべてのビデオフレームデータが一括エンドポイントで1つのビデオフレームパケットで転送されるため)。

UVC メタデータのサポートは、フレームベースのペイロードでのみ使用できます。

UVC メタデータのサポートは、メディアファンデーション (MF) キャプチャパイプラインを通じてのみ使用できます。

UVC メタデータはオプトインされます。 メタデータをサポートする必要があるすべての IHV/OEM は、カスタムの INF ファイルを使用してこれを有効にする必要があります。

UVC メタデータは、システムによって割り当てられたメモリのみをサポートします。 VRAM または DX サーフェイスはサポートされません。

## <a name="2-architectural-overview"></a>2アーキテクチャの概要

### <a name="21-description"></a>2.1 の説明

#### <a name="221-capability-discovery-through-inf"></a>2.2.1 INF を使用した機能の検出

##### <a name="2211-still-image-capture--method-2"></a>2.2.1.1 静止イメージキャプチャ–方法2

一部の既存の UVC デバイスは、 *uvc 1.5 specification.pdfクラス*のセクション 2.4.2.4 (静止イメージキャプチャ) で説明されている方法2をサポートしていない可能性があります。このメソッドは、 [USB Video class specification](https://www.usb.org/document-library/video-class-v15-document-set) web サイトからダウンロードできます。

Windows 10 バージョン1607以前では、デバイスが UVC 1.5 仕様に従ってサポートを提供している場合でも、キャプチャパイプラインはメソッド2を利用しませんでした。

Windows 10 バージョン1703では、この方法を利用するデバイスでは、カメラドライバーにカスタムの INF ファイルを使用する必要がありますが、メソッド2で静止したイメージのキャプチャを有効にするために、特定のハードウェアにカスタムの INF が必要です。

注: カメラドライバーは、Windows USBVIDEO.SYS をベースにすることも、カスタムのドライバーバイナリに基づいて作成することもできます。

カスタム INF ファイル (カスタム UVC ドライバーまたは受信トレイ UVC ドライバー) には、次の AddReg エントリが含まれている必要があります。

**EnableDependentStillPinCapture**: REG_DWORD: 0X0 (無効) から 0X1 (有効)

このエントリが有効 (0x1) に設定されている場合、キャプチャパイプラインでは引き続きイメージのキャプチャにメソッド2を利用します (このファームウェアでは、UVC 1.5 仕様で指定されている方法2のサポートもアドバタイズされることを前提としています)。

カスタム INF セクションの例を次に示します。

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

#### <a name="222-extension-unit-controls"></a>2.2.2 拡張機能の単位コントロール

新しいコントロールを有効にするための**USB ビデオクラス仕様**に対する microsoft の拡張機能は、GUID MS_CAMERA_CONTROL_XU (microsoft-xu と呼ばれます) で識別される拡張機能ユニットを介して行われます。

```cpp
// {0F3F95DC-2632-4C4E-92C9-A04782F43BC8}
DEFINE_GUID(MS_CAMERA_CONTROL_XU,
    0xf3f95dc, 0x2632, 0x4c4e, 0x92, 0xc9, 0xa0, 0x47, 0x82, 0xf4, 0x3b, 0xc8);
```

デバイスファームウェアによって実装された Microsoft-XU は、次のサブセクションで定義されている新しいコントロールを格納します。 次の要求定義は、そのコントロールに対してオーバーライド定義が明示的に指定されている場合を除き、すべてのコントロールに適用されます。 D3、D4、GET_INFO などの定義については、 **Uvc 1.5 クラス specification.pdf**を参照してください。

GET_INFO 要求では、自動更新と非同期機能を使用せずにコントロールを報告する必要があります (つまり、D3 と D4 のビットは0に設定する必要があります)。

GET_LEN 要求は、このコントロールのペイロードの最大長 (**Wlength**) を報告します。

GET_RES 要求では、 **Qwvalue/dwValue**の解決 (ステップサイズ) を報告します。 その他のすべてのフィールドは0に設定する必要があります。

GET_MIN 要求では、 **Qwvalue/dwValue**のサポートされる最小値が報告されます。 その他のすべてのフィールドは0に設定する必要があります。

GET_MAX 要求では、 **Qwvalue/dwValue**のサポートされる最大値が報告されます。 また、 **Bmcontrolflags**では、サポートされているすべてのフラグを1に設定する必要があります。 その他のすべてのフィールドは0に設定する必要があります。

GET_DEF 要求と GET_CUR 要求では、" **Qwvalue/dwValue** " フィールドと " **Bmcontrolflags**" フィールドにそれぞれ既定値と現在の設定がレポートされます。 その他のすべてのフィールドは0に設定する必要があります。

すべてのフィールドを設定した後、ホストによって SET_CUR 要求が発行されます。

次の表は、Microsoft-XU のコントロールセレクターをそれぞれの値にマップし、拡張単位記述子の*Bmcontrols*フィールドのビット位置を示しています。

![拡張機能の単位コントロール](images/uvc-1-15-01.png)

##### <a name="2221-cancelable-asynchronous-controls"></a>2.2.2.1 キャンセル可能非同期コントロール

ここでは、自動更新機能を利用して、キャンセル可能な非同期コントロールを定義します。

GET_INFO 要求では、このようなコントロールを自動更新コントロールとして報告する必要があります (たとえば、D3 ビットを1に設定する必要がありますが、たとえば D4 ビットは0に設定されます)。

このようなコントロールでは、SET_CUR 要求を発行して新しい値 ( **bmOperationFlags: d0**ビットが0に設定された SET_CUR (normal) 要求) を設定したり、前の SET_CUR (通常の) 要求 ( **bmOperationFlags: d0**ビットが1に設定されている SET_CUR (キャンセル) 要求) をキャンセルしたりできます。 SET_CUR 要求は、要求が受信されるとすぐにデバイスによって完了される必要があります (ハードウェアが構成されていないか、要求された新しい設定に収束している場合でも)。 デバイスは、SET_CUR (通常の) 要求ごとに、新しい設定が適用されたとき、または SET_CUR (キャンセル) 要求が到着したときに発生する、このコントロールの対応するコントロール変更割り込みを生成します。この割り込みが到着するまでは、SET_CUR (通常) の要求が進行中であると見なされます。 SET_CUR (通常) の要求が進行中の場合、この特定のコントロールに対する追加の SET_CUR (通常) 要求によって、エラーが発生します。 SET_CUR (キャンセル) 要求は常に成功します。 キャンセルするものがない場合、デバイスは何も行いません。

制御変更割り込みペイロードでは、SET_CUR (NORMAL) によって指定された設定が適用された場合 (つまり収束が発生した場合)、ビット**bmOperationFlags: D0**が0に設定されます。これは、SET_CUR (通常) 要求の後に発生した SET_CUR (キャンセル) 要求のために設定が適用されなかった場合 (つまり

##### <a name="2222-focus-control"></a>2.2.2.2 フォーカスコントロール

このコントロールにより、ホストソフトウェアはカメラのフォーカス設定を指定できます。 これは、ビデオコントロールインターフェイスに関連付けられているすべてのビデオストリーミングインターフェイスのすべてのエンドポイントに影響を与えるグローバルコントロールです。

![フォーカスコントロール](images/uvc-1-15-02.png)

このコントロールは、キャンセル可能な非同期コントロールとして機能する必要があります (GET_INFO 要求の要件と SET_CUR 要求の機能動作の詳細については、「」を参照してください)。

GET_MAX 要件: このコントロールでは、 **Bmcontrolflags**にビット D0、D1、D2、D8、D18 のサポートを提供する必要があります。

GET_DEF 要件: **Bmcontrolflags**の既定値は D0 で、D18 は1に設定され、 **dwValue**は0に設定されている必要があります。

GET_CUR/SET_CUR 要求の場合、フィールド**Bmcontrolflags**には次の制限が適用されます。

- D0、D1、および D8 ビットの間では、1つのビットのみを設定できます。D2 ビットが設定されている場合は、どの設定も有効になりません。

- D16、D17、D18、D19、D20 の間では、1つのビットのみを設定できます。どの設定も有効ではありません。

- D1 は、現在定義されている他のすべてのビット (D0、D2、D8、D16、D17、D18、D19、および D20) と互換性がありません。

- D2 は D1 および D8 と互換性がありません。

D2 が設定されていない場合、D16、D17、D18、D19、および D20 と互換性がありません。

##### <a name="2223-exposure-control"></a>2.2.2.3 露出コントロール

このコントロールにより、ホストソフトウェアはカメラの露出設定を指定できます。 これは、ビデオコントロールインターフェイスに関連付けられているすべてのビデオストリーミングインターフェイスのすべてのエンドポイントに影響を与えるグローバルコントロールです。

![露出コントロール](images/uvc-1-15-03.png)

GET_INFO 要求では、このコントロールを非同期コントロールとして報告する必要があります (つまり、D4 ビットは1に設定されている必要があります) が、自動更新コントロール (D3 ビットは0に設定されている必要があります) ではありません。

GET_MAX 要件: このコントロールでは、 **Bmcontrolflags**にビット D0、D1、および D2 のサポートを提供する必要があります。

GET_DEF 要件: **Bmcontrolflags**の既定値は、D0 を1に設定し、 **qwvalue**を0に設定する必要があります。

GET_CUR/SET_CUR 要求の場合、フィールド**Bmcontrolflags**には次の制限が適用されます。

- D0、D1、および D2 ビットの中で、少なくとも1つのビットを設定する必要があります。

- D1 は、D0 および D2 と互換性がありません。

##### <a name="2224-ev-compensation-control"></a>2.2.2.4 EV 補正コントロール

このコントロールにより、ホストソフトウェアは、カメラの EV 補正設定を指定できます。 これは、ビデオコントロールインターフェイスに関連付けられているすべてのビデオストリーミングインターフェイスのすべてのエンドポイントに影響を与えるグローバルコントロールです。

![EV 補正コントロール](images/uvc-1-15-04.png)

GET_INFO 要求では、このコントロールを非同期コントロールとして報告する必要があります (つまり、D4 ビットは1に設定されている必要があります) が、自動更新コントロール (D3 ビットは0に設定されている必要があります) ではありません。

GET_RES 要求では、 **Bmcontrolflags**で対応するビットを設定することによって、サポートされているすべての解像度 (ステップサイズ) を報告する必要があります。 その他のすべてのフィールドは0に設定する必要があります。

GET_MIN 要求と GET_MAX 要求では、 **dwValue**でサポートされる最小値と最大値が報告されます。 ビット D4 (ステップサイズ1を示す) は、 **Bmcontrolflags**で唯一のビットセットである必要があります。 その他のすべてのフィールドは0に設定する必要があります。

GET_DEF、GET_CUR、SET_CUR の要求は、セクション2.2.2.1 の定義に従っている必要がありますが、フィールド**Bmcontrolflags**では、D0、D1、D2、D3、D4 の各ビットの間に1つのビットだけを設定する必要があります。 さらに、GET_DEF 要求では**dwValue**が0に設定されている必要があります。

##### <a name="2225-white-balance-control"></a>2.2.2.5 ホワイトバランス制御

このコントロールにより、ホストソフトウェアは、カメラの白のバランス設定を指定できます。 これは、ビデオコントロールインターフェイスに関連付けられているすべてのビデオストリーミングインターフェイスのすべてのエンドポイントに影響を与えるグローバルコントロールです。

![ホワイトバランス制御](images/uvc-1-15-05.png)

GET_INFO 要求では、このコントロールを非同期コントロールとして報告する必要があります (つまり、D4 ビットは1に設定されている必要があります) が、自動更新コントロール (D3 ビットは0に設定されている必要があります) ではありません。

GET_RES、GET_MIN、GET_MAX 要求は、セクション2.2.2.1 の定義に従っている必要がありますが、 **Dwvalueformat**を1に設定する必要があります。

GET_MAX 要件: このコントロールでは、 **Bmcontrolflags**にビット D0、D1、および D2 のサポートを提供する必要があります。

GET_DEF 要件: **Bmcontrolflags**の既定値は、D0 を1、 **dwvalueformat**に設定し、dwValue を0に設定する必要があります。

GET_CUR/SET_CUR 要求の場合、フィールド**Bmcontrolflags**には次の制限が適用されます。

- D0、D1、および D2 ビットの中で、少なくとも1つのビットを設定する必要があります。

- D1 は、D0 および D2 と互換性がありません。

##### <a name="2226-iso-control"></a>2.2.2.6 ISO コントロール

このコントロールにより、ホストソフトウェアは、カメラ上の静止イメージキャプチャの ISO フィルム速度設定を指定できます。 このコントロールは、指定されたビデオ/静止エンドポイント (ビデオコントロールインターフェイスに関連付けられているすべてのビデオストリーミングインターフェイス上のすべてのビデオ/静止エンドポイントのサブセットである) にのみ適用されます。 まだキャプチャのためのメソッド1が使用されている場合、このコントロールはビデオエンドポイントでサポートされている必要があります。 メソッド2またはメソッド3を引き続きキャプチャする場合は、このコントロールが引き続きエンドポイントでサポートされている必要があります。

![ISO コントロール](images/uvc-1-15-06.png)

GET_INFO 要求では、このコントロールを非同期コントロールとして報告する必要があります (つまり、D4 ビットは1に設定されている必要があります) が、自動更新コントロール (D3 ビットは0に設定されている必要があります) ではありません。

GET_RES、GET_MIN、GET_MAX、GET_DEF、GET_CUR 要求は、セクション2.2.2.1 の定義に従っている必要があります。 また、これらの要求の出力には、D0 (Auto モード) または D52 (手動モード) のいずれかに対応するエンドポイントだけが一覧表示されます。つまり、エンドポイントが D0 または D52 のいずれかである場合は、一覧に表示されます。それ以外の場合、一覧に表示されません。

##### <a name="2227-face-authentication-control"></a>2.2.2.7 Face 認証コントロール

このコントロールにより、ホストソフトウェアは、顔認証に使用されるストリーミングモードをカメラがサポートするかどうかを指定できます。 このコントロールは、カメラが顔認証をサポートする場合にのみサポートされます。

このコントロールは、赤外線 (IR) データを生成できるカメラにのみ適用され、指定されたビデオエンドポイント (ビデオコントロールインターフェイスに関連付けられているすべてのビデオストリーミングインターフェイスのすべてのビデオエンドポイントのサブセット) にのみ適用されます。

![顔認証コントロール](images/uvc-1-15-07.png)

GET_RES 要求と GET_MIN 要求では、フィールド**Bnumentries**が0に設定されているため、追加のフィールドはありません。

GET_MAX 要求の場合、 **Bmcontrolflags**フィールドのビットを1に設定すると、対応するモードがそのエンドポイントでサポートされていることが示されます。 GET_MAX 要求の出力には、D1 または D2 のいずれかに対応するエンドポイントのみが表示されます (つまり、エンドポイントが D1 または d2 のいずれかに対応している場合は一覧表示されます。それ以外の場合は一覧に表示されません)。 また、D1 と D2 の両方に対応できるように、エンドポイントを提供する必要はありません。 エンドポイントが一般的な目的で動作することが予想される場合 (つまり、顔認証の場合を除きます)、そのエンドポイントの場合は D0 を1に設定する必要があります (D1/D2 に加えて)。

GET_DEF/GET_CUR/SET_CUR 要求の場合、1に設定されたビットは、対応するモードがそのエンドポイントに対して選択されていることを示します。 これらの要求では、特定のエンドポイントに対して1ビットのみ (D0、D1 & D2) を設定する必要があります。 既定の選択 (実装固有のもの) を返す GET_DEF 要求の場合、エンドポイントが一般的な目的で動作することが予想される場合 (つまり、顔認証の目的ではありません)、そのエンドポイントで D0 を既定で1に設定する必要があります。それ以外の場合は、D1 または D2 (両方ではない) を既定で1に設定する必要があります。 GET_DEF/GET_CUR 要求出力には GET_MAX 要求出力に示されているすべてのエンドポイントに関する情報が含まれている必要があります。ただし、SET_CUR 要求には、GET_MAX 要求出力に記載されているエンドポイントのサブセットのみを含めることができます。

##### <a name="2228-camera-extrinsics-control"></a>2.2.2.8 カメラ Extrの Ics コントロール

このコントロールにより、ホストソフトウェアは、ビデオコントロールインターフェイスに関連付けられているビデオストリーミングインターフェイス上のエンドポイントのカメラ extrを取得できます。 各エンドポイントに対して取得されたデータは、対応するストリームの属性ストア (IMFDeviceTransform:: GetOutputStreamAttributes 呼び出しを使用して取得) の属性 MFStreamExtension_CameraExtrinsics として表示されます。

![カメラ extrの ics コントロール](images/uvc-1-15-08.png)

GET_RES、GET_MIN、GET_MAX、GET_CUR 要求では、フィールド**Bnumentries**が0に設定されます。そのため、フィールドは追加されません。

GET_DEF 要求では、extrの ics 情報が使用可能なすべてのエンドポイントが一覧表示されます。

##### <a name="2229-camera-intrinsics-control"></a>2.2.2.9 Camera 組み込みコントロール

このコントロールにより、ホストソフトウェアは、ビデオコントロールインターフェイスに関連付けられているビデオストリーミングインターフェイス上のエンドポイントのカメラ組み込みデータを取得できます。 各エンドポイントに対して取得されたデータは、対応するストリームの属性ストア (IMFDeviceTransform:: GetOutputStreamAttributes 呼び出しを使用して取得) の属性 MFStreamExtension_PinholeCameraIntrinsics として表示されます。

![カメラの組み込みコントロール](images/uvc-1-15-09.png)

GET_RES、GET_MIN、GET_MAX、GET_CUR 要求では、フィールド**Bnumentries**が0に設定されます。そのため、フィールドは追加されません。

GET_DEF 要求では、使用可能な組み込み情報を持つすべてのエンドポイントが一覧表示されます。

##### <a name="22210-metadata-control"></a>2.2.2.10 Metadata コントロール

このコントロールにより、ホストソフトウェアは、カメラによって生成されたメタデータのクエリや制御を行うことができます。 これは、ビデオコントロールインターフェイスに関連付けられているすべてのビデオストリーミングインターフェイスのすべてのエンドポイントに影響を与えるグローバルコントロールです。 このコントロールは、カメラドライバーによって[**KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA**](ksproperty-cameracontrol-extended-metadata.md)にマップされます。

![メタデータコントロール](images/uvc-1-15-metadata-control.png)

ファームウェアで SET_CUR 要求がサポートされている場合は、次のことが適用されます。

- GET_MIN、GET_DEF 要求では、フィールド dwValue が0に設定されます。
- GET_RES 要求は、GET_MAX 要求によって報告されたのと同じ値としてフィールド dwValue を報告する必要があります。
- DwValue が0に設定された SET_CUR 要求を受信すると、カメラはメタデータを生成しません。 DwValue が GET_MAX 要求によって報告された値と同じ値に設定された SET_CUR 要求を受信すると、カメラはメタデータを生成でき、そのようなメタデータのサイズはどのフレームに対しても dwValue を超えることはできません。

ファームウェアで SET_CUR 要求がサポートされていない場合は、次のことが当てはまります。

- GET_MIN、GET_DEF 要求は、GET_MAX 要求によって報告されたのと同じ値としてフィールド dwValue を報告する必要があります。
- GET_RES 要求では、フィールド dwValue が0に設定されます。
- カメラはメタデータを生成できます。また、このようなメタデータの合計サイズは、GET_MAX 要求によって報告された dwValue を超えることはできません。これは、任意のフレームに対して、UsbVideoHeader メタデータペイロードのサイズが1024バイトになります。  
- UsbVideoHeader メタデータペイロードは、sizeof (KSCAMERA_METADATA_ITEMHEADER) + sizeof (KSTREAM_UVC_METADATA) または24バイトです。
生成されるメタデータは、「2.2.3」で説明されている Microsoft の標準形式のメタデータに準拠している必要があります。

##### <a name="22211-ir-torch-control"></a>2.2.2.11 IR Torch コントロール

このコントロールは、IR LED ハードウェアが制御できる範囲を報告し、制御する機能を提供する、柔軟な手段を提供します。  これは、カメラに接続されている IR ランプの電源を調整することによって、ビデオコントロールインターフェイスに関連付けられているすべてのビデオストリーミングインターフェイス上のすべてのエンドポイントに影響を与えるグローバルコントロールです。 このコントロールは、カメラドライバーによって[**KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE**](ksproperty-cameracontrol-extended-irtorchmode.md)にマップされます。

![IR Torch コントロール](images/uvc-1-15-irtorch-control.png)

次の制約があります。

- GET_LEN 要求は、値8を報告します。
- GET_INFO 要求では、3を報告します。  この値は、GET_CUR と SET_CUR をサポートする同期コントロールを示します。
- GET_MIN 要求では、dwMode を0に設定し、dwValue を最小電力を示す値に設定する必要があります。  電源レベル0はオフであることがありますが、操作の最低電力レベルは0以外である必要があります。
- GET_RES 要求では、フィールド dwMode が0に設定され、dwValue が GET_MAX (dwValue) – GET_MIN (dwValue) 以下の数値に設定され、GET_MAX (dwValue) – GET_MIN (dwValue) がその値で均等に割り切れます。  dwValue を0にすることはできません。
- GET_MAX 要求は、このコントロールの機能を識別するために設定された、bits D [0-2] で設定された dwMode のフィールドを報告します。  dwMode にはビット D0 を設定する必要があります。これは、OFF がサポートされていること、およびアクティブな状態をサポートする他のビットセットが少なくとも1つ必要であることを示します。  dwValue は、通常の電源を示す値に設定する必要があります。
- GET_DEF 要求は、ストリーミングを開始する前に、システムが存在している必要があります dwMode が既定のモードに設定されていることを報告します。  dwMode は、2 (ON) または 4 (交互) に設定する必要があります。  dwValue は、FaceAuth コントロールに通常使用される電源レベルに設定する必要があります。  dwValue は製造元によって定義されます。
- GET_CUR 要求は、[dwMode] を現在の動作モードに設定し、dwValue を現在の照明に設定します。
- SET_CUR 要求を受信すると、IR Torch は、要求された動作モードを使用して、edition の輝度を設定します。

IR Torch は、すべてのフレームに対して[**MF_CAPTURE_METADATA_FRAME_ILLUMINATION**](standardized-extended-controls-.md)属性を生成する必要があります。  これは、デバイスの MFT を通じて、またはカメラからメタデータペイロードに**MetadataId_FrameIllumination**属性を含めることによって提供できます。  「2.2.3.4.4」を参照してください。  

このメタデータの唯一の目的は、フレームが照明されているかどうかを示すことです。  これは[**KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE**](ksproperty-cameracontrol-extended-faceauth-mode.md) DDI で必要とされるメタデータと、セクション2.2.2.7 で定義されている**MSXU_FACE_AUTHENTICATION_CONTROL**と同じです。  

#### <a name="223-metadata"></a>2.2.3 メタデータ

標準形式のフレームメタデータのデザインは、Windows 10 からの UVC カスタムメタデータデザインでビルドされます。 Windows 10 の場合、カスタムメタデータは、カメラドライバー用のカスタム INF を使用した UVC でサポートされています (注: カメラドライバーは Windows USBVIDEO.SYS に基づくことができますが、メタデータを取得するために特定のハードウェアにカスタムの INF が必要です)。 `MetadataBufferSizeInKB<PinIndex>`レジストリエントリが存在し、0以外の場合、その pin ではカスタムメタデータがサポートされ、値はメタデータに使用されるバッファーサイズを示します。 この `<PinIndex>` フィールドは、ビデオの pin のインデックスの0から始まるインデックスを示します。

Windows 10 バージョン1703では、カメラドライバーは、次の AddReg エントリを含めることによって、Microsoft 標準形式のメタデータのサポートに信号を送ることができます。

`StandardFormatMetadata<PinIndex>`: REG_DWORD: 0x0 (NotSupported) から 0x1 (サポートされています)

このレジストリキーは DevProxy によって読み取られ、KSSTREAM_METADATA_INFO 構造の Flags フィールドに KSSTREAM_METADATA_INFO_FLAG_STANDARDFORMAT フラグを設定することによって、メタデータが標準形式であることを UVC ドライバーに通知します。

##### <a name="2231-microsoft-standard-format-metadata"></a>2.2.3.1 Microsoft 標準形式のメタデータ

Microsoft 標準形式のメタデータは、次の構造の1つ以上のインスタンスです。

![標準形式のメタデータ](images/extension-standard-format-metadata.png)

```cpp
typedef struct tagKSCAMERA_METADATA_ITEMHEADER {
    ULONG MetadataId;
    ULONG Size; // Size of this header + metadata payload following
} KSCAMERA_METADATA_ITEMHEADER, *PKSCAMERA_METADATA_ITEMHEADER;
```

MetadataId フィールドは、適切に定義された識別子とカスタム識別子 (識別子 >= MetadataId_Custom_Start) を含む、次の列挙型定義の識別子によって入力されます。

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

Size フィールドは sizeof (KSCAMERA_METADATA_ITEMHEADER) + sizeof (メタデータペイロード) に設定されます。

##### <a name="2232-firmware-generated-standard-format-metadata-from-usb-video-frame-packets"></a>2.2.3.2 ファームウェアによって生成された標準形式のメタデータを USB ビデオフレームパケットから生成する

フレームベースのビデオに対する UVC 経由の転送中、ビデオフレームは一連のパケットに packetized され、それぞれ UVC ペイロードヘッダーが前に付いています。 各 UVC ペイロードヘッダーは、USB ビデオクラスドライバーフレームベースのペイロード仕様によって定義されます。

**ペイロードヘッダー**

次に、フレームベースの形式のペイロードヘッダー形式について説明します。

![ペイロードヘッダー](images/uvc-1-15-10.png)

**HLE (ヘッダー長) フィールド**

ヘッダー長フィールドは、ヘッダーの長さをバイト単位で指定します。

**ビットフィールドヘッダーフィールド**

*FID: フレーム識別子*

- このビットは、各フレームの開始境界で切り替わり、フレームの残りの部分では一定のままになります。

*EOF: フレームの終わり*

- このビットは、ビデオフレームの終わりを示し、フレームに属する最後のビデオサンプルで設定されています。 このビットの使用は、フレーム転送が完了するまでの待機時間を短縮するための最適化であり、省略可能です。

*PTS: プレゼンテーションタイムスタンプ*

- このビットが設定されている場合、PTS フィールドが存在することを示します。

*SCR: ソースクロックリファレンス*

- このビットが設定されている場合、SCR フィールドが存在することを示します。

*RES: 予約済み。*

- を0に設定します。

*STI: 静止画像*

- このビットが設定されている場合、静止画像に属しているビデオのサンプルを識別します。

*エラー: エラービット*

- このビットが設定されている場合、デバイスのストリーミングでエラーが発生したことを示します。

*EOH: ヘッダーの終わり*

- このビットが設定されている場合は、BFH フィールドの末尾を示します。

*PTS: プレゼンテーションのタイムスタンプ、サイズ: 4 バイト、値: 数値*

- PTS フィールドは、b の BFH [0] フィールドに PTS ビットが設定されている場合に存在します。 ビデオデバイスの仕様については、「 *USB デバイスクラスの定義*」の「ビデオと静止画ペイロードヘッダー」を2.4.3.3。

*SCR: ソースクロック参照、サイズ: 6 バイト、値: 数値*

- SCR フィールドは、SCR ビットが BFH [0] フィールドに設定されている場合に存在します。 ビデオデバイスの仕様については、 *USB デバイスクラス定義*の 2.4.3.3*ビデオと静止画像ペイロードヘッダー*に関するセクションを参照してください。

既存の UVC ドライバーの HLE フィールドは、2バイト (PTS/SCR が存在しない) または最大12バイト (PTS/SCR が存在する) のいずれかに固定されています。 ただし、HLE フィールドはバイトサイズのフィールドであるため、最大255バイトのヘッダーデータを指定できます。 PTS/SCR の両方が存在し、HLE が12バイトより大きい場合、INF エントリが設定されると、ペイロードヘッダーの最初の12バイトに続く追加データが、ビデオフレームに固有の標準メタデータとして選択され `StandardFormatMetadata<PinIndex>` ます。

フレームの標準形式のメタデータ (ファームウェアによって生成される) は、そのフレームを表すビデオフレームパケットで見つかった部分的な blob を連結することによって取得されます。

![メタデータフレームパケット](images/extension-metadata-frame-packets.png)

##### <a name="2233-metadata-buffer-provided-to-user-mode-component"></a>2.2.3.3 ユーザーモードコンポーネントに提供されたメタデータバッファー

ユーザーモードコンポーネントに提供されるメタデータバッファーには、UVC タイムスタンプ (UVC ドライバーによって生成される) のメタデータ項目と、ファームウェアによって生成されるメタデータ項目が含まれます。これらは次のようにレイアウトされます。

![メタデータバッファー](images/extension-metadata-buffer.png)

##### <a name="2234-metadata-format-for-standard-metadata-identifiers"></a>標準メタデータ識別子の2.2.3.4 メタデータ形式

ファームウェアは、識別子に対応するメタデータを生成するかどうかを選択できます。 ファームウェアが id に対応するメタデータを生成することを選択した場合、その識別子のメタデータは、ファームウェアによって出力されるすべてのフレームに存在している必要があります。

###### <a name="22341-metadataid_capturestats"></a>2.2.3.4.1 MetadataId_CaptureStats

この識別子のメタデータ形式は、次の構造によって定義されます。

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

**Flags**フィールドは、構造体の後のフィールドのうち、どのフィールドに有効なデータが格納されているかを示します。 Flags フィールドはフレームごとに異なるものにする必要があります。 現時点では、次のフラグが定義されています。

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

**予約**されているフィールドは、将来使用するために予約されており、0に設定する必要があります。

**ExposureTime**フィールドには、フレームがキャプチャされたときにセンサーに適用される露出時間 (100 ナノ秒単位) が含まれています。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_EXPOSURE_TIME として表示されます。

**ExposureCompensationFlags**フィールドには、ev 補正の値を伝えるために使用される ev 補正ステップ (KSCAMERA_EXTENDEDPROP_EVCOMP_XXX ステップフラグとして設定する必要があります) が含まれています。 **ExposureCompensationValue**フィールドには、フレームがキャプチャされたときにセンサーに適用されるステップの単位での EV 補正値が含まれています。 これらは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_EXPOSURE_COMPENSATION として表示されます。

**Isospeed**フィールドには、フレームがキャプチャされたときにセンサーに適用される ISO 速度の値が含まれます。 これは、単位はありません。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_ISO_SPEED として表示されます。

**FocusState**フィールドには、列挙 KSCAMERA_EXTENDEDPROP_FOCUSSTATE で定義されている値のいずれかを取ることができる現在のフォーカス状態が含まれています。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_FOCUSSTATE として表示されます。

**LensPosition**フィールドには、フレームがキャプチャされたときの論理レンズ位置が格納されます。これは、単位はありません。 これは、GET 呼び出しで KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUS からクエリを実行できるのと同じ値です。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_LENS_POSITION として表示されます。

[ホワイト**バランス**] フィールドには、フレームがキャプチャされたときにセンサーに適用された白いバランスが含まれます。これは、ケルビン単位の値です。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_WHITEBALANCE として表示されます。

[**フラッシュ**] フィールドには、[フラッシュオン] が1であるブール値と、フレームがキャプチャされたときは 0 (フラッシュオフ) が含まれています。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_FLASH として表示されます。

**FlashPower**フィールドには、キャプチャされたフレームに適用されるフラッシュパワーが格納されます。これは [0, 100] の範囲の値です。 ドライバーで flash の調整可能な電力がサポートされていない場合は、このフィールドを省略する必要があります。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_FLASH_POWER として表示されます。

**ZoomFactor**フィールドには、キャプチャされたフレームに適用される Q16 形式のズーム値が含まれています。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_ZOOMFACTOR として表示されます。

**SceneMode**フィールドには、キャプチャされたフレームに適用されるシーンモードが含まれます。これは、64ビット KSCAMERA_EXTENDEDPROP_SCENEMODE_XXX フラグです。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_SCENE_MODE として表示されます。

**Sensorframerate**フィールドには、フレームがキャプチャされたときの測定値 (ヘルツ) が格納されます。これは、32ビットの分子値と下位32ビットの分母値で構成されます。 これは、対応する MF サンプルで属性 MF_CAPTURE_METADATA_SENSORFRAMERATE として表示されます。

###### <a name="22342-metadataid_cameraextrinsics"></a>2.2.3.4.2 MetadataId_CameraExtrinsics

この識別子のメタデータ形式では、標準の KSCAMERA_METADATA_ITEMHEADER の後にバイト配列ペイロードが含まれます。 ペイロードは、 [MFCameraExtrinsics](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-_mfcameraextrinsics)構造体の後に0個以上の[MFCameraExtrinsic_CalibratedTransform](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-_mfcameraextrinsic_calibratedtransform)構造体を配置する必要があります。 ペイロードは8バイトでアラインされている必要があり、すべての未使用バイトはペイロードの最後に発生し、0に設定される必要があります。

###### <a name="22343-metadataid_cameraintrinsics"></a>2.2.3.4.3 MetadataId_CameraIntrinsics

この識別子のメタデータ形式では、標準の KSCAMERA_METADATA_ITEMHEADER の後にバイト配列ペイロードが含まれます。 ペイロードは[MFPinholeCameraIntrinsics](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-_mfpinholecameraintrinsics)構造体に配置する必要があります。 ペイロードは8バイトでアラインされている必要があり、すべての未使用バイトはペイロードの最後に発生し、0に設定される必要があります。

###### <a name="22344-metadataid_frameillumination"></a>2.2.3.4.4 MetadataId_FrameIllumination

この識別子のメタデータ形式は、次の構造によって定義されます。

```cpp
typedef struct tagKSCAMERA_METADATA_FRAMEILLUMINATION {
    KSCAMERA_METADATA_ITEMHEADER Header;
    ULONG Flags;
    ULONG Reserved;
} KSCAMERA_METADATA_FRAMEILLUMINATION, *PKSCAMERA_METADATA_FRAMEILLUMINATION;
```

**Flags**フィールドは、キャプチャされたフレームに関する情報を示します。 現時点では、次のフラグが定義されています。

```cpp
#define KSCAMERA_METADATA_FRAMEILLUMINATION_FLAG_ON 0x00000001
```

照明がオンになったときにフレームがキャプチャされた場合は、フラグ KSCAMERA_METADATA_FRAMEILLUMINATION_FLAG_ON を設定する必要があります。 それ以外の場合、このフラグは設定しないでください。

**予約済み**フィールドは将来使用するために予約されており、0に設定する必要があります。
