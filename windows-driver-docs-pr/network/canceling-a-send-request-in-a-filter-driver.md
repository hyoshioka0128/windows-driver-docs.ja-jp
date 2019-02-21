---
title: フィルター ドライバーでは、送信要求を取り消す
description: フィルター ドライバーでは、送信要求を取り消す
ms.assetid: afa9c8d3-b30b-4009-8428-d31719885154
keywords:
- 送信操作の WDK ネットワー キングのキャンセル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dfeda07f9ef8a4178781f2c8a9fb18fc3ac98e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531388"
---
# <a name="canceling-a-send-request-in-a-filter-driver"></a>フィルター ドライバーでは、送信要求を取り消す





フィルター ドライバーには、フィルター ドライバーによって生成されたされたまたはドライバーに関連して発生したが、送信要求をキャンセルできます。

### <a name="canceling-filter-driver-send-requests"></a>フィルター ドライバーの送信要求をキャンセルします。

次の図は、フィルター ドライバーによって送信されたが、送信要求を取り消すかを示しています。

![フィルター ドライバーによって開始された送信要求のキャンセルを示す図](images/filtercancelsend.png)

フィルター ドライバーは呼び出し、 [ **NDIS\_設定\_NET\_バッファー\_一覧\_キャンセル\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff567299)各用のマクロ[**NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体の送信操作が作成されます。 NDIS\_設定\_NET\_バッファー\_一覧\_キャンセル\_ID 関数は、キャンセルの識別子を持つ指定されたデータをマークします。

ネットワーク データをキャンセル Id を割り当てる前に、フィルター ドライバーを呼び出す必要があります[ **NdisGeneratePartialCancelId** ](https://msdn.microsoft.com/library/windows/hardware/ff562623)各キャンセル ID を割り当てることの高位のバイトを取得します。 これにより、ドライバーに取り消しシステム内の他のドライバーによって割り当てられた Id が重複していないこと。 ドライバーを呼び出す通常**NdisGeneratePartialCancelId**から 1 回、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。 呼び出すことで、ドライバーが 1 つ以上の部分取り消し識別子を取得するただし、 **NdisGeneratePartialCancelId**複数回です。

マークされたネットワーク内のデータの保留中の転送をキャンセルする\_バッファー\_リスト構造では、フィルター ドライバーにキャンセル ID に渡す、 [ **NdisFCancelSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561794)関数。 ドライバーとして使用できるは、NET\_バッファー\_リスト構造体のキャンセルの ID を呼び出して、 [ **NDIS\_取得\_NET\_バッファー\_一覧\_キャンセル\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff565683)マクロ。

場合、フィルター ドライバーはすべて NET\_バッファー\_同じキャンセル識別子を持つリスト構造体は、これを単一の呼び出しですべての保留中の転送を取り消すことができます**NdisFCancelSendNetBufferLists**します。 場合、フィルター ドライバーはすべて NET\_バッファー\_NET のサブグループ リスト構造\_バッファー\_リストの一意の識別子を持つ構造体、これとそのサブグループ内ですべての保留中の転送を取り消すことができます、単一の呼び出しを**NdisFCancelSendNetBufferLists**します。

NDIS は、基になるドライバーのキャンセル送信関数を呼び出します。 基になるドライバーが送信の完全な関数を呼び出して、保留中の転送を中止した後 (たとえば[ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)) を返す、NET\_バッファー\_NDIS の完了状態でリストの構造体\_状態\_送信\_中止されました。 NDIS、さらに、フィルター ドライバーの[ *FilterSendNetBufferListsComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549967)関数。

*FilterSendNetBufferListsComplete*、フィルター ドライバーは、NDIS を呼び出すことができます\_設定\_NET\_バッファー\_一覧\_キャンセル\_ID を*CancelId*設定**NULL**します。 これにより、NET\_バッファー\_から古いキャンセル ID に置き換えますもう一度使用されている誤って一覧。

### <a name="canceling-send-requests-originated-by-overlying-drivers"></a>上にあるドライバーの送信要求のキャンセル

次の図は、上にある、ドライバーによって開始された送信要求のキャンセルを示します。

![上にある、ドライバーによって開始された送信要求のキャンセルを示す図](images/cancelfiltersend.png)

上にあるドライバーは、[キャンセル] 送信関数を呼び出す ( [ **NdisFCancelSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561794)または[ **NdisCancelSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561623)) する未処理の送信要求を取り消します。 これらの上にあるドライバーは、送信要求を行う前に、データを送信する id がキャンセルをマークする必要があります。

NDIS フィルター ドライバーを呼び出す[ *FilterCancelSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549915)関数のすべての送信をキャンセルする[ **NET\_バッファー\_一覧** ](https://msdn.microsoft.com/library/windows/hardware/ff568388)指定したキャンセル識別子でマークされている構造体。

*FilterCancelSendNetBufferLists*は、次の操作を実行します。

1.  キューに置かれた NET のフィルター ドライバーのリストを走査\_バッファー\_モジュールの指定したフィルターおよび呼び出しリストの構造体、 [ **NDIS\_取得\_NET\_バッファー\_リスト\_キャンセル\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff565683)マクロを各構造体のキャンセルの識別子を取得します。 フィルター ドライバーは、その NDIS キャンセル ID を比較します\_取得\_NET\_バッファー\_一覧\_キャンセル\_NDIS はに渡されるキャンセル ID の ID を返します *。FilterCancelSendNetBufferLists*します。

2.  (リンクを解除) を送信キューから取り出したすべて NET\_バッファー\_リストの構造体がキャンセル識別子が指定されたキャンセル識別子に一致します。

3.  呼び出し、 [ **NdisFSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562618)関数のすべてのリンクされていない NET\_バッファー\_リストの構造体を構造体を返します。 フィルター ドライバーは、NET の状態フィールドを設定\_バッファー\_NDIS をリストの構造体\_状態\_送信\_中止されました。

4.  呼び出し、 **NdisFCancelSendNetBufferLists**キャンセルを渡す関数が基になるドライバーに要求を送信します。 フィルター ドライバーは、上にあるドライバーから受け取ったキャンセル識別子に渡します。 取り消し操作には、フィルター ドライバーの発生元のキャンセルを送信する操作が処理されます。

 

 





