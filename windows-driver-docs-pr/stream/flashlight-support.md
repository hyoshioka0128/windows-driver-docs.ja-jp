---
title: 懐中電灯のサポート
description: このトピックでは、デバイスで WinRT ランプ API をサポートする方法に関するガイダンスを提供します。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0d4f857edc85bd4549a9180b3cd6953af4f1c671
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565926"
---
# <a name="flashlight-support"></a>懐中電灯のサポート

## <a name="overview"></a>概要

Windows Threshold から開始すると、新しい WinRT*ランプ*API が公開されます。これにより、1つの[MediaCapture](http://msdn.microsoft.com/en-us/library/windows/apps/windows.media.capture.mediacapture.aspx)インスタンスを作成することなく、*カメラフラッシュ*をプログラミングできます。 これにより、開発者は、電力などの最小限のリソースを描画することによって (照明目的でのみ)*懐中電灯*アプリケーションを作成できます。これにより、コンピューティングデバイスをバッテリの寿命とパフォーマンスのために最適化することができます。

これを実現するために、IHV/OEM は、次の機能をサポートする WDM ドライバーを実装する必要があります。

- システムですべてのフラッシュデバイスを列挙できるようにします。
- デバイスごとに懐中電灯をオンまたはオフにします。
- 必要に応じて、デバイスごとに明るい輝度を調整します (PowerPercent に似ています)。
- 必要に応じて、デバイスごとに明るい色を指定します。

機能の観点から見ると、上記のリストは、MediaCapture (例: [FlashControl](http://msdn.microsoft.com/en-us/library/windows/apps/windows.media.devices.flashcontrol.aspx)や[torchcontrol](http://msdn.microsoft.com/en-us/library/windows/apps/windows.media.devices.torchcontrol.aspx)) と大きく重なっています。
さらに、同じフラッシュハードウェアが*ランプ*と*フラッシュ中*の両方に使用されています。 そのため、1つの WDM ドライバーを使用して両方の種類の操作をサポートし、flash を排他的に制御することをお勧めします。 次の図は、概念を示しています。

![排他的なフラッシュ制御の概念図](images/exclusive-flash-control.png)

上記の例では、1つのフラッシュハードウェアインスタンス (として示されています) のみが存在し、1つの*Kmdf フラッシュドライバー*によって管理されています。 Flash driver は、それぞれが特定の種類のクライアント (または WinRT API) を対象とする2つのデバイスインターフェイスを公開します。 たとえば、上の図では次のようになります。

- WinRT*メディア* *キャプチャ*API と avstream ミニドライバーは、常に GUID\_devinterface\_カメラ\_フラッシュインターフェイスを使用して flash ドライバーと通信します。
- WinRT*ランプ*API は、GUID\_devinterface\_ランプインターフェイスを使用して、常に flash ドライバーと通信します。

GUID\_devinterface\_カメラ\_のフラッシュインターフェイスはベンダー固有の avstream ミニドライバーによって使用されるため、IHV/OEM はその機能を自由に定義できます。 Windows による制限はありません。

ただし、Microsoft は、インターフェイスの GUID\_devinterface\_ランプを標準化します。これは、WinRT*ランプ API*で使用されるためです。
GUID\_devinterface\_ランプの詳細については、「[デバイスインターフェイスクラス guid](#device-interface-class-guid) 」を参照してください。

### <a name="concurrency-use-cases"></a>同時実行のユースケース

#### <a name="sharing-flash-between-camera-and-flashlight-applications"></a>カメラと懐中電灯アプリケーション間でフラッシュを共有する

カメラフラッシュは、通常、キャプチャデバイスの*スレーブ*周辺機器として扱われます。 キャプチャの実行中は、カメラ以外のシナリオで共有することは想定されていません。 さらに複雑になると、シャーシ上のフラッシュデバイスの数は非常に限られています。これは、実際には、懐中電灯専用の予備のフラッシュがないということです。

ソフトウェアの観点から見ると、カメラアプリケーションと懐中電灯アプリケーションが同時に flash にアクセスしてアクセスできるという課題があります。 たとえば、理論的には、カメラのファインダーが実行されている間に、ユーザーが懐中電灯アプリケーションを使用して LED の状態を切り替えることができます。

カメラでは、フォーカスとキャプチャをサポートするために flash を正確に制御する必要があるため、競合している可能性のある flash 要求をドライバーが解決して画質を保証するのが困難な場合があります。 この問題に対処するために、次のポリシーをシステムレベルでコントラクトとして配置します。

- **キャプチャセッションが最初に開始された場合**、キャプチャが停止するまで、懐中電灯アプリケーションで flash を操作することはできません。
  - 懐中電灯アプリケーションは引き続き flash ドライバーへのハンドルを取得できますが、フラッシュ状態を変更する操作によってすぐにエラーが発生します。
  - Avstream ミニドライバーがフラッシュをリリースするようにキャプチャが停止した場合、PnP 通知を送信するにはフラッシュドライバー\_が\_必要\_です (「[非同期通知](#asynchronous-notifications)で使用できる GUID ランプリソース」を参照してください)。基になるハードウェアが使用可能になったことを示します。 このような通知を受け取ったときに、懐中電灯アプリケーションは、それに応じて flash をプログラムすることができます。
- **懐中電灯のアプリケーションが最初に起動した場合**、キャプチャセッションは、明示的な同意なしにフラッシュハードウェアをハイジャックすることができます。
  - "ハイジャック" によって、IHV/OEM は任意のプロトコルを (場合によって\_は GUID\_devinterface カメラ\_フラッシュインターフェイスを介して) 実装できます。これにより、avstream ミニドライバーは、ハードウェアが使用されていないかのように FLASH を取得できるようになります。まったく使用されていません。
  - ハイジャックが発生すると、別の PnP 通知を送信するためにフラッシュドライバーが\_必要\_に\_なります (「[非同期通知](#asynchronous-notifications)での GUID ランプリソース損失」を参照してください)。フラッシュが involuntarily に再割り当てされたことを示します。(UI を更新するなどして) 懐中電灯アプリケーションがそれに応じて動作するようにします。

#### <a name="sharing-flash-between-multiple-flashlight-applications"></a>複数の懐中電灯アプリケーション間での Flash の共有

カメラが関係せず、2つの懐中電灯アプリケーションが連続して実行される場合、ドライバーは、GUID\_devinterface\_ランプインターフェイスを既に取得している最初のクライアントのサービスを維持し、追加のクライアントをすべて拒否する必要があります。最初の方法では、インターフェイスが最終的に解放されます。

つまり、GUID\_devinterface\_ランプインターフェイスは一度に1つのフラッシュクライアントのみを許可し、インターフェイスを取得する最初のクライアントは、他のクライアントを実行できないようにします (カメラ/avstream は除外されます)。

## <a name="device-interface-class-guid"></a>デバイスインターフェイスクラス GUID

MediaCapture に依存しない懐中電灯をサポートできる IHV/OEM フラッシュドライバーは、それ自体を *[デバイスインターフェイスクラス](http://msdn.microsoft.com/en-us/library/windows/hardware/ff541339\(v=vs.85\).aspx)guid*、 **\_guid\_devinterface ランプ**に登録する必要があります。

| 属性  | 設定                                |
| ---------- | -------------------------------------- |
| 識別子 | GUID\_DEVINTERFACE\_ランプ               |
| クラス GUID | {6C11E9E3-8232-4F0A-AD19-AAEC26CA5E98} |

Guid\_devinterface\_カメラ\_フラッシュのデバイスインターフェイスクラス guid は、ihv/oem によってカスタムに定義できます。
ただし、guid\_devinterface\_ランプのデバイスインターフェイスクラス guid は、Windows によって定義されています。

### <a name="remarks"></a>コメント

コントラクトにより、デバイスインターフェイスである GUID\_devinterface\_ランプを公開するドライバーは、次の機能をサポートするために必要です (詳細については、後のセクションを参照してください)。

- **\_IOCTL\_ランプ\_の機能\_の取得 {ホワイト |COLOR}** –基になるハードウェアでサポートされているすべてのモード (白のみ、色など) を取得します。
- **IOCTL\_ランプ\_{GET |SET}\_モード**–現在のモードを取得または設定します。
- **IOCTL\_ランプ\_{GET |SET}\_輝度\_{白 |COLOR}** –明るい輝度を取得または設定します。
- **IOCTL\_ランプ\_{GET |SET}\_ライト\_の出力**– flash の状態を取得または設定します (たとえば、ON/OFF)

デバイスに異なる種類の複数のフラッシュハードウェア (*白い LED*と*Xenon flash*の両方) がある場合、これらのハードウェアは異なるフラッシュドライバーによって制御されるため、各ドライバーは同じ\_GUID devinterface\_を公開します。一意の[インスタンス ID](http://msdn.microsoft.com/en-us/library/windows/hardware/ff547656\(v=vs.85\).aspx)を持つランプインターフェイス。

## <a name="device-interface-property"></a>デバイスインターフェイスプロパティ

コンピューティングデバイスは、異なるパネルに0個以上のフラッシュデバイスを持つことができるので、WinRT*ランプ API*は、アプリケーションが特定のインスタンスをプログラミングできるように、すべてのフラッシュハードウェアを列挙するメカニズムを必要とします。

カメラドライバーと同様に、デバイスの列挙をサポートするために、flash driver は、ACPI \_pld v2 構造体を各\_GUID devinterface\_ランプインターフェイスにインターフェイスプロパティデータとして関連付ける必要があります。

## <a name="ioctl_lamp_get_capabilities_white"></a>IOCTL_LAMP_GET_CAPABILITIES_WHITE

IOCTL\_ランプ\_は、ホワイトライトを出力するようにデバイスが構成されている場合に、ホワイトi/o要求によってフラッシュの機能に対してクエリを行います。\_\_

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_BASE FILE_DEVICE_UNKNOWN
#define IOCTL_LAMP_GET_CAPABILITIES_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0000, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

AssociatedIrp は、タイプがランプ\_機能\_のバッファーを指します。\> 詳細については、「**解説**」を参照してください。

IO\_スタック\_の場所。DeviceIoControl は、\>AssociatedIrp フィールドに渡されたバッファーの長さ (バイト単位) です。この長さはバイト単位です。

### <a name="output-parameters"></a>出力パラメーター

\>AssociatedIrp は、フラッシュハードウェアによってサポートされるすべての機能を使用して入力されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。 Irp-\>iostatus は、バッファーを保持するために必要なバイト数に設定されます。

### <a name="remarks"></a>コメント

要件により、ドライバーが GUID\_devinterface\_ランプインターフェイスをサポートする flash は、ホワイトライトの出力をサポートするために必要です。 この IOCTL のペイロードは、次のように定義されます。

```cpp
// The output parameter type of IOCTL_LAMP_GET_CAPABILITIES_WHITE.
typedef struct LAMP_CAPABILITIES_WHITE
{
    BOOLEAN IsLightIntensityAdjustable;
} LAMP_CAPABILITIES_WHITE;
```

IsLightIntensityAdjustable フィールドは、輝度レベルをプログラミングできるかどうかを示します。 このフィールドが false と評価された場合は、基になるデバイスがオン/オフスイッチのみをサポートし、明るい輝度を調整できないことを意味します。

## <a name="ioctl_lamp_get_capabilities_color"></a>IOCTL_LAMP_GET_CAPABILITIES_COLOR

IOCTL\_ランプ\_GET\_機能カラーi/o要求は、デバイスがカラーライトを発するように構成されている場合に、フラッシュの機能を照会します。\_

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_CAPABILITIES_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0001, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

AssociatedIrp は、タイプランプ\_機能\_の色を指すバッファーを指します。\> 詳細については、「**解説**」を参照してください。

IO\_スタック\_の場所。DeviceIoControl は、\>AssociatedIrp フィールドに渡されたバッファーの長さ (バイト単位) です。この長さはバイト単位です。

### <a name="output-parameters"></a>出力パラメーター

\>AssociatedIrp は、フラッシュハードウェアによってサポートされるすべての機能を使用して入力されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。 Irp-\>iostatus は、バッファーを保持するために必要なバイト数に設定されます。

### <a name="remarks"></a>コメント

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

2番目のフィールド IsLightIntensityAdjustable は、輝度レベルをプログラミングできるかどうかを示します。 フラッシュでカラーライトがサポートされていない場合 (IsSupported の評価が false の場合)、クライアントは IsLightIntensityAdjustable の値を破棄する必要があります。

## <a name="ioctl_lamp_get_mode"></a>IOCTL_LAMP_GET_MODE

IOCTL\_ランプ\_取得モードのi/o要求は、flashが現在構成されているモードを照会します。\_

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0002, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

AssociatedIrp は、次のように定義されている、\_タイプがランプモードのバッファーを指します。\>

```cpp
typedef enum LAMP_MODE
{
    LAMP_MODE_WHITE = 0,
    LAMP_MODE_COLOR
} LAMP_MODE;
```

IO\_スタック\_の場所。DeviceIoControl は、\>AssociatedIrp フィールドに渡されたバッファーの長さ (バイト単位) です。この長さはバイト単位です。

### <a name="output-parameters"></a>出力パラメーター

AssociatedIrp には、ランプ\_モード値が設定されています。\>

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。 これにより、Irp\>-iostatus が設定されます。 DWORD 値を保持するために必要なバイト数になります。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは\_Irp-\>iostatus.\_status\_を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_set_mode"></a>IOCTL_LAMP_SET_MODE

IOCTL\_ランプ\_SETmodei/o要求は、flashが動作するモードを設定します。\_

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0003, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

AssociatedIrp は、タイプがランプ\_モードのバッファーを指します。\>

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは\_Irp-\>iostatus.\_status\_を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_get_intensity_white"></a>IOCTL_LAMP_GET_INTENSITY_WHITE

IOCTL\_ランプ\_GET\_輝度ホワイトi/o要求では、flashが白灯を出力するように構成されている場合、光強度がクエリされます。\_

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0004, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

AssociatedIrp は、ランプ\_の輝度\_の白の構造体をポイントします。\> 詳細については、「**解説**」を参照してください。

IO\_スタック\_の場所。DeviceIoControl は、\>AssociatedIrp フィールドに渡されたバッファーの長さ (バイト単位) です。この長さはバイト単位です。

### <a name="output-parameters"></a>出力パラメーター

\>AssociatedIrp には、明るい輝度情報が格納されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは\_Irp-\>iostatus.\_status\_を使用してエラー (使用中の状態リソース) を返します。

### <a name="remarks"></a>コメント

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

IOCTL\_ランプ\_セットの\_輝度ホワイトi/o要求により、フラッシュが指定された照度に設定\_されます。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0005, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

AssociatedIrp は、ランプ\_の輝度\_の白の構造体を指します (詳細については、 [IOCTL_LAMP_GET_INTENSITY_WHITE](#ioctl_lamp_get_intensity_white)を参照してください)。\>

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは\_Irp-\>iostatus.\_status\_を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_get_intensity_color"></a>IOCTL_LAMP_GET_INTENSITY_COLOR
IOCTL\_\_ランプの輝度\_を取得する\_

IOCTL\_ランプ\_GET\_輝度i/o要求は、フラッシュがカラーライトを発するように構成されている場合に、光強度をクエリします。\_

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0006, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

AssociatedIrp は、ランプ\_の輝度\_の色の構造体をポイントします。\> 詳細については、「**解説**」を参照してください。

IO\_スタック\_の場所。DeviceIoControl は、\>AssociatedIrp フィールドに渡されたバッファーの長さ (バイト単位) です。この長さはバイト単位です。

### <a name="output-parameters"></a>出力パラメーター

\>AssociatedIrp には、明るい輝度情報が格納されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは\_Irp-\>iostatus.\_status\_を使用してエラー (使用中の状態リソース) を返します。

### <a name="remarks"></a>コメント

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

IOCTL\_ランプ\_セットの\_輝度のi/o要求により、フラッシュが指定された光の強さに設定\_されます。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0007, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

AssociatedIrp は、ランプ\_の輝度\_の色の構造体をポイントします (詳細については、 [IOCTL_LAMP_GET_INTENSITY_COLOR](#ioctl_lamp_get_intensity_color)を参照してください)。\>

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは\_Irp-\>iostatus.\_status\_を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_get_emitting_light"></a>IOCTL_LAMP_GET_EMITTING_LIGHT

(フラッシュ\_) ライト\_がオンになっている場合、IOCTL ランプ\_はライト i/o 要求のクエリを出力\_します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_EMITTING_LIGHT
    CTL_CODE(IOCTL_LAMP_BASE, 0x0008, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

\>AssociatedIrp は、ブール型のバッファーを指しています。

IO\_スタック\_の場所。DeviceIoControl は、\>AssociatedIrp フィールドに渡されたバッファーの長さ (バイト単位) です。この長さはバイト単位です。

### <a name="output-parameters"></a>出力パラメーター

\>AssociatedIrp は、flash の状態を TRUE に設定します。これは、フラッシュが有効になっていることを意味します (光の出力など)。それ以外の場合は FALSE。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。 これにより、Irp\>-iostatus が設定されます。 DWORD 値を保持するために必要なバイト数になります。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは\_Irp-\>iostatus.\_status\_を使用してエラー (使用中の状態リソース) を返します。

## <a name="ioctl_lamp_set_emitting_light"></a>IOCTL_LAMP_SET_EMITTING_LIGHT

ライト i/o\_要求\_を\_出力\_する IOCTL ランプは、(フラッシュ) ライトをオン/オフにします。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_EMITTING_LIGHT 
    CTL_CODE(IOCTL_LAMP_BASE, 0x0009, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

\>AssociatedIrp はブール型のバッファーをポイントし、では TRUE を示します。それ以外の場合は FALSE。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp-\>iostatus を、状態\_が SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは\_Irp-\>iostatus.\_status\_を使用してエラー (使用中の状態リソース) を返します。

## <a name="asynchronous-notifications"></a>非同期通知

「[*同時実行のユースケース*](#concurrency-use-cases)」で説明されているように、フラッシュドライバーは、レポートリソースの可用性に PnP 通知を送信するために必要です。 これを行うには、シナリオに応じて、次の Guid で IoReportTargetDeviceChange (または IoReportTargetDeviceChangeAsynchronous) を呼び出します。

- キャプチャセッション (またはその他の懐中電灯アプリケーション) が開始されるため、フラッシュリソースが削除されました。
  | 属性  | 設定                                |
  | ---------- | -------------------------------------- |
  | 識別子 | GUID\_ランプ\_のリソース\_が失われました            |
  | クラス GUID | {F770E98C-4403-48C9-B1D2-4EEC3302E41F} |
- Flash リソースが使用できるようになりました。
  | 属性  | 設定                                |
  | ---------- | -------------------------------------- |
  | 識別子 | 使用\_可能\_な\_GUID ランプリソース       |
  | クラス GUID | {185FE7CE19616-481B9094-20BB893ACD81} |
