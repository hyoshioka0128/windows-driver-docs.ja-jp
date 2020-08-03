---
title: NDIS ミニポート ドライバーの NetAdapterCx への移植
description: NDIS ミニポート ドライバーの NetAdapterCx への移植
ms.assetid: F5C798C6-B746-43CB-BF63-DBA7DD0975ED
keywords:
- ミニポートドライバーをネットワークアダプタークラス拡張に移植し、ネットワークアダプターの WDF クラス拡張に移植し、NDIS 6.x を NetAdapterCx に移植する
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 53d09037d633a6003b9a5471a5f9ecb5350e017f
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473758"
---
# <a name="porting-ndis-miniport-drivers-to-netadaptercx"></a>NDIS ミニポート ドライバーの NetAdapterCx への移植

このページでは、NDIS 6.x ミニポートドライバーを NetAdapterCx クライアントドライバーに変換する方法について説明します。

WDF に関する一般情報については、 [WDF ドライバー開発ガイド](../wdf/index.md)を参照してください。

## <a name="compilation-settings"></a>コンパイル設定

Visual Studio で既存の NDIS ミニポートドライバープロジェクトを開き、次の手順を使用してそれを KMDF プロジェクトに変換します。

1. 最初に、[**構成プロパティ->ドライバーの設定->ドライバーモデル**] に移動し、**ドライバーの種類**が kmdf に設定されていること、および**kmdf バージョンのメジャー**と**kmdf バージョンのマイナー**が両方とも空であることを確認します。
2. [プロジェクトのプロパティ] で、[**ドライバーの設定->ネットワークアダプタードライバー** ] を開き、[**ネットワークアダプター] クラス拡張へのリンクを** **[はい]** に設定します。
   * 変換されたドライバーが引き続き NDIS Api を呼び出す場合は、へのリンクを続行 `ndis.lib` します。
3. などの NDIS プリプロセッサマクロを削除 `NDIS650_MINIPORT=1` します。
4. すべてのソースファイル (または、共通/プリコンパイル済みヘッダー) に次のヘッダーを追加します。
  
   ```C++
   #include <ntddk.h>
   #include <wdf.h>
   #include <netadaptercx.h>
   ```
  
5. [標準の WDF デコレーション](../wdf/specifying-wdf-directives-in-inf-files.md)を INF に追加します。
  
   ```INF
   [Yourdriver.Wdf]
   KmdfService = Yourdriverservice, Yourdriver.wdfsect

   [Yourdriver.wdfsect]
   KmdfLibraryVersion = <insert here>
   ```
6. 新しい必要なネットワークキーワードを INF の NT セクションに追加します。

   - **\*Ifコネクターが存在します**
   - **\*ConnectionType**
   - **\*Direction 型**
   - **\*AccessType**
   - **\*ハードウェアループバック**

     これらのキーワードと例の詳細については、「 [INF files For NetAdapterCx client drivers](inf-files-for-netadaptercx-client-drivers.md)」を参照してください。

## <a name="driver-initialization"></a>ドライバーの初期化

[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)から[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)への呼び出しを削除し、次を追加します。

```C++
WDF_DRIVER_CONFIG_INIT(&config, EvtDriverDeviceAdd);
status = WdfDriverCreate(. . . );
if (!NT_SUCCESS(status)) {
  return status;
}
```

設定されている場合は、 [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)への呼び出しから**WdfDriverInitNoDispatchOverride**フラグを削除します。

*Driverunload*は、WDF ネットワーククライアントドライバーのオプションのルーチンであるため、必要に応じて削除できます。 *Driverunload*から[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver)を呼び出さないでください。

## <a name="device-initialization"></a>デバイスの初期化

次に、 *MiniportInitializeEx*から適切な WDF イベントコールバックハンドラーにコードを配布します。そのうちのいくつかは省略可能です。 コールバックシーケンスの詳細については、「[ネットワークアダプターの WDF クライアントドライバーの電源シーケンス](power-up-sequence-for-a-netadaptercx-client-driver.md)」を参照してください。

Net アダプターを起動しているときに、 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す前に、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)と同等のメソッドを呼び出します。 ただし、ジェネリック[**NDIS_MINIPORT_ADAPTER_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)構造体を使用して1つのルーチンを呼び出すのではなく、クライアントドライバーは異なる関数を呼び出してさまざまな種類の機能を設定します。

提供する必要があるコールバックと、net アダプターを開始するタイミングの詳細については、「[デバイスとアダプターの初期化](device-and-adapter-initialization.md)」を参照してください。

## <a name="creating-queues-to-manage-control-requests"></a>制御要求を管理するためのキューの作成

次に、引き続き[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)で、オブジェクト識別子 (OID) のパスを設定します。 OID パスは WDF キューとしてモデル化されますが、WDFREQUESTs ではなく Oid を取得します。

これを移植する際には、2つの高レベルのアプローチを取ることができます。 最初のオプションは、ミニポートドライバーが NDIS からの要求を受信するのとよく似た方法で OID 要求を受信する[*EVT_NET_REQUEST_DEFAULT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default)ハンドラーを登録することです。 これは最も簡単なポートです。これは、古い MINIPORT_OID_REQUEST ハンドラーから関数シグネチャを調整するだけで済むためです。

もう1つのオプションは、OID ハンドラーの switch ステートメントを分割し、個々の OID に個別のハンドラーを提供することです。 デバイスで OID 固有の機能が必要な場合は、このオプションを選択できます。

[**NDIS 6.1 で直接 OID 要求インターフェイス**](../network/direct-oid-request-interface-in-ndis-6-1.md)を使用した場合は、parallel WDF queue で置き換えます。 同様に、NDIS の通常の (シリアル) 要求インターフェイスは順次 WDF キューになります。

Oid のハンドラーの登録の詳細については、「[制御要求の処理](handling-control-requests.md)」を参照してください。

## <a name="reading-configuration-from-the-registry"></a>レジストリから構成を読み取っています

次に、 [**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)および関連する関数への呼び出しをメソッドに置き換え `NetConfiguration*` ます。 `NetConfiguration*`メソッドは関数に似ているため、コードを再 `Ndis*Configuration*` 構築する必要はありません。

詳細については、「[構成情報へのアクセス](accessing-configuration-information.md)」を参照してください。

## <a name="receiving-io-control-codes-iotcls-from-user-mode"></a>ユーザーモードからの i/o 制御コード (IOTCLs) の受信

NDIS ドライバーが[**NdisRegisterDeviceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterdeviceex)を呼び出す場合は、このセクションをお読みください。これは、ユーザーモードから ioctl を受信するためのコントロールデバイスオブジェクト (CDO) を作成するために使用されるルーチンです。

WDF ネットワーククライアントドライバーでこれを行うには、次の2つの方法があります。

最も単純なポートは、クライアントの[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックから[**Wdfcontroldeviceinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)を呼び出して、コントロールデバイスオブジェクトを作成することです。 詳細については、「[コントロールデバイスオブジェクトの使用](../wdf/using-control-device-objects.md)」を参照してください。

ただし、「デバイスインターフェイスの[使用](../wdf/using-device-interfaces.md)」で説明されているように、デバイスインターフェイスを作成することをお勧めします。

## <a name="finishing-device-initialization"></a>デバイスの初期化の終了

[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)のこの時点で、割り込みの割り当てなど、デバイスを初期化する他の操作を行うことができます。

## <a name="handling-power-state-change-notifications"></a>電源状態の変更通知の処理

WDF クライアントドライバーは、電源状態の変更の[**OID_PNP_SET_POWER**](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)を受信しません。

代わりに、WDF クライアントは、オプションのコールバック関数を登録して、電源状態の変更通知を受信します。 概要については、「[関数ドライバーでの PnP と電源管理のサポート](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)」を参照してください。

通常、 [**OID_PNP_SET_POWER**](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)ハンドラーのコードは[*EVT_WDF_DEVICE_D0_EXIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)と[*EVT_WDF_DEVICE_D0_ENTRY*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)に移動します。

WDF の電源状態のマシンは少し異なります。そのため、コードに若干の変更を加える必要がある場合があります。

具体的には、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) callback 関数では、NDIS ミニポートドライバーは、1回だけの初期化タスクを実行し、デバイスを D0 状態にするための作業を行います。 次に、処理を繰り返して、 [*OID_PNP_SET_POWER*](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)ハンドラーで D0 にアクセスします。

これに対して、WDF クライアントは[**EVT_WDF_DEVICE_D0_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)する前にイベントコールバックで1回限りの初期化タスクを実行します。その間、デバイスは低電力状態になります。 次に、 [**EVT_WDF_DEVICE_D0_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)の D0 にアクセスします。

まとめると、WDF では、"D0 に移動" コードを2つではなく1つの場所に配置します。

コールバックシーケンスの詳細については、「 [NetAdapterCx クライアントドライバーの電源シーケンス](power-up-sequence-for-a-netadaptercx-client-driver.md)」を参照してください。

## <a name="querying-and-setting-power-management-capabilities"></a>クエリと電源管理機能の設定

同様に、WDF クライアントドライバーは、ネットワークアダプターの電源管理のハードウェア機能を照会または設定するための[**OID_PM_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)を受け取りません。

代わりに、ドライバーは NETPOWERSETTINGS オブジェクトから必要な wake on LAN (WoL) 構成を照会します。 詳細については、「[電源管理の構成](configuring-power-management.md)」を参照してください。

実際に返されるフラグは、NDIS 6 ミニポートの場合と同じセマンティクスを持っているため、ロジックに対して詳細な変更を行う必要はありません。 主な違いは、電源を入れたときにこれらのフラグをクエリできるようになったことです。 「 [NetAdapterCx client driver の電源ダウンシーケンス」を](power-down-sequence-for-a-netadaptercx-client-driver.md)参照してください。

このコードを移動したら、 [*OID_PNP_SET_POWER*](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)と[*OID_PM_PARAMETERS*](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)の OID ハンドラーを削除できます。

NetAdapter フレームワークは、ホストがネットワークインターフェイスを使用している間にデバイスを D0 に保持するので、クライアントは通常、電源ロジックを実装しません。既定の NetAdapter の電源動作で十分です。

## <a name="data-path"></a>データパス

データパスプログラミングモデルが大幅に変更されました。 主な相違点を次に示します。

* NetAdapter モデルでは、NDIS の場合と同様に、アダプターごとにネットワークトラフィックがなくなります。ただし、WDF キューではなくなります。 「 [I/o キューの作成](../wdf/creating-i-o-queues.md)」を参照してください。
* NetAdapterCx は NET_BUFFER_LIST と NET_BUFFER プールではなく、次のように NDIS にマップするネットパケットで構成されるリングバッファーを導入します。
  * [**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)は NET_BUFFER_LIST + NET_BUFFER に似ています。
  * [**NET_PACKET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet_fragment)は、メモリ記述子リスト (MDL) に似ています。 各[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)には、これらのうち1つ以上があります。
  * 置換構造とその使用方法の詳細については、「[パケット記述子と拡張機能](packet-descriptors-and-extensions.md)」を参照してください。
* NDIS 6.x では、ミニポートで開始と一時停止のセマンティクスを処理する必要があります。 NetAdapterCx モデルでは、そうではなくなりました。
* [*EVT_RXQUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nc-netrxqueue-evt_rxqueue_advance)のコールバックは、NDIS 6.x の[**MINIPORT_RETURN_NET_BUFFER_LISTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)に似ています。
* [*EVT_TXQUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nc-nettxqueue-evt_txqueue_advance)のコールバックは、NDIS 6.x の[**MINIPORT_SEND_NET_BUFFER_LISTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)に似ています。

## <a name="device-removal"></a>デバイスの削除

WDF NIC ドライバーのデバイスの削除は、他の WDF デバイスドライバーと同じですが、ネットワーク固有の処理は必要ありません。 最初にネットワークデータパスがシャットダウンされ、次に WDF デバイスが終了します。 WDF shutdown の詳細については、「[ユーザー Unplugs a デバイス](../wdf/a-user-unplugs-a-device.md)」を参照してください。

*ミニ Porthaltex*ハンドラーは、 [*EVT_WDF_DEVICE_D0_EXIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)と[*EVT_WDF_DEVICE_RELEASE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)の間に分散される可能性があります。

WDF クライアントでは、NetAdapter または作成した OID キューとデータパスキューを削除する必要はありません。 WDF は、これらのオブジェクトを自動的に削除します。

*Miniportshutdownex*、 *miniportresetex* 、 *MiniportCheckForHangEx*を削除できます。 これらのコールバックはサポートされなくなりました。

## <a name="ndis-wdf-function-equivalents"></a>NDIS-WDF 関数に対応する関数

ほとんどの `NdisXxx` 関数は、同等の WDF に置き換えることができます。 一般に、からインポートされる機能はごくわずかであることがわかり `NDIS.SYS` ます。

同等の関数の一覧については、「 [WDF 関数に相当する関数](ndis-wdf-function-equivalents.md)」を参照してください。

## <a name="debugging"></a>デバッグ

「 [NetAdapterCx クライアントドライバーのデバッグ」を](debugging-a-netadaptercx-client-driver.md)参照してください。

[! Ndiskd netadapter](../debugger/-ndiskd-netadapter.md)デバッガー拡張機能では **、次の**ような結果が表示されます。

## <a name="conclusion"></a>結論

このトピックの手順に従って、デバイスを開始および停止する動作するドライバーが必要です。
