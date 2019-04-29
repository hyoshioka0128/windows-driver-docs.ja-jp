---
title: パケット タグ付けの使用
description: パケット タグ付けの使用
ms.assetid: a151256b-d69f-4abb-bf68-644f157dfdd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec219e75870164c7a5810431868525d0b174302c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323326"
---
# <a name="using-packet-tagging"></a>パケット タグ付けの使用


コールアウト ドライバーは、関心のあるパケットをタグ付けし、タグ付きパケットに発生するイベントの通知を受信できます。 Windows 7 および Windows の以降のバージョンでは、パケットがタグ付けがサポートされています。

パケットがタグ付けを使用する、コールアウト ドライバーを実装する必要があります、 [ *FWPS\_NET\_バッファー\_一覧\_通知\_FN0* ](https://msdn.microsoft.com/library/windows/hardware/ff552406)または[*FWPS\_NET\_バッファー\_一覧\_通知\_FN1* ](https://msdn.microsoft.com/library/windows/hardware/hh451260)コールバック関数。 この関数は、すべてのタグ付きパケットのステータス通知に表示されます。 コールアウト ドライバーが、特別なコンテキスト タグを呼び出すことによって取得する必要があります前に、個々 のパケットをタグ付けすることができます、 [ **FwpsNetBufferListGetTagForContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551192)します。 コールアウト ドライバーでは、タグ付きパケットの一部またはすべてを同じコンテキストのタグを使用できます。 たとえば、別のコンテキストのタグを使用してタグ付きパケットの種類とコールアウト ドライバーを区別可能性があります。

タグをパケット、コールアウト ドライバーの使用に[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 コールアウト ドライバーへの呼び出しは、 [ **FwpsNetBufferListAssociateContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551191)タグを個々 に**NET\_バッファー\_一覧**構造体。 コールアウト ドライバーがパケットを関連付けますコンテキストは、任意の符号なし 64 ビット値です。 イベントがトリガーされたときに、 [ *FWPS\_NET\_バッファー\_一覧\_通知\_FN0* ](https://msdn.microsoft.com/library/windows/hardware/ff552406)または[ *FWPS\_NET\_バッファー\_一覧\_通知\_FN1* ](https://msdn.microsoft.com/library/windows/hardware/hh451260)コールアウト ドライバーが実行できるように、コールバックが入力パラメーターとしてコンテキストを渡します個々 のタグ付きパケットを識別します。 コンテキストの使用し、フィルター処理エンジンによって評価されます。 のみ渡されますコールバックに使用するため、コールアウト ドライバーによって。

パケットがスタックを離れるときにコンテキストがタグ付きパケットから自動的に削除されます。 ただし、パケット、TCP/IP スタックを入力しない場合などの場合は、NDIS フィルター ドライバーの — コンテキストは呼び出すことによって手動で削除する必要があります[ **FwpsNetBufferListRemoveContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551194)で*netBufferList*パラメーターに設定**NULL**します。

コンテキストを呼び出すことで削除できる吹き出しは、早期にタグ付けの操作を中止する必要がある場合、 [ **FwpsNetBufferListRemoveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551194)します。 一般に、コンテキストを削除するトリガーを**FWPS\_NET\_バッファー\_一覧\_コンテキスト\_から削除された**イベント。 トリガーできるイベントの詳細については、次を参照してください、 [ **FWPS\_NET\_バッファー\_一覧\_イベント\_TYPE0** ](https://msdn.microsoft.com/library/windows/hardware/ff552403) 。列挙体です。 イベントが発生しない場合によっては、パケットことはありませんが入ったとき、TCP/IP などの処理をスタックします。

タグ付きパケットを複製すると、コールアウト ドライバーが移動または複製パケットをコンテキストにコピーできます。 コールアウト ドライバーを呼び出す必要があります (複製) の場合、コンテキストに移動する[ **FwpsNetBufferListRetrieveContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551196)で、 *removeContext* にパラメーターが設定**TRUE**します。 コンテキストは、新しいパケットを関連付けることができます。 (重複) の場合、コンテキストをコピーするためのプロセスは、同じことを除いて、 *removeContext*パラメーターの**FwpsNetBufferListRetrieveContext0**に設定する必要があります**FALSE**.

TCP/IP のレイヤーからタグ付きパケットから取得できる、 [NDIS フィルター ドライバー](ndis-filter-drivers2.md)します。 この逆も当てはまります。 パケットがタグ付けは、パケットが示されていないデータ セグメントを除くのストリーム レイヤーから使用できません。

コールアウト ドライバーは、外側のパケットのコンテキストを取得できます、 [ *FWPS\_NET\_バッファー\_一覧\_通知\_FN0* ](https://msdn.microsoft.com/library/windows/hardware/ff552406)または[ *FWPS\_NET\_バッファー\_一覧\_通知\_FN1* ](https://msdn.microsoft.com/library/windows/hardware/hh451260)関数を呼び出して[ **FwpsNetBufferListRetrieveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551196)します。 コールアウト ドライバーがコンテキストを取得する通常、その[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)コールバック。

## <a name="related-topics"></a>関連トピック


[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)

[**FWPS\_NET\_バッファー\_一覧\_イベント\_TYPE0**](https://msdn.microsoft.com/library/windows/hardware/ff552403)

[*FWPS\_NET\_バッファー\_一覧\_通知\_FN0*](https://msdn.microsoft.com/library/windows/hardware/ff552406)

[*FWPS\_NET\_バッファー\_一覧\_通知\_FN1*](https://msdn.microsoft.com/library/windows/hardware/hh451260)

[**FwpsNetBufferListAssociateContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551191)

[**FwpsNetBufferListGetTagForContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551192)

[**FwpsNetBufferListRemoveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551194)

[**FwpsNetBufferListRetrieveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551196)

[**NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[NDIS フィルター ドライバー](ndis-filter-drivers2.md)

 

 






