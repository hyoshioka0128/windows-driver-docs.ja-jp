---
title: NDIS プロトコル ドライバーの概要
description: NDIS プロトコル ドライバーの概要
ms.assetid: 398a1cf1-9bf8-45a5-9b6d-65467d061e99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2deccc9dfccbb36ad7120146d009ea1e1c50f317
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844161"
---
# <a name="introduction-to-ndis-protocol-drivers"></a>NDIS プロトコル ドライバーの概要


NDIS プロトコルドライバーは、その下の端にある*Protocolxxx*関数のセットをエクスポートします。 このようなプロトコルドライバーは、NDIS と通信してネットワークデータを送受信します。 プロトコルドライバーは、基礎となるミニポートドライバーまたは中間ドライバーにバインドされます。これにより、その上端に*Miniportxxx*インターフェイスがエクスポートされます。

**注**  中間ドライバー (仮想ミニポート) の上端にあるミニポートドライバーは、物理デバイスを管理しません。 基になるミニポートドライバーは、物理デバイスを管理します。

 

プロトコルドライバーは、常に、NDIS に用意されている関数を使用して、基盤となる NDIS ドライバーと通信し、ネットワークデータを送受信します。 たとえば、コネクションレスの低速な (イーサネットなどのコネクションレスメディアの基になるドライバーと通信する) プロトコルドライバーは、 [**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)を呼び出して、基になる NDIS ドライバーにネットワークデータを送信する必要があります。 プロトコルドライバーは、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出して、基になるコネクションレスドライバーがサポートしている oid を照会または設定できます。 接続指向のエッジがあるプロトコルドライバー (ISDN などの接続指向メディアの基になるドライバーと通信する) は、 [**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)を呼び出して、ネットワークデータを低レベルの NDIS ドライバーに送信する必要があります。 また、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を呼び出して、基になる接続指向ドライバーでサポートされている oid を照会または設定することもできます。

また、NDIS には、基になるオペレーティングシステムの詳細を非表示にする**Ndis<em>Xxx</em>** 関数のセットも用意されています。 たとえば、プロトコルドライバーは、 [**NdisInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializeevent)を呼び出して同期用のイベントを作成したり、 [**NdisInitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializelisthead)を使用してリンクリストを作成したりできます。 このような機能の NDIS バージョンを使用するプロトコルドライバーは、Microsoft オペレーティングシステム全体で移植性が高くなります。 ただし、プロトコルドライバーでは、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)などのカーネルモードサポートルーチンを呼び出すこともできます。 詳細については、「[カーネルモードサポートルーチンの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

プロトコルドライバーの開発者は、他の NDIS ドライバーに適用されるのと同じプログラミング上の[考慮事項](network-driver-programming-considerations.md)を使用する必要があります。

 

 





