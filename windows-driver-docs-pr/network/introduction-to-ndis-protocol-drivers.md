---
title: NDIS プロトコル ドライバーの概要
description: NDIS プロトコル ドライバーの概要
ms.assetid: 398a1cf1-9bf8-45a5-9b6d-65467d061e99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9ec2dd808ed09dce6dc12428a0eebcd5d7d5885
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717001"
---
# <a name="introduction-to-ndis-protocol-drivers"></a>NDIS プロトコル ドライバーの概要


NDIS プロトコル ドライバーのセットをエクスポートします*ProtocolXxx*下端にある関数。 このようなプロトコル ドライバーは、ネットワーク データを送受信する NDIS と通信します。 プロトコル ドライバーには、基になるミニポート ドライバーまたはエクスポートする中間のドライバーにバインドする*MiniportXxx*上端のインターフェイス。

**注**  中間ドライバー (仮想ミニポート) のミニポート ドライバー上端は、物理デバイスを管理しません。 基になるミニポート ドライバーでは、物理デバイスを管理します。

 

プロトコル ドライバーは、常にネットワークのデータを送受信する基になる NDIS ドライバーとの通信に NDIS で提供される関数を使用します。 たとえば、プロトコル ドライバーを持つ、コネクションレス下-edge (これは、イーサネットなどのコネクションレスのメディアの基になるドライバーとの通信) を呼び出す必要があります[ **NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists)にネットワーク データを基になる NDIS ドライバーに送信します。 プロトコル ドライバーに呼び出せる[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)照会または設定する Oid を基になるコネクションレス ドライバーをサポートします。 呼び出す必要があります (これは、ISDN などの接続指向のメディアの基になるドライバーとの通信) 接続指向下隅のあるプロトコル ドライバー [ **NdisCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)を送信するには下位レベルの NDIS ドライバーにデータをネットワーク。 呼び出すことができますも[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)クエリまたは基になる接続指向のドライバーでサポートされている Oid を設定します。

NDIS は、のセットも用意されています。 **Ndis<em>Xxx</em>** 基になるオペレーティング システムの詳細を非表示にする関数。 たとえば、プロトコルのドライバーを呼び出すことができます[ **NdisInitializeEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisinitializeevent)同期を行うためのイベントを作成し、 [ **NdisInitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisinitializelisthead)リンク リストを作成します。 このような関数の NDIS バージョンを使用するプロトコル ドライバーは、Microsoft オペレーティング システム間で移植性を向上。 ただし、プロトコル ドライバー呼び出すこともできますカーネル モードのサポートのルーチンなど[ **IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)します。 詳細については、次を参照してください。[カーネル モードのサポート ルーチンの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

プロトコル ドライバーの開発者が使用する必要があります、同じ[プログラミングの注意点](network-driver-programming-considerations.md)他 NDIS ドライバーに適用されます。

 

 





