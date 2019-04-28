---
title: 複製された NET_BUFFER_LIST 構造
description: 複製された NET_BUFFER_LIST 構造
ms.assetid: efcf7d03-401e-46da-9ca3-8423af1e385a
keywords:
- NET_BUFFER_LIST
- 複製された構造体の WDK ネットワーク
- 構造体の WDK ネットワー キングが重複しています
- 親/子 NET_BUFFER_LIST リレーションシップ WDK ネットワーク
- 子/親 NET_BUFFER_LIST リレーションシップ WDK ネットワーク
- WDK NET_BUFFER_LIST のリレーションシップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 302d4a906b04bd8340f8a42d400edad5d66c8098
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373137"
---
# <a name="cloned-netbufferlist-structures"></a>NET の複製\_バッファー\_リストの構造体





NDIS ドライバーを作成、複製された[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)既存のネットから構造\_バッファー\_リスト構造体。 複製された構造体は、元のデータ構造を参照します。 ドライバーは、構造体のこの型を使用して、複数のパスを同じデータを効率的に転送します。

次の図は、親 NET 間の関係を示します\_バッファー\_リスト構造と複製された子構造体。

![net の親の間の関係を示す図\-バッファー\-構造および複製された子構造体を一覧表示](images/netbufferlistclone.png)

上記の図には、親が含まれています。 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造とその親から派生した子構造体。 親の構造体が 1 つ[ **NET\_バッファー\_一覧\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff568389)構造と 1 つ[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) MDLs 接続を含む構造体。 親構造体の親ポインターが**NULL**派生構造ではないことを示します。

子 NET\_バッファー\_リスト構造が 1 つの NET\_アタッチ MDLs のバッファーの構造体。 子 NET\_バッファー\_リストが親構造体へのポインター。 **NULL**場合、NET\_バッファー\_一覧\_コンテキスト構造体のポインターは、子に NET がないことを示しますなります\_バッファー\_一覧\_コンテキスト構造体。

ドライバーの呼び出し、 [ **NdisAllocateCloneNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff560705)クローンを作成する関数[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 NDIS が新しい割り当て[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造と複製された net MDLs\_バッファー\_リスト構造体。 NDIS は割り当てられません、 [ **NET\_バッファー\_一覧\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff568389)複製された構造体の構造体。 新しい NET\_バッファーの構造と MDLs が親構造体と同じデータについて説明します。 データはコピーされません。

ドライバーの呼び出し、 [ **NdisFreeCloneNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff561841) 、NET の解放関数\_バッファー\_リスト構造とすべての関連する NET\_バッファーの構造と MDL呼び出して以前に割り当てられたチェーン**NdisAllocateCloneNetBufferList**します。

## <a name="related-topics"></a>関連トピック


[NET の派生\_バッファー\_リストの構造体](derived-net-buffer-list-structures.md)

 

 






