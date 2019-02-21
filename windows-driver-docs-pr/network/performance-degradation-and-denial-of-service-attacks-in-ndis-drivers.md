---
title: パフォーマンスの低下と NDIS ドライバーで DoS 攻撃を受ける
description: パフォーマンスが低下し、サービス拒否攻撃、NDIS ドライバーには
ms.assetid: 0e80c6e2-3e6d-4189-b2df-bdd9a4a40dd6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ee2aa40e48fb33f4e27e8c687389dd5598242be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530541"
---
# <a name="performance-degradation-and-denial-of-service-attacks-in-ndis-drivers"></a>パフォーマンスが低下し、サービス拒否攻撃、NDIS ドライバーには




NDIS ドライバー割り込みハンドラーは、受信したパケットを解析し場合に、パフォーマンスが低下し、サービス拒否攻撃、割り込みハンドラーの実装が生じる可能性があります。 たとえば、悪意のあるユーザーは、ミニポート ドライバーは、割り込みハンドラーで無効なパケット上のチェックサムを計算できるように、多くのパケットを送信することによって、コンピューターを対象ことができます。

ドライバーを実行すると、ドライバーが受信したパケットを処理する方法に注意が必要ですが、場合でもディスパッチ IRQL での操作を受信します。 代わりに、受信したパケットの処理はドライバー スタックができるようにする必要があります。 この場合は、上にあるドライバー スタックは、パケットをコピーし、パッシブ IRQL で後でそれを操作します。

 

 





