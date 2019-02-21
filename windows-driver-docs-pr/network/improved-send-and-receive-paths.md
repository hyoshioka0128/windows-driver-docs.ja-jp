---
title: 改善の送信と受信パス
description: 改善の送信と受信パス
ms.assetid: 7edecb49-576f-4058-92e8-39f14268a130
keywords:
- NDIS WDK、データを送受信します。
- WDK ネットワークのデータを送信します。
- 受信側のデータの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3abde686105c8f92a86c9068e75647d1ad58e86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553913"
---
# <a name="improved-send-and-receive-paths"></a>改善の送信と受信パス





NDIS 6.0 の送信し、受信パス パフォーマンスを向上させるのには次のように改良されています。

-   NDIS 6.0 とそれ以降のドライバーのすべての送信し、受信機能のリンク リストを転送できる[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造とそれに関連付けられた[**NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) 1 つの関数呼び出しを含む構造体。 このサポートは true。 multipacket 送信および受信操作を大幅には、ドライバーが行う必要があります関数呼び出しの数を減らします。

-   送信を呼び出すときに、関数のディスパッチで実行されているドライバーの受信または\_レベルの IRQL NDIS を示すことができます。 これらのドライバーの IRQL をテストまたはディスパッチに設定する必要はありません NDIS には、スタック内の他のドライバーへの呼び出し、その後が行うと、\_レベル。 これには、テスト、および critical コードのセクションで、IRQL の設定に関連付けられたオーバーヘッドが削減されます。

-   NET を調整する NDIS ドライバーがドライバー スタックの上下のパケットを渡すときに要求できます\_ヘッダー情報に対応するためにデータをバッファーのオフセットします。 パケットを送信するときに、ドライバーはドライバーのヘッダー情報に対応するために使用されるデータ領域を展開できます。 ドライバーが完了した後に、ドライバーが使用されているデータ領域を減らすことができます受信パケットを指定する際に、ヘッダー情報にアクセスします。 この機能を .NET で使用されるデータ領域を動的に調整する\_バッファーの構造体の割り当てやメモリの解放およびデータをコピーしなくてもネットワーク データの処理に必要なオーバーヘッドが減少します。

送信し、処理 NDIS 6.0 のデータの受信についての詳細についてを参照してください。 [NET\_バッファー アーキテクチャ](net-buffer-architecture.md)します。

 

 





