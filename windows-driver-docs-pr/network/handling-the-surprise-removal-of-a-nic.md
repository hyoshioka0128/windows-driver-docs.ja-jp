---
title: NIC の突然の取り外しの処理
description: NIC の突然の取り外しの処理
ms.assetid: afd94749-8f2a-4cce-a646-1f616a845a0e
keywords:
- 予期しない WDK ネットワークの削除
- Nic WDK ネットワーク、驚くべき削除
- ネットワークインターフェイスカード WDK ネットワーク, 驚くべき削除
- プラグアンドプレイ WDK NDIS ミニポート、突然の NIC の削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ac8ba30425578fe336d0317786927c491b5ee25
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842547"
---
# <a name="handling-the-surprise-removal-of-a-nic"></a>NIC の突然の取り外しの処理





ユーザーインターフェイス (UI) を使用してシステムに事前に通知することなく、実行中のシステムからネットワークインターフェイスカード (NIC) を削除すると、突然削除されることがあります。

Windows Vista 以降のバージョンのオペレーティングシステム用のミニポートドライバーでは、突然の削除を処理できなければなりません。 特に、Windows Driver Model (WDM) のエッジを持つ NDIS ミニポートドライバーは、このようなイベントを処理できる必要があります。 NDIS WDM ミニポートドライバーが突然の削除を処理しない場合、予期しない削除の前にミニポートドライバーが基になるバスドライバーに送信した保留中の Irp は完了できません。

Windows Vista 以降のバージョンでは、ハードウェアを直接制御しないミニポートドライバー (たとえば、WDM が搭載されているミニポートドライバー) では、NDIS\_ミニポート\_属性を設定して、\_突然\_OK 属性を削除\_必要があります。[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出すときにフラグを付ける。 このフラグを設定すると、ユーザーが NIC の削除を実行したときに警告が表示されなくなります。 突然の削除を処理できないミニポートドライバーでは、このフラグを設定しないでください。

突然の削除をサポートするミニポートドライバーは、 [*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)のコンテキストの外部で、通常の操作中に突然の削除を検出しようとします。 NIC を削除すると、通常、NIC の i/o ポートを読み取ろうとすると、すべてのビットが1に設定された戻り値になります。 ミニポートドライバーがこのような値を読み取った場合は、ハードウェアの存在を確認し、より決定的なテストを行う必要があります。 たとえば、ミニポートドライバーは、i/o ポートに値を書き込み、そのポートから値の読み取りを試みることができます。 また、ミニポートドライバーは、NIC の i/o レジスタに有効な値があるかどうかを確認することもできます。 このような方法で突然削除を検出すると、割り込み DPC で削除された NIC のレジスタを読み取ろうとしたときに、ミニポートドライバーが無限ループでハングするのを防ぐことができます。「」を参照してください。 このように応答を停止するミニポートドライバーは、NDIS によってドライバーの*MiniportDevicePnPEventNotify*関数の呼び出しを停止します。

 

 





