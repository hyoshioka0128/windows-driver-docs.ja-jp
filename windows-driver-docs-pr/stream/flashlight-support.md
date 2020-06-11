---
title: 懐中電灯のサポート
description: このトピックでは、デバイスで WinRT ランプ API をサポートする方法に関するガイダンスを提供します。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6ae80820792c6dbd8f4cfb6ccc3f53ae964876e0
ms.sourcegitcommit: bd120d96651f9e338956388c618acec7d215b0d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681682"
---
# <a name="flashlight-support"></a>懐中電灯のサポート

Windows Threshold から開始すると、新しい WinRT*ランプ*API が公開されます。これにより、1つの[MediaCapture](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture)インスタンスを作成することなく、*カメラフラッシュ*をプログラミングできます。 これにより、開発者は、電力などの最小限のリソースを描画することによって (照明目的でのみ)*懐中電灯*アプリケーションを作成できます。これにより、コンピューティングデバイスをバッテリの寿命とパフォーマンスのために最適化することができます。

これを実現するために、IHV/OEM は、次の機能をサポートする WDM ドライバーを実装する必要があります。

- システムですべてのフラッシュデバイスを列挙できるようにします。

- デバイスごとに懐中電灯をオンまたはオフにします。

- 必要に応じて、デバイスごとに明るい輝度を調整します (PowerPercent に似ています)。

- 必要に応じて、デバイスごとに明るい色を指定します。

機能の観点から見ると、上記のリストは、MediaCapture ( [FlashControl](https://docs.microsoft.com/uwp/api/Windows.Media.Devices.FlashControl)や[torchcontrol](https://docs.microsoft.com/uwp/api/Windows.Media.Devices.TorchControl)など) の場合と大きく重なっています。 さらに、同じフラッシュハードウェアが*ランプ*と*フラッシュ中*の両方に使用されています。 そのため、1つの WDM ドライバーを使用して両方の種類の操作をサポートし、flash を排他的に制御することをお勧めします。 次の図は、概念を示しています。

![排他的なフラッシュ制御の概念図](images/exclusive-flash-control.png)

上記の例では、1つのフラッシュハードウェアインスタンス (として示されています) のみが存在し、1つの*Kmdf フラッシュドライバー*によって管理されています。 Flash driver は、それぞれが特定の種類のクライアント (または WinRT API) を対象とする2つのデバイスインターフェイスを公開します。 たとえば、上の図では次のようになります。

- WinRT*メディア**キャプチャ*API と avstream ミニドライバーは、常に GUID \_ devinterface \_ カメラ \_ フラッシュインターフェイスを使用して flash ドライバーと通信します。

- WinRT*ランプ*API は、GUID \_ devinterface ランプインターフェイスを使用して、常に flash ドライバーと通信し \_ ます。

GUID \_ devinterface カメラの \_ \_ フラッシュインターフェイスはベンダー固有の avstream ミニドライバーによって使用されるため、IHV/OEM はその機能を自由に定義できます。 Windows による制限はありません。

ただし、Microsoft は、インターフェイスの GUID \_ devinterface ランプを標準化し \_ ます。これは、WINRT*ランプ API*で使用されるためです。 GUID devinterface ランプの詳細について \_ \_ は、「[デバイスインターフェイスクラス guid](#device-interface-class-guid) 」を参照してください。

## <a name="concurrency-use-cases"></a>同時実行のユースケース

### <a name="sharing-flash-between-camera-and-flashlight-applications"></a>カメラと懐中電灯アプリケーション間でフラッシュを共有する

カメラフラッシュは、通常、キャプチャデバイスの*下位*周辺機器として扱われます。 キャプチャの実行中は、カメラ以外のシナリオで共有することは想定されていません。 さらに複雑になると、シャーシ上のフラッシュデバイスの数は非常に限られています。これは、実際には、懐中電灯専用の予備のフラッシュがないということです。

ソフトウェアの観点から見ると、カメラアプリケーションと懐中電灯アプリケーションが同時に flash にアクセスしてアクセスできるという課題があります。 たとえば、理論的には、カメラのファインダーが実行されている間に、ユーザーが懐中電灯アプリケーションを使用して LED の状態を切り替えることができます。

カメラでは、フォーカスとキャプチャをサポートするために flash を正確に制御する必要があるため、競合している可能性のある flash 要求をドライバーが解決して画質を保証するのが困難な場合があります。 この問題に対処するために、次のポリシーがシステムレベルでコントラクトとして適用されます。

- **キャプチャセッションが最初に開始された場合**、キャプチャが停止するまで、懐中電灯アプリケーションで flash を操作することはできません。

  - 懐中電灯アプリケーションは引き続き flash ドライバーへのハンドルを取得できますが、フラッシュ状態を変更する操作によってすぐにエラーが発生します。

  - AVStream ミニドライバーによってフラッシュが解放されるようにキャプチャが停止した場合、フラッシュドライバーは、基に \_ なるハードウェアが使用可能になったことを示す PnP 通知を post する必要があります (「 \_ \_ [非同期通知](#asynchronous-notifications)で使用可能な GUID ランプリソース」を参照してください)。 このような通知を受け取ったときに、懐中電灯アプリケーションは、それに応じて flash をプログラムすることができます。

- **懐中電灯のアプリケーションが最初に起動した場合**、キャプチャセッションは、明示的な同意なしにフラッシュハードウェアをハイジャックすることができます。

  - "ハイジャック" により、IHV/OEM は任意のプロトコルを (場合によっては GUID devinterface カメラフラッシュインターフェイスを介して) 実装できます。これにより、 \_ \_ \_ avstream ミニドライバーは、ハードウェアがまったく使用されていないように FLASH を取得できます。

  - ハイジャックが発生した場合、フラッシュドライバーは別の PnP 通知を送信する必要があります (「非同期通知での GUID ランプリソースの損失」を参照してください)。フラッシュが involuntarily に再割り当てされたことを示しています \_ \_ \_ (UI を更新するなど)。 [Asynchronous Notifications](#asynchronous-notifications)

### <a name="sharing-flash-between-multiple-flashlight-applications"></a>複数の懐中電灯アプリケーション間での Flash の共有

カメラが関係しておらず、2つの懐中電灯アプリケーションが連続して実行されている場合、ドライバーは、GUID devinterface ランプインターフェイスを既に取得している最初のクライアントのサービスを維持 \_ \_ し、最初のクライアントがインターフェイスを最終的に解放するまで、追加のクライアントをすべて拒否します。

つまり、GUID \_ devinterface \_ ランプインターフェイスは一度に1つのフラッシュクライアントのみを許可し、インターフェイスを取得する最初のクライアントは、他のクライアントを実行できないようにします (カメラ/avstream は除外されます)。

## <a name="device-interface-class-guid"></a>デバイスインターフェイスクラス GUID

MediaCapture に依存しない懐中電灯をサポートできる IHV/OEM フラッシュドライバーは、それ自体を[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)Guid、 **guid \_ devinterface \_ ランプ**に登録する必要があります。

| 属性  | 設定                                |
| ---------- | -------------------------------------- |
| 識別子 | GUID \_ DEVINTERFACE \_ ランプ               |
| クラス GUID | {6C11E9E3-8232-4F0A-AD19-AAEC26CA5E98} |

GUID devinterface カメラフラッシュのデバイスインターフェイスクラス GUID は、 \_ \_ \_ ihv/oem によってカスタムに定義できます。 ただし、GUID devinterface ランプのデバイスインターフェイスクラス GUID \_ \_ は、Windows によって定義されています。

コントラクトにより、デバイスインターフェイスである GUID devinterface ランプを公開するドライバーは、 \_ \_ 次の機能をサポートするために必要です (詳細については、後のセクションを参照してください)。

- **IOCTL \_ランプ \_ の \_ 機能の取得 \_ {ホワイト |COLOR}** –基になるハードウェアでサポートされているすべてのモード (白のみ、色など) を取得します。

- **IOCTL \_ランプ \_ {GET |SET} \_ モード**–現在のモードを取得または設定します。

- **IOCTL \_ランプ \_ {GET |SET} \_ 輝度 \_ {白 |COLOR}** –明るい輝度を取得または設定します。

- **IOCTL \_ランプ \_ {GET |SET} \_ \_ ライトの出力**– flash の状態を取得または設定します (たとえば、ON/OFF)。

デバイスに異なる種類の複数のフラッシュハードウェアがある場合 (たとえば、*白い LED*と*Xenon フラッシュ*の両方)、これらのハードウェアが異なるフラッシュドライバーによって制御される場合、各ドライバーは、 \_ 一意のインスタンス ID を持つ同じ GUID devinterface ランプインターフェイスを公開する必要があり \_ ます。

## <a name="device-interface-property"></a>デバイスインターフェイスプロパティ

コンピューティングデバイスは、異なるパネルに0個以上のフラッシュデバイスを持つことができるので、WinRT*ランプ API*は、アプリケーションが特定のインスタンスをプログラミングできるように、すべてのフラッシュハードウェアを列挙するメカニズムを必要とします。

カメラドライバーと同様に、デバイスの列挙をサポートするために、flash driver は、ACPI \_ pld v2 構造体を各 GUID \_ devinterface \_ ランプインターフェイスにインターフェイスプロパティデータとして関連付ける必要があります。

## <a name="ioctl_lamp_get_capabilities_white"></a>IOCTL_LAMP_GET_CAPABILITIES_WHITE

IOCTL ランプは、ホワイト \_ \_ \_ \_ ライトを出力するようにデバイスが構成されている場合に、ホワイト i/o 要求によってフラッシュの機能に対してクエリを行います。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_BASE FILE_DEVICE_UNKNOWN
#define IOCTL_LAMP_GET_CAPABILITIES_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0000, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、種類がランプ機能のバッファーを指し \_ \_ ます。 詳細については、「**解説**」を参照してください。

IO \_ スタック \_ の場所。DeviceIoControl temBuffer フィールドAssociatedIrp.Sysで渡されるバッファーの長さ (バイト単位)。これは、の長さです。 \>

### <a name="output-parameters"></a>出力パラメーター

Irp \>AssociatedIrp.SystemBuffer には、フラッシュハードウェアでサポートされているすべての機能が格納されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。 Irp- \> iostatus は、バッファーを保持するために必要なバイト数に設定されます。

### <a name="remarks"></a>Remarks

要件により、ドライバー \_ が GUID devinterface ランプインターフェイスをサポートする flash は、 \_ ホワイトライトの出力をサポートするために必要です。 この IOCTL のペイロードは、次のように定義されます。

```cpp
// The output parameter type of IOCTL_LAMP_GET_CAPABILITIES_WHITE.
typedef struct LAMP_CAPABILITIES_WHITE
{
    BOOLEAN IsLightIntensityAdjustable;
} LAMP_CAPABILITIES_WHITE;
```

IsLightIntensityAdjustable フィールドは、輝度レベルをプログラミングできるかどうかを示します。 このフィールドが false と評価された場合は、基になるデバイスがオン/オフスイッチのみをサポートし、明るい輝度を調整できないことを意味します。

## <a name="ioctl_lamp_get_capabilities_color"></a>IOCTL_LAMP_GET_CAPABILITIES_COLOR

IOCTL \_ ランプ \_ GET \_ 機能 \_ カラー i/o 要求は、デバイスがカラーライトを発するように構成されている場合に、フラッシュの機能を照会します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_CAPABILITIES_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0001, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、タイプランプ機能の色のバッファーをポイント \_ \_ します。 詳細については、「**解説**」を参照してください。

IO \_ スタック \_ の場所。DeviceIoControl temBuffer フィールドAssociatedIrp.Sysで渡されるバッファーの長さ (バイト単位)。これは、の長さです。 \>

### <a name="output-parameters"></a>出力パラメーター

Irp \>AssociatedIrp.SystemBuffer には、フラッシュハードウェアでサポートされているすべての機能が格納されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。 Irp- \> iostatus は、バッファーを保持するために必要なバイト数に設定されます。

### <a name="remarks"></a>Remarks

この IOCTL のペイロードは、次のように定義されます。

```cpp
// The output parameter type of IOCTL_LAMP_GET_CAPABILITIES_COLOR.
typedef struct LAMP_CAPABILITIES_COLOR
{
    BOOLEAN IsSupported;
    BOOLEAN IsLightIntensityAdjustable;
} LAMP_CAPABILITIES_COLOR;
```

最初の "IsSupported" フィールドは、フラッシュがカラーライトを出力できるかどうかを示します。 ハードウェアでカラーライトがサポートされていない場合、ドライバーはこのフィールドを false に設定する必要があります。

2番目のフィールド IsLightIntensityAdjustable は、輝度レベルをプログラミングできるかどうかを示します。 Flash でカラーライトがサポートされていない場合 (IsSupported で false が評価された場合など)、クライアントは IsLightIntensityAdjustable の値を破棄する必要があります。

## <a name="ioctl_lamp_get_mode"></a>IOCTL_LAMP_GET_MODE

IOCTL \_ ランプ \_ 取得モードの i/o 要求は、 \_ flash が現在構成されているモードを照会します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0002, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、次のように定義されている、タイプがランプモードのバッファーを指し \_ ます。

```cpp
typedef enum LAMP_MODE
{
    LAMP_MODE_WHITE = 0,
    LAMP_MODE_COLOR
} LAMP_MODE;
```

IO \_ スタック \_ の場所。DeviceIoControl temBuffer フィールドAssociatedIrp.Sysで渡されるバッファーの長さ (バイト単位)。これは、の長さです。 \>

### <a name="output-parameters"></a>出力パラメーター

Irp \>AssociatedIrp.SystemBuffer には、ランプモード値が設定されてい \_ ます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。 これにより、Irp-iostatus が設定され \> ます。 DWORD 値を保持するために必要なバイト数になります。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは \_ \_ \_ Irp- \> iostatus. status を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_set_mode"></a>IOCTL_LAMP_SET_MODE

IOCTL \_ ランプ \_ SET \_ mode i/o 要求は、flash が動作するモードを設定します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0003, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、タイプがランプモードのバッファーを指して \_ います。

### <a name="output-parameters"></a>出力パラメーター

[なし] :

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは \_ \_ \_ Irp- \> iostatus. status を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_get_intensity_white"></a>IOCTL_LAMP_GET_INTENSITY_WHITE

IOCTL \_ ランプ \_ GET \_ 輝度ホワイト i/o 要求では、 \_ flash が白灯を出力するように構成されている場合、光強度がクエリされます。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0004, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、ランプの強度が白の構造を指して \_ \_ います。 詳細については、「**解説**」を参照してください。

IO \_ スタック \_ の場所。DeviceIoControl temBuffer フィールドAssociatedIrp.Sysで渡されるバッファーの長さ (バイト単位)。これは、の長さです。 \>

### <a name="output-parameters"></a>出力パラメーター

Irp \>AssociatedIrp.SystemBuffer には、明るい輝度情報が格納されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは \_ \_ \_ Irp- \> iostatus. status を使用してエラー (使用中の状態リソース) を返します。

### <a name="remarks"></a>Remarks

この IOCTL のペイロードの種類は、次のように定義されます。

```cpp
// The I/O parameter type of IOCTL_LAMP_{GET|SET}_INTENSITY_WHITE.
typedef struct LAMP_INTENSITY_WHITE
{
    BYTE Value;
} LAMP_INTENSITY_WHITE;
```

[値] フィールドは、0 ~ 100 の範囲の白の明るい濃度です。

## <a name="ioctl_lamp_set_intensity_white"></a>IOCTL_LAMP_SET_INTENSITY_WHITE

IOCTL \_ ランプ \_ セットの \_ 輝度 \_ ホワイト i/o 要求により、フラッシュが指定された照度に設定されます。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0005, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、ランプ \_ の輝度の白の構造をポイント \_ します (詳細については、 [IOCTL_LAMP_GET_INTENSITY_WHITE](#ioctl_lamp_get_intensity_white)を参照してください)。

### <a name="output-parameters"></a>出力パラメーター

[なし] :

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは \_ \_ \_ Irp- \> iostatus. status を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_get_intensity_color"></a>IOCTL_LAMP_GET_INTENSITY_COLOR

IOCTL \_ ランプ \_ GET \_ 輝度 i/o 要求は、 \_ フラッシュがカラーライトを発するように構成されている場合に、光強度をクエリします。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0006, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、ランプの \_ 輝度の \_ 色の構造体をポイントします。 詳細については、「**解説**」を参照してください。

IO \_ スタック \_ の場所。DeviceIoControl temBuffer フィールドAssociatedIrp.Sysで渡されるバッファーの長さ (バイト単位)。これは、の長さです。 \>

### <a name="output-parameters"></a>出力パラメーター

Irp \>AssociatedIrp.SystemBuffer には、明るい輝度情報が格納されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは \_ \_ \_ Irp- \> iostatus. status を使用してエラー (使用中の状態リソース) を返します。

### <a name="remarks"></a>Remarks

この IOCTL のペイロードの種類は、次のように定義されます。

```cpp
// The I/O parameter type of IOCTL_LAMP_{GET|SET}_INTENSITY_COLOR.
typedef struct LAMP_INTENSITY_COLOR
{
    BYTE Red; // Red light intensity in percentage (0-100)
    BYTE Green; // Green light intensity in percentage (0-100)
    BYTE Blue; // Blue light intensity in percentage (0-100)
} LAMP_INTENSITY_COLOR;
```

## <a name="ioctl_lamp_set_intensity_color"></a>IOCTL_LAMP_SET_INTENSITY_COLOR

IOCTL \_ ランプセットの輝度の i/o 要求により、 \_ \_ \_ フラッシュが指定された光の強さに設定されます。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0007, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、ランプの \_ 輝度の \_ 色の構造体を指します (詳細については、 [IOCTL_LAMP_GET_INTENSITY_COLOR](#ioctl_lamp_get_intensity_color)を参照してください)。

### <a name="output-parameters"></a>出力パラメーター

[なし] :

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは \_ \_ \_ Irp- \> iostatus. status を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_get_emitting_light"></a>IOCTL_LAMP_GET_EMITTING_LIGHT

\_ \_ \_ \_ (フラッシュ) ライトがオンになっている場合、IOCTL ランプはライト i/o 要求のクエリを出力します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_EMITTING_LIGHT
    CTL_CODE(IOCTL_LAMP_BASE, 0x0008, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、ブール型のバッファーを指しています。

IO \_ スタック \_ の場所。DeviceIoControl temBuffer フィールドAssociatedIrp.Sysで渡されるバッファーの長さ (バイト単位)。これは、の長さです。 \>

### <a name="output-parameters"></a>出力パラメーター

Irp \>AssociatedIrp.SystemBuffer には、flash の状態が TRUE に設定されています。これは、フラッシュが有効になっていることを意味します (たとえば、ライトの出力)。それ以外の場合は FALSE。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。 これにより、Irp-iostatus が設定され \> ます。 DWORD 値を保持するために必要なバイト数になります。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは \_ \_ \_ Irp- \> iostatus. status を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_set_emitting_light"></a>IOCTL_LAMP_SET_EMITTING_LIGHT

\_ライト i/o 要求を出力する IOCTL ランプは、 \_ \_ \_ (フラッシュ) ライトをオン/オフにします。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_EMITTING_LIGHT
    CTL_CODE(IOCTL_LAMP_BASE, 0x0009, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp \>AssociatedIrp.SystemBuffer は、で TRUE を示すブール型のバッファーを指しています。それ以外の場合は FALSE。

### <a name="output-parameters"></a>出力パラメーター

[なし] :

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp- \> iostatus を、状態が \_ SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは \_ \_ \_ Irp- \> iostatus. status を使用してエラー (使用中の状態リソース) を返します。

## <a name="asynchronous-notifications"></a>非同期通知

「[*同時実行のユースケース*](#concurrency-use-cases)」で説明されているように、フラッシュドライバーは、レポートリソースの可用性に PnP 通知を送信するために必要です。 これを行うには、シナリオに応じて、次の Guid で IoReportTargetDeviceChange (または IoReportTargetDeviceChangeAsynchronous) を呼び出します。

- キャプチャセッション (またはその他の懐中電灯アプリケーション) が開始されるため、フラッシュリソースが削除されました。

  | 属性  | 設定                                |
  | ---------- | -------------------------------------- |
  | 識別子 | GUID \_ ランプの \_ リソースが \_ 失われました            |
  | クラス GUID | {F770E98C-4403-48C9-B1D2-4EEC3302E41F} |

- Flash リソースが使用できるようになりました。

  | 属性  | 設定                                |
  | ---------- | -------------------------------------- |
  | 識別子 | \_ \_ \_ 使用可能な GUID ランプリソース       |
  | クラス GUID | {185FE7CE19616-481B9094-20BB893ACD81} |
