---
title: パケット結合受信フィルター
description: パケット結合受信フィルター
ms.assetid: B5C17A9D-A495-4A3D-B53E-B10F53C732D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e8d8aa3f72516fe5234a77a52b5e42a927ffd60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383178"
---
#  <a name="packet-coalescing-receive-filters"></a>パケット結合受信フィルター


NDIS 6.30、以降[NDIS 受信フィルター](https://msdn.microsoft.com/library/windows/hardware/hh205393)パケットの結合をサポートするために拡張されています。 パケットの結合の場合は、各受信フィルターでは、次の項目を定義します。

-   ユーザー データグラム プロトコル (UDP) ヘッダーのメディア アクセス制御 (MAC) のヘッダーまたは転送先ポートの送信先アドレスなどのパケットのさまざまなプロトコル ヘッダー内のフィールドのセット。

-   合体受信フィルターに一致するパケットがネットワーク アダプターによって結合された最大時間。 アダプターでは、この値を使用して、アダプターのハードウェアのタイマーの有効期限値の設定。 タイマーが満了するとすぐに、アダプターは、ミニポート ドライバーは、結合されたパケットを処理できるように、ホストを中断する必要があります。

    **注**  受信フィルターに一致する最初のパケットを結合すると、タイマーが起動、ネットワーク アダプターをリセットして、タイマーを再起動することがなく受信フィルターに一致する追加のパケットを結合する必要があります。

     

ドライバーは、プロトコルとフィルター ドライバーなどの後続パケット結合ダウンロード受信ミニポート ドライバーにフィルターのオブジェクト識別子 (OID) のセット要求を発行して[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。 詳細については、次を参照してください。[パケット結合受信フィルターの設定](setting-packet-coalescing-receive-filters.md)します。

ドライバーの後続パケット結合クエリを受け取ることもフィルター ミニポート ドライバーをダウンロードします。 上にあるドライバーでは、これを行うの OID メソッド要求を発行して[OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)ミニポート ドライバーにします。 詳細については、次を参照してください。[クエリを実行するパケット結合受信フィルター](querying-packet-coalescing-receive-filters.md)します。

 

 





