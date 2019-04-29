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
ms.openlocfilehash: bfaa258619df88f0b8fbf11809b2ee5ddbe3258e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325234"
---
# <a name="ks-interfaces"></a>KS のインターフェイス





*インターフェイス*暗証番号 (pin) との通信方法を定義する記述子のパラメーターです。 配列へのポインターを提供することで、pin をサポートするインターフェイスを示します、ミニドライバー [ **KSPIN\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff563537)構造、関連する[ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)構造体。 KS は、潜在的な接続とグラフの構築を決定するため、この情報を使用します。

などのメディア、およびそのセットの要素をセットとしてインターフェイスは説明もします。 KSPIN\_インターフェイス構造体、インターフェイスのセット内の特定のインターフェイスを定義します。

使用して、ユーザー モードのクライアントが接続のインターフェイスの種類にしを指定します、**インターフェイス**の関連メンバー [ **KSPIN\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff563531)構造体。 クライアントはこの KSPIN を渡します\_CONNECT インスタンスへの呼び出しで[ **KsCreatePin**](https://msdn.microsoft.com/library/windows/hardware/ff561652)、IRP になる\_MJ\_ようにミニドライバーに送信される作成します。

 

 




