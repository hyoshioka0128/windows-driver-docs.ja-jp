---
title: WDI IHV ドライバー インターフェイス
description: WDI IHV ミニポートは他の NDIS ミニポート ドライバーに似ています、開発手法と任意の NDIS ミニポートのドキュメントに実行します。
ms.assetid: B4528C70-9FE4-4E00-9D0B-8832CCEC982E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cd10bc2af08445689c1ffd96bda3598b567c13a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551899"
---
# <a name="wdi-ihv-driver-interfaces"></a>WDI IHV ドライバー インターフェイス


WDI IHV ミニポートは他の NDIS ミニポート ドライバーに似ています、開発手法と任意の NDIS ミニポートのドキュメントに実行します。 NDIS ハンドラーのネイティブ WLAN ミニポート ドライバーの責任は、MS コンポーネントと WDI IHV ドライバーの間に分割されます。 Microsoft の WLAN のコンポーネントが動作するすべての IHV が元に戻す必要があるないようにすべての Wi-fi ミニポートに適用される NDIS 要件処理します。 マッピングとネイティブの WLAN IHV ミニポート WDI IHV ミニポートに適用する場合の NDIS ハンドラーの動作の変更を以下に示します。

-   [ドライバーのインストール](#driver-installation)
-   [DriverEntry](#driverentry)
-   [MiniportSetOptions](#miniportsetoptions)
-   [MiniportInitializeEx](#miniportinitializeex)
-   [MiniportHaltEx](#miniporthaltex)
-   [MiniportDriverUnload](#miniportdriverunload)
-   [MiniportPause](#miniportpause)
-   [MiniportRestart](#miniportrestart)
-   [MiniportResetEx](#miniportresetex)
-   [MiniportDevicePnPEventNotify](#miniportdevicepnpeventnotify)
-   [MiniportShutdownEx](#miniportshutdownex)
-   [MiniportOidRequest](#miniportoidrequest)
-   [MiniportCancelOidRequest](#miniportcanceloidrequest)
-   [NdisMIndicateStatusEx](#ndismindicatestatusex)
-   [MiniportDirectOidRequest](#miniportdirectoidrequest)
-   [MiniportCancelDirectOidRequest](#miniportcanceldirectoidrequest)
-   [MiniportSendNetBufferLists](#miniportsendnetbufferlists)
-   [MiniportCancelSend](#miniportcancelsend)
-   [MiniportReturnNetBufferLists](#miniportreturnnetbufferlists)
-   [WDI ハンドラー:MiniportWdiOpenAdapter](#wdi-handler-miniportwdiopenadapter)
-   [WDI ハンドラー:MiniportWdiCloseAdapter](#wdi-handler-miniportwdicloseadapter)

## <a name="driver-installation"></a>ドライバーのインストール


WDI IHV ミニポート ドライバーが読み込まれ、システムにインストールされている方法を変更することはありません。 INF とインストール プロセスは、IHV ネイティブ WLAN のミニポート ドライバーに似ています。 既存の NDIS ドライバーなど、IHV ドライバーは IHV の WLAN のアダプターを使用するロードする必要がある場合、オペレーティング システムは、IHV ミニポート ドライバーの DriverEntry ルーチンを呼び出します。

## <a name="driverentry"></a>DriverEntry


オペレーティング システムは、直接、WDI IHV ミニポート ドライバーの DriverEntry ルーチンを呼び出します。 IHV ミニポートでは、ほとんどの通常の NDIS ミニポート DriverEntry ルーチンのガイドラインに従います。 1 つの例外は呼び出し元ではなく[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)、IHV ミニポート呼び出し[ **NdisMRegisterWdiMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/mt297596) Microsoft WLAN のコンポーネントを有効にするオペレーティング システムに通知します。

次に、キー パラメーターの[ **NdisMRegisterWdiMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/mt297596)します。

-   [**NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958):これは、NDIS を登録するネイティブ Wi-fi ミニポートを使用して、元の NDIS 構造体です。 WDI モデルでは、ほとんどのハンドラーのパラメーターは省略可能です。 唯一必要なハンドラーは**ミニポート\_OID\_要求\_ハンドラー**と**ミニポート\_ドライバー\_アンロード**します。 **ミニポート\_OID\_要求\_ハンドラー** IHV ドライバーに WDI メッセージを渡すために使用します。 その他の任意のハンドラーが指定されている場合、Microsoft の WLAN コンポーネント一般にハンドラーを呼び出します行われた後に独自のハンドラーの処理します。
-   [**NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://msdn.microsoft.com/library/windows/hardware/mt297617):これは、WDI ミニポート ドライバーを実装する必要があるハンドラーの新しいセットです。 コントロールのパスに対して追加のハンドラーを登録する IHV ドライバーによって使用され、データ パスのハンドラーの完全なセットします。

Microsoft の WLAN コンポーネント更新のハンドラーで IHV ミニポート NdisMRegisterWdiMiniportDriver を呼び出すと[ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958) NDIS の呼び出しと[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)します。 Microsoft の WLAN のコンポーネントが WDI IHV ミニポート ドライバーに単純化のサポートを提供できるハンドラーをインターセプトできるように、更新プログラムが実行されます。

WDI IHV ミニポート ドライバーの DriverEntry プロセスの一般的なフローを次に示します

![wdi driverentry フロー](images/wdi-driverentry-flow.png)

DriverEntry の詳細については、次を参照してください。 [ **NDIS ミニポート ドライバーの DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff548818)します。

## <a name="miniportsetoptions"></a>MiniportSetOptions


図のように、上記 DriverEntry、WDI IHV ミニポートが登録されている場合、 [ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)ハンドラー、オペレーティング システムが、ミニポート ドライバーのコンテキストでその関数を呼び出す呼び出す[ **NdisMRegisterWdiMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/mt297596)します。

IHV ミニポート ドライバーを使用して、オプションのハンドラーを登録するかどうか[ **NdisSetOptionalHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff564550)、これらのハンドラーしない Microsoft コンポーネントによって、WDI 層を介してシリアル化するに場合があります。 そのため、IHV コンポーネントは、これらのハンドラーの同期要件を処理する責任を負います。

## <a name="miniportinitializeex"></a>MiniportInitializeEx


WDI モデルを分割、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)インターフェイスの呼び出しを複数 WDI に動作します。

1.  呼び出す[ *MiniportWdiAllocateAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297559)します。

    オペレーティング システムには、IHV ハードウェアのインスタンスが検出されると、これは、WDI IHV ミニポート ドライバーには、最初の呼び出しになります。 この呼び出しで、WDI ミニポートは、ソフトウェアの表現を作成するために必要な操作を実行します (**MiniportAdapterContext**) のデバイス。 埋めるために、デバイスに関する情報も決定、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体。 Microsoft コンポーネントを特定の初期化を実行する WDI コマンドを送信するときに、後で、デバイスと Wi-fi スタックの実際の初期化が行われます。

    Microsoft コンポーネントを呼び出し、WDI IHV ミニポート ドライバーから取得したデータを使用して、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)設定と、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934) NDIS にします。 ほとんどのフィールドの**NDIS\_ミニポート\_アダプター\_登録\_属性**Microsoft コンポーネントによって既定値が格納されます。 IHV ドライバーを設定する必要があります、 **MiniportAdapterContext**と**InterfaceType**フィールド。

    使用して、WDI コマンドの受信を開始、IHV ミニポート ドライバーからこの呼び出しが返されると、その[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)ハンドラー。 この呼び出し中に、Microsoft コンポーネントは可能性がありますので、ここで実行される任意のアクティビティが迅速かつ信頼性の高いになるはずのリセット/復旧操作を実行できません。

2.  呼び出す[ *MiniportWdiOpenAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297564)します。

    後[ *MiniportWdiAllocateAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297559)、Microsoft のコンポーネントの呼び出し[ *MiniportWdiOpenAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297564)ファームウェアを読み込むとハードウェアを初期化します。

3.  使用して複数の WDI コマンド[ *MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)します。

    後[ *MiniportWdiOpenAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297564)、Microsoft コンポーネント IHV ミニポートに以下のタスク/プロパティ/呼び出しを送信します。

    1.  呼び出す[ *MiniportWdiTalTxRxInitialize* ](https://msdn.microsoft.com/library/windows/hardware/mt297580)データ パスを初期化し、ハンドラーを交換します。
    2.  呼び出す[OID\_WDI\_取得\_アダプター\_機能](https://msdn.microsoft.com/library/windows/hardware/dn925838)アダプターの機能を取得します。
    3.  呼び出す[OID\_WDI\_設定\_アダプター\_構成](https://msdn.microsoft.com/library/windows/hardware/dn925853)にアダプターを構成します。
    4.  呼び出す[OID\_WDI\_タスク\_設定\_ラジオ\_状態](https://msdn.microsoft.com/library/windows/hardware/dn925963)になっていない予期された状態でラジオを初期状態を設定します。
    5.  呼び出す[ *MiniportWdiTalTxRxStart* ](https://msdn.microsoft.com/library/windows/hardware/mt297585)データ パスを設定します。
    6.  呼び出す[OID\_WDI\_タスク\_作成\_ポート](https://msdn.microsoft.com/library/windows/hardware/dn925949)初期のポートを作成します。

    その他のコマンドを Microsoft コンポーネントの MiniportInitializeEx 処理の一環として、IHV コンポーネントに送信も可能性があります。 ただし、まで[ *MiniportWdiStartOperation* ](https://msdn.microsoft.com/library/windows/hardware/mt297575)を呼び出すと、無線通信を必要がある Microsoft コンポーネントをすべてのタスクを送信しません。 除く[OID\_WDI\_タスク\_オープン](https://msdn.microsoft.com/library/windows/hardware/dn925954)常に送信される最初に、他のコマンド/呼び出しの順序が変わる可能性があります。

    Microsoft コンポーネントを呼び出し、WDI IHV ミニポート ドライバーから取得したデータを使用して、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)設定と[ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)と[ **NDIS\_ミニポート\_アダプター\_ネイティブ\_802\_11\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565926) NDIS にします。

4.  呼び出す[ *MiniportWdiStartOperation*](https://msdn.microsoft.com/library/windows/hardware/mt297575)します。

    これは、省略可能な WDI ミニポート ハンドラー内で[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://msdn.microsoft.com/library/windows/hardware/mt297617) IHV ドライバーを使用しています。その他の MiniportInitializeEx タスクを実行します。 これは、こともできます IHV ミニポートによって Microsoft コンポーネントのミニポートとミニポートの初期化が完了したことのヒントが必要なバック グラウンドのすべてのアクティビティを開始します。

    次の図は、MiniportInitializeEx の流れを示しています。

    ![wdi ミニポート初期化フロー](images/wdi-miniport-initialization-flow.png)

    中間の操作が失敗した場合は、Microsoft コンポーネントには、以前の操作とミニポートの起動が失敗した元に戻します。 たとえば場合、 [OID\_WDI\_タスク\_作成\_ポート](https://msdn.microsoft.com/library/windows/hardware/dn925949)失敗した場合、データ パスは、クリーンアップ、 [OID\_WDI\_タスク\_閉じる](https://msdn.microsoft.com/library/windows/hardware/dn925947)が送信され、ミニポートが失敗したとします。

## <a name="miniporthaltex"></a>MiniportHaltEx


ネイティブ Wi-fi ミニポート[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)操作を停止し、アダプターのインスタンスをクリーンアップするミニポートを指示するために使用します。 Microsoft コンポーネントの元の処理、WDI モデルで*MiniportHaltEx*を呼び出すし、WDI インターフェイスの複数の呼び出しに分割されます。

1.  呼び出す[ *MiniportWdiStopOperation*](https://msdn.microsoft.com/library/windows/hardware/mt297576)します。

    これは、省略可能な WDI ミニポート ハンドラー内で[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://msdn.microsoft.com/library/windows/hardware/mt297617)を元に戻す、IHV ドライバーが使用できます。実行された操作[ *MiniportWdiStartOperation*](https://msdn.microsoft.com/library/windows/hardware/mt297575)します。

2.  複数 WDI コマンドを使用して[ *MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)します。

    後[ *MiniportWdiStopOperation*](https://msdn.microsoft.com/library/windows/hardware/mt297576)、Microsoft コンポーネント/タスクのプロパティを IHV ドライバーの現在の状態をクリーンアップする IHV ミニポートに送信します。 このクリーンアップは、次に含めることができます。

    1.  呼び出す[OID\_WDI\_タスク\_切断](https://msdn.microsoft.com/library/windows/hardware/dn925951)/[OID\_WDI\_タスク\_停止\_AP](https://msdn.microsoft.com/library/windows/hardware/dn925965)の既存の接続を破棄します。
    2.  呼び出す[OID\_WDI\_タスク\_削除\_ポート](https://msdn.microsoft.com/library/windows/hardware/dn925950)ポートの削除をすべて作成します。
    3.  呼び出す[ *MiniportWdiTalTxRxStop* ](https://msdn.microsoft.com/library/windows/hardware/mt297586)データ パスを停止します。
    4.  呼び出す[ *MiniportWdiTalTxRxDeinitialize* ](https://msdn.microsoft.com/library/windows/hardware/mt297578) deinitialize データ パスにします。
    5.  ハードウェアの状態をクリーンアップする呼び出しです。 これは、送信、IHV を使用して、 [ *MiniportWdiCloseAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297561) IHV ドライバーに登録されています。

3.  Microsoft コンポーネントを呼び出すすべての上記のコマンドが呼び出されると、 [ *MiniportWdiFreeAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297562) IHV ドライバーがする可能性があります、ソフトウェアの状態を削除します。

次の図は、MiniportHaltEx の流れを示しています。

![wdi ミニポート halt フロー](images/wdi-miniport-halt-flow.png)

デバイスが突然削除されたか、システムの電源がオフされるかどうかがある場合は、MiniportHaltEx 処理は実行されません。 突然削除するを参照してください、 [MiniportDevicePnPEventNotify](#miniportdevicepnpeventnotify)ハンドラーの動作。 システムのシャット ダウンを参照してください、 [MiniportShutdownEx](#miniportshutdownex)ハンドラーの動作。

## <a name="miniportdriverunload"></a>MiniportDriverUnload


[*MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378) WDI IHV ミニポートが読み込まれる前に呼び出されるハンドラーします。 WDI IHV ミニポート ドライバーでは、Microsoft 自体の登録を解除するコンポーネントを呼び出します。 Microsoft コンポーネントの呼び出し[ **NdisMDeregisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563578)します。

次の図は、MiniportDriverUnload の流れを示しています。

![wdi ミニポート ドライバー アンロード フロー](images/wdi-miniport-driver-unload-flow.png)

## <a name="miniportpause"></a>MiniportPause


NDIS [ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)要件は、Microsoft コンポーネントによって処理されます。 MiniportPause の一環としては、Microsoft コンポーネントは、データ パスを停止し、クリーンアップするまで待機します。 WDI IHV ミニポートに登録できます必要に応じて、 [ *MiniportWdiPostAdapterPause* ](https://msdn.microsoft.com/library/windows/hardware/mt297565)データ パスのクリーンアップが完了した後に、Microsoft コンポーネントによって呼び出されるコールバック。

次の図は、MiniportPause の流れを示しています。

![wdi ミニポート フローの一時停止](images/wdi-miniport-pause-flow.png)

## <a name="miniportrestart"></a>MiniportRestart


NDIS [ *MiniportRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff559435)要件は、Microsoft コンポーネントによって処理されます。 MiniportRestart の一環として、Microsoft コンポーネント MiniportPause の一部として実行されたデータ パスの一時停止作業を元に戻します。 WDI IHV ミニポートに登録できます必要に応じて、 [ *MiniportWdiPostAdapterRestart* ](https://msdn.microsoft.com/library/windows/hardware/mt297566)データ パスの再起動が完了した後に、Microsoft コンポーネントによって呼び出されるコールバック。

次の図は、MiniportRestart の流れを示しています。

![フローが再起動 wdi ミニポート](images/wdi-miniport-restart-flow.png)

## <a name="miniportresetex"></a>MiniportResetEx


[*MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432) Microsoft コンポーネントによって処理されません。 WDI IHV ミニポートに登録できます必要に応じて、 *MiniportResetEx* Microsoft コンポーネントによって呼び出されるコールバック。

## <a name="miniportdevicepnpeventnotify"></a>MiniportDevicePnPEventNotify


[*MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369) PNP イベント デバイスの突然の削除などの NDIS ドライバーに通知するために使用します。 NDIS は、この通知を送信するときに最初に処理 WDI IHV ミニポートに転送されます。 IHV コンポーネントは、処理が終了したら、Microsoft のコンポーネントは、このイベントの適切な処理を実行します。 IHV コンポーネントに転送される呼び出しは他のタスクのコールバックとシリアル化されません。

次の図は、MiniportDevicePnPEventNotify の流れを示しています。

![wdi ミニポート ドライブ pnp 通知フロー](images/wdi-miniport-device-pnp-notification-flow.png)

## <a name="miniportshutdownex"></a>MiniportShutdownEx


[*MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)システム シャット ダウン イベントの NDIS ドライバーに通知するために使用します。 NDIS は、この通知を送信するときに最初に Microsoft コンポーネントによって処理されます。 Microsoft コンポーネントでは、処理が完了すると、WDI IHV ミニポート処理のためにイベントを渡します。

次の図は、MiniportShutdownEx の流れを示しています。

![wdi ミニポート シャット ダウンのフロー](images/wdi-miniport-shutdown-flow.png)

## <a name="miniportoidrequest"></a>MiniportOidRequest


[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)ハンドラーが、必要なハンドラー WDI IHV ミニポートを実装する必要があります。 IHV ミニポートに WDI コマンドを送信する Microsoft コンポーネントによって使用されます。 Microsoft コンポーネントが IHV ミニポートに処理しない Oid を転送するようにも使用されます。

[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416) WDI コマンドのメッセージ M1 見なさ WDI IHV ミニポートに呼び出す必要があります。 OID が完成したら、(いずれかによって[ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)または非保留中からの戻り値を使用して*MiniportOidRequest*) M3 のメッセージとして考慮する必要があります、WDI タスク/コマンド。

すべて WDI コマンドがある 2 つの潜在的なフィールドが、NDIS\_操作--からのステータス コードが返されるステータス コード、 [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)呼び出し (または[ **NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)) と状態コード、 [ **WDI\_メッセージ\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/dn926074)フィールド (OID が完成したら、またはを使用して[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600))。 NDIS で常に次の Microsoft コンポーネント\_見て前に OID 完了から状態、 **WDI\_メッセージ\_HEADERStatus**フィールド。 処理 WDI OID の IHV コンポーネントへの期待は、次のとおりです。

1.  WDI Oid が IHV コンポーネントを使用して送信された、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)**RequestType**の**NdisRequestMethod**、および対応するメッセージとメッセージの長さで、**データ。メソッド\_INFORMATION.InformationBuffer**と**データ。メソッド\_情報。InputBufferLength**それぞれフィールドします。
2.  IHV コンポーネントは、コマンドの処理中にエラーがある場合は、OID が完了するまでエラーが報告されの [状態] フィールドを設定、 [ **WDI\_メッセージ\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/dn926074)に非-成功 Wi-fi レベルの障害がある場合。
3.  タスクとプロパティは、要求のポート番号はでは、 [ **WDI\_メッセージ\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/dn926074)**PortId**フィールド。 **PortNumber**で、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)は常に 0 に設定します。
4.  OID が完了したが、許容、 [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)を返す NDIS\_状態\_PENDING OID を後で完了し、(同期または非同期)[ **NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)します。
5.  IHV コンポーネント NDIS に OID が完了すると\_状態\_成功するを設定する必要がありますが、 **BytesWritten**適切な数の空白を含むバイトの OID は要求のフィールド、 [**WDI\_メッセージ\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/dn926074)します。
6.  かどうか、IHV コンポーネントが十分な領域、**データ。メソッド\_情報。OutputBufferLength** 、応答を入力するフィールド NDIS に OID が完了すると\_状態\_バッファー\_すぎます\_短いし、設定、**データ。メソッド\_情報。BytesNeeded**フィールド。 Microsoft コンポーネントは可能性があります、要求されたサイズのバッファーを割り当てるし、IHV に新しい要求の送信を試みます。
7.  タスクに M4 の場合、タスクは、([**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)) かどうか、タスクとして報告された - 正常に開始 OID 入力候補が正常に完了する必要があります指定のみと**の状態**で、 [ **WDI\_メッセージ\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/dn926074) OID で完了が成功します。

次の図は、1 つの WDI コマンドにマップする NDIS OID 要求の例を示します。 オペレーティング システムによって OID 要求が送信されると、Microsoft コンポーネントが WDI OID 要求に変換し、IHV ミニポートに WDI OID 要求を送信します。 IHV ミニポート OID が完了すると、Microsoft コンポーネントは、元の OID 要求を適切に完了します。

![wdi miniport oid request sequence for single wdi command](images/wdi-miniport-oid-request-single.png)

複数 WDI OidRequests、OriginalOidRequest にマップし、WDI 要求の 1 つが失敗した場合、OriginalOidRequest も失敗します。 中間操作のサブセットが既に完了している場合、Microsoft コンポーネントは、サポートのクリーンアップ操作を元に戻すしようとします。

次の図は、Microsoft コンポーネントによって完了、NDIS OID 要求処理の例を示します。 ときに OID 要求は、オペレーティング システムで Microsoft コンポーネント プロセスが送信され、OID が完了します。 この OID が WDI IHV ミニポートに渡されません。

![microsoft コンポーネントによって処理される oid の wdi ミニポート oid 要求シーケンス](images/wdi-miniport-oid-request-wdi-handled.png)

Microsoft コンポーネントによって認識されない Oid は、処理の IHV コンポーネントに直接転送されます。

![microsoft コンポーネントによって処理されない oid の wdi ミニポート oid 要求シーケンス](images/wdi-miniport-oid-request-unknown.png)

MiniportOidRequest の動作では、(ネイティブ Wi-fi ミニポート) と比較して WDI IHV ミニポート ドライバーに変更されません。 呼び出しはシリアル化され、IHV ミニポートできますが完了するか、同期または非同期の呼び出しで[ **NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)します。

## <a name="miniportcanceloidrequest"></a>MiniportCancelOidRequest


これは、WDI メッセージにマップされていない Oid を処理する必要がある WDI IHV ミニポートによって使用される、省略可能なハンドラーです。 このハンドラーは、WDI Oid には使用されません。 WDI Oid がすぐに完了する必要があり、保留中の OID をキャンセルしようとする IHV ミニポート ドライバーの必要はありません。 WDI タスクのキャンセルは、適切な取り消しタスク OID 要求を使用して処理されます。 マップされていない Oid は、想定される動作は、NDIS によって定義されます。

## <a name="ndismindicatestatusex"></a>NdisMIndicateStatusEx


[**NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600) WDI IHV ミニポートによって Microsoft コンポーネントに指示を送信するために使用します。 指標は、一方的な兆候 TKIP MIC の障害などがあります。 またはタスクの完了 (M4) の指示を要請します。

次の図を対応する NDIS/ネイティブ Wi-fi を示す値を持つ WDI indication の例を示します。 Microsoft コンポーネントを IHV ミニポートによって指示が送信されると、Microsoft のコンポーネントは既存を示す値に変換し、オペレーティング システムに転送します。

![wdi ミニポートの状態を示す値のフロー](images/wdi-miniport-status-indication-flow.png)

次の図は、対応する NDIS/ネイティブ Wi-fi を示す値を持たない WDI indication の例を示します。 これは、Microsoft コンポーネントによって処理されます。

![ndis へ直接マッピングすることがなく wdi 状態の表示](images/wdi-miniport-status-indication-not-ndis.png)

次の図は、Microsoft コンポーネントによって認識されないものを示す値を示します。 として示す値が転送されるは、オペレーティング システムを。

![microsoft コンポーネントによって認識されない wdi 状態の表示](images/wdi-miniport-status-indication-unknown.png)

NdisMIndicateStatusEx の動作では、(ネイティブ Wi-fi ミニポート) と比較して WDI IHV ミニポート ドライバーに変更されません。

## <a name="miniportdirectoidrequest"></a>MiniportDirectOidRequest


これは、WDI メッセージにマップされていない直接の Oid を処理する必要がある場合、WDI IHV ミニポート ドライバーによって登録されているオプションのハンドラーです。 Wi-Fi Direct のすべての既存の直接 Oid は、このハンドラーは、その機能をサポートする必要はありませんので、WDI メッセージにマップされます。 サポートされていない直接 Oid は Microsoft コンポーネントによってシリアル化されません。

## <a name="miniportcanceldirectoidrequest"></a>MiniportCancelDirectOidRequest


これは、WDI メッセージにマップされていない直接の Oid を処理する必要がある WDI IHV ミニポートによって使用される、省略可能なハンドラーです。 マップされていない Oid は、想定される動作は、NDIS によって定義されます。

## <a name="miniportsendnetbufferlists"></a>MiniportSendNetBufferLists


このハンドラーは、WDI IHV ミニポート ドライバーでは使用されませんし、指定されていない必要があります。 Microsoft コンポーネントを介して登録されたデータ パスのハンドラーを使用して[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://msdn.microsoft.com/library/windows/hardware/mt297617)にIHV ミニポートへの送信パケットを送信します。

## <a name="miniportcancelsend"></a>MiniportCancelSend


このハンドラーは、WDI IHV ミニポート ドライバーでは使用されませんし、指定されていない必要があります。

## <a name="miniportreturnnetbufferlists"></a>MiniportReturnNetBufferLists


このハンドラーは、WDI IHV ミニポート ドライバーでは使用されませんし、指定されていない必要があります。 Microsoft コンポーネントを介して登録されたデータ パスのハンドラーを使用して[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://msdn.microsoft.com/library/windows/hardware/mt297617)にIHV ミニポートに受信したパケットを返します。

## <a name="wdi-handler-miniportwdiopenadapter"></a>WDI ハンドラー:MiniportWdiOpenAdapter


[ *MiniportWdiOpenAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297564)ハンドラーは IHV ドライバーで開いているタスクの操作を開始する Microsoft コンポーネントによって使用されます。 この呼び出しはすぐに完了する必要があり、オープン操作が正常に開始された場合、IHV が NDIS を返す必要があります\_状態\_この呼び出しと呼び出しの成功、 [ **OpenAdapterComplete** ](https://msdn.microsoft.com/library/windows/hardware/mt297602)ハンドラーに渡される、 [ **NDIS\_WDI\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/mt297621)パラメーターの[ *MiniportWdiAllocateAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297559)します。

## <a name="wdi-handler-miniportwdicloseadapter"></a>WDI ハンドラー:MiniportWdiCloseAdapter


[ *MiniportWdiCloseAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297561)ハンドラーは IHV ドライバーでタスクを閉じる操作を開始する Microsoft コンポーネントによって使用されます。 この呼び出しはすぐに完了する必要があり、オープン操作が正常に開始された場合、IHV が NDIS を返す必要があります\_状態\_この呼び出しと呼び出しの成功、 [ **CloseAdapterComplete** ](https://msdn.microsoft.com/library/windows/hardware/mt297598)ハンドラーに渡される、 [ **NDIS\_WDI\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/mt297621)のパラメーター、 [ *MiniportWdiAllocateAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297559)します。

 

 





