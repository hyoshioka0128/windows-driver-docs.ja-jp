---
title: フィルター ID の使用
description: フィルター ID の使用
ms.assetid: 005AD1CF-37EB-44E8-BFA0-676ACCF69D47
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f65bd0a76e721999b7516d7f58a83fdddf1641ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373757"
---
# <a name="using-the-filter-id"></a>フィルター ID の使用


ドライバーのダウンロードを後続の OID メソッド要求を発行してミニポート ドライバーにフィルターを受信[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。 各受信フィルター ミニポート ドライバーにダウンロードするには、NDIS によって生成される一意のフィルタ識別子 (ID) があります。 上にあるドライバーは、以下を実行するためにこのフィルター ID 以降の OID 要求で使用する必要があります。

-   受信のフィルター パラメーターをクエリします。 受信フィルターのパラメーターをクエリする方法の詳細については、次を参照してください。[クエリを実行するパケット結合受信フィルター](querying-packet-coalescing-receive-filters.md)します。

-   受信のフィルター パラメーターを変更します。 受信フィルターのパラメーターを変更する方法の詳細については、次を参照してください。[変更パケット結合受信フィルター](modifying-packet-coalescing-receive-filters.md)します。

-   無料、または*オフ*、受信フィルター。 フィルターをクリアに受信する方法の詳細については、次を参照してください。[クリア パケット結合受信フィルター](clearing-packet-coalescing-receive-filters.md)します。

ミニポート ドライバーでは、割り当てられた受信のフィルターのフィルター Id を保持する必要があります。 ミニポート ドライバーが OID 要求で指定したフィルター ID の前の OID メソッド要求から、割り当てられた受信フィルターが一致することを確認する必要がありますを変更し、クエリ、または、受信フィルターを無料の OID 要求を受信した場合[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。 フィルター ID が割り当てられている受信フィルターを一致しない場合、ミニポート ドライバーは、失敗したステータスの OID 要求を完了する必要があります。

 

 





