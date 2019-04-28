---
title: ネットワーク データの受信
description: ネットワーク データの受信
ms.assetid: d929c956-73dc-433f-9e60-bc3f8e0bcc14
keywords:
- ネットワーク データ、WDK の受信
- WDK のデータ ネットワークの受信
- WDK のパケットの受信ネットワーク
- WDK ネットワークのデータを返す
- ネットワーク データを返す WDK
- データ WDK ネットワー キング、返す
- パケット WDK ネットワー キング、返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3996091aeaef798ca1cd7bd3551377ec26760c21
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372484"
---
# <a name="receiving-network-data"></a>ネットワーク データの受信





次の図は、基本的な受信操作で、ミニポート ドライバー、NDIS、およびプロトコルのドライバーが含まれます。

![受信操作の基本的なを示す図](images/netbufferreceive.png)

ミニポート ドライバーの呼び出し、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)関数を示す[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)高いレベルのドライバーを構造体。 すべての NET\_バッファーの構造体は別に通常アタッチする必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 これにより、NET の元のリストのサブセットを作成するプロトコル ドライバー\_バッファー\_構造体を一覧表示し、それらを異なるクライアントに転送します。 ネイティブ IEEE 802.11 ミニポート ドライバーなど、一部のドライバーでは、複数の NET などもアタッチ\_バッファー構造体、NET\_バッファー\_リスト構造体。

リンクを作成した後すべての NET\_バッファー\_リストの構造体、ミニポート ドライバーの最初の NET にポインターを渡します\_バッファー\_リスト構造の一覧で、 **NdisMIndicateReceiveNetBufferLists**関数。 NDIS 調べ、NET\_バッファー\_リスト構造とそれを呼び出す、 [ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267) NET に関連付けられている各プロトコル ドライバーの機能\_バッファー\_リストの構造体。 NDIS NET のみを含むリストのサブセットを通過する\_バッファー\_プロトコル ドライバーごとに、正しいバインディングに関連付けられているリストの構造体。 NDIS と一致する、 **NetBufferListFrameType** NET で指定されている値\_バッファー\_各プロトコル ドライバーに登録するフレームの種類のリストの構造体。

場合は、NDIS\_受信\_フラグ\_リソース フラグ、 *ReceiveFlags*プロトコル ドライバーに渡されるパラメーター *ProtocolReceiveNetBufferLists*関数が設定されている、NDIS の所有権を再度獲得、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)後すぐに構造体、 *ProtocolReceiveNetBufferLists*返しますを呼び出します。

**注**  場合は、NDIS\_受信\_フラグ\_リソース フラグが設定されており、プロトコル ドライバーには、NET の元のセットを保持する必要があります\_バッファー\_リンクされたリストの構造体リスト。 たとえば、このフラグが設定されている場合、ドライバー可能性があります、構造を処理、返しますが、元のリンクされたリストを復元する必要があります前に、一度に 1 つ、スタックにそれらを示します。

 

場合は、NDIS\_受信\_フラグ\_リソース フラグ、 *ReceiveFlags*プロトコル ドライバーに渡されるパラメーター *ProtocolReceiveNetBufferLists*関数が設定されていない、プロトコル ドライバーには、NET の所有権を保持できます\_バッファー\_リストの構造体。 この場合、プロトコル ドライバーには、NET を返す必要があります\_バッファー\_呼び出すことによってリストの構造体、 [ **NdisReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564534)関数。

リソース受信ミニポート ドライバーが不足している場合は、NDIS を設定できます\_受信\_フラグ\_リソース フラグ、 *ReceiveFlags*への呼び出しでパラメーター **NdisMIndicateReceiveNetBufferLists**します。 ドライバーがすべての所有権を解放する場合、指定された[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体し、埋め込み[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体とすぐに**NdisMIndicateReceiveNetBufferLists**を返します。 NET を示す\_バッファー構造体、NDIS\_受信\_フラグ\_フラグに設定するリソースの強制的にデータをコピーするプロトコル ドライバーと避ける必要があります。 実行しようとしているときに、ミニポート ドライバーを検出する必要がありますのリソースを受信し、このような状況を回避するために必要な手順を実行します。

NDIS ミニポート ドライバーを呼び出す[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)関数プロトコル ドライバーの呼び出し後**NdisReturnNetBufferLists**します。

**注**  ミニポート ドライバーには、NET が示されている場合\_バッファー\_の構造と、NDIS\_受信\_フラグ\_フラグは NDIS がないことが、セットのリソースNET を示す\_バッファー\_リスト構造プロトコル ドライバーに同じ状態にします。 たとえば、NDIS はコピー、NET\_バッファー\_の構造と、NDIS\_受信\_フラグ\_リソース フラグが設定とプロトコル ドライバーへのコピーを示すフラグをクリアします。

 

NDIS を返すことができます[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)ミニポート ドライバーの任意の順序で、任意の組み合わせでの構造体。 NET のリンクのリストは、\_バッファー\_構造体への呼び出しによって返されるミニポート ドライバーへのリスト、 *MiniportReturnNetBufferLists* NET を持つことができます、関数\_バッファー\_以前別の呼び出しからリスト構造**NdisMIndicateReceiveNetBufferLists**します。

ミニポート ドライバーを設定する必要があります、 **SourceHandle**ネット メンバー\_バッファー\_に構造体のリスト、 *MiniportAdapterHandle*その NDIS ミニポート ドライバーに提供されます。[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 フィルター ドライバーを設定する必要があります、 **SourceHandle**各 net メンバー\_バッファー\_フィルターのフィルター ドライバーに送られる複数リスト構造**NdisFilterHandle**その NDISフィルター ドライバーに提供される、 [ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)関数。 フィルター ドライバーは変更しないで、 **SourceHandle**純でメンバー\_バッファー\_フィルター ドライバーによって実行されたいないリストの構造体。

中間ドライバーの設定も、 **SourceHandle**ネット メンバー\_バッファー\_リスト構造体を*MiniportAdapterHandle*値の中間に提供する NDIS内のドライバー、 *MiniportInitializeEx*関数。 中間のドライバーでは、受信を示す値を転送する場合、ドライバーを保存する必要があります、 **SourceHandle**値に書き込みを行う前に提供される基になるドライバー、 **SourceHandle**メンバー。 NDIS に転送された NET が返されるときに\_バッファー\_中間のドライバーでは、中間のドライバーをリストの構造を復元する必要があります、 **SourceHandle**保存することです。

 

 





