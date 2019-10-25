---
title: KS のインターフェイス
description: KS のインターフェイス
ms.assetid: cc6fad32-0587-44a8-92d1-54bc0370e5c0
keywords:
- インターフェイス WDK カーネルストリーミング
- KSPIN_INTERFACE
- カーネルストリーミング WDK、インターフェイス
- KS WDK、インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 575992aec5b1e33801aa4395c0d7c6dcc866aff3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844349"
---
# <a name="ks-interfaces"></a>KS のインターフェイス





*インターフェイス*は、pin がどのように通信するかを定義する記述子パラメーターです。 ミニドライバーは、関連する[**kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造内の[**KSPIN\_インターフェイス**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))構造の配列へのポインターを提供することで、ピンがサポートするインターフェイスを示します。 次に、この情報を使用して、潜在的な接続とグラフの作成を決定します。

メディアと同様に、インターフェイスはセットとしても、そのセットの要素としても記述されます。 KSPIN\_インターフェイス構造体は、インターフェイスセット内の特定のインターフェイスを定義します。

次に、ユーザーモードクライアントは、関連する[**Kspin\_CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)構造体の**インターフェイス**メンバーを使用して、接続のインターフェイスの種類を指定します。 クライアントはこの KSPIN\_CONNECT インスタンスを[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)の呼び出しで渡します。これにより、IRP\_MJ\_がミニドライバーに送信されます。

 

 




