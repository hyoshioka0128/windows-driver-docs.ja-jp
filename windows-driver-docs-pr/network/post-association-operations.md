---
title: 関連付け後の操作の概要
description: 関連付け後の操作の概要
ms.assetid: e4c7ea7a-53ad-41b2-bf3f-03c770e58043
keywords:
- IHV 拡張 DLL WDK ネイティブ802.11、関連付け後の操作
- アソシエーション後の操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- ネイティブ 802.11 IHV 拡張 DLL WDK、関連付け後の操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a670e81fdffa71b3dcd61d5366a96b47d8faf9c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843683"
---
# <a name="post-association-operations-overview"></a>関連付け後の操作の概要

ワイヤレス LAN (WLAN) アダプターがアクセスポイント (AP) との関連付け操作を正常に完了すると、オペレーティングシステムは関連付け用のデータポートを作成します。 次に、オペレーティングシステムは、 [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数を呼び出すことによって、データポートに対して関連付け後の操作を開始します。

**注**  Windows Vista では、IHV 拡張 DLL は、インフラストラクチャの基本サービスセット (BSS) ネットワークのみをサポートしています。

 

関連付け後の操作を実行すると、IHV 拡張 DLL は次のことを実行できます。

-   新しいデータポートに必要なリソースを割り当てます。

-   データポートに対して独自のセキュリティ処理を実行します。これには、関連付け前の操作中に構成された認証アルゴリズムのパケットの送受信も含まれます。 この操作の詳細については、「[事前関連付け操作](pre-association-operations.md)」を参照してください。

-   暗号化キーを取得し、WLAN アダプターにダウンロードします。

WLAN アダプターが AP との関連付け操作を完了すると、オペレーティングシステムは[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)関数を呼び出して、データポートの関連付け後の操作を終了します。 この呼び出しの後、オペレーティングシステムは関連付けのデータポートを削除します。

次のトピックでは、IHV 拡張 DLL が関連付け後の操作を実行または停止するために行う必要があることについて説明します。

[関連付け後の操作の実行](performing-a-post-association-operation.md)

[関連付け後の操作を停止しています](stopping-a-post-association-operation.md)

[ネイティブ 802.11 802.1 X モジュールへのインターフェイス](interface-to-the-native-802-11-802-1x-module.md)

アソシエーション操作の詳細については、「[アソシエーション操作](association-operations.md)」を参照してください。

関連付け操作の詳細については、「[関連付け操作](disassociation-operations.md)」を参照してください。

ポート管理に関連する手順の詳細については、「[ポートベースのネットワークアクセス](port-based-network-access.md)」を参照してください。

 

 





