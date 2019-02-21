---
title: NET_BUFFER_LIST_CONTEXT 構造体
description: NET_BUFFER_LIST_CONTEXT 構造体
ms.assetid: 45be8503-2c5f-46e6-9fc3-b1b3c42f0d91
keywords:
- NET_BUFFER_LIST_CONTEXT
- ネットワーク データ WDK、構造体
- ネットワー キング WDK データ、構造体
- パケットの WDK ネットワーク、データ構造体
- データ コンテキスト データ、WDK をネットワークします。
- データの WDK ネットワー キング、コンテキスト データ
- コンテキスト データ、パケットの WDK ネットワーク
- コンテキスト da
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc5666609e5751a93bc7aec1b5d30cafb5df4201
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561015"
---
# <a name="netbufferlistcontext-structure"></a>NET\_バッファー\_一覧\_CONTEXT 構造体





NDIS ドライバーを使用して、 [ **NET\_バッファー\_一覧\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff568389)に関連付けられている追加のデータを格納する構造体、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 **コンテキスト**net メンバー\_バッファー\_リスト構造は、NET へのポインター\_バッファー\_一覧\_CONTEXT 構造体。 NET に格納された情報\_バッファー\_一覧\_CONTEXT 構造体は、NDIS とスタックの他のドライバーに対して非透過的です。

次の図は、NET でフィールドを示します\_バッファー\_一覧\_CONTEXT 構造体。

![net のフィールドを示す図\-バッファー\-一覧\-context 構造体](images/netbufferlistcontext.png)

[ **NET\_バッファー\_一覧\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff568389)構造が含まれます**ContextData**コンテキスト データが含まれるメンバー。 このデータをドライバーが必要とするコンテキスト情報を指定できます、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

ドライバーがアクセスして、NET 内のメンバーを操作する次の NDIS マクロと関数を使用する必要があります\_バッファー\_一覧\_CONTEXT 構造体。

[**NdisAllocateNetBufferListContext**](https://msdn.microsoft.com/library/windows/hardware/ff561610)

[**NdisFreeNetBufferListContext**](https://msdn.microsoft.com/library/windows/hardware/ff562587)

[**NET\_バッファー\_一覧\_コンテキスト\_データ\_開始**](https://msdn.microsoft.com/library/windows/hardware/ff568391)

[**NET\_バッファー\_一覧\_コンテキスト\_データ\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff568390)

 

 





