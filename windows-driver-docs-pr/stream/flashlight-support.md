---
title: 懐中電灯のサポート
description: このトピックでは、デバイスで WinRT ランプ API をサポートする方法に関するガイダンスを提供します。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0152992467bf2ec49165b5a22db9b4509b84af31
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881939"
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

- WinRT*メディア* *キャプチャ*API と avstream ミニドライバーは、常に GUID\_devinterface\_カメラ\_flash インターフェイスを使用して、フラッシュドライバーと通信します。

- WinRT*ランプ*API は、GUID\_devinterface\_ランプインターフェイスを使用して、常に flash ドライバーと通信します。

\_DEVINTERFACE\_カメラ\_の GUID は、ベンダー固有の AVStream ミニドライバーによって使用されるため、IHV/OEM はその機能を自由に定義できます。 Windows には制限が課されません。

ただし、Microsoft は、インターフェイス、GUID\_DEVINTERFACE\_ランプを標準化します。これは、WinRT*ランプ API*によって使用されるためです。 GUID\_DEVINTERFACE\_ランプの詳細については、「[デバイスインターフェイスクラス guid](#device-interface-class-guid) 」を参照してください。

## <a name="concurrency-use-cases"></a>同時実行のユースケース

### <a name="sharing-flash-between-camera-and-flashlight-applications"></a>カメラと懐中電灯アプリケーション間でフラッシュを共有する

カメラフラッシュは、通常、キャプチャデバイスの*スレーブ*周辺機器として扱われます。 キャプチャの実行中は、カメラ以外のシナリオで共有することは想定されていません。 さらに複雑になると、シャーシ上のフラッシュデバイスの数は非常に限られています。これは、実際には、懐中電灯専用の予備のフラッシュがないということです。

ソフトウェアの観点から見ると、カメラアプリケーションと懐中電灯アプリケーションが同時に flash にアクセスしてアクセスできるという課題があります。 たとえば、理論的には、カメラのファインダーが実行されている間に、ユーザーが懐中電灯アプリケーションを使用して LED の状態を切り替えることができます。

カメラでは、フォーカスとキャプチャをサポートするために flash を正確に制御する必要があるため、競合している可能性のある flash 要求をドライバーが解決して画質を保証するのが困難な場合があります。 この問題に対処するために、次のポリシーがシステムレベルでコントラクトとして適用されます。

- **キャプチャセッションが最初に開始された場合**、キャプチャが停止するまで、懐中電灯アプリケーションで flash を操作することはできません。

  - 懐中電灯アプリケーションは引き続き flash ドライバーへのハンドルを取得できますが、フラッシュ状態を変更する操作によってすぐにエラーが発生します。

  - AVStream ミニドライバーによってフラッシュが解放されるようにキャプチャが停止した場合、基になるハードウェアが使用可能になったことを示す PnP 通知 (「[非同期通知](#asynchronous-notifications)で使用可能な GUID\_ランプ\_リソース\_を参照) を送信するためにフラッシュドライバーが必要です。 このような通知を受け取ったときに、懐中電灯アプリケーションは、それに応じて flash をプログラムすることができます。

- **懐中電灯のアプリケーションが最初に起動した場合**、キャプチャセッションは、明示的な同意なしにフラッシュハードウェアをハイジャックすることができます。

  - "ハイジャック" とは、IHV/OEM が任意の\_\_\_プロトコルを実装できることを意味します。これにより、AVStream ミニドライバーは、ハードウェアがまったく使用されていないかのように FLASH を取得できます。

  - ハイジャックが発生すると、別の PnP 通知を送信するためにフラッシュドライバーが必要になります (「[非同期通知](#asynchronous-notifications)での GUID\_ランプ\_リソース\_失われた」を参照)。これにより、フラッシュが (UI を更新することによって) それに応じて動作できるように involuntarily 再割り当てされたことを示します。

### <a name="sharing-flash-between-multiple-flashlight-applications"></a>複数の懐中電灯アプリケーション間での Flash の共有

カメラが関係せず、2つの懐中電灯アプリケーションが連続して実行されている場合、ドライバーは、GUID\_DEVINTERFACE\_ランプインターフェイスを既に取得している最初のクライアントのサービスを維持し、最初のクライアントが最終的にインターフェイスを解放するまで、追加のすべてのクライアントを拒否します。

つまり、GUID\_DEVINTERFACE\_ランプインターフェイスは一度に1つのフラッシュクライアントのみを許可し、インターフェイスを取得する最初のクライアントは、他のクライアントを実行できないようにします (カメラ/AVStream は除外されます)。

## <a name="device-interface-class-guid"></a>デバイスインターフェイスクラス GUID

MediaCapture に依存しない懐中電灯をサポートできる IHV/OEM フラッシュドライバーは、[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)Guid、 **GUID\_DEVINTERFACE\_ランプ**にそれ自体を登録する必要があります。

| 備わっている  | 設定                                |
| ---------- | -------------------------------------- |
| 識別子 | GUID\_DEVINTERFACE\_ランプ               |
| クラス GUID | {6C11E9E3-8232-4F0A-AD19-AAEC26CA5E98} |

GUID\_DEVINTERFACE\_カメラ\_FLASH のデバイスインターフェイスクラス GUID は、Ihv/Oem によってカスタムに定義できます。 ただし、GUID のデバイスインターフェイスクラス GUID\_DEVINTERFACE\_ランプは、Windows によって定義されています。

コントラクトにより、デバイスインターフェイス、GUID\_DEVINTERFACE\_ランプを公開するドライバーは、次の機能をサポートするために必要です (詳細については、後のセクションを参照してください)。

- **IOCTL\_ランプ\_\_の機能を取得\_{白 |COLOR}** –基になるハードウェアでサポートされているすべてのモード (白のみ、色など) を取得します。

- **IOCTL\_ランプ\_{GET |SET}\_モード**–現在のモードを取得または設定します。

- **IOCTL\_ランプ\_{GET |SET}\_の輝度\_{白 |COLOR}** –明るい輝度を取得または設定します。

- **IOCTL\_ランプ\_{GET |SET}\_\_ライトの出力**–フラッシュの状態を取得または設定します (たとえば、ON/OFF)。

デバイスに異なる種類の複数のフラッシュハードウェアがある場合 (たとえば、*白い LED*と*Xenon フラッシュ*の両方)、これらのハードウェアが異なるフラッシュドライバーによって制御される場合、各ドライバーは、一意のインスタンス ID を持つ同じ GUID\_devinterface\_ランプインターフェイスを公開する必要があります。

## <a name="device-interface-property"></a>デバイスインターフェイスプロパティ

コンピューティングデバイスは、異なるパネルに0個以上のフラッシュデバイスを持つことができるので、WinRT*ランプ API*は、アプリケーションが特定のインスタンスをプログラミングできるように、すべてのフラッシュハードウェアを列挙するメカニズムを必要とします。

カメラドライバーと同様に、デバイスの列挙をサポートするために、flash driver は、ACPI \_PLD v2 構造体を各 GUID に関連付けて、インターフェイスプロパティデータとして\_DEVINTERFACE\_ランプインターフェイスに関連付ける必要があります。

## <a name="ioctl_lamp_get_capabilities_white"></a>IOCTL_LAMP_GET_CAPABILITIES_WHITE

IOCTL\_ランプ\_\_機能を取得します。白い i/o 要求\_、デバイスが白灯を出力するように構成されている場合にフラッシュの機能を照会します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_BASE FILE_DEVICE_UNKNOWN
#define IOCTL_LAMP_GET_CAPABILITIES_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0000, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp は、種類がランプ\_機能\_白のバッファーを指します。 詳細については、「**解説**」を参照してください。

IO\_スタック\_の場所。DeviceIoControl は、Irp\>AssociatedIrp フィールドで渡されるバッファーの長さ (バイト単位) を示しています。

### <a name="output-parameters"></a>出力パラメーター

Irp\>AssociatedIrp は、フラッシュハードウェアでサポートされているすべての機能を使用して入力されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。 これにより、Irp\>IoStatus. 情報が、バッファーを保持するために必要なバイト数に設定されます。

### <a name="remarks"></a>注釈

要件によって、ドライバーが GUID をサポートする\_DEVINTERFACE\_ランプインターフェイスは、ホワイトライトの出力をサポートするために必要です。 この IOCTL のペイロードは、次のように定義されます。

```cpp
// The output parameter type of IOCTL_LAMP_GET_CAPABILITIES_WHITE.
typedef struct LAMP_CAPABILITIES_WHITE
{
    BOOLEAN IsLightIntensityAdjustable;
} LAMP_CAPABILITIES_WHITE;
```

IsLightIntensityAdjustable フィールドは、輝度レベルをプログラミングできるかどうかを示します。 このフィールドが false と評価された場合は、基になるデバイスがオン/オフスイッチのみをサポートし、明るい輝度を調整できないことを意味します。

## <a name="ioctl_lamp_get_capabilities_color"></a>IOCTL_LAMP_GET_CAPABILITIES_COLOR

IOCTL\_ランプ\_\_機能を取得\_カラー i/o 要求は、デバイスがカラーライトを出力するように構成されている場合に、フラッシュの機能に対してクエリを行います。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_CAPABILITIES_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0001, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp は、種類がランプ\_機能\_色を指します。 詳細については、「**解説**」を参照してください。

IO\_スタック\_の場所。DeviceIoControl は、Irp\>AssociatedIrp フィールドで渡されるバッファーの長さ (バイト単位) を示しています。

### <a name="output-parameters"></a>出力パラメーター

Irp\>AssociatedIrp は、フラッシュハードウェアでサポートされているすべての機能を使用して入力されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。 これにより、Irp\>IoStatus. 情報が、バッファーを保持するために必要なバイト数に設定されます。

### <a name="remarks"></a>注釈

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

IOCTL\_ランプ\_取得\_モードの i/o 要求は、flash が現在構成されているモードを照会します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0002, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp は、次のように定義されている、タイプがランプ\_モードのバッファーを指します。

```cpp
typedef enum LAMP_MODE
{
    LAMP_MODE_WHITE = 0,
    LAMP_MODE_COLOR
} LAMP_MODE;
```

IO\_スタック\_の場所。DeviceIoControl は、Irp\>AssociatedIrp フィールドで渡されるバッファーの長さ (バイト単位) を示しています。

### <a name="output-parameters"></a>出力パラメーター

Irp-\>AssociatedIrp は、ランプ\_MODE 値で埋められます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。 これにより、Irp\>IoStatus. 情報が DWORD 値を保持するために必要なバイト数に設定されます。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは、Irp\>IoStatus. Status を使用して、エラー (状態\_リソース\_\_使用) を返します。

## <a name="ioctl_lamp_set_mode"></a>IOCTL_LAMP_SET_MODE

IOCTL\_ランプ\_設定\_モードの i/o 要求は、フラッシュが動作するモードを設定します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0003, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp は、タイプがランプ\_モードのバッファーを指します。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは、Irp\>IoStatus. Status を使用して、エラー (状態\_リソース\_\_使用) を返します。

## <a name="ioctl_lamp_get_intensity_white"></a>IOCTL_LAMP_GET_INTENSITY_WHITE

IOCTL\_ランプ\_\_の輝度\_白の i/o 要求は、フラッシュが白灯を出力するように構成されている場合に光強度を照会します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0004, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp は、ライト\_輝度\_白の構造をポイントします。 詳細については、「**解説**」を参照してください。

IO\_スタック\_の場所。DeviceIoControl は、Irp\>AssociatedIrp フィールドで渡されるバッファーの長さ (バイト単位) を示しています。

### <a name="output-parameters"></a>出力パラメーター

Irp-\>AssociatedIrp には、明るい輝度情報が格納されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは、Irp\>IoStatus. Status を使用して、エラー (状態\_リソース\_\_使用) を返します。

### <a name="remarks"></a>注釈

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

IOCTL\_ランプ\_設定\_輝度\_白い i/o 要求によって、フラッシュが指定された照度に設定されます。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0005, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp は、ライト\_輝度\_白の構造を指します (詳細については[IOCTL_LAMP_GET_INTENSITY_WHITE](#ioctl_lamp_get_intensity_white)を参照してください)。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは、Irp\>IoStatus. Status を使用して、エラー (状態\_リソース\_\_使用) を返します。

## <a name="ioctl_lamp_get_intensity_color"></a>IOCTL_LAMP_GET_INTENSITY_COLOR

IOCTL\_ランプ\_\_輝度\_カラー i/o 要求は、フラッシュがカラーライトを出力するように構成されている場合に光強度を照会します。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0006, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp は、ランプ\_輝度\_色の構造をポイントします。 詳細については、「**解説**」を参照してください。

IO\_スタック\_の場所。DeviceIoControl は、Irp\>AssociatedIrp フィールドで渡されるバッファーの長さ (バイト単位) を示しています。

### <a name="output-parameters"></a>出力パラメーター

Irp-\>AssociatedIrp には、明るい輝度情報が格納されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは、Irp\>IoStatus. Status を使用して、エラー (状態\_リソース\_\_使用) を返します。

### <a name="remarks"></a>注釈

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

IOCTL\_ランプ\_\_輝度\_カラー i/o 要求によって、指定された照度にフラッシュが設定されます。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0007, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp は、\_輝度\_色の構造をポイントします (詳細については[IOCTL_LAMP_GET_INTENSITY_COLOR](#ioctl_lamp_get_intensity_color)を参照してください)。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは、Irp\>IoStatus. Status を使用して、エラー (状態\_リソース\_\_使用) を返します。

## <a name="ioctl_lamp_get_emitting_light"></a>IOCTL_LAMP_GET_EMITTING_LIGHT

IOCTL\_ランプ\_(フラッシュ) ライトがオンになっている場合は、ライト i/o 要求クエリを\_出力\_ます。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_GET_EMITTING_LIGHT
    CTL_CODE(IOCTL_LAMP_BASE, 0x0008, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp は、ブール型のバッファーを指しています。

IO\_スタック\_の場所。DeviceIoControl は、Irp\>AssociatedIrp フィールドで渡されるバッファーの長さ (バイト単位) を示しています。

### <a name="output-parameters"></a>出力パラメーター

Irp\>AssociatedIrp は、flash が有効になっていることを意味します (たとえば、ライトの出力など)。それ以外の場合は FALSE。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。 これにより、Irp\>IoStatus. 情報が DWORD 値を保持するために必要なバイト数に設定されます。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは、Irp\>IoStatus. Status を使用して、エラー (状態\_リソース\_\_使用) を返します。

## <a name="ioctl_lamp_set_emitting_light"></a>IOCTL_LAMP_SET_EMITTING_LIGHT

ライト i/o 要求を\_出力する\_\_IOCTL\_ランプは、(フラッシュ) ライトをオン/オフにします。

### <a name="definition"></a>定義

```cpp
#define IOCTL_LAMP_SET_EMITTING_LIGHT
    CTL_CODE(IOCTL_LAMP_BASE, 0x0009, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>入力パラメーター

Irp\>AssociatedIrp はブール型のバッファーをポイントし、では TRUE を示します。それ以外の場合は FALSE。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/O ステータス ブロック

ドライバーは、Irp\>IoStatus. Status を STATUS\_SUCCESS または適切なエラー状態に設定します。

この要求が行われた時点で MediaCapture セッションがデータをストリーミングしている場合、ドライバーは、Irp\>IoStatus. Status を使用して、エラー (状態\_リソース\_\_使用) を返します。

## <a name="asynchronous-notifications"></a>非同期通知

「[*同時実行のユースケース*](#concurrency-use-cases)」で説明されているように、フラッシュドライバーは、レポートリソースの可用性に PnP 通知を送信するために必要です。 これを行うには、シナリオに応じて、次の Guid で IoReportTargetDeviceChange (または IoReportTargetDeviceChangeAsynchronous) を呼び出します。

- キャプチャセッション (またはその他の懐中電灯アプリケーション) が開始されるため、フラッシュリソースが削除されました。

  | 備わっている  | 設定                                |
  | ---------- | -------------------------------------- |
  | 識別子 | GUID\_ランプ\_リソース\_紛失            |
  | クラス GUID | {F770E98C-4403-48C9-B1D2-4EEC3302E41F} |

- Flash リソースが使用できるようになりました。

  | 備わっている  | 設定                                |
  | ---------- | -------------------------------------- |
  | 識別子 | GUID\_ランプ\_リソース\_利用可能       |
  | クラス GUID | {185FE7CE19616-481B9094-20BB893ACD81} |
