---
title: 移植の NDIS ミニポート ドライバー NetAdapterCx に
description: 移植の NDIS ミニポート ドライバー NetAdapterCx に
ms.assetid: F5C798C6-B746-43CB-BF63-DBA7DD0975ED
keywords:
- ミニポート ドライバーにネットワーク アダプター WDF クラスの拡張機能への移植、NDIS の移植のネットワーク アダプター クラス拡張を移植する NetAdapterCx 6.x
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: d404e1dcdf1d4b26b01873c00c1d997fcec7a701
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552263"
---
# <a name="porting-ndis-miniport-drivers-to-netadaptercx"></a>移植の NDIS ミニポート ドライバー NetAdapterCx に

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

このページには、NDIS 6.x ミニポート ドライバーを NetAdapterCx クライアント ドライバーに変換する方法について説明します。

WDF の詳細についてを参照してください、 [WDF ドライバー開発ガイド](../wdf/index.md)します。

## <a name="compilation-settings"></a>コンパイルの設定

Visual Studio で NDIS ミニポート ドライバーの既存のプロジェクトを開き、KMDF プロジェクトに変換する、次の手順を使用します。

1. まずに移動します**構成プロパティには、ドライバーが]-> [設定]、[ドライバー モデル**ことを確認します**ドライバーの種類**KMDF とに設定されている**KMDF のメジャー バージョン**と**KMDF マイナー バージョン**はどちらも空です。
2. プロジェクトのプロパティ で開きます**ドライバーの設定には、ネットワーク アダプター ドライバーが-> **設定と**ネットワーク アダプター クラスの拡張機能へのリンク**に**はい**。
   * 変換には、ドライバーでは、NDIS Api を呼び出すは引き続き場合、へのリンクを引き続き`ndis.lib`します。
3. NDIS プリプロセッサのマクロのような削除`NDIS650_MINIPORT=1`します。
4. すべてのソース ファイル (または、一般的な/プリコンパイル済みヘッダー) は、次のヘッダーを追加します。
  
   ```C++
   #include <ntddk.h>
   #include <wdf.h>
   #include <netadaptercx.h>
   ```
  
5. 追加[標準 WDF 装飾](../wdf/specifying-wdf-directives-in-inf-files.md)INF に。
  
   ```INF
   [Yourdriver.Wdf]
   KmdfService = Yourdriverservice, Yourdriver.wdfsect

   [Yourdriver.wdfsect]
   KmdfLibraryVersion = <insert here>
   ```
6. INF の NT セクションに必要なネットワークの新しいキーワードを追加します。

   - **\*IfConnectorPresent**
   - **\*ConnectionType**
   - **\*DirectionType**
   - **\*AccessType**
   - **\*HardwareLoopback**

     詳細については、これらのキーワードと例については、次を参照してください。 [NetAdapterCx クライアント ドライバーの INF ファイル](inf-files-for-netadaptercx-client-drivers.md)します。

## <a name="driver-initialization"></a>ドライバーの初期化

呼び出しを削除[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)から[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff540807)以下を追加します。

```C++
WDF_DRIVER_CONFIG_INIT(&config, EvtDriverDeviceAdd);
status = WdfDriverCreate(. . . );
if (!NT_SUCCESS(status)) {
  return status;
}
```

設定されている場合は、削除、 **WdfDriverInitNoDispatchOverride**への呼び出しからフラグ[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)します。

*DriverUnload* WDF のネットワーク クライアントのドライバーのオプションのルーチンは、必要に応じて削除できるようにします。 呼び出さない[ **NdisMDeregisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563578)から*DriverUnload*します。

## <a name="device-initialization"></a>デバイスの初期化

次に、コードからの配布*MiniportInitializeEx*に適切な WDF イベントのコールバック ハンドラーをいくつかの省略可能です。 コールバック シーケンスの詳細については、「 [WDF クライアントのネットワーク アダプター ドライバーの電源投入シーケンス](power-up-sequence-for-a-netadaptercx-client-driver.md)します。

同じメソッドを呼び出すことが[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672) 、ネット アダプターを開始しているが、前に呼び出すときに[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart). ジェネリック型の 1 つのルーチンを呼び出す代わりに、ただし、 [ **NDIS_MINIPORT_ADAPTER_ATTRIBUTES** ](https://msdn.microsoft.com/library/windows/hardware/ff565920)構造体、クライアント ドライバーは、さまざまな種類の機能を設定する別の関数を呼び出します。

コールバックを提供する必要があり、ネット アダプターを開始する方法については、次を参照してください。[デバイスとアダプターの初期化](device-and-adapter-initialization.md)します。

## <a name="creating-queues-to-manage-control-requests"></a>コントロールの要求を管理するキューの作成

次に、引き続き内[ *EVT_WDF_DRIVER_DEVICE_ADD*](https://msdn.microsoft.com/library/windows/hardware/ff541693)、オブジェクト識別子 (OID) のパスを設定します。 OID のパスは、WDF キューのようにモデル化されますが、WDFREQUESTs ではなく Oid を取得します。

これを移植するとき、2 つの高レベル方法はあります。 最初のオプションでは、登録、 [ *EVT_NET_REQUEST_DEFAULT* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default) NDIS からミニポート ドライバーが要求を受信する方法に非常に同様の方法で要求を OID を受け取るハンドラー。 これは、おそらくだけ必要になるため、古い MINIPORT_OID_REQUEST ハンドラーから関数のシグネチャを調整する最も簡単なポートです。

その他のオプションでは、OID ハンドラーの switch ステートメントを分割し、個々 の OID ごとの個別のハンドラーを提供します。 デバイス OID 固有の機能が必要な場合は、このオプションを選択する可能性があります。

使用した場合、 [ **Direct OID 要求インターフェイスで NDIS 6.1**](../network/direct-oid-request-interface-in-ndis-6-1.md)、WDF キューを並列に置き換えます。 同様に、NDIS で正規の (シリアル) 要求インターフェイスは、シーケンシャル WDF キューになります。

Oid のハンドラーを登録する方法の詳細については、次を参照してください。[処理に対する制御要求](handling-control-requests.md)します。

## <a name="reading-configuration-from-the-registry"></a>レジストリから構成の読み取り

次への呼び出しを置き換える[ **NdisOpenConfigurationEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563717)および関連する関数で、`NetConfiguration*`メソッド。 `NetConfiguration*`メソッドと似ています、`Ndis*Configuration*`関数、およびするが、コードを再構築する必要はありません。

詳細については、次を参照してください。[構成情報にアクセスする](accessing-configuration-information.md)します。

## <a name="receiving-io-control-codes-iotcls-from-user-mode"></a>ユーザー モードから受信側の I/O 制御コード (IOTCLs)

NDIS ドライバーを呼び出す場合は、このセクションを読む[ **NdisRegisterDeviceEx**](https://msdn.microsoft.com/library/windows/hardware/ff564518)ルーチンがユーザー モードから Ioctl を受信するには、(CDO) 制御デバイス オブジェクトを作成するために使用します。

これは、WDF ネットワーク クライアント ドライバーで 2 つの方法を示します。

呼び出すことによって、制御デバイス オブジェクトを作成する最も簡単なポートは、 [ **WdfControlDeviceInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff545841)からクライアントの[ *EVT_WDF_DRIVER_DEVICE_ADD*](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック。 詳細については、次を参照してください。[コントロール デバイス オブジェクトを使用する](../wdf/using-control-device-objects.md)します。

ただし、推奨されるソリューションは、デバイスのインターフェイスを作成する」の説明に従って[を使用してデバイスのインターフェイス](using-device-interfaces.md)します。

## <a name="finishing-device-initialization"></a>デバイスの初期化を終了

この時点で[ *EVT_WDF_DRIVER_DEVICE_ADD*](https://msdn.microsoft.com/library/windows/hardware/ff541693)、その他の割り込みの割り当てのようなデバイスを初期化するには行うことができます。

## <a name="handling-power-state-change-notifications"></a>電源状態の変更通知の処理

WDF のクライアント ドライバーは受信しません[ **OID_PNP_SET_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff569780)の電力状態を変更します。

代わりに、WDF クライアントは、電源の状態変更通知を受信する省略可能なコールバック関数を登録します。 概要については、次を参照してください。 [PnP をサポートしていると関数のドライバーでの電源管理](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)します。

通常、コードで、 [ **OID_PNP_SET_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff569780)ハンドラーに移動[ *EVT_WDF_DEVICE_D0_EXIT* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)と[ *EVT_WDF_DEVICE_D0_ENTRY*](https://msdn.microsoft.com/library/windows/hardware/ff540848)します。

WDF の電源のステート マシンは若干異なるためは、コードに小さな変更を加える必要があります。

具体的には、その[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389) one-time initialization タスクと作業を D0 状態、デバイスにコールバック関数では、NDIS ミニポート ドライバーを実行します。 D0 に移動する作業が繰り返されますし、その[ *OID_PNP_SET_POWER* ](https://msdn.microsoft.com/library/windows/hardware/ff569780)ハンドラー。

WDF クライアントが前に、イベントのコールバックで one-time initialization タスクを実行する一方、 [ **EVT_WDF_DEVICE_D0_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/ff540848)、中、低電力状態では、デバイスにします。 D0 に移動するのには、 [ **EVT_WDF_DEVICE_D0_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/ff540848)します。

まとめると、WDF には、2 つではなく、1 つの場所で、"go to D0"のコードを配置します。

コールバック シーケンスの詳細については、「 [NetAdapterCx クライアント ドライバーの電源投入シーケンス](power-up-sequence-for-a-netadaptercx-client-driver.md)します。

## <a name="querying-and-setting-power-management-capabilities"></a>クエリを実行して、電源管理機能の設定

同様に、WDF のクライアント ドライバーは受信しません[ **OID_PM_PARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff569768)クエリまたは電源管理を設定するには、ネットワーク アダプターのハードウェア機能。

代わりに、ドライバーは、NETPOWERSETTINGS オブジェクトから、必要な wake on LAN (WoL) 構成を照会します。 詳細については、次を参照してください。[電源管理の構成](configuring-power-management.md)します。

返される実際のフラグは、ロジックに詳細な変更を加える必要はありませんので、6 の NDIS ミニポートの場合と同じセマンティクスを持ちます。 主な違いは、電源ダウン シーケンス中にこれらのフラグを照会できますようになりましたことです。 参照してください[NetAdapterCx クライアント ドライバーの電源切断シーケンス](power-down-sequence-for-a-netadaptercx-client-driver.md)します。

OID のハンドラーを削除するには、このコードの周りを移動した後[ *OID_PNP_SET_POWER* ](https://msdn.microsoft.com/library/windows/hardware/ff569780)と[ *OID_PM_PARAMETERS*](https://msdn.microsoft.com/library/windows/hardware/ff569768)します。

NetAdapter フレームワークは、ホスト、ネットワーク インターフェイスを使用しますが、D0 でデバイスを繰り返し、ためクライアント通常実装しません power ロジック。既定の NetAdapter 電源動作で十分です。

## <a name="data-path"></a>データ パス

データ パスのプログラミング モデルが大幅に変更します。 主な相違点を次に示します。

* モデルでは、NetAdapter、ネットワーク トラフィックは WDF キューごとではなくが、NDIS のように、アダプターごとに不要になったです。 参照してください[I/O キューを作成する](../wdf/creating-i-o-queues.md)します。
* NET_BUFFER_LIST と NET_BUFFER のプールではなく NetAdapterCx には、net パケットは、次のように NDIS にマップから構成されるリング バッファーが導入されています。
  * A [ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet) NET_BUFFER_LIST + NET_BUFFER に似ています。
  * A [ **NET_PACKET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)メモリ記述子のリスト (MDL) に似ています。 各[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)がこれらの 1 つ以上。
  * 置換構造とその使用方法の詳細については、次を参照してください。[パケット記述子と拡張機能](packet-descriptors-and-extensions.md)します。
* Ndis 6.x、ミニポートは開始の処理し、セマンティクスを一時停止する必要があります。 NetAdapterCx モデルで、これは不要になった場合です。
* [ *EVT_RXQUEUE_ADVANCE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nc-netrxqueue-evt_rxqueue_advance)コールバックはのような[ **MINIPORT_RETURN_NET_BUFFER_LISTS** ](https://msdn.microsoft.com/library/windows/hardware/ff559437) ndis 6.x します。
* [ *EVT_TXQUEUE_ADVANCE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nc-nettxqueue-evt_txqueue_advance)コールバックはのような[ **MINIPORT_SEND_NET_BUFFER_LISTS** ](https://msdn.microsoft.com/library/windows/hardware/ff559440) ndis 6.x します。

## <a name="device-removal"></a>デバイスの削除

WDF NIC ドライバーのデバイスの削除は、その他の WDF デバイス ドライバー、必要なネットワーク特定処理なしでの場合と同様です。 WDF デバイスで最初に、ネットワークのデータ パスがシャット ダウンの後にします。 WDF のシャット ダウンについては、次を参照してください。[ユーザーがデバイスから切り離し](../wdf/a-user-unplugs-a-device.md)します。

*MiniportHaltEx*ハンドラーがの間で配布される可能性があります[ *EVT_WDF_DEVICE_D0_EXIT* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)と[ *EVT_WDF_DEVICE_RELEASE_ハードウェア*](https://msdn.microsoft.com/library/windows/hardware/ff540890)します。

WDF のクライアントは、NetAdapter または作成した OID とデータパス キューのいずれかを削除する必要はありません。 WDF では、これらのオブジェクトが自動的に削除します。

削除することができます*MiniportShutdownEx*、 *MiniportResetEx*と*MiniportCheckForHangEx*します。 これらのコールバックがサポートされていません。

## <a name="ndis-wdf-function-equivalents"></a>対応する NDIS WDF 関数

ほとんど`NdisXxx`関数は、WDF と等価に置き換えることができます。 インポートされるほとんどの機能を必要があることを確認する必要があります一般に、`NDIS.SYS`します。

対応する関数の一覧は、次を参照してください。 [NDIS WDF 関数と等価な](ndis-wdf-function-equivalents.md)します。

等価の WDF なしに関数の場合、クライアントが呼び出すことができます[ **NetAdapterWdmGetNdisHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterwdmgetndishandle) NDIS 関数で使用するため、NDIS_HANDLE を取得します。 次に、例を示します。

```C++
NdisGetRssProcessorInformation(NetAdapterWdmGetNdisHandle(NetAdapter), . . .);
```

## <a name="debugging"></a>デバッグ

参照してください[NetAdapterCx クライアント ドライバーをデバッグ](debugging-a-netadaptercx-client-driver.md)します。

[! Ndiskd.netadapter](../debugger/-ndiskd-netadapter.md)デバッガー拡張機能には、もののような結果が表示されます。 **! ndiskd.miniport**の NDIS 6 ドライバを示しています。

## <a name="conclusion"></a>まとめ

このトピックの手順を使用して、開始と停止、デバイス、ドライバーが必要です。
