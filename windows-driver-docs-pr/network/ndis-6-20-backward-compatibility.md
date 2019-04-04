---
title: NDIS 6.20 旧バージョンとの互換性
description: NDIS 6.20 旧バージョンとの互換性
ms.assetid: a2d71cae-aed2-4c23-9ad2-5c32d4ab2294
keywords:
- NDIS 6.20 WDK、旧バージョンとの互換性
- 旧バージョンとの互換性 WDK NDIS 6.20 が動作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e9c56a0c1522da4a934aef8160c95ec9802e09f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553332"
---
# <a name="ndis-620-backward-compatibility"></a>NDIS 6.20 旧バージョンとの互換性





NDIS 6.20 が動作は、NDIS 6.0 のドライバーに適用されるものに旧バージョンとの互換性機能を追加します。 NDIS 6.0 の互換性の問題については、[NDIS 6.0 の下位互換性](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)を参照してください。 NDIS 6.0 の NDIS の翻訳機能だけでなく 5.x と以前のドライバーでは、NDIS 6.20 が動作は、電源管理のインターフェイスの翻訳も提供します。 NDIS 6.20 ドライバーでは、NDIS 6.20 電源管理のインターフェイスをサポートする必要があります。

NDIS 6.20 が動作には、NDIS 6.1 に追加された機能の更新バージョンがサポートしています。 NDIS 6.1 機能の更新プログラムの詳細については、[NDIS 6.1 機能の NDIS 6.20 サポート](ndis-6-20-updates-to-ndis-6-1-features.md)を参照してください。

**注**  NDIS 6.20 インターフェイスは、64 を超えるプロセッサをサポートしています。 以前のバージョンの NDIS は 64 個のプロセッサに制限されます (x86 32 オペレーティング システムのバージョン)。

 

プロセッサに 64 を超えるプロセッサの既定値をサポートするために更新されていないドライバーを以前のバージョンの NDIS との下位互換性を維持するには、0 をグループ化します。 プロセッサ グループの詳細については、プロセッサ グループのカーネル モード ドライバーのアーキテクチャ デザイン ドキュメントを参照してください。

一部の NDIS 6.1 と以前の関数が廃止され、NDIS 6.20 ドライバーでは使用できません。 その NDIS バージョン互換性を判定する特定の関数のリファレンス ページの必要条件」を参照してください。 古い形式のインターフェイスの一覧は、[NDIS 6.20 で古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)を参照してください。

NDIS 6.20 が動作する Windows 7 に同梱されている TCP/IP プロトコル ドライバーが更新されました。 TCP/IP プロトコル ドライバーは、NDIS 6.1 と以前のドライバーのドライバー スタックとの下位互換性です。 ただし、Windows 7 ドライバー スタックの最大のパフォーマンスを取得するは、すべてのドライバーを NDIS 6.20 が動作を更新する必要があります。

NDIS 5.x と以前の NDIS ドライバーは非推奨と Microsoft Windows のバージョンで Windows 7 の後にします。 新しい NDIS 5.x ドライバーには、WHQL の認定はされません。 すべての新しいドライバーには、NDIS 6.0 またはそれ以降のドライバーがあります。

Windows 7 の後に、Microsoft Windows のバージョンでこの IrDA ミニポート ドライバーはサポートされません。

[IPsec タスク オフロード バージョン 1](ipsec-offload-version-1.md) Windows 7 の後に Microsoft Windows のバージョンでサポートされません。 IPsec タスク オフロードをサポートするすべてのドライバーをサポートするために更新する必要があります[IPsec タスク オフロード バージョン 2](ipsec-offload-version-2.md)します。

Windows 7 の後に、Microsoft Windows のバージョンでこの中間のフィルター ドライバーはサポートされません。 NDIS 6.0 フィルター ドライバー インターフェイスを使用する必要があります。 フィルター ドライバーの詳細については、[NDIS フィルター ドライバー](ndis-filter-drivers.md)を参照してください。

Windows 7 の後に、Microsoft Windows のバージョンでこの 802.3 をエミュレートするドライバーが 802.11 はサポートされません。 NDIS 802.11 ドライバーでは、ネイティブの 802.11 インターフェイスをサポートする必要があります。 ネイティブの 802.11 の詳細については、[ネイティブ 802.11 ワイヤレス LAN](https://msdn.microsoft.com/library/windows/hardware/ff560689)を参照してください。

Windows 7 の後に、Microsoft Windows のバージョンでこの NDIS WAN ドライバーはサポートされません。 NDIS 6.0 いる CoNDIS WAN ドライバー モデルには、NDIS WAN のドライバーを移植する必要があります。 いる CoNDIS WAN の詳細については、WAN ミニポート ドライバーを参照してください。

Windows 7 の後に、Microsoft Windows のバージョンでこの ATM とトークン リングのドライバーはサポートされません。

 

 





