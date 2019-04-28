---
title: 受信バッファー内の共有メモリ
description: 受信バッファー内の共有メモリ
ms.assetid: 3e4d0534-3cbd-40df-b7c1-4f2c15bcd757
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c89f14edf1f48f555134913bf7c6118833e51fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362135"
---
# <a name="shared-memory-in-receive-buffers"></a>受信バッファー内の共有メモリ





このセクションでは、共有のレイアウトを記述 VMQ のメモリ バッファーを受信します。受信表示でバッファーの使用の詳細についてを参照してください[VMQ 受信パス](vmq-receive-path.md)します。

上位のプロトコル ドライバーの設定、NDIS 場合\_受信\_キュー\_パラメーター\_先読み\_分割\_で必須フラグ、**フラグ**のメンバー[ **NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)構造、ネットワーク アダプターを分割受信パケットのオフセットに等しいまたは先読みアサーションが要求されたサイズと使用 DMA 先読みデータと post 先読みのデータを別の共有メモリ セグメントに転送するよりも大きい。

ミニポート ドライバー先読み型の設定の指定 (**NdisSharedMemoryUsageReceiveLookahead**) または共有メモリを割り当てるときにその他の共有メモリ型。 たとえば、ミニポート ドライバーが呼び出す、 [ **NdisAllocateSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561616)関数とセット、**使用状況**内のメンバー、 [ **NDIS\_共有\_メモリ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567303)構造体を**NdisSharedMemoryUsageReceiveLookahead**します。 ミニポート ドライバーは、キューの割り当てが完了すると、キューの共有メモリを割り当てる必要があります。 割り当てとキューの共有メモリ リソースの解放については、次を参照してください。[共有メモリ リソース割り当て](shared-memory-resource-allocation.md)します。

次の図は、受信データは 2 つの共有メモリ バッファーに分割するときに、ネットワーク データのリレーションシップを示します。

![受信データは 2 つの共有メモリ バッファーに分割するときは、ネットワーク データのリレーションシップを示す図](images/vmqpacket.png)

[ **NET\_バッファー\_SHARED\_メモリ**](https://msdn.microsoft.com/library/windows/hardware/ff568419)構造体は、共有メモリ情報を指定します。 関連付けられているこのような共有メモリ バッファーのリンク リストがあります、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。

使用して、 [ **NET\_バッファー\_共有\_MEM\_次\_セグメント**](https://msdn.microsoft.com/library/windows/hardware/ff568726)、 [ **NET\_バッファー\_SHARED\_MEM\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff568420)、 [ **NET\_バッファー\_SHARED\_をメモリ最適化\_処理**](https://msdn.microsoft.com/library/windows/hardware/ff568421)、 [ **NET\_バッファー\_SHARED\_MEM\_オフセット**](https://msdn.microsoft.com/library/windows/hardware/ff568727)、および[**NET\_バッファー\_共有\_MEM\_長さ**](https://msdn.microsoft.com/library/windows/hardware/ff568725) NET へのアクセスにマクロ\_バッファー\_SHARED\_、NET メモリ\_バッファーの構造体。 **SharedMemoryInfo** net メンバー\_バッファーの構造体には、最初のネットワークが含まれています。\_バッファー\_SHARED\_リンク リスト内のメモリ構造体。

**注**  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。 Windows Server 2012 以降では、上位のプロトコル ドライバーは未設定、 **NDIS\_受信\_キュー\_パラメーター\_先読み\_分割\_必要な作業**フラグ、**フラグ**のメンバー、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)構造体。

 

 

 





