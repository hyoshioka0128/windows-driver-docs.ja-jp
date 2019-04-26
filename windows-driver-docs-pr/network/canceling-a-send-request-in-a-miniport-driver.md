---
title: ミニポート ドライバーでの送信要求のキャンセル
description: ミニポート ドライバーでの送信要求のキャンセル
ms.assetid: 9339e661-b91a-49e1-9924-66c85cc80ee8
keywords:
- NdisCancelSendNetBufferLists
- MiniportCancelSend
- WDK のネットワー キングを要求する送信のキャンセル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 323ff3f63d506620382aa38dc574e50603d68597
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351994"
---
# <a name="canceling-a-send-request-in-a-miniport-driver"></a>ミニポート ドライバーでの送信要求のキャンセル





次の図は、送信操作がキャンセル ミニポート ドライバーを示します。

![送信操作がキャンセル ミニポート ドライバーを示す図](images/miniportcancelsend.png)

プロトコル、フィルター、および中間ドライバーを呼び出すことができます[ **NdisCancelSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561623)未処理の送信要求をキャンセルします。 これらの上にあるドライバーは、送信要求を行う前に、データを送信する id がキャンセルをマークする必要があります。

NDIS ミニポート ドライバーを呼び出す[ *MiniportCancelSend* ](https://msdn.microsoft.com/library/windows/hardware/ff559342)関数のすべての送信をキャンセルする[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)指定したキャンセル識別子でマークされている構造体。

ミニポート ドライバーの*MiniportCancelSend*関数は、次の操作を実行します。

1.  指定したアダプターと呼び出しの未処理の送信要求のリストを走査[ **NDIS\_取得\_NET\_バッファー\_一覧\_キャンセル\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff565683)各 NET のキャンセル識別子を取得する\_バッファー\_リスト構造体。 ミニポート ドライバーがその NDIS キャンセル ID を比較します\_取得\_NET\_バッファー\_一覧\_キャンセル\_NDIS に渡されるキャンセル ID の ID を返します*MiniportCancelSend*します。

2.  すべてのネットワークから削除します\_バッファー\_要求を送信するリストの構造体がキャンセル識別子が未処理の一覧から指定したキャンセル識別子と一致します。

3.  呼び出し、 [ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)関数のすべての取り消された NET\_バッファー\_リストの構造体を構造体を返します。ミニポート ドライバーは、NET の状態フィールドを設定\_バッファー\_NDIS をリストの構造体\_状態\_送信\_中止されました。

 

 





