---
title: NetAdapterCx Receive Side Scaling (RSS)
description: NetAdapterCx Receive Side Scaling (RSS)
ms.assetid: 85A819E2-6352-4DE9-9689-3DCEB9B0AAD8
keywords:
- WDF ネットワークアダプタークラス拡張 Receive Side Scaling、NetAdapterCx receive side scaling、NetAdapterCx RSS、NetAdapter RSS
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2f8728ba643240275e2023e6d34e1b0e30058277
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838271"
---
# <a name="netadaptercx-receive-side-scaling-rss"></a>NetAdapterCx Receive Side Scaling (RSS)

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Receive side scaling (RSS) は、マルチプロセッサシステムの複数の Cpu にわたってネットワークの受信処理を効率的に分散できるようにするネットワークドライバーテクノロジです。 RSS は、システムの使用可能なすべてのプロセッサを利用し、CPU の負荷を動的に再調整することにより、システムのパフォーマンスを向上させ、ネットワークのスケーラビリティを高めます。 

このトピックでは、NetAdapterCx クライアントドライバーの RSS について説明し、RSS の概念と用語についての知識を前提としています。 さまざまなハードウェアシナリオでの RSS を示す図を含む、一般的な RSS の詳細については、「 [Receive Side Scaling](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-receive-side-scaling2)」を参照してください。

## <a name="overview-of-rss-in-netadaptercx"></a>NetAdapterCx の RSS の概要

NetAdapterCx の RSS は、構成の容易さ、有効化と無効化の単純化、プロセッサから割り込みの複雑さの抽象化に焦点を当てています。 RSS 対応 NIC のクライアントドライバーは、NetAdapterCx で RSS をサポートするために、次の3つの条件を満たす必要があります。

1. ドライバーは、net アダプターを起動するときに、 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す前に RSS 機能を設定する必要があります。 これには、4つの RSS コールバックの実装と RSS 機能の構造での登録が含まれます。
2. ドライバーのデータパスキューを作成し、要求を受け入れる準備ができている必要があります。
3. ドライバーは、 *D0*の電源状態である必要があります。

NetAdapterCx の RSS の設計により、システムは、クライアントの RSS コールバックを呼び出し[たり、最後](power-up-sequence-for-a-netadaptercx-client-driver.md)までの間に rss を有効にしたりすることが保証されます。 クライアントは、必要なすべてのものが準備できるまで、間接テーブルの移動要求を管理したり、他の RSS イベントを処理したりする必要はありません。 

その後、ドライバーがアンロードされると、NetAdapterCx は、データパスキューが[パワーダウンシーケンス](power-down-sequence-for-a-netadaptercx-client-driver.md)中に破棄された後に RSS コールバックを呼び出しません。 データパスのキューは、電源を切るときの最初の手順として破棄されるので、クライアントは、電源を切るときに、他の段階で RSS イベントを処理する必要がありません。

## <a name="setting-rss-capabilities"></a>RSS 機能の設定

NetAdapterCx で RSS の使用を開始するには、次の手順を実行します。

1. Net アダプターを起動するときに、 [NET_ADAPTER_RECEIVE_SCALING_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_capabilities)構造を使用して、ハードウェアの RSS 機能と制約についてシステムに指示します。
2. [NET_ADAPTER_RECEIVE_SCALING_CAPABILITIES_INIT](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nf-netreceivescaling-net_adapter_receive_scaling_capabilities_init)を呼び出して、機能の構造を初期化します。 
3. RSS 機能の構造を初期化するときに、構造体の RSS コールバックメンバーを設定して、これらのコールバックの実装を登録します。
    1. *[EvtNetAdapterReceiveScalingEnable](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)*
    2. *[EvtNetAdapterReceiveScalingDisable](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)*
    3. *[EvtNetAdapterReceiveScalingSetHashSecretKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)*
    4. *[EvtNetAdapterReceiveScalingSetIndirectionEntries](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)*
4. 必要に応じて RSS 機能構造の**SynchronizeSetIndirectionEntries**を設定します。
5. 初期化された RSS 機能構造を[NetAdapterSetReceiveScalingCapabilities](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nf-netreceivescaling-netadaptersetreceivescalingcapabilities)メソッドに渡します。

## <a name="enabling-and-disabling-rss"></a>RSS の有効化と無効化

RSS 機能を設定した後、システムはドライバーの電源を入れ続けます。 NetAdapterCx は、データパスキューを作成する最後の手順が完了すると、ドライバーの RSS コールバックの呼び出しを開始します。 この時点で、システムによって必要になったときに RSS を有効または無効にすることができます。 

> [!IMPORTANT]
> RSS を有効または無効にする場合は、間接テーブルをクリアまたはリセット**しない**でください。 フレームワークは、初期の間接テーブル状態を設定します。

### <a name="enabling-rss"></a>RSS の有効化

NetAdapterCx は、ドライバーの *[EvtNetAdapterReceiveScalingEnable](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)* コールバックを呼び出すことによって RSS を有効にします。 このコールバックのコンテキストでは、通常、ハードウェアで制御ビットを有効にします。 

RSS を有効にするコード例については、「 *[EvtNetAdapterReceiveScalingEnable](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)* 」を参照してください。

### <a name="disabling-rss"></a>RSS の無効化

NetAdapterCx は、ドライバーの *[EvtNetAdapterReceiveScalingDisable](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)* コールバックを呼び出すことで RSS を無効にします。 ここでは、通常、 *EvtNetAdapterReceiveScalingEnable*で以前に設定したハードウェアの制御ビットを無効にします。 

RSS を無効にするコード例については、「 *[EvtNetAdapterReceiveScalingDisable](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)* 」を参照してください。

## <a name="setting-the-hash-secret-key"></a>ハッシュシークレットキーを設定しています

RSS を有効にすると、NetAdapterCx は *[EvtNetAdapterReceiveScalingSetHashSecretKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)* コールバックを呼び出して、NIC がハッシュ計算の検証に使用するハッシュシークレットキーをドライバーに提供します。 このコールバックは、ハッシュシークレットキーが変更された場合に RSS が実行されているときにいつでも呼び出すことができます。 

ハッシュシークレットキーを設定するコード例については、「 *[EvtNetAdapterReceiveScalingSetHashSecretKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)* 」を参照してください。

## <a name="moving-indirection-table-entries"></a>間接テーブルのエントリの移動

RSS はシステム上で実行されていますが、上位層のプロトコルドライバーはプロセッサのワークロードを監視し、受信キューをプロセッサにマップする間接テーブルを維持します。 プロトコルドライバーが RSS でプロセッサのワークロードを再調整する必要がある場合は、まず、新しいプロセッサに対する各間接テーブルエントリに対して新しいマッピングを計算します。 次に、この情報を NetAdapterCx に渡します。これにより、受信キューとハードウェア割り込みベクターを NIC クライアントドライバーの代わりに正しいプロセッサにマッピングする複雑さが処理されます。 NetAdapterCx は、receive queue Id にマップされたエントリを含む新しい間接テーブルを[NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_indirection_entries)構造体に格納し、 *[EvtNetAdapterReceiveScalingSetIndirectionEntries](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)* callback 関数を呼び出すときにドライバーに渡します。 

このコールバックでは、NIC の間接テーブル内の各エントリを指定された受信キューに移動します。 **NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRIES**配列の各[NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_indirection_entry)構造には、テーブル内のそのエントリのハッシュインデックス、エントリを割り当てる新しい受信キュー、および個々の移動が成功したかどうかを示す状態フィールドが含まれています。 

ハードウェアの受信キューにインデックスエントリを割り当てる方法は、NIC の設計と、それに含まれる受信キューの数によって異なります。 詳細とコード例については、「 *[EvtNetAdapterReceiveScalingSetIndirectionEntries](https://docs.microsoft.com/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)* 」を参照してください。
