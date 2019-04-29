---
title: NDIS プロトコル ドライバーの概要
description: NDIS プロトコル ドライバーの概要
ms.assetid: 398a1cf1-9bf8-45a5-9b6d-65467d061e99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c85109f5611e60fd47575ee30e97b46b208a2874
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329627"
---
# <a name="introduction-to-ndis-protocol-drivers"></a>NDIS プロトコル ドライバーの概要


NDIS プロトコル ドライバーのセットをエクスポートします*ProtocolXxx*下端にある関数。 このようなプロトコル ドライバーは、ネットワーク データを送受信する NDIS と通信します。 プロトコル ドライバーには、基になるミニポート ドライバーまたはエクスポートする中間のドライバーにバインドする*MiniportXxx*上端のインターフェイス。

**注**  中間ドライバー (仮想ミニポート) のミニポート ドライバー上端は、物理デバイスを管理しません。 基になるミニポート ドライバーでは、物理デバイスを管理します。

 

プロトコル ドライバーは、常にネットワークのデータを送受信する基になる NDIS ドライバーとの通信に NDIS で提供される関数を使用します。 たとえば、プロトコル ドライバーを持つ、コネクションレス下-edge (これは、イーサネットなどのコネクションレスのメディアの基になるドライバーとの通信) を呼び出す必要があります[ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)にネットワーク データを基になる NDIS ドライバーに送信します。 プロトコル ドライバーに呼び出せる[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)照会または設定する Oid を基になるコネクションレス ドライバーをサポートします。 呼び出す必要があります (これは、ISDN などの接続指向のメディアの基になるドライバーとの通信) 接続指向下隅のあるプロトコル ドライバー [ **NdisCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561728)を送信するには下位レベルの NDIS ドライバーにデータをネットワーク。 呼び出すことができますも[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)クエリまたは基になる接続指向のドライバーでサポートされている Oid を設定します。

NDIS は、のセットも用意されています。 **Ndis * Xxx*** 基になるオペレーティング システムの詳細を非表示にする関数。 たとえば、プロトコルのドライバーを呼び出すことができます[ **NdisInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562732)同期を行うためのイベントを作成し、 [ **NdisInitializeListHead**](https://msdn.microsoft.com/library/windows/hardware/ff562734)リンク リストを作成します。 このような関数の NDIS バージョンを使用するプロトコル ドライバーは、Microsoft オペレーティング システム間で移植性を向上。 ただし、プロトコル ドライバー呼び出すこともできますカーネル モードのサポートのルーチンなど[ **IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)します。 詳細については、次を参照してください。[カーネル モードのサポート ルーチンの概要](https://msdn.microsoft.com/library/windows/hardware/ff563889)します。

プロトコル ドライバーの開発者が使用する必要があります、同じ[プログラミングの注意点](network-driver-programming-considerations.md)他 NDIS ドライバーに適用されます。

 

 





