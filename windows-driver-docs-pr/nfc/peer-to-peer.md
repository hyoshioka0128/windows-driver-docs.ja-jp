---
title: ピアツーピア
ms.assetid: 0234BA57-477E-408C-94C8-8DD8922FD386
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: NFC フォーラムに関する情報は、ピア ツー ピアの標準を定義して、デバイスを確認します。 プロトコルは NFC を使用してやり取りできます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8212c433858234ceeb26aeb821e873339ae6ad6e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383161"
---
# <a name="peer-to-peer"></a>ピアツーピア


2 つのデバイスが NFC を使用してやり取りできるように、ドライバーが次の NFC フォーラムを使用してデータを送受信する必要がありますには、ピア ツー ピアの規格とプロトコルを定義しました。

-   LLCP v1.1
-   SNEP v1.0

## <a name="driver-requirements"></a>ドライバーの要件


LLCP NDEF メッセージ交換を実行している既定の SNEP サーバーをサポートするドライバーの必要があります。

-   リモートの P2P デバイスの着信、ドライバーは、("DeviceArrived"サブスクリプションがトリガーされた後に)、リモート デバイスの既定の SNEP サーバーとクライアント SNEP 接続を確立する必要があります。
-   ドライバーは、その既定の SNEP サーバー リモート デバイスの SNEP クライアント接続からで接続を受け入れることもあります。
-   このドキュメントで定義されている、SNEP サーバーで受信したすべての NDEF メッセージをメッセージの種類に変換する必要があります。
-   パブリッシュするすべてのメッセージの種類は NDEF メッセージに変換および前述のように、リモート デバイスに送信する必要があります。 メッセージが送信されると、 [ **IOCTL\_NFP\_取得\_[次へ]\_送信\_メッセージ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)で定義されているとおりに完了このドキュメントでは。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
