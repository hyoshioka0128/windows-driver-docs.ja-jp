---
title: IPsec オフロード バージョン 2 で NET_BUFFER_LIST 情報にアクセスします。
description: IPsec Offload Version 2 での NET_BUFFER_LIST 情報へのアクセス
ms.assetid: 0c27b594-2c61-4459-96df-1d7445100bc5
keywords:
- IPsecOV2 WDK TCP/IP トランスポート、NET_BUFFER_LIST 情報
- NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d7c15eefeb4ae8cdc2c57095a3f457531f29127
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571987"
---
# <a name="accessing-netbufferlist-information-in-ipsec-offload-version-2"></a>NET にアクセスする\_バッファー\_IPsec オフロード バージョン 2 でリストの情報

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




NDIS でアウト オブ バンド (OOB) データを提供する、 **NetBufferListInfo**のメンバー、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体を指定します、リンク リスト[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。 **NetBufferListInfo**メンバーは、NET のすべてに共通する情報が含まれている値の配列\_リスト内のバッファーの構造体。

次の識別子を使用して、 [ **NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff568401)設定および IPsec オフロード バージョン 2 (IPsecOV2) を取得するマクロ、でOOBデータ**NetBufferListInfo**配列。

<a href="" id="ipsecoffloadv2netbufferlistinfo"></a>**IPsecOffloadV2NetBufferListInfo**  
NIC に TCP/IP プロトコルからの IPsec タスク オフロードで使用される IPsecOV2 情報を指定します 指定すると**IPsecOffloadV2NetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、 [ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565818)構造体。

<a href="" id="ipsecoffloadv2tunnelnetbufferlistinfo"></a>**IPsecOffloadV2TunnelNetBufferListInfo**  
NIC に TCP/IP プロトコルからの IPsec タスク オフロードで使用される IPsecOV2 トンネル情報を指定します 指定すると**IPsecOffloadV2TunnelNetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、 [ **NDIS\_IPSEC\_オフロード\_V2\_トンネル\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565843)構造体。

<a href="" id="ipsecoffloadv2headernetbufferlistinfo"></a>**IPsecOffloadV2HeaderNetBufferListInfo**  
IPsec ヘッダーでのヘッダー オフセットを指定します、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)と、次のヘッダーとパッドの長さの値。 指定すると**IPsecOffloadV2HeaderNetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、 [ **NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565812)構造体。

 

 





