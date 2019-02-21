---
title: フィルター ドライバーのデータの受信
description: フィルター ドライバーのデータの受信
ms.assetid: 4f6d44e9-c351-452d-aadf-505e6bb30fc2
keywords:
- 受信側のデータの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd10cf33474ad24f6b4b6d692caadb6e7ed64d17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531022"
---
# <a name="receiving-data-in-a-filter-driver"></a>フィルター ドライバーのデータの受信





フィルター ドライバー開始受信表示またはフィルターでは、基になるドライバーからインジケーターが表示されることができます。 ミニポート ドライバーを呼び出すと、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)関数、NDIS を指定された送信[ **NET\_バッファー\_リスト**](https://msdn.microsoft.com/library/windows/hardware/ff568388)ドライバー スタックの上にある最小のフィルター モジュールに構造体。

### <a name="receive-indications-initiated-by-a-filter-driver"></a>受信フィルター ドライバーによる表示

次の図は、フィルター ドライバーによって開始される受信を示す値を示します。

![フィルター ドライバーによって開始された受信示す値を示す図](images/filterreceive.png)

ドライバーの呼び出しをフィルター処理、 [ **NdisFIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561820)を受信したデータを示す関数。 **NdisFIndicateReceiveNetBufferLists**関数の指定された一覧を渡します[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体にスタックをセットアップします。上にあるドライバー。 フィルター ドライバーは、初期化中に作成されたプールから、構造体を割り当てます。

フィルター ドライバーが設定されている場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820)、これは、フィルター ドライバーの所有権を取り戻す必要があることを示します、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)すぐに構造体します。 この場合は、NDIS 呼び出しませんフィルター ドライバーの[ *FilterReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549964)を返す関数、 **NET\_バッファー\_一覧**構造体。 フィルター ドライバーが所有権を得た直後後**NdisFIndicateReceiveNetBufferLists**を返します。

フィルター ドライバーが設定されていない場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820)、NDIS を返します、指定された[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造をフィルター ドライバーの[ *FilterReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549964)関数。 フィルター ドライバーが指定された構造体の所有権を解放する NDIS が返す順序にするまでこの場合、 *FilterReturnNetBufferLists*します。

**注**  フィルター ドライバーはの追跡を開始する指示を受け取り、呼び出しがないことを確認、 [ **NdisFReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562613)関数と、受信操作が完了しました。

 

### <a name="filtering-receive-indications"></a>受信の表示をフィルター処理

次の図に示しますをフィルター処理された受信は、基になるドライバーによって開始されたことを示しています。

![フィルターされたを示す図を基になるドライバーによって開始を示す値を受信します。](images/receivefilter.png)

NDIS フィルター ドライバーを呼び出す[ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)を処理する関数が基になるドライバーからインジケーターを受信します。 NDIS 呼び出し*FilterReceiveNetBufferLists*受信を示す値の関数を呼び出して、基になるドライバーから (たとえば、 [ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598))受信したネットワーク データまたはループバック データを示します。

場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)フィルター ドライバーの所有権が設定されている、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体にそれを呼び出すまで、 [ **NdisFReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562613)関数。

場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターが設定されている、フィルター ドライバーが保持することはできません、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造と関連付けられている基になるドライバーに割り当てられたリソース。 このフラグは、基になるドライバーが不足している分かりますでリソースを受信します。 [ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)関数がすぐに返す必要があります。

**注**  場合、 **NDIS\_受信\_フラグ\_リソース**フラグが設定されて、フィルター ドライバーは、元のセットを保持する必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)リンク リスト内の構造体。 たとえば、このフラグが設定されている場合、ドライバー可能性があります、構造を処理関数を返します前に、一度にいずれかのスタックを示すに、元のリンク リストを復元する必要があります。

 

フィルター ドライバーは、上にあるドライバーにデータを示す前に、受信したデータのフィルター操作を実行できます。 送信される各バッファーの[ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)関数フィルター ドライバーは、次を実行できます。

-   呼び出すことで、[次へ] の上にあるドライバーに渡して[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820)します。 ドライバーは、バッファーの内容を変更できます。 コンテキストの領域の可用性を保証する NDIS (を参照してください[NET\_バッファー\_一覧\_CONTEXT 構造](net-buffer-list-context-structure.md))。

    フィルター ドライバーに渡される NDIS 状態を変更できます[ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)に渡すだけで済みますまたは[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820).

    **注**  フィルター ドライバーを使用して、バッファーに渡すことができます[ **NdisFIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561820) NDIS 設定する場合でも、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ *FilterReceiveNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549960)します。 この場合、フィルター ドライバーから返す必要がありますいない*FilterReceiveNetBufferLists*まで、バッファーの所有権を再度獲得します。

     

-   バッファーを破棄します。 NDIS がオフにした場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ *FilterReceiveNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549960)を呼び出し、 [ **NdisFReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562613)バッファーを破棄する関数。 NDIS を設定する場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの*FilterReceiveNetBufferLists*、何もしないおよびから返す*FilterReceiveNetBufferLists*バッファーを破棄します。

-   後で処理するためのローカル データ構造内のバッファーをキューします。 NDIS を設定する場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ *FilterReceiveNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549960)から戻る前に、フィルター ドライバーがコピーを作成する必要があります*FilterReceiveNetBufferLists*します。

-   バッファーをコピーして、コピーを使用して、受信を示す値を生成します。 受信の表示は、受信のフィルター ドライバー開始を示す値に似ています。 この場合、ドライバーは、基になるドライバーに元のバッファーを返す必要があります。

[ **NdisFIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561820)関数の指定された一覧を渡します[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体がドライバーに関連するドライバー スタックをセットアップします。 受信操作は、受信のフィルターがドライバーで開始した操作に同様に進みます。

NDIS を呼び出す場合は、上にあるドライバーには、バッファーの所有権が保持される場合、 [ *FilterReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549964)フィルター モジュールの関数。 その*FilterReturnNetBufferLists*関数の場合、フィルター ドライバーは、受信を示す値のパス上のバッファーで実行された操作を元に戻します。

最下位のレイヤーのフィルター モジュールでは、バッファーで実行されたことを示します、NDIS はミニポート ドライバーにバッファーを返します。 NDIS がオフにした場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ *FilterReceiveNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549960)、フィルター ドライバーの呼び出し[ **NdisFReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562613)をバッファーを返します。 NDIS を設定する場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの*FilterReceiveNetBufferLists*から返される、 *FilterReceiveNetBufferLists*バッファーを返します。

 

 





