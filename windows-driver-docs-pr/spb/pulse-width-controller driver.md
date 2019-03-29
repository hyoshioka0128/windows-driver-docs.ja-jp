---
title: on-SoC PWM モジュールの PWM ドライバー
description: PWM コント ローラーは、SoC の一部であるため、メモリ マップト SoC のアドレス空間にします。 書き込み PWM を操作するカーネル モード ドライバーの登録し、アプリケーションへのアクセスを提供します。
ms.assetid: 911375A9-6761-45C1-BB5E-79BC0E4409AC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa980ceb8c5e2d9108c5763ee9bfee6d99331032
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578182"
---
# <a name="pwm-driver-for-an-on-soc-pwm-module"></a>on-SoC PWM モジュールの PWM ドライバー
SoC の一部であるパルス幅変調 (PWM) コント ローラーへのアクセスを提供して、メモリ マップト SoC のアドレス空間に、する必要があるライターはカーネル モード ドライバー。 ドライバーは、UWP アプリは Windows.Devices.Pwm 名前空間で定義されている PWM WinRT Api を介して公開されているシステム PWM デバイスにアクセスできるように、PWM コント ローラーのデバイス クラスのインターフェイスを登録する必要があります。 

**注**経由では、アドオン PWM モジュールがあれば<sup>2</sup>C、SPI、または UART コント ローラーの場合は、UWP アプリからのモジュールをアクセスで定義されている Api を使用して、 [ **Windows.Devices.Pwm**](https://docs.microsoft.com/uwp/api/windows.devices.pwm)と[ **Windows.Devices.Pwm.Provider** ](https://docs.microsoft.com/uwp/api/windows.devices.pwm.provider)名前空間。 

PWM デバイスは、単一のコント ローラーと 1 つまたは複数の pin に抽象化されています。 コント ローラーまたはピンのいずれかを制御する、PWM 定義 Ioctl を通じて行われます。 たとえば、LCD のディスプレイ ドライバーでは、LCD バックライトのレベルを制御する PWM ドライバーにこのような要求を送信します。 

複数のコント ローラーとマルチ チャネル PWM シグナルの生成により、次のタスク構成可能な期間、極性、およびデューティ サイクルで: 

-   モーターを促進します。 
-   LED、または DC つや消しモーターと同様に、負荷をドライブします。 
-   アナログ信号を生成します。 
-   正確なクロックを生成します。 

このトピックを説明します。 

-   PWM のシステムに公開されているデバイスに UWP へのアクセスを有効にする方法。 

-   Win32 アプリケーションやサード パーティのカーネル モード ドライバーによって送信された PWM IOCTL 要求を処理する方法。

**対象読者**

-   Oem および Ihv SoC に PWM コント ローラーでシステムを開発します。 

**最終更新日**

-   2017 年 8 月

**Windows のバージョン**

-   Windows 10 のバージョン

**重要な API**

-   [PWM IOCTLs](https://msdn.microsoft.com/library/windows/desktop/mt826481)

## <a name="about-pwm"></a>PWM について
PWM では、波形の平均値のバリエーションで変調されたパルス幅を四角形のパルス wave を生成するための基本的な手法について説明します。  

2 つのパラメーターによって、PWM 波形を分類できます: 波形期間 (T) とデューティ サイクルです。 波形の頻度 (f) は、波形期間 f の逆数 = 1/t です。 デューティ サイクルには、'on' または 'Active'、一定の間隔または 'Period' の時間の時間の割合がについて説明します低デューティ サイクルは、電源がオフ、時間のほとんどのため、低出力電力の平均値に対応します。 100 でデューティ サイクルがパーセントで表される % にするために、完全にオフは、'Active'、時間の 50% をされている 50% をされている 0% をされています。

![ドライバー](images/pwm.png)


## <a name="accessing-the-system-exposed-pwm-controller-and-pins"></a>PWM コント ローラーのシステムに公開されているとピンへのアクセス

PWM ドライバーを登録する必要があります。  
デバイスのインターフェイスを公開して、PWM デバイスへのアクセスの GUID として GUID_DEVINTERFACE_PWM_CONTROLLER します。 

```cpp
// {60824B4C-EED1-4C9C-B49C-1B961461A819} 

DEFINE_GUID(GUID_DEVINTERFACE_PWM_CONTROLLER, 0x60824b4c, 0xeed1, 0x4c9c, 0xb4, 0x9c, 0x1b, 0x96, 0x14, 0x61, 0xa8, 0x19); 

#define GUID_DEVINTERFACE_PWM_CONTROLLER_WSZ L"{60824B4C-EED1-4C9C-B49C-1B961461A819}" 
```

ドライバーは、デバイス インターフェイスの GUID を登録するには、EVT_WDF_DRIVER_DEVICE_ADD コールバック関数のドライバーの実装で WdfDeviceCreateDeviceInterface を呼び出す必要があります。 登録後に、コント ローラーとピンにシンボリック リンクが割り当てられます。

PWM を通じてピンには、Ioctl が定義されているまたはアプリケーションまたは別のドライバーは、コント ローラーのいずれかを制御できます。 Ioctl を送信する前に、送信側アプリケーションまたはドライバーは、シンボリック リンクを指定することで、コント ローラーと、暗証番号 (pin) へのファイル ハンドルを開く必要があります。 これには、ドライバー ファイルを作成し、イベントを閉じるを登録する必要があります。 (リンク) を参照してください。 


コント ローラーのシンボル パスの例を次に示します。
```cpp
\??\ACPI#FSCL000E#1#{60824b4c-eed1-4c9c-b49c-1b961461a819}  
```
同様に、ピンの形式のとおりです。パスの形式は次のとおりです。

```cpp
<DeviceInterfaceSymbolicLinkName>\<PinNumber>
```
場所<PinNumber>開きますにピン留めの 0 から始まるインデックスです。 

ピンのシンボル パスの例を次に示します。
```cpp
\??\ACPI#FSCL000E#1#{60824b4c-eed1-4c9c-b49c-1b961461a819}\0 ; Opens pin 0 

\??\ACPI#FSCL000E#1#{60824b4c-eed1-4c9c-b49c-1b961461a819}\0001 ; Opens pin 1 with the leading 0s have no effect.
```

ファイル ハンドルを開くには、アプリケーションは、Configuration Manager の Api (CM_Get_Device_Interface_ *) を呼び出す必要があります。 

ファイル ハンドルが開かれた後に、アプリケーションは、DeviceIoControl 関数を呼び出すことによってこれらの要求を送信できます。 PWM セクションを参照してください。



ドライバーは、解析し、暗証番号 (pin) のパスを検証する、指定された PWM サポート ルーチン PwmParsePinPath を使用し、暗証番号 (pin) を抽出する必要があります。 

## <a name="setting-device-interface-properties"></a>デバイス インターフェイスのプロパティの設定

UWP アプリから PWM WinRT Api を使用してこれら[デバイス インターフェイスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541409(v=vs.85).aspx)設定する必要があります。

-   [DEVPKEY_DeviceInterface_Restricted](https://msdn.microsoft.com/library/windows/hardware/hh406291(v=vs.85).aspx) 

    現在の UWP デバイスへのアクセス モデルに従って、PWM デバイス インターフェイスへの UWP アプリへのアクセスを提供する設定の制限付きデバイス インターフェイスのプロパティを FALSE が必要です。   

-   DEVPKEY_DeviceInterface_SchematicName (リンク ビルダー)

    PWM の静的に接続されたデバイスの PWM デバイス インターフェイスへの概略図の名前の割り当ては、PwmController.GetDeviceSelector(FriendlyName) のファクトリ メソッドを使用する必要があります。 (PWM0、PWM_1、et..)、システム設計の概略図などの PWM のデバイスに指定された名前をという名前の概略図 スキーマの名前は、システム全体で一意であると見なされますは適用されません。 少なくとも、することはできません同じスキーマ名を持つ 2 つの PWM デバイス、WinRT PWM PwmController.GetDeviceSelector(FriendlyName) 動作が不明確にあるそれ以外の場合。 

プロパティは、2 つの方法で設定できます。

1. PWM ドライバーの INF ファイルを使用

   使用して、 **AddProperty**ディレクティブをデバイスのプロパティを設定します。 INF ファイルは、1 つまたは PWM デバイスのインスタンスのサブセットに同じプロパティに対して異なる値を設定できるようにする必要があります。 DEVPKEY_DeviceInterface_Restricted を設定する例を次に示します。
    ```cpp
    ;***************************************** 
    ; Device interface installation 
    ;***************************************** 

    [PWM_Device.NT.Interfaces] 
    AddInterface={60824B4C-EED1-4C9C-B49C-1B961461A819},,PWM_Interface 

    [PWM_Interface] 
    AddProperty=PWM_Interface_AddProperty 

    ; Set DEVPKEY_DeviceInterface_Restricted property to false to allow UWP access 
    ; to the device interface without the need to be bound with device metadata. 
    ; If Restricted property is set to true, then only applications which are bound 
    ; with device metadata would be allowed access to the device interface. 

    [PWM_Interface_AddProperty] 
    {026e516e-b814-414b-83cd-856d6fef4822},6,0x11,,0 
    ```
    すべての設計では、UWP に PWM デバイスを公開するため同じポリシーを持ちます。 たとえば、PWM デバイス インスタンスのサブセットに UWP へのアクセスを許可するポリシー場合があります。 PWM デバイスのサブセットを公開するか、1 つまたは PWM のサブセットに別のプロパティ値を割り当てるデバイス インスタンスでは、各 PWM デバイス インスタンスと一致する INF セクションでは、ポリシーに基づいて、選択的に別のハードウェア ID を含める必要があります。

    SoC に基づく設計がありますは 4 つと同じ PWM デバイス (IP ブロック) という名前のインスタンス PWM0、…、PWM3、ACPI にハードウェア ID (_HID) が割り当てられている FSCL00E0 あり、一意 ID (_UID)..., 0 の場合は、3 を検討してください。 UWP へのすべての PWM デバイスを公開すると、ハードウェア ID の ACPI\FSCL00E0 に一致するように DEVPKEY_DeviceInterface_Restricted を設定する INF セクションでは、必要があります。 

    この方法でプロパティの設定では、ドライバー コードの変更は必要ありません。 これは簡単なオプション、INF をサービスとしてファイルがバイナリのドライバーよりも簡単です。 この方法がそれぞれの設計を調整した INF ファイルが必要であるという欠点が。 


2.  プログラムで、PWM ドライバー 

    PWM ドライバーには、作成し、PWM デバイス インターフェイスを公開後に、その EVT_WDF_DRIVER_DEVICE_ADD 実装でデバイス インターフェイスのプロパティを設定する IoSetDeviceInterfacePropertyData を呼び出すことができます。 ドライバーは、代入する値と、デバイス プロパティを決定します。 その情報は通常、SoC ベースの設計の ACPI システムに格納されます。 各デバイス インターフェイスのプロパティの値は、デバイスのプロパティとして各 ACPI デバイス ノード _DSD メソッドで指定できます。 ドライバーは、ACPI から _DSD をクエリ、デバイスのプロパティのデータを解析、各プロパティの値を抽出、およびデバイス インターフェイスを割り当てる必要があります。 

    ドライバーとその INF の設計の間で移植可能なファイルは、プログラムによって、プロパティを設定し、そのため Bsp の唯一の変更は ACPI PWM デバイスの各ノードを定義します。 をに。 ただし、読み取りと解析 ACPI バイナリ ブロックは手間のかかると、多くのエラーをより大きなエラー画面での脆弱性が発生しやすい可能性があるコードが必要です。 

## <a name="handling-file-openclose-events"></a>ファイルを開く/閉じるイベントの処理

PWM ドライバーは、ファイルの作成し、EVT_WDF_DEVICE_FILE_CREATE および EVT_WDF_FILE_CLEANUP/EVT_WDF_FILE_CLOSE のコールバック関数を実装することでイベントを閉じるを登録する必要があります。 実装では、ドライバーは、これらのタスクを実行する必要があります。

1.  コント ローラーまたは pin の作成要求であるかどうかを確認します。 
2.  ドライバーが解析する必要があり、暗証番号 (pin) のパスを検証、pin の要求の場合、pin の要求を作成し、要求の暗証番号 (pin) がコント ローラーの境界内にあるかどうかを確認します。 
3.  コント ローラーへのアクセス許可または拒否し、pin が要求を作成します。 
4.  適切に定義されたステート マシンあたりコント ローラーとピンの状態の整合性を維持します。 

上記の一連のタスクでは、検証の 2 番目のタスクを実行できます EVT_WDF_DEVICE_FILE_CREATE で、次のように。

1. 要求のファイル オブジェクトに関連付けられたファイル名が null の場合は、STATUS_INVALID_DEVICE_REQUEST で要求を完了します。 

2. 要求のファイル オブジェクトに関連付けられたファイル名が空の文字列としている場合、これは、コント ローラーの要求を作成、暗証番号 (pin) の作成要求がそれ以外の場合。 

3. 要求の pin の作成がこれ: 場合 

    1. 形式に基づく暗証番号 (pin) のパスの解析\<DecimalName > PwmParsePinPath を呼び出すことによって、暗証番号 (pin) を抽出します。 

    2. 解析に失敗しました暗証番号 (pin) のパスの検証、STATUS_NO_SUCH_FILE で要求を完了します。 

    3. 暗証番号 (pin) がより大きいか等しい場合、コント ローラーは、カウントをピン留めし、STATUS_NO_SUCH_FILE で要求を完了します。 暗証番号 (pin) は 0 から始まるインデックスであることに注意してください。 

    4. それ以外の場合、EVT_WDF_DEVICE_FILE_CREATE の処理を続行します。 

次のサンプル コード、EVT_WDF_DEVICE_FILE_CREATE ハンドラーの実装前に説明した検証手順に示します。 

```cpp
EVT_WDF_DEVICE_FILE_CREATE PwmEvtDeviceFileCreate;

VOID 

PwmEvtDeviceFileCreate ( 
    WDFDEVICE WdfDevice, 
    WDFREQUEST WdfRequest, 
    WDFFILEOBJECT WdfFileObject 
    ) 
{ 

    UNICODE_STRING* filenamePtr = WdfFileObjectGetFileName(WdfFileObject); 
    IMXPWM_DEVICE_CONTEXT* deviceContextPtr = PwmGetDeviceContext(WdfDevice); 
    NTSTATUS status; 
    ULONG pinNumber; 

    // 
    // Parse and validate the filename associated with the file object 
    // 

    bool isPinInterface; 

    if (filenamePtr == nullptr) { 

        WdfRequestComplete(WdfRequest, STATUS_INVALID_DEVICE_REQUEST); 

        return; 

    } else if (filenamePtr->Length > 0) { 

        // 
        // A non-empty filename means to open a pin under the controller namespace 
        // 

        status = PwmParsePinPath(filenamePtr, &pinNumber); 

        if (!NT_SUCCESS(status)) { 

            WdfRequestComplete(WdfRequest, status); 

            return; 

        } 


        if (pinNumber >= deviceContextPtr->ControllerInfo.PinCount) { 

            WdfRequestComplete(WdfRequest, STATUS_NO_SUCH_FILE); 

            return; 

        } 


        isPinInterface = true; 

    } else { 

        // 
        // An empty filename means that the create is against the root controller 
        // 

        isPinInterface = false; 
    } 

    // 
    // Continue request processing here 
    // 
} 
```
### <a name="controller-and-pin-sharing"></a>コント ローラーと pin 共有 

コント ローラーと pin を共有モデルでは、複数のリーダーでは、単一のライターのパターンに従います。 によって複数の呼び出し元の読み取りコント ローラーと pin を開くことができますが、1 つだけの呼び出し元は、同時書き込みのコント ローラーと pin を開くことができます。 

ファイル ハンドルを開くときに必要なアクセスと共有アクセス フラグの組み合わせを使用して、そのモデルを実装できます。 アクセスを制御するアクセスの必要な指定のみが使用されている単純な共有セマンティクスを選んだ DDI 共有モデル。 共有へのアクセス仕様では、任意のロール、共有モデルで再生されないがコント ローラーまたは暗証番号 (pin) を開くときに指定されている場合に適用することできません。  

EVT_WDF_DEVICE_FILE_CREATE、作成にベースのコント ローラーと pin 状態または次のように必要なアクセスと共有アクセスを抽出して検証を要求します。 

1. 共有へのアクセスがない場合 0 を拒否し、アクセス、および STATUS_SHARING_VIOLATION で要求を完了します。 

2. 必要なアクセスが読み取りの場合にのみ、アクセス権を付与し、EVT_WDF_DEVICE_FILE_CREATE の処理を続行します。 

3. 必要なアクセスは、書き込み、しが: 場合 

コント ローラーと pin が書き込みを開いて場合、アクセスが拒否し STATUS_SHARING_VIOLATION で要求を完了、それ以外の場合のアクセスを許可、書き込み用に開くように、コント ローラーまたは暗証番号 (pin) をマークおよび EVT_WDF_DEVICE_FILE_CREATE の処理を続行します。 

ここでは一例が必要なアクセスと共有へのアクセスを要求の作成から抽出する方法を示します。 

```cpp
void 
PwmCreateRequestGetAccess( 
    _In_ WDFREQUEST WdfRequest, 
    _Out_ ACCESS_MASK* DesiredAccessPtr, 
    _Out_ ULONG* ShareAccessPtr 
    ) 
{ 

    NT_ASSERT(ARGUMENT_PRESENT(DesiredAccessPtr)); 

    NT_ASSERT(ARGUMENT_PRESENT(ShareAccessPtr)); 


    WDF_REQUEST_PARAMETERS wdfRequestParameters; 

    WDF_REQUEST_PARAMETERS_INIT(&wdfRequestParameters); 

    WdfRequestGetParameters(WdfRequest, &wdfRequestParameters); 


    NT_ASSERTMSG( 

        "Expected create request", 
        wdfRequestParameters.Type == WdfRequestTypeCreate); 


    *DesiredAccessPtr = 
        wdfRequestParameters.Parameters.Create.SecurityContext->DesiredAccess; 

    *ShareAccessPtr = wdfRequestParameters.Parameters.Create.ShareAccess; 
} 
```

### <a name="controller-and-pin-independence"></a>コント ローラーと pin の独立性

コント ローラーと暗証番号 (pin)、親子 relatioship があります。 Pin を開くには、するには、親のコント ローラーを初めて開く必要があります。 別の方法がピンを見て個別のエンティティとして、親のコント ローラーがそのコント ローラーで、グローバル PWM 期間に含まれているすべての pin の設定の pin に 1 つのサービスを提供します。 

一部のシナリオの例を次に示します。 

- 単一プロセスへのアクセス: 

    -   プロセス A ことができます、暗証番号 (pin) を開きます、デューティ サイクルを設定、コント ローラーの既定の期間を使用して開始し後で、コント ローラーを開くおよびオンデマンドの期間を設定します。 既定の期間では、[ok] は、アプリケーションの場合、コント ローラーを開き、必要があることはありません。 

    -   プロセスでは複数スレッドそれぞれ同じコント ローラーの下に別々 の pin の制御の場所。 

- マルチ プロセスへのアクセス: 

    -   コマンド ライン ユーティリティでは、コンソールに情報を表示するために読み取り専用アクセス権を持つ、コント ローラーを開くことができます。 同時に UWP のバック グラウンド タスクは書き込み用に、コント ローラーを開くことができ、ピンが 1 つでいくつかの LED を制御します。 

    -   書き込みのコント ローラーを保持していると、PWM 期間のロック中に Pin0 を通じて LCD バックライトを制御する、カーネル モードのディスプレイ ドライバー。 、同時に、Win32 サービスを使用して、PWM 期間、ディスプレイ ドライバーによって設定すると、暗転 Pin1 を使用していくつかの LED をユーザーにいくつかの状態を通信するためにします。 

そのピンから独立してコント ローラーを開いたり閉じたりするいくつかの重要な意味があることに注意してください。 詳細については、ステート マシンのセクションを参照してください。 

## <a name="controller-and-pin-state-machines"></a>コント ローラーと pin のステート マシン

**コント ローラーの状態の定義**

|状態の機能|既定値|説明|
|---|---|--|
|開く-の-書き込み|False| False は、コント ローラーが閉じられるか、または読み取りのために開くことを示します。True は、書き込み用に開くことことを示します。|
|必要な期間| MinimumPeriod| |

![コント ローラーのステート マシン](images/controller-state-machine.png)

以下のコント ローラー ステート マシンが開かれた-の-書き込み状態のみの中心となります。 目的の期間値もを含めなかったため、コント ローラーで実行できる操作の種類には影響しません。 書き込み用に開かれているコント ローラーが、呼び出し元が書き込み用に開くが閉じられる、たびに、コント ローラーがその既定値 (必要な既定の期間) にリセット取得ことに注意してください。

**暗証番号 (pin) の状態の定義**


|    状態の機能    | 既定値 |                                                   説明                                                    |
|---------------------|---------------|------------------------------------------------------------------------------------------------------------------|
| 開く-の-書き込み |     False     | False は、pin が閉じているか、または読み取りのために開くことを示します。True は、書き込み用に開くことことを示します。 |
|  Active-Duty-Cycle  |       0       |                                                                                                                  |
|     -開始      |     False     |                                 False が停止します。True が開始されたことを示します。                                 |

![ピンのステート マシン](images/pins-state-machine.png)

Pin のステート マシンは、2 つの状態は/を開く-の-書き込みおよびが開始の組み合わせの中心となります。 他の暗証番号 (pin) の状態などの極性とその値は、暗証番号 (pin) で実行できる操作の種類に影響しないため、アクティブな負荷サイクルは省略しています。 書き込み用に開かれている pin を取得、呼び出し元が書き込み用に開く、閉じると、ときに、暗証番号 (pin) が残りの部分を既定値を取得ことに注意してください (極性、および active デューティ サイクル停止すると、既定)。 そのセット極性の遷移が開始状態に注意してください = true が除外されてない有効な状態にあるためです。

特定の状態に記載されていない任意の遷移は、このような切り替えが無効であるか実行可能でないことと、該当するエラー状態に対応する要求を完了する必要がありますを意味します。 

### <a name="implementation-considerations-for-state-transitions"></a>状態遷移の実装に関する考慮事項

- EVT_WDF_DEVICE_FILE_CREATE、ドライバーが許可または、次のように、作成要求が必要なアクセスとコント ローラーまたは暗証番号 (pin) が開かれた-の-書き込み状態に基づくアクセスを拒否する必要があります。

    要求が必要な書き込みアクセスとし、書き込みのコント ローラーと pin が既に開かれて、完了 STATUS_SHARING_VIOLATION を使用して要求をそれ以外の場合、コント ローラーと pin としてマーク書き込み用に開く (が開いて-の-書き込み = true)、アクセスを許可し、続行処理しています。

    この例では、前述のアクセスの検証手順を省略すると同時実行ファイルを処理するために必要なロックのロジックが要求を作成、EVT_WDF_DEVICE_FILE_CREATE ハンドラーの実装します。 
    ```cpp
    //
    // Verify request desired access
    //

    const bool hasWriteAccess = desiredAccess & FILE_WRITE_DATA;

    if (isPinInterface) {
        PWM_PIN_STATE* pinPtr = deviceContextPtr->Pins + pinNumber;
        if (hasWriteAccess) {
            if (pinPtr->IsOpenForReadWrite) {
                PWM_LOG_TRACE("Pin%lu access denied.", pinNumber);
                WdfRequestComplete(WdfRequest, STATUS_SHARING_VIOLATION);
                return;
            }
            pinPtr->IsOpenForReadWrite = true;
        }
        PWM_LOG_TRACE(
            "Pin%lu Opened. (IsOpenForReadWrite = %lu)",
            pinNumber,
            (pinPtr->IsOpenForReadWrite ? 1 : 0));

    } else {
        if (hasWriteAccess) {
            if (deviceContextPtr->IsControllerOpenForReadWrite) {
                PWM_LOG_TRACE("Controller access denied.");
                WdfRequestComplete(WdfRequest, STATUS_SHARING_VIOLATION);
                return;
            }
            deviceContextPtr->IsControllerOpenForReadWrite = true;
        }
        PWM_LOG_TRACE(
            "Controller Opened. (IsControllerOpenForReadWrite = %lu)",
            (deviceContextPtr->IsControllerOpenForReadWrite ? 1 : 0));
    }

    //
    // Allocate and fill a file object context
    //
    IMXPWM_FILE_OBJECT_CONTEXT* fileObjectContextPtr;
    {
        WDF_OBJECT_ATTRIBUTES wdfObjectAttributes;
        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(
            &wdfObjectAttributes,
            IMXPWM_FILE_OBJECT_CONTEXT);

        void* contextPtr;
        NTSTATUS status = WdfObjectAllocateContext(
                WdfFileObject,
                &wdfObjectAttributes,
                &contextPtr);
        if (!NT_SUCCESS(status)) {
            IMXPWM_LOG_ERROR(
                "WdfObjectAllocateContext(...) failed. (status = %!STATUS!)",
                status);
            WdfRequestComplete(WdfRequest, status);
            return;
        }

        fileObjectContextPtr =
            static_cast<IMXPWM_FILE_OBJECT_CONTEXT*>(contextPtr);

        NT_ASSERT(fileObjectContextPtr != nullptr);
        fileObjectContextPtr->IsPinInterface = isPinInterface;
        fileObjectContextPtr->IsOpenForWrite = hasWriteAccess;
        fileObjectContextPtr->PinNumber = pinNumber;
    }
    ```

- EVT_WDF_FILE_CLOSE で/EVT_WDF_FILE_CLEANUP、ドライバーはコント ローラーおよびピンの状態の整合性を維持する必要があります。 

  ファイル オブジェクトに属する場合の書き込み、そのコント ローラーと pin を開くことがコント ローラーと pin、既定の状態にコント ローラーと pin をリセットおよび書き込み用に開かれからそのコント ローラー pin/のマークの解除 (が開いて-の-書き込み = false)。

  この例では、同時実行ファイルの閉じる要求を処理するために必要なロックのロジックを省略すると、EVT_WDF_DEVICE_FILE_CLOSE ハンドラーの前に説明したアクセスの検証手順を実装します。
  ```cpp
  EVT_WDF_DEVICE_FILE_CLOSE PwmEvtFileClose;

  VOID
  PwmEvtFileClose (
      WDFFILEOBJECT WdfFileObject
      )
  {
      WDFDEVICE wdfDevice = WdfFileObjectGetDevice(WdfFileObject);
      PWM_DEVICE_CONTEXT* deviceContextPtr = PwmGetDeviceContext(wdfDevice);
      PWM_FILE_OBJECT_CONTEXT* fileObjectContextPtr = PwmGetFileObjectContext(WdfFileObject);

      if (fileObjectContextPtr->IsPinInterface) {
          if (fileObjectContextPtr->IsOpenForReadWrite) {
              const ULONG pinNumber = fileObjectContextPtr->PinNumber;

              NTSTATUS status = PwmResetPinDefaults(deviceContextPtr, pinNumber);
              if (!NT_SUCCESS(status)) {
                  PWM_LOG_ERROR(
                      "PwmResetPinDefaults(...) failed. "
                      "(pinNumber = %lu, status = %!STATUS!)",
                      pinNumber,
                      status);
                  //
                  // HW Error Recovery
                  //
              }

              NT_ASSERT(deviceContextPtr->Pins[pinNumber].IsOpenForReadWrite);
              deviceContextPtr->Pins[pinNumber].IsOpenForReadWrite = false;
          }

          PWM_LOG_TRACE("Pin%lu Closed.", fileObjectContextPtr->PinNumber);

      } else {
          if (fileObjectContextPtr->IsOpenForReadWrite) {
              NTSTATUS status = PwmResetControllerDefaults(deviceContextPtr);
              if (!NT_SUCCESS(status)) {
                  IMXPWM_LOG_ERROR(
                      "PwmResetControllerDefaults(...) failed. (status = %!STATUS!)",
                      status);
                  //
                  // HW Error Recovery
                  //  
              }

              NT_ASSERT(deviceContextPtr->IsControllerOpenForReadWrite);
              deviceContextPtr->IsControllerOpenForReadWrite = false;
          }

          PWM_LOG_TRACE("Controller Closed.");
      }
  }
  ```
  ## <a name="pwm-ioctl-requests"></a>PWM IOCTL 要求

PWM IOCTL 要求は、アプリケーションまたは別のドライバーによって送信されは、コント ローラーまたは特定の暗証番号 (pin) を対象とします。

**コント ローラーの Ioctl**

-    [**IOCTL_PWM_CONTROLLER_GET_ACTUAL_PERIOD**](https://msdn.microsoft.com/library/windows/desktop/mt826475) 
-    [**IOCTL_PWM_CONTROLLER_GET_INFO**](https://msdn.microsoft.com/library/windows/desktop/mt826476) 
-    [**IOCTL_PWM_CONTROLLER_SET_DESIRED_PERIOD**](https://msdn.microsoft.com/library/windows/desktop/mt826478)


**Pin の Ioctl**

-    [**IOCTL_PWM_PIN_GET_ACTIVE_DUTY_CYCLE_PERCENTAGE**](https://msdn.microsoft.com/library/windows/desktop/mt843915)
-    [**IOCTL_PWM_PIN_SET_ACTIVE_DUTY_CYCLE_PERCENTAGE**](https://msdn.microsoft.com/library/windows/desktop/mt843918)
-    [**IOCTL_PWM_PIN_GET_POLARITY**](https://msdn.microsoft.com/library/windows/desktop/mt843916)
-    [**IOCTL_PWM_PIN_SET_POLARITY**](https://msdn.microsoft.com/library/windows/desktop/mt843919)
-    [**IOCTL_PWM_PIN_START**](https://msdn.microsoft.com/library/windows/desktop/mt843920)
-    [**IOCTL_PWM_PIN_STOP**](https://msdn.microsoft.com/library/windows/desktop/mt843921)
-    [**IOCTL_PWM_PIN_IS_STARTED**](https://msdn.microsoft.com/library/windows/desktop/mt843917)    

IOCTL 要求ごとに、PWM drivr が、次を確認する必要があります。 

1. 要求された操作 (IOCTL コード) は、要求のファイルが関連付けられているオブジェクトに有効です。 

2. 入力と出力バッファーを要求し、少なくともあるかどうかを確認、最小のサイズを想定します。 

3. 現在のコント ローラーおよびピンの状態で要求された操作の有効性。 

4. 個々 の入力パラメーターの有効性。 例: 必要な期間を 0 は IOCTL_PWM_CONTROLLER_SET_DESIRED_PERIOD に対して無効なパラメーター。 

### <a name="ioctl-completion-status-codes"></a>IOCTL 完了の状態コード 

PWM ドライバーでは、適切な状態コードと IOCTL 要求を完了する必要があります。 完了する一般的なステータス コードを次に示します。 一般に、既に設定されている値を持つプロパティを設定する IOCTL は常に成功する必要があります。 敵対例では、正確な同じ期間の設定は既に設定されて、暗証番号 (pin) は既に停止している、既に設定されている設定極性具合を停止しています。 

**STATUS_NOT_SUPPORTED** 

要求された IOCTL 操作は実装もサポートします。 たとえば、一部のコント ローラーでは、IOCTL_PWM_PIN_SET_POLARITY が実装する必要がありますが、既定以外の極性の STATUS_NOT_SUPPORTED で失敗する場合はそのような出力信号の極性を設定する可能性がありますできません。 

**STATUS_INVALID_DEVICE_REQUEST** 

IOCTL 要求は、正しくないターゲットに送信されました。 たとえば、コント ローラーの IOCTL 要求は、暗証番号 (pin) のファイル ハンドルを使用して送信されました。 

**STATUS_BUFFER_TOO_SMALL** 

入力または出力バッファー サイズは、要求を処理するための最低限必要なバッファー サイズより小さい。 WdfRequestRetrieveInputBuffer または WdfRequestRetrieveOutputBuffer を使用して取得し、入力と出力バッファーを検証する WDF ドライバーでは、その対応するエラー状態をそのままを返すことができます。 すべての Ioctl で入力または出力バッファーの定義に対応する入力と出力の構造体名がある、そのバッファーを記述する構造体がある*入力と _OUTPUT それぞれ後置形式します。入力バッファーの最小サイズは sizeof (PWM*<em>*入力)、出力バッファーの最小サイズは sizeof (PWM*</em>_OUTPUT)。 

IOCTL コード | 説明|
---|---|
|IOCTL_PWM_CONTROLLER_GET_ACTUAL_PERIOD | その出力チャネルで計測したことには、パルス幅変調 (PWM) コント ローラーの有効な出力シグナル期間を取得します。 PWM_CONTROLLER_GET_ACTUAL_PERIOD_OUTPUT 値を返します。 Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。 <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
| IOCTL_PWM_CONTROLLER_GET_INFO| パルス幅変調 (PWM) コント ローラーに関する情報を取得します。 この情報は、コント ローラーが初期化された後は変更されません。 <p>呼び出し元を正確に PWM_CONTROLLER_INFO 構造体のサイズを持つ出力バッファーを渡す必要があります。 ドライバーは、要求の出力バッファーのサイズから構造のバージョンを推測します。 </p><p>バッファー サイズが、構造体の最小バージョンのサイズより小さい場合は、STATUS_BUFFER_TOO_SMALL の IOCTL 完了状態を使用して、要求が完了します。 それ以外の場合、ドライバーでは、指定された出力バッファーに収まるし、要求を正常に完了する構造の最上位バージョンを前提としています。 </p><p>新しい PWM_CONTROLLER_INFO バージョンが、以前のバージョンよりも大きいバイト サイズ</p>Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。 <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_CONTROLLER_SET_DESIRED_PERIOD|推奨値には、パルス幅変調 (PWM) コント ローラーの出力シグナル期間を設定します。 <p>PWM コント ローラーは、その機能に基づいて、要求された値にできるだけ近いである期間を設定しようとします。 有効期間は、IOCTL 出力として返されます。 IOCTL_PWM_CONTROLLER_GET_ACTUAL_PERIOD を使用して、後で取得できます。</p><p>目的の期間が期間のコント ローラーがサポートされている範囲でゼロ (0) より大きい必要があります。 これは、範囲の MinimumPeriod と MaximumPeriod、両端を含む IOCTL_PWM_CONTROLLER_GET_INFO を使用して取得できますに存在する必要があります。 </p>Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。 <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_INVALID_PARAMETER</li><li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_GET_ACTIVE_DUTY_CYCLE_PERCENTAGE| 現在の義務を取得します。 pin またはチャネルの比率を切り替えます。 コントロールのコードは、PWM_PIN_GET_ACTIVE_DUTY_CYCLE_PERCENTAGE_OUTPUT 構造体としての割合を返します。<p>Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_SET_ACTIVE_DUTY_CYCLE_PERCENTAGE|コント ローラーの暗証番号 (pin) またはチャネルに対する必要な関税サイクル百分率の値を設定します。 コントロールのコードでは、PWM_PIN_SET_ACTIVE_DUTY_CYCLE_PERCENTAGE_INPUT 構造として、割合を指定します。<p>Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。</p> <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_GET_POLARITY| 暗証番号 (pin) またはチャネルの現在の信号の極性を取得します。 制御コードを信号の極性 PWM_PIN_GET_POLARITY_OUTPUT 構造体として取得します。 信号の極性は高アクティブまたはアクティブ ロー、PWM_POLARITY 列挙で定義されているです。<p>Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。</p> <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_SET_POLARITY| 暗証番号 (pin) またはチャネルの信号の極性を設定します。 コントロールのコードでは、PWM_PIN_SET_POLARITY_INPUT 構造に基づく、信号の極性を設定します。 信号の極性は高アクティブまたはアクティブ ロー、PWM_POLARITY 列挙型で定義されているです。 <p>Pin が停止したときに、極性の変更をできるだけです。 IOCTL_PWM_PIN_IS_STARTED コントロールのコードを使用して、暗証番号 (pin) が停止したかどうかを判断できます。 Pin が停止され、要求の極性が現在の pin の極性と異なる、STATUS_INVALID_DEVICE_STATE 値を持つ要求が完了します。</p><p>極性の変更、ピン留めを開始する際にについては、いくつかパルス幅変調 (PWM) コント ローラーの問題につながります。 極性を変更する場合は、最初に、暗証番号 (pin) を停止、極性によって、変更および、暗証番号 (pin) を開始します。</p><p>Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_INVALID_PARAMETER</li><li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_START|Pin またはチャネルでは、パルス幅変調 (PWM) シグナルの生成を開始します。 Pin が開始されているかどうかを確認するには、IOCTL_PWM_PIN_IS_STARTED を使用します。<p>Pin または既に開始されているチャネルでは、この IOCTL の発行、影響を与えませんが成功します。</p><p>Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。</p>><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_STOP|Pin またはチャネルでは、パルス幅変調 (PWM) シグナルの生成を停止します。 Pin が開始されているかどうかを確認するには、IOCTL_PWM_PIN_IS_STARTED を使用します。<p>Pin または既に停止しているチャネルでは、この IOCTL の発行、影響を与えませんが成功します。</p><p>Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_IS_STARTED|Pin またはチャネルのシグナルの生成の状態を取得します。 各ピンでは、開始または停止 PWM_PIN_IS_STARTED_OUTPUT 構造体としての状態があります。 開始状態では、true のブール値を持ちます。 停止状態では false です。 <p>既定では、pin は、開かれたときに停止し、それを閉じたときの状態を停止しているが閉じられるか解放を返します。</p><p>Irp IoStatus.Status]-> [が次の一覧で値のいずれかに設定します。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|


