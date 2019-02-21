---
title: ピア ツー ピア
ms.assetid: 0234BA57-477E-408C-94C8-8DD8922FD386
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
description: NFC フォーラムに関する情報は、ピア ツー ピアの標準を定義して、デバイスを確認します。 プロトコルは NFC を使用してやり取りできます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c0272feb0fd890058c34c911742fb0155b9c466
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550241"
---
# <a name="peer-to-peer"></a>ピア ツー ピア


2 つのデバイスが NFC を使用してやり取りできるように、ドライバーが次の NFC フォーラムを使用してデータを送受信する必要がありますには、ピア ツー ピアの規格とプロトコルを定義しました。

-   LLCP v1.1
-   SNEP v1.0

## <a name="driver-requirements"></a>ドライバーの要件


LLCP NDEF メッセージ交換を実行している既定の SNEP サーバーをサポートするドライバーの必要があります。

-   リモートの P2P デバイスの着信、ドライバーは、("DeviceArrived"サブスクリプションがトリガーされた後に)、リモート デバイスの既定の SNEP サーバーとクライアント SNEP 接続を確立する必要があります。
-   ドライバーは、その既定の SNEP サーバー リモート デバイスの SNEP クライアント接続からで接続を受け入れることもあります。
-   このドキュメントで定義されている、SNEP サーバーで受信したすべての NDEF メッセージをメッセージの種類に変換する必要があります。
-   パブリッシュするすべてのメッセージの種類は NDEF メッセージに変換および前述のように、リモート デバイスに送信する必要があります。 メッセージが送信されると、 [ **IOCTL\_NFP\_取得\_[次へ]\_送信\_メッセージ**](https://msdn.microsoft.com/library/windows/hardware/jj853320)で定義されているとおりに完了このドキュメントでは。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  
