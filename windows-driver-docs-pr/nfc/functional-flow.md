---
title: 機能のフロー
description: スマートカード検出時の NDEF メッセージの階層的な読み取りと書き込みに関するフローチャートと短い説明。
ms.assetid: 7B4B4902-FD16-4C9B-BB54-A1D6EFCAE9DB
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c13f44d4a66554810cb41f275f51a9fa75cf502
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843412"
---
# <a name="functional-flow"></a>機能のフロー


スマートカードは、NFP とドライバーを共有しているので、スマートカードを使用すると、NDEF の処理が優先されます。これにより、アプリケーションがカードと通信する前に、上位レベルのサービスが NDEF メッセージの種類で動作する機会が与えられます。

![スマートカード検出時の NDEF メッセージの階層的な読み取りと書き込みを記述するフローチャート。](images/smartcardfunctionalflow.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[スマートカード DDI とコマンドリファレンス](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85))  
