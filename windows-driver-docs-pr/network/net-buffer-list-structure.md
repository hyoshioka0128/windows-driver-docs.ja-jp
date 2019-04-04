---
title: NET_BUFFER_LIST 構造
description: NET_BUFFER_LIST 構造
ms.assetid: f7f19e48-cb63-458d-b175-6f99080e4cdf
keywords:
- NET_BUFFER_LIST
- ネットワーク データ WDK、構造体
- ネットワー キング WDK データ、構造体
- パケットの WDK ネットワーク、データ構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce60b4adcbb38b5090190385a7cc03b711bbf5cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580253"
---
# <a name="netbufferlist-structure"></a>NET\_バッファー\_リスト構造





A [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体は、NET のリンク リストをパッケージ\_バッファーの構造体。

次の図は、NET でフィールドを示します\_バッファー\_リスト構造体。

![net のフィールドを示す図\-バッファー\-構造体を一覧表示](images/netbufferlist.png)

NET\_バッファー\_リスト構造が含まれています、 [ **NET\_バッファー\_一覧\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff568400)構造体、 **NetBufferListHeader**メンバー。 NET\_バッファー\_一覧\_ヘッダー構造が含まれています、 [ **NET\_バッファー\_一覧\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568393)構造体**NetBufferListData**メンバー。 NET のアクセスに NDIS マクロを使用する必要があります\_バッファー\_構造体メンバーの一覧。 これらのマクロの詳細については、、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造のリファレンス ページを参照してください。

一部のメンバーは NDIS でのみ使用されます。 ドライバーが最もよく使用するメンバーは、次の一覧で定義されます。

<a href="" id="parentnetbufferlist"></a>**ParentNetBufferList**  
場合、NET\_バッファー\_リスト構造は、親 (複製、断片化、または再構築) から派生した子**ParentNetBufferList** NET 親へのポインターを指定します\_バッファー\_リスト構造体。 このパラメーターは、それ以外の場合、 **NULL**します。

<a href="" id="ndispoolhandle"></a>**NdisPoolHandle**  
ネットを識別するプール ハンドルを指定します\_バッファー\_元となるプールを一覧、NET\_バッファー\_リスト構造が割り当てられます。

<a href="" id="protocolreserved"></a>**ProtocolReserved**  
プロトコル ドライバーで使用するために予約されています。

<a href="" id="miniportreserved"></a>**MiniportReserved**  
ミニポート ドライバーで使用するために予約されています。

<a href="" id="sourcehandle"></a>**SourceHandle**  
ドライバーに、バインディングまたは、次のドライバーによって提供されるルーチンのいずれかを使用して操作を添付する NDIS が提供されるハンドル:

<a href="" id="miniport-driver"></a>ミニポート ドライバー  
[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

<a href="" id="protocol-driver"></a>プロトコル ドライバー  
[*ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)

<a href="" id="filter-driver"></a>フィルター ドライバー  
[*FilterAttach*](https://msdn.microsoft.com/library/windows/hardware/ff549905)

NDIS を使用して**SourceHandle**を返す、NET\_バッファー\_ネットを送信するドライバーにリスト構造\_バッファー\_リスト構造体。 NDIS ドライバーは、このハンドルを読み取りません。

<a href="" id="childrefcount"></a>**ChildRefCount**  
場合、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体は、親 (複製、フラグメント、または再アセンブリの操作によって派生した子がある)、 **ChildRefCount**既存の子の数を指定します。 それ以外の場合、このパラメーターは 0 です。

<a href="" id="flags"></a>**フラグ**  
NET の属性の将来の仕様用に予約\_バッファー\_リスト構造体。 現在、フラグはドライバーはありません。

<a href="" id="status"></a>**状態**  
このネットワークにネットワークのデータ操作の最終的な完了状態を示す\_バッファー\_リスト構造体。 ミニポート ドライバーでは、送信操作を完了する前にこの値を記述します。

<a href="" id="netbufferlistinfo"></a>**NetBufferListInfo**  
指定します[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)すべてに共通する情報を構造体[ **NET\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff568376)リスト内の構造体。 この情報は、「帯域外の (OOB) データ」と呼ばれる多くの場合、

<a href="" id="next"></a>**次に**  
[次へ] のネットワークへのポインターを指定します\_バッファー\_NET のリンク リストにリスト構造\_バッファー\_リストの構造体。 場合、NET\_バッファー\_リスト構造は、最後の構造の一覧で、このメンバーは**NULL**します。

<a href="" id="firstnetbuffer"></a>**FirstNetBuffer**  
最初のネットワークへのポインターを指定します\_NET のリンク リストにバッファー構造\_この NET に関連付けられているバッファーの構造体\_バッファー\_リスト構造体。

**注**  **コンテキスト**へのポインターを[ **NET\_バッファー\_一覧\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff568389)構造体。 NDIS マクロとにデータを操作する関数を提供する**コンテキスト**します。 NET の詳細については\_バッファー\_一覧\_CONTEXT 構造体を参照してください[NET\_バッファー\_一覧\_CONTEXT 構造](net-buffer-list-context-structure.md)します。

 

 

 





