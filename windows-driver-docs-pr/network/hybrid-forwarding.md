---
title: ハイブリッド転送の HYPER-V 拡張可能スイッチ
description: このセクションには、HYPER-V 拡張可能なスイッチを使用してハイブリッド転送がについて説明します
ms.assetid: 135CA734-1C92-4EEA-81DC-96A6A68ABBE8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6739599d1f22dffadb2906c10a3353fc29a37c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530920"
---
# <a name="hybrid-forwarding"></a>ハイブリッド転送


NDIS 6.40 以降 (Windows Server 2012 R2、HYPER-V 拡張可能スイッチのアーキテクチャをサポート ハイブリッド転送転送拡張機能と拡張可能スイッチの HYPER-V ネットワーク仮想化 (HNV) コンポーネントによってします。

**注**  このページに精通していることを前提としています[Network Virtualization using Generic Routing Encapsulation (NVGRE) タスク オフロード](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)と[Hyper-v 拡張可能スイッチの概要。](overview-of-the-hyper-v-extensible-switch.md).

 

## <a name="nvgre-and-non-nvgre-packets"></a>NVGRE と非 NVGRE パケット


転送のハイブリッド環境では、入力し、HYPER-V 拡張可能スイッチのままにしたパケットの 2 つの種類があります。NVGRE パケットと非 NVGRE パケットの場合:

-   NVGRE パケット カプセル化された形式で指定されているである、 [NVGRE:Generic Routing Encapsulation によるネットワーク仮想化](http://ietfreport.isoc.org/idref/draft-sridharan-virtualization-nvgre/)インターネット ドラフトです。 NVGRE パケットは、HYPER-V 拡張可能スイッチの HNV コンポーネントによって転送されます。
-   非 NVGRE パケットは、ごく普通のネットワーク パケットをされます。 非 NVGRE パケットは、転送拡張機能によって転送されます (またはの転送拡張機能がない場合、拡張可能なスイッチ自体)。

## <a name="flow-of-nvgre-and-non-nvgre-packets-through-the-switch"></a>スイッチを介して NVGRE と非 NVGRE パケットのフロー


イングレス データ パスで、キャプチャおよびフィルター処理拡張機能が、転送拡張機能の前にパケットが、NVGRE パケットの場合、拡張可能スイッチ設定、 **NativeForwardingRequired**フラグ、 [ **NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)パケットの構造体。 この構造体に含まれている、 **NetBufferListInfo**のパケットのメンバー [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

**注**  、 **NetBufferListInfo**のメンバー、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)とも呼ばしますパケットの「アウト オブ バンド (OOB) データ」

 

場合、 **NativeForwardingRequired**パケットの OOB データにフラグが設定、パケットは、NVGRE パケット。 設定されていない場合、パケットは、非 NVGRE パケットです。

拡張機能を使用する必要があります、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)マクロ、の値を確認するには**NativeForwardingRequired**フラグ。

NVGRE と非 NVGRE パケットは、次のように扱われます。

-   HYPER-V 拡張可能スイッチの HNV のコンポーネントに転送されます (つまりの変換先テーブルを決定する) すべての NVGRE パケット
-   HNV のコンポーネントは、NVGRE カプセル化し、必要に応じて、カプセル化解除を実行します。
-   転送拡張機能は、すべての非 NVGRE パケットを転送します。
-   転送拡張機能は、NVGRE パケットを転送できませんが、フィルター拡張機能の追加または変換先のポートを除くやパケットを破棄してもなどのフィルター処理操作を実行できます。
-   転送拡張機能がない場合は、HYPER-V 拡張可能スイッチは、すべてのパケットを転送します。

詳細については、[パケットがスイッチの拡張のデータ パスを通過](packet-flow-through-the-extensible-switch-data-path.md)を参照してください。

## <a name="support-for-third-party-network-virtualization"></a>サードパーティ製のネットワーク仮想化のサポート


A **VirtualSubnetId**外部の仮想サブネットと VM ネットワーク アダプターのポートで構成できます。 サードパーティ製のネットワーク仮想化ソリューションを提供する転送拡張機能を有効にするこの機能が追加されました。 受信時、HYPER-V 拡張可能スイッチを設定しません、 **NativeForwardingRequired**フラグ、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)これらのパケットの構造体。 転送拡張機能は、転送中に、必要に応じて、パケット ヘッダーを変更できます。 変更されるパケットを複製して、その**ParentNetBufferList**ポインターは、元に設定**NET\_バッファー\_一覧**。 (を参照してください[パケット トラフィックを複製](cloning-or-duplicating-packet-traffic.md))。

## <a name="related-topics"></a>関連トピック


[拡張可能スイッチの宛先ポート データ パケットを追加します。](adding-extensible-switch-destination-port-data-to-a-packet.md)

[トラフィックのパケットの複製](cloning-or-duplicating-packet-traffic.md)

[転送拡張機能](forwarding-extensions.md)

[拡張可能スイッチのデータ パスを通じてパケットのフロー](packet-flow-through-the-extensible-switch-data-path.md)

[**NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)

[**NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)

 

 






