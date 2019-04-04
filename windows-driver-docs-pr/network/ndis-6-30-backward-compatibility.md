---
title: NDIS 6.30 の下位互換性
description: NDIS 6.30 では、NDIS 6.20 が動作し、NDIS 6.0 のドライバーに適用されるものを旧バージョンとの互換性機能を追加します。
ms.assetid: 71C2BBCF-206A-4C2D-BF9C-C4074FB9276D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73d185f4b116eb7b9a7eb66af2b7a5176664a67d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574994"
---
# <a name="ndis-630-backward-compatibility"></a>NDIS 6.30 の下位互換性


NDIS 6.30 では、NDIS 6.20 が動作し、NDIS 6.0 のドライバーに適用されるものを旧バージョンとの互換性機能を追加します。 NDIS 6.20 互換性の問題については、[NDIS 6.20 が動作の下位互換性](ndis-6-20-backward-compatibility.md)を参照してください。 NDIS 6.0 の互換性の問題については、[NDIS 6.0 の下位互換性](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)を参照してください。

NDIS 6.30 機能の詳細については、[NDIS 6.30 概要](introduction-to-ndis-6-30.md)を参照してください。

## <a name="features-that-are-no-longer-supported"></a>サポートされなくなった機能


Windows 8 以降、次の機能がサポートされていません。

-   仮想マシンの場合は、TCP chimney オフロードがサポートされていません。 ただし、ネイティブの使用はまだことできます。
-   [IPsec タスク オフロード バージョン 1](ipsec-offload-version-1.md)します。 IPsec タスク オフロードをサポートするすべてのドライバーをサポートするために更新する必要があります[IPsec タスク オフロード バージョン 2](ipsec-offload-version-2.md)します。
-   中間ドライバーをフィルター処理します。 代わりに、NDIS 6 を使用します。*x*フィルター ドライバー インターフェイス。 フィルター ドライバーの詳細については、[NDIS フィルター ドライバー](ndis-filter-drivers.md)を参照してください。
-   802.3 をエミュレートする 802.11 ドライバーです。 NDIS 802.11 ドライバーでは、ネイティブの 802.11 インターフェイスをサポートする必要があります。 ネイティブの 802.11 の詳細については、[ネイティブ 802.11 ワイヤレス LAN](https://msdn.microsoft.com/library/windows/hardware/ff560689)を参照してください。
-   NDIS WAN ドライバーです。 NDIS 6.0 いる CoNDIS WAN ドライバー モデルには、NDIS WAN のドライバーを移植する必要があります。 いる CoNDIS WAN の詳細については、[WAN ミニポート ドライバー](wan-miniport-drivers.md)を参照してください。

## <a name="features-that-have-been-removed"></a>削除された機能


Windows 8 以降、次の機能が削除されました。

-   NDIS 5.x 以前のバージョン
-   IrDA ミニポート ドライバー
-   NetDMA
-   トークン リング (802.5)

## <a name="other-changes"></a>その他の変更


-   NDIS 6.30 に Windows 8 に付属している TCP/IP プロトコル ドライバーが更新されました。 ただし、この変更は、この機能にのみ、ドライバーを移植する価値がないように比較的小さなでした。 TCP/IP プロトコル ドライバーは、NDIS 6.20 が動作し、以前のドライバーのドライバー スタックとの下位互換性です。

 

 





