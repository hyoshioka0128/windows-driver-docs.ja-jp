---
title: フィルター ドライバーからのデータの送信
description: フィルター ドライバーからのデータの送信
ms.assetid: 09189010-d12c-43d6-ac9b-8fc7424edfd5
keywords:
- WDK ネットワークのデータを送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1681950b654ea6f01ca8b56eeea3a3f7b99071e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579044"
---
# <a name="sending-data-from-a-filter-driver"></a>フィルター ドライバーからのデータの送信





フィルター ドライバーでは、送信要求を開始したり、上にあるドライバーを開始する送信要求をフィルター処理することができます。 プロトコル ドライバーを呼び出すと、 [ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)関数、NDIS を指定された送信[ **NET\_バッファー\_ボックスの一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)ドライバー スタックの最上位フィルター モジュールに構造体。

### <a name="send-requests-initiated-by-a-filter-driver"></a>フィルター ドライバーによって開始された要求を送信します。

次の図は、フィルター ドライバーによって開始される送信操作を示しています。

![フィルター ドライバーによって開始された送信操作を示す図](images/filtersend.png)

ドライバーの呼び出しをフィルター処理、 [ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)関数の一覧で定義されているネットワーク データを送信する[ **NET\_バッファー\_リスト**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

フィルター ドライバーを設定する必要があります、 **SourceHandle**各 net メンバー\_バッファー\_に渡されるのと同じ値を作成したリストの構造、 *NdisFilterHandle*パラメーター**NdisFSendNetBufferLists**します。 NDIS ドライバーは変更しないでください、 **SourceHandle** NET のメンバー\_バッファー\_ドライバーが取得されなかったリストの構造体。

呼び出しの前に**NdisFSendNetBufferLists**、フィルター ドライバーの詳細情報を使用して送信要求を設定できます、 [ **NET\_バッファー\_一覧\_情報** ](https://msdn.microsoft.com/library/windows/hardware/ff568401)マクロ。 基になるドライバーは、net には、この情報を取得できます\_バッファー\_一覧\_情報マクロ。

フィルター ドライバーを呼び出すと、すぐ**NdisFSendNetBufferLists**、NET の所有権を渡し、\_バッファー\_リストの構造体と関連付けられているすべてのリソース。 NDIS は、送信要求を処理または基になるドライバーに要求を渡すことができます。

NDIS 呼び出し、 [ *FilterSendNetBufferListsComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549967)構造とデータをフィルター ドライバーに返される関数。 NDIS は、構造体を収集でき、複数のデータは、NET のシングル リンク リストに要求を送信\_バッファー\_構造体のリストにリストを渡す前に*FilterSendNetBufferListsComplete*

NDIS 呼び出されるまで*FilterSendNetBufferListsComplete*、送信要求の現在の状態が不明です。 フィルター ドライバーにする必要があります*決して*確認しようとしています、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体、またはそのいずれかの関連データを保存 NDIS が戻る前に、構造を*FilterSendNetBufferListsComplete*します。

*FilterSendNetBufferListsComplete*送信操作を完了するために必要な後処理を実行します。

NDIS を呼び出すと*FilterSendNetBufferListsComplete*、フィルター ドライバーがネットワークに関連付けられているすべてのリソースの所有権を再度獲得\_バッファー\_リストの構造体で指定されている、 *NetBufferLists*パラメーター。 *FilterSendNetBufferListsComplete*これらのリソースを解放できますか (など、呼び出すことによって、 [ **NdisFreeNetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff562582)と[ **NdisFreeNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff562583)関数) に後続の呼び出しで再利用できるように準備または**NdisFSendNetBufferLists**します。

NDIS 常にデータを送信するフィルターが指定したネットワーク フィルター ドライバー確認の順序で基になるドライバーに渡された**NdisFSendNetBufferLists**します。 ただし、データを送信すると、指定した順序で、基になるドライバーできるバッファーを返す任意の順序で。

フィルター ドライバーは、送信要求をその it のループバックに要求できますの発生元します。 ループバックを要求するには、ドライバーは、NDIS を設定\_送信\_フラグ\_確認\_の\_でループバック フラグ、 *SendFlags*パラメーターの[ **NdisFSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562616)します。 NDIS は、送信データを含む受信パケットを示します。

**注**  フィルター ドライバーの発生元の送信要求の追跡し、呼び出されないことを確認する必要があります、 [ **NdisFSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562618)関数とこのような要求が完了します。

 

### <a name="filtering-send-requests"></a>送信要求のフィルター処理

次の図は、上位のドライバーによって開始される送信要求をフィルター処理を示しています。

![上位のドライバーによって開始される送信要求をフィルター処理を示す図](images/sendfilter.png)

NDIS フィルター ドライバーを呼び出す[ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)上にあるドライバーの送信要求をフィルター処理する関数。

フィルター ドライバーは変更しないで、 **SourceHandle**ネット メンバー\_バッファー\_他のドライバーから受信したリストの構造体。

フィルター ドライバーでは、データをフィルター処理でき、基になるドライバーをフィルター選択されたデータを送信することができます。 各ネットの\_バッファーの構造体に送信された*FilterSendNetBufferLists*、フィルター ドライバーは、次を実行できます。

-   呼び出すことで、[次へ] の基になるドライバーにバッファーを渡す、 [ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)関数。 NDIS は、コンテキストの領域の可用性を保証 (を参照してください[NET\_バッファー\_一覧\_CONTEXT 構造](net-buffer-list-context-structure.md)) フィルター ドライバー。 フィルター ドライバーは、呼び出す前に、バッファーの内容を変更できます**NdisFSendNetBufferLists**します。 フィルター ドライバーによって開始された送信操作と同様に、フィルター選択されたデータの処理が続行されます。

-   呼び出してバッファーを削除、 [ **NdisFSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562618)関数。

-   後で処理するためのローカル データ構造内のバッファーをキューします。 フィルター ドライバーの設計では、キューに置かれたバッファーの処理、ドライバーの原因は何を決定します。 いくつかの例には、処理のタイムアウト後または特定のバッファーを受信した後の処理が含まれます。

    **注**  キャンセル要求の送信をサポートする必要がありますドライバー キューでは、後で処理するための要求を送信する場合、。 キャンセル要求の送信の詳細については、[フィルター ドライバーの送信要求をキャンセル](canceling-a-send-request-in-a-filter-driver.md)を参照してください。

     

-   バッファーをコピーして、コピーでの送信要求を送信します。 送信操作は、フィルター ドライバーの送信が開始される要求に似ています。 この場合、ドライバー返す必要があります、元のバッファー上にあるドライバーを呼び出すことによって、 [ **NdisFSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562618)関数。

送信要求の完了は、ドライバー スタックの上位します。 ミニポート ドライバーを呼び出すと、 [ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)関数では、NDIS 呼び出し、 [ *FilterSendNetBufferListsComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549967)上にある最小のフィルター モジュールの関数。

送信操作が完了したら、フィルター ドライバーは、フィルター ドライバーに加え、上にあるドライバーのバッファー記述子への変更を反転させます*FilterSendNetBufferLists*します。 ドライバーの呼び出し、 [ **NdisFSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562618) NET のリンクの一覧を返す関数\_バッファー\_リスト構造の上にあるドライバーし取得するため、送信要求の最終的な状態です。

最上位フィルター モジュールを呼び出すと**NdisFSendNetBufferListsComplete**、NDIS 呼び出し元のプロトコル ドライバーの[ **ProtocolSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570268)関数。

用意されていないフィルター ドライバー、 *FilterSendNetBufferLists*関数は、送信要求を開始できますも。 このようなドライバーは、送信要求を開始する場合は、必要な*FilterSendNetBufferListsComplete*関数とそのによりいないドライバー スタックを完全なイベントが渡す必要があります。

フィルター ドライバーでは、渡すしたり、上位のドライバーのループバック要求をフィルター処理することができます。 NDIS NDIS を設定する場合は、ループバックの要求で渡す\_送信\_フラグ\_確認\_の\_でループバック、 *SendFlags*パラメーターの*FilterSendNetBufferLists*、フィルター ドライバー設定 NDIS\_送信\_フラグ\_確認\_の\_でループバック、 *SendFlags*パラメーターを呼び出すときに**NdisFSendNetBufferLists**します。 NDIS は、送信データを含む受信パケットを示します。

一般に、フィルター ドライバーは、NDIS が (ループバック) などの標準的なサービスを提供できない方法で任意の動作を変更、フィルター ドライバーは NDIS のサービスを提供する必要があります。 たとえば、ハードウェアのアドレスの要求を変更しますフィルター ドライバー (を参照してください[OID\_802\_3\_現在\_アドレス](https://msdn.microsoft.com/library/windows/hardware/ff569069))、バッファーの新しい宛てのループバックを処理する必要があります。ハードウェアのアドレス。 この場合は、NDIS は、フィルターには、アドレスが変更されるため、これは、通常はループバック サービスを提供することはできません。 また、フィルター ドライバーが無作為検出モードを設定する場合 (を参照してください[OID\_GEN\_現在\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569575))、受信した追加のデータのドライバーに関連する渡す必要がありますされません。

 

 





