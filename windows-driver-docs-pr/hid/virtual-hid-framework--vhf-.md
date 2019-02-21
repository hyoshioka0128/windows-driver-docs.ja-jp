---
title: 仮想 HID フレームワーク (VHF) を使用して、HID ソース ドライバーを作成します。
description: オペレーティング システムに HID ソース ドライバー HID レポート データの記述方法について説明します。
ms.assetid: 26964963-792F-4529-B4FC-110BF5C65B35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92286f38db7ec35cd94b6f64f2ab7ac8fdd4a539
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532911"
---
# <a name="write-a-hid-source-driver-by-using-virtual-hid-framework-vhf"></a>仮想 HID フレームワーク (VHF) を使用して、HID ソース ドライバーを作成します。

**要約**

-   オペレーティング システムに読み取りの HID レポートを送信するカーネル モード ドライバー フレームワーク (KMDF) HID ソース ドライバーを記述します。
-   仮想の HID デバイス スタックの HID ソース ドライバーには、下位のフィルターとして VHF ドライバーを読み込みます。

**適用されます。**

-   Windows 10
-   HID デバイスのドライバー開発者向け

**重要な API**

-   [仮想 HID Framework コールバック関数](https://msdn.microsoft.com/library/windows/hardware/dn925049)
-   [仮想 HID Framework メソッド](https://msdn.microsoft.com/library/windows/hardware/dn925053)
-   [仮想 HID フレームワークの構造体](https://msdn.microsoft.com/library/windows/hardware/dn925054)

オペレーティング システムに HID ソース ドライバー HID レポート データの記述方法について説明します。

HID の入力デバイスでは、次のように – キーボード、マウス、ペン、タッチ、またはボタン、さまざまなレポートを送信しますオペレーティング システム、デバイスの目的を理解し、必要なアクションを実行できるようにします。 レポートは、の形式で[HID コレクション](opening-hid-collections.md)と[HID の使用](hid-usages.md)します。 デバイスなど、Windows でサポートされるうちいくつかのさまざまなトランスポート経由でそれらのレポートを送信する[I2C 経由で非表示に](hid-over-i2c-guide.md)と[USB 経由で HID](hid-over-usb.md)します。 場合によっては、トランスポートは、Windows でサポートされていない可能性があります。 またはレポートが実際のハードウェアに直接マップがいません。 非 GPIO ボタンやセンサーなどの仮想ハードウェアの別のソフトウェア コンポーネントによって送信される HID 形式のデータのストリームがあります。 たとえば、加速度計データから、携帯電話、PC にワイヤレス接続で送信しながら、ゲーム コント ローラーとして動作するかを検討してください。 別の例では、コンピューターをリモートから入力を受け取り Miracast デバイス UIBC プロトコルを使用しています。

Windows の以前のバージョンで新しいトランスポート (実際のハードウェアまたはソフトウェア) をサポートするために記述しなければ、 [HID トランスポート ミニドライバー](transport-minidrivers.md) Hidclass.sys、Microsoft 提供のインボックス クラス ドライバーにバインドします。 など、クラス/ミニ ドライバー ペアに、HID コレクションが提供されている[最上位のコレクション](top-level-collections.md)上位レベルのドライバーとアプリケーションのユーザー モードにします。 モデルでは、課題は、書き込み、ミニドライバーは、複雑な作業をすることができます。

Windows 10 以降、新しい仮想 HID フレームワーク (VHF) トランスポート ミニドライバーを記述する必要はありません。 代わりにか WDM、KMDF のプログラミング インターフェイスを使用して、HID ソース ドライバーを作成することができます。 フレームワークは、ドライバーによって使用されるプログラミング要素を公開するための Microsoft から提供された静的ライブラリで構成されます。 1 つまたは複数の子デバイスを列挙し、構築して仮想 HID ツリーの管理を実行する Microsoft 提供のインボックス ドライバーも含まれています。

**注**  VHF をこのリリースでは、カーネル モードでのみ HID ソース ドライバーをサポートしています。

このトピックでは、フレームワーク、仮想の HID デバイス ツリー、および構成シナリオのアーキテクチャについて説明します。

## <a name="virtual-hid-device-tree"></a>仮想の HID デバイス ツリー

この図では、デバイス ツリーは、ドライバーとその関連するデバイス オブジェクトを示します。

![仮想の hid デバイス ツリー](images/vhf.png)

**HID ソース ドライバー (ドライバー)**

HID のソースのドライバーは Vhfkm.lib へのリンクし、Vhf.h にはそのビルド プロジェクトが含まれています。 いずれかを使用して、ドライバーを記述できます[Windows Driver Model](https://msdn.microsoft.com/library/windows/hardware/ff565698) (WDM) の一部であるカーネル モード ドライバー フレームワーク (KMDF)、または、 [Windows Driver Frameworks (WDF)](https://msdn.microsoft.com/library/windows/hardware/dn312126)します。 ドライバー、フィルター ドライバーまたはデバイス スタックの関数のドライバーとして読み込むことができます。

**VHF スタティック ライブラリ (vhfkm.lib)**

スタティック ライブラリには、Windows 10 用 Windows Driver Kit (WDK) では含まれます。 ライブラリは、ルーチンには、HID ソース ドライバーによって使用されているコールバック関数などのプログラミング インターフェイスを公開します。 ドライバーが関数を呼び出すときに、スタティック ライブラリは、要求を処理する VHF ドライバーに要求を転送します。

**VHF ドライバー (Vhf.sys)**

Microsoft 提供のインボックス ドライバー。 このドライバーは HID ソース デバイス スタックで、ドライバーの下に下位のフィルター ドライバーとして読み込む必要があります。 動的に VHF ドライバーは、子デバイスを列挙し、HID ソースのドライバーで指定されている 1 つまたは複数の HID デバイスの物理デバイス オブジェクト (PDO) を作成します。 列挙子のデバイスのトランスポートの HID ミニ ドライバー機能も実装します。

**HID クラス ドライバーのペア (Hidclass.sys、Mshidkmdf.sys)**

Hidclass/Mshidkmdf ペアを列挙[最上位のコレクション (TLC)](top-level-collections.md)実際の HID デバイスのこれらのコレクションを列挙する方法に似ています。 HID クライアントは、要求および実際の HID デバイスと同じよう TLCs の使用を続行できます。 このドライバーのペアは、デバイス スタックの関数のドライバーとしてインストールされます。

**注**  一部のシナリオでは HID クライアント HID データのソースを識別する必要があります。 など、システムを組み込みセンサーして、同じ種類のリモートのセンサーからデータを受信します。 システムは、信頼性を 1 つのセンサーを選択する場合があります。 2 つのセンサーを区別するためには、コンテナー id が、TLC の HID クライアント クエリ、システムに接続されています。 この場合は、HID ソースのドライバーは VHF によって仮想 HID デバイスのコンテナーの ID として報告されるコンテナー ID を提供できます。

**HID クライアント (アプリケーション)**

クエリを実行し、HID デバイス スタックによって報告される TLCs を使用します。

## <a name="header-and-library-requirements"></a>ヘッダーとライブラリの要件

この手順では、オペレーティング システムにそのレポート ヘッドセット ボタンの単純な HID ソース ドライバーを記述する方法について説明します。 ここでは、このコードを実装するドライバーは VHF を使用して、ヘッドセット ボタンを報告する HID ソースとして機能するように変更されている既存の KMDF オーディオ ドライバーを指定できます。

1.  Windows 10 の WDK に含まれる Vhf.h が含まれます。
2.  WDK に含まれる vhfkm.lib にリンクします。
3.  デバイスがオペレーティング システムに報告する HID レポート記述子を作成します。 この例では、HID レポート記述子には、ヘッドセット ボタンがについて説明します。 レポートには、HID 入力レポート、サイズ 8 ビット (1 バイト) を指定します。 最初の 3 つのビットはヘッドセットのミドル ネーム、ボリュームをおよびボリューム ダウン ボタンです。 残りのビットは、使用されません。

```cpp
UCHAR HeadSetReportDescriptor[] = {
    0x05, 0x01,         // USAGE_PAGE (Generic Desktop Controls)
    0x09, 0x0D,         // USAGE (Portable Device Buttons)
    0xA1, 0x01,         // COLLECTION (Application)
    0x85, 0x01,         //   REPORT_ID (1)
    0x05, 0x09,         //   USAGE_PAGE (Button Page)
    0x09, 0x01,         //   USAGE (Button 1 - HeadSet : middle button)
    0x09, 0x02,         //   USAGE (Button 2 - HeadSet : volume up button)
    0x09, 0x03,         //   USAGE (Button 3 - HeadSet : volume down button)
    0x15, 0x00,         //   LOGICAL_MINIMUM (0)
    0x25, 0x01,         //   LOGICAL_MAXIMUM (1)
    0x75, 0x01,         //   REPORT_SIZE (1)
    0x95, 0x03,         //   REPORT_COUNT (3)
    0x81, 0x02,         //   INPUT (Data,Var,Abs)
    0x95, 0x05,         //   REPORT_COUNT (5)
    0x81, 0x03,         //   INPUT (Cnst,Var,Abs)
    0xC0,               // END_COLLECTION
};
```

## <a name="create-a-virtual-hid-device"></a>仮想 HID デバイスを作成します。

初期化を[ **VHF\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/dn925044)構造を呼び出すことによって、 [ **VHF\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/dn925046)マクロと、呼び出し、 [ **VhfCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn925036)メソッド。 ドライバーを呼び出す必要があります**VhfCreate**パッシブで\_後レベル、 [ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)呼び出し、通常、ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。

[ **VhfCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn925036)呼び出し、ドライバーは非同期的に処理されたか、設定のデバイス情報 (ベンダーと製品 Id) にする必要がある操作など、特定の構成オプションを指定できます。

たとえば、アプリケーションは、TLC を要求します。 ペアが要求の種類を決定し、適切な作成 HID クラス ドライバーのペアは、その要求を受信したときに[HID ミニドライバー IOCTL](https://msdn.microsoft.com/library/windows/hardware/ff539926)要求および VHF に転送します。 IOCTL 要求を取得するには、時に VHF 要求を処理、処理に HID ソース ドライバーに依存したり、ステータスの要求を完了\_いない\_サポートされています。

VHF では、これらの Ioctl を処理します。

-   [**IOCTL\_HID\_取得\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff541167)
-   [**IOCTL\_HID\_取得\_デバイス\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff541093)
-   [**IOCTL\_HID\_取得\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541098)
-   [**IOCTL\_HID\_取得\_レポート\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541147)

要求が場合**GetFeature**、 **SetFeature**、 **WriteReport**、または**GetInputReport**、HID ソース ドライバーが登録されている、対応するコールバック関数、VHF では、コールバック関数を呼び出します。 その関数内で、HID ソース ドライバーは、取得または HID データ HID 仮想デバイスを設定します。 VHF の状態で要求が完了すると、ドライバーがコールバックを登録しない場合\_いない\_サポートされています。

VHF は、これらの Ioctl の HID ソース ドライバー実装イベントのコールバック関数を呼び出します。

-   [**IOCTL\_HID\_読み取り\_レポート**](https://msdn.microsoft.com/library/windows/hardware/ff541172)

    これを実装する必要があります、ドライバーは、入力の HID レポートを取得するバッファーを送信中に、バッファリング ポリシーを処理する必要がある場合、 [ *EvtVhfReadyForNextReadReport* ](https://msdn.microsoft.com/library/windows/hardware/dn897135) でポインターを指定して**EvtVhfAsyncOperationGetInputReport**メンバー。 詳細については、次を参照してください。[入力の HID レポートを提出](#submit)します。

-   [**IOCTL\_HID\_取得\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff541103)または[ **IOCTL\_HID\_設定\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff541184)

    取得または機能を非表示にレポートを非同期的に設定する場合、ドライバーは、ドライバーを実装する必要があります、 [ *EvtVhfAsyncOperation* ](https://msdn.microsoft.com/library/windows/hardware/dn897133)関数 get へのポインターを指定するかで実装関数を設定します**EvtVhfAsyncOperationGetFeature**または**EvtVhfAsyncOperationSetFeature**のメンバー [ **VHF\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/dn925044).

-   [**IOCTL\_HID\_取得\_入力\_レポート**](https://msdn.microsoft.com/library/windows/hardware/ff541128)

    ドライバーを実装する必要があります、ドライバーは、入力を非表示にレポートを非同期的に取得する必要がある場合、 [ *EvtVhfAsyncOperation* ](https://msdn.microsoft.com/library/windows/hardware/dn897133)関数を指定の関数へのポインター、 **EvtVhfAsyncOperationGetInputReport**のメンバー [ **VHF\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/dn925044)します。

-   [**IOCTL\_HID\_書き込み\_レポート**](https://msdn.microsoft.com/library/windows/hardware/ff541221)

    ドライバーは、書き込みの入力を非表示にレポートを非同期的に取得する必要がある場合、ドライバーを実装する必要があります、 [ *EvtVhfAsyncOperation* ](https://msdn.microsoft.com/library/windows/hardware/dn897133)関数を指定の関数へのポインター、 **EvtVhfAsyncOperationWriteReport**のメンバー [ **VHF\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/dn925044)します。

その他の[HID ミニドライバー IOCTL](https://msdn.microsoft.com/library/windows/hardware/ff539926)、VHF 状態要求が完了すると\_いない\_サポートされています。

呼び出すことによって仮想 HID デバイスが削除された、 [ **VhfDelete**](https://msdn.microsoft.com/library/windows/hardware/dn925038)します。 [ *EvtVhfCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn897134)ドライバーでは、仮想の HID デバイスのリソースが割り当てられている場合は、callback は必須です。 ドライバーを実装する必要があります、 *EvtVhfCleanup*関数し、その関数へのポインターを指定、 **EvtVhfCleanup**のメンバー [ **VHF\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/dn925044). *EvtVhfCleanup*する前に呼び出される、 **VhfDelete**呼び出しが完了します。 詳細については、次を参照してください。[仮想 HID デバイスを削除](#delete-the-virtual-hid-device)します。

**注**  非同期の操作の完了後、ドライバーを呼び出す必要があります[ **VhfAsyncOperationComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn925060)操作の結果を設定します。 または、コールバックから戻った後に後で、イベント コールバックからメソッドを呼び出すことができます。

```cpp
NTSTATUS
VhfSourceCreateDevice(
_Inout_ PWDFDEVICE_INIT DeviceInit
)

{
    WDF_OBJECT_ATTRIBUTES   deviceAttributes;
    PDEVICE_CONTEXT deviceContext;
    VHF_CONFIG vhfConfig;
    WDFDEVICE device;
    NTSTATUS status;

    PAGED_CODE();

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&deviceAttributes, DEVICE_CONTEXT);
    deviceAttributes.EvtCleanupCallback = VhfSourceDeviceCleanup;

    status = WdfDeviceCreate(&DeviceInit, &deviceAttributes, &device);

    if (NT_SUCCESS(status))
    {
        deviceContext = DeviceGetContext(device);

        VHF_CONFIG_INIT(&vhfConfig,
            WdfDeviceWdmGetDeviceObject(device),
            sizeof(VhfHeadSetReportDescriptor),
            VhfHeadSetReportDescriptor);

        status = VhfCreate(&vhfConfig, &deviceContext->VhfHandle);

        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, "VhfCreate failed %!STATUS!", status);
            goto Error;
        }

        status = VhfStart(deviceContext->VhfHandle);
        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, "VhfStart failed %!STATUS!", status);
            goto Error;
        }

    }

Error:
    return status;
}
```

## <a name="submit-the-hid-input-report"></a>HID 入力レポートを送信します。

レポートを送信する HID 入力呼び出して[ **VhfReadReportSubmit**](https://msdn.microsoft.com/library/windows/hardware/dn925040)します。

通常、HID デバイスでは、割り込みを介して入力のレポートを送信して状態の変更に関する情報を送信します。 たとえば、ヘッドセット デバイス ボタンの状態が変更されたときに、レポートを送信可能性があります。 このようなイベントでは、ドライバーの割り込みサービス ルーチン (ISR) が呼び出されます。 ルーチン、ドライバーは遅延プロシージャ呼び出し (DPC) を入力のレポートを処理し、オペレーティング システムに情報を送信する、VHF に送信をスケジュール可能性があります。 既定では、VHF バッファーのレポートとでやり取りされるように入力の HID レポートを送信する HID ソースのドライバーを開始できます。 これは、複雑な同期を実装する HID ソース ドライバーの必要がありません。

HID ソースのドライバーでは、保留中のレポートのバッファリング ポリシーを実装することで、入力のレポートを送信できます。 重複するバッファリングを避けるためには、HID ソースのドライバーを実装できます、 [ *EvtVhfReadyForNextReadReport* ](https://msdn.microsoft.com/library/windows/hardware/dn897135) VHF にこのコールバックが呼び出されるかどうかのコールバック関数と保持を追跡します。 HID のソースのドライバーを呼び出すことができる場合、呼び出された以前[ **VhfReadReportSubmit** ](https://msdn.microsoft.com/library/windows/hardware/dn925040)レポートを送信します。 待機する*EvtVhfReadyForNextReadReport*を呼び出すことができる前に呼び出される**VhfReadReportSubmit**もう一度です。

```cpp
VOID
MY_SubmitReadReport(
    PMY_CONTEXT  Context,
    BUTTON_TYPE  ButtonType,
    BUTTON_STATE ButtonState
    )
{
    PDEVICE_CONTEXT deviceContext = (PDEVICE_CONTEXT)(Context);

    if (ButtonState == ButtonStateUp) {
        deviceContext->VhfHidReport.ReportBuffer[0] &= ~(0x01 << ButtonType);
    } else {
        deviceContext->VhfHidReport.ReportBuffer[0] |=  (0x01 << ButtonType);
    }

    status = VhfSubmitReadReport(deviceContext->VhfHandle, &deviceContext->VhfHidReport);

    if (!NT_SUCCESS(status)) {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE,"VhfSubmitReadReport failed %!STATUS!", status);
    }
}
```

## <a name="delete-the-virtual-hid-device"></a>仮想の HID デバイスを削除します。

呼び出すことにより、仮想の HID デバイスを削除[ **VhfDelete**](https://msdn.microsoft.com/library/windows/hardware/dn925038)します。

[**VhfDelete** ](https://msdn.microsoft.com/library/windows/hardware/dn925038)同期呼び出すことができるまたは Wait パラメーターの値を非同期的を指定します。 同期呼び出しでは、パッシブに、メソッドを呼び出す必要があります\_からなど、レベル、 [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)のデバイス オブジェクト。 **VhfDelete**仮想 HID デバイスを削除した後に返されます。 ドライバーを呼び出す場合**VhfDelete** VHF を呼び出すし、すぐに返されます。 非同期的に[ *EvtVhfCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn897134)削除操作が完了した後。 ディスパッチの最大のメソッドを呼び出すことができます\_レベル。 この場合、ドライバーを登録して、実装がある必要があります、 *EvtVhfCleanup*コールバック関数が、以前に呼び出されたときに[ **VhfCreate**](https://msdn.microsoft.com/library/windows/hardware/dn925036)します。 HID のソースのドライバーが仮想の HID デバイスを削除するときのイベントのシーケンスを次に示します。

1.  VHF への呼び出しを開始する HID ソース ドライバーを停止します。
2.  HID ソース呼び出し[ **VhfDelete** ](https://msdn.microsoft.com/library/windows/hardware/dn925038)で*待機*を FALSE に設定します。
3.  VHF は、HID ソース ドライバーによって実装されるコールバック関数の呼び出しを停止します。
4.  VHF PnP マネージャーに存在しないデバイスをレポート作成を開始します。 この時点では、VhfDelete 呼び出しを返す可能性があります。
5.  デバイスが紛失したデバイスとして報告されると、VHF を呼び出す[ *EvtVhfCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn897134) HID ソースのドライバーには、その実装が登録されている場合。
6.  後[ *EvtVhfCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn897134)返します、VHF のクリーンアップを実行します。

```cpp
VOID
VhfSourceDeviceCleanup(
_In_ WDFOBJECT DeviceObject
)
{
    PDEVICE_CONTEXT deviceContext;

    PAGED_CODE();

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

    deviceContext = DeviceGetContext(DeviceObject);

    if (deviceContext->VhfHandle != WDF_NO_HANDLE)
    {
        VhfDelete(deviceContext->VhfHandle, TRUE);
    }

}
```

## <a name="install-the-hid-source-driver"></a>HID ソース ドライバーをインストールします。

HID ソースのドライバーをインストールする INF ファイルで宣言すること Vhf.sys 低いフィルター ドライバーとして HID ソース ドライバーを使用することを確認、 [ **AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。

```cpp
[HIDVHF_Inst.NT.HW]
AddReg = HIDVHF_Inst.NT.AddReg

[HIDVHF_Inst.NT.AddReg]
HKR,,"LowerFilters",0x00010000,"vhf"
```

## <a name="related-topics"></a>関連トピック
[ヒューマン インターフェイス デバイス](https://msdn.microsoft.com/library/windows/hardware/ff543301)

