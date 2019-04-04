---
title: NetAdapterCx Receive Side Scaling (RSS)
description: NetAdapterCx Receive Side Scaling (RSS)
ms.assetid: 85A819E2-6352-4DE9-9689-3DCEB9B0AAD8
keywords:
- WDF ネットワーク アダプター クラスの拡張機能 Receive Side Scaling、NetAdapterCx 受信側 scaling、NetAdapterCx RSS、NetAdapter RSS
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8afa43147869c8add2237cf6fa1a46e44644cdee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570621"
---
# <a name="netadaptercx-receive-side-scaling-rss"></a>NetAdapterCx Receive Side Scaling (RSS)

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

受信側が scaling (RSS) がネットワークを効率的に分散できるようにするネットワーク ドライバー テクノロジは、マルチプロセッサ システムで複数の cpu 処理を受信します。 RSS は、システム パフォーマンスが向上し、システムで使用可能なすべてのプロセッサを利用して、CPU の負荷を動的に再調整によってネットワーク スケーラビリティが向上します。 

このトピックでは、NetAdapterCx クライアント ドライバーの RSS を強調表示し、RSS の概念と用語の知識を前提としています。 RSS の詳細については一般に、別のハードウェアでは、RSS を表すダイアグラムを含む表示[Receive Side Scaling](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-receive-side-scaling2)します。

## <a name="overview-of-rss-in-netadaptercx"></a>NetAdapterCx で RSS の概要

RSS NetAdapterCx には、構成、わかりやすくするための有効化と無効化、およびプロセッサの割り込みの複雑さを抽象化の容易さについて説明します。 RSS 対応の NIC 用のクライアント ドライバーのみ、NetAdapterCx で RSS をサポートするために 3 つの条件を満たす必要があります。

1. ネット アダプターを開始するときに、呼び出す前に、ドライバーは RSS の機能を設定する必要があります[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)します。 これには、4 つの RSS コールバックを実装して、RSS の機能の構造で登録が含まれます。
2. ドライバーのデータパス キュー作成され、要求を受け入れる必要があります。
3. ドライバーがである必要があります、 *D0*電源の状態。

NetAdapterCx で RSS の設計により、システムがクライアントの RSS のコールバックを呼び出していないの最後まで RSS を有効にして、[電源投入シーケンス](power-up-sequence-for-a-netadaptercx-client-driver.md)します。 クライアントは、間接指定テーブルの移動要求の管理またはその他の必要なものすべてが準備できるまでは、RSS のイベントを処理する必要はありません。 

後で、ドライバーをアンロードすると、NetAdapterCx はコールバックを呼び出しません RSS 中にデータパス キューが破棄された後、[電源シーケンス](power-down-sequence-for-a-netadaptercx-client-driver.md)します。 データパス キューは、電源ダウン中に最初のステップとして破棄は後、は、電源ダウン中に他の何らかの段階で RSS の可能なイベントを処理するためにクライアントがないことを意味します。

## <a name="setting-rss-capabilities"></a>RSS の機能を設定

NetAdapterCx で RSS を開始するには、次の手順を実行します。

1. ネット アダプターを開始するときに、システム、ハードウェアの RSS 機能や通知を使用して制約、 [NET_ADAPTER_RECEIVE_SCALING_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_capabilities)構造体。
2. 機能の構造を呼び出して初期化[NET_ADAPTER_RECEIVE_SCALING_CAPABILITIES_INIT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nf-netreceivescaling-net_adapter_receive_scaling_capabilities_init)します。 
3. RSS の機能の構造を初期化するときに、実装のこれらのコールバックを登録する構造体の RSS コールバック メンバーを設定します。
    1. *[EvtNetAdapterReceiveScalingEnable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)*
    2. *[EvtNetAdapterReceiveScalingDisable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)*
    3. *[EvtNetAdapterReceiveScalingSetHashSecretKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)*
    4. *[EvtNetAdapterReceiveScalingSetIndirectionEntries](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)*
4. RSS の機能の構造体の設定**SynchronizeSetIndirectionEntries**に応じて。
5. 初期化された RSS 機能構造体を渡す、 [NetAdapterSetReceiveScalingCapabilities](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nf-netreceivescaling-netadaptersetreceivescalingcapabilities)メソッド。

## <a name="enabling-and-disabling-rss"></a>有効にして、RSS を無効化

RSS の機能を設定した後、システムは、ドライバーの電源投入シーケンスに進みます。 NetAdapterCx は、データパス キューの作成の最後の手順が完了すると、ドライバーの RSS のコールバックの呼び出しを開始します。 この時点では、RSS を有効になっているし、システムの必要に応じて無効になっています。 

> [!IMPORTANT]
> 必要があります**いない**クリアまたはリセットを有効にするか、RSS を無効にするときに、間接指定テーブル。 フレームワークの設定は、初期の間接参照テーブルの状態。

### <a name="enabling-rss"></a>RSS を有効にします。

呼び出してドライバーの RSS を有効に NetAdapterCx *[EvtNetAdapterReceiveScalingEnable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)* コールバック。 このコールバックのコンテキストで一般的に、ハードウェアの制御ビットを有効します。 

RSS を有効化のコード例では、 *[EvtNetAdapterReceiveScalingEnable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)* を参照してください。

### <a name="disabling-rss"></a>RSS を無効にします。

NetAdapterCx を呼び出してドライバーの RSS を無効にします*[EvtNetAdapterReceiveScalingDisable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)* コールバック。 ここでは、通常で無効にする制御ビットで以前に設定したハードウェア*EvtNetAdapterReceiveScalingEnable*します。 

RSS を無効化のコード例では、 *[EvtNetAdapterReceiveScalingDisable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)* を参照してください。

## <a name="setting-the-hash-secret-key"></a>ハッシュの秘密キーを設定します。

NetAdapterCx が呼び出す RSS が有効にすると、 *[EvtNetAdapterReceiveScalingSetHashSecretKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)* ハッシュの秘密キーを使用して、NIC には、ドライバーを提供するコールバックをハッシュの検証に使用する必要があります計算します。 このコールバックは、RSS を秘密キーをハッシュが変更された場合に実行するときにいつでも呼び出されることができます。 

ハッシュの秘密キーの設定のコード例では、 *[EvtNetAdapterReceiveScalingSetHashSecretKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)* を参照してください。

## <a name="moving-indirection-table-entries"></a>間接指定テーブル エントリの移動

RSS は、システムで実行中に、上位層プロトコル ドライバーはプロセッサの負荷を監視し、マップする間接指定テーブル プロセッサ キューの受信を維持します。 プロトコル ドライバーは、rss プロセッサの負荷を再調整する必要がある、最初に、新しいプロセッサに間接指定テーブル エントリごとに新しいマッピングを計算します。 プロトコルは、キューおよび、NIC のクライアント ドライバーの代わりに適切なプロセッサ ハードウェア割り込みベクトル、NetAdapterCx、マッピングの複雑さを受信するハンドルをこの情報を渡します。 NetAdapterCx でキューの Id を受信するマップ エントリを含む新しいの間接指定テーブルを格納する、 [NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_indirection_entries)構造体を呼び出すときに、ドライバーに渡します、 *[EvtNetAdapterReceiveScalingSetIndirectionEntries](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)* コールバック関数。 

このコールバックで、指定された受信キューに NIC の間接指定テーブル内の各エントリを移動します。 各[NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_indirection_entry)構造体、 **NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRIES**配列には、表に、そのエントリのハッシュ インデックスが含まれています新しい。エントリとか、その個々 の移動が成功したかどうかを示す状態フィールドの割り当て先となるキューが表示されます。 

ハードウェアにインデックス エントリを割り当てる方法が、受信キューが受信キューの数と、NIC の設計によって変わります。 詳細とコード例では、 *[EvtNetAdapterReceiveScalingSetIndirectionEntries](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)* を参照してください。
