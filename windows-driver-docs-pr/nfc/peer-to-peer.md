---
title: ピアツーピア
ms.assetid: 0234BA57-477E-408C-94C8-8DD8922FD386
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: デバイスが NFC を使用して対話できることを保証する、NFC フォーラムで定義されているピアツーピア標準とプロトコルに関する情報。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7867e588b2b534512e8fd38c24ba87b5f7240485
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834085"
---
# <a name="peer-to-peer"></a>ピアツーピア


2つのデバイスが NFC を使用して対話できるようにするには、ドライバーは次の NFC フォーラムで定義されているピアツーピアの標準とプロトコルを使用してデータを送受信する必要があります。

-   LLCP v1.1
-   SNEP v1.0

## <a name="driver-requirements"></a>ドライバーの要件


ドライバーは、LLCP 経由で実行されている既定の SNEP サーバーをサポートし、NDEF メッセージを交換する必要があります。

-   リモートの P2P デバイスに到着した場合、ドライバーは、リモートデバイスの既定の SNEP サーバーとのクライアント SNEP 接続を確立する必要があります (その後に "DeviceArrived" サブスクリプションがトリガーされます)。
-   また、ドライバーは、リモートデバイスの SNEP クライアント接続から、既定の SNEP サーバーでの接続を受け入れることもできなければなりません。
-   SNEP サーバーで受信したすべての NDEF メッセージは、このドキュメントで定義されているメッセージの種類に変換される必要があります。
-   公開されるすべてのメッセージの種類は、NDEF メッセージに変換され、前述のようにリモートデバイスに送信される必要があります。 メッセージが送信されると、このドキュメントで定義されているように、 [**IOCTL\_NFP\_\_次\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)された\_メッセージが完了します。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
