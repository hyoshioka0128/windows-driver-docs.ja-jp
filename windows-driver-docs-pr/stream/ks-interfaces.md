---
title: KS のインターフェイス
description: KS のインターフェイス
ms.assetid: cc6fad32-0587-44a8-92d1-54bc0370e5c0
keywords:
- ストリーミング インターフェイス WDK カーネル
- KSPIN_INTERFACE
- カーネルの WDK、インターフェイスのストリーミング
- KS WDK、インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 574853d4d05fb0fff7a384e4a14b60846833fe5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382497"
---
# <a name="ks-interfaces"></a>KS のインターフェイス





*インターフェイス*暗証番号 (pin) との通信方法を定義する記述子のパラメーターです。 配列へのポインターを提供することで、pin をサポートするインターフェイスを示します、ミニドライバー [ **KSPIN\_インターフェイス**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))構造、関連する[ **KSPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)構造体。 KS は、潜在的な接続とグラフの構築を決定するため、この情報を使用します。

などのメディア、およびそのセットの要素をセットとしてインターフェイスは説明もします。 KSPIN\_インターフェイス構造体、インターフェイスのセット内の特定のインターフェイスを定義します。

使用して、ユーザー モードのクライアントが接続のインターフェイスの種類にしを指定します、**インターフェイス**の関連メンバー [ **KSPIN\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_connect)構造体。 クライアントはこの KSPIN を渡します\_CONNECT インスタンスへの呼び出しで[ **KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatepin)、IRP になる\_MJ\_ようにミニドライバーに送信される作成します。

 

 




