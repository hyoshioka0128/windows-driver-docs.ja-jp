---
title: 断片化された NET_BUFFER_LIST 構造体
description: 断片化された NET_BUFFER_LIST 構造体
ms.assetid: a72bc0cf-8c92-4c3e-ad10-710e5b93c74c
keywords:
- NET_BUFFER_LIST
- 断片化された構造体の WDK ネットワーク
- 分割データ構造体の WDK ネットワーク
- 親/子 NET_BUFFER_LIST リレーションシップ WDK ネットワーク
- 子/親 NET_BUFFER_LIST リレーションシップ WDK ネットワーク
- WDK NET_BUFFER_LIST のリレーションシップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a3ae0737449e89f582b33bd74d589ce8bc84c4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539374"
---
# <a name="fragmented-netbufferlist-structures"></a>NET の断片化\_バッファー\_リストの構造体





NDIS ドライバーをフラグメントに作成できます[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)既存のネットから構造\_バッファー\_リスト構造体。 断片化された構造体のセットを参照する[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体を参照する、元のデータは、データを最大サイズを超えない単位に分割するただし、します。 ドライバーは、大きなバッファー サイズより小さなバッファーを効率的に分割するこの種類の構造体を使用できます。

次の図は、親 NET 間の関係を示します\_バッファー\_リスト構造と断片化の子。

![net の親の間の関係を示す図\-バッファー\-構造と断片化の子構造体を一覧表示](images/netbufferlistfragment.png)

上記の図には、親が含まれています。 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造とその親から派生した子構造体。 親の構造体が 1 つ[ **NET\_バッファー\_一覧\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff568389)構造と 1 つ[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) MDLs 接続を含む構造体。 親構造体の親ポインターが**NULL**派生構造ではないことを示します。

子 NET\_バッファー\_リスト構造が 3 つの NET\_MDLs アタッチによるバッファーの構造体。 子 NET\_バッファー\_リスト構造が親構造体へのポインター。 **NULL**場合、NET\_バッファー\_一覧\_コンテキスト構造体のポインターは、子に NET がないことを示しますなります\_バッファー\_一覧\_コンテキスト構造体。

NDIS ドライバー呼び出し、 [ **NdisAllocateFragmentNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff560707)新たに作成する関数が断片化している[ **NET\_バッファー\_]ボックスの一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)既存のネットワーク内のデータに基づく構造\_バッファー\_リスト構造体。 NDIS が新しい割り当て[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造と断片化の NET の MDLs\_バッファー\_リスト構造体。 NDIS は割り当てられません、 [ **NET\_バッファー\_一覧\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff568389)断片化された構造体の構造体。 フラグメント NET\_バッファーの構造と MDLs 親構造体と同じデータを記述します。 データはコピーされません。

**NdisAllocateFragmentNetBufferList**作成の開始から、フラグメント、*使用中のデータ領域*NET の各親の\_バッファーの構造と、で指定された値のオフセット*StartOffset*パラメーター。

[**NdisAllocateFragmentNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff560707)分割、*使用データ領域*NET の各ソースで\_フラグメントにバッファーの構造体。 長さ、*使用データ領域*各フラグメントがで指定された値以下、 *MaximumLength*パラメーター。 *使用データ領域*、最後のフラグメントができるより小さい*MaximumLength* 。 新しい NET のデータ オフセット\_で指定されたバイト数でバッファーの構造体が割り込んで、 *DataOffsetDelta*パラメーター。

複数ある場合は[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)親内の構造体[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造 (の図に示されていません) するプロセスの各ネットワーク\_バッファーの構造は、同じ 1 つの構造です。 たとえば、次のいずれかにデータの最後の部分は親 NET\_バッファーの構造が最大サイズより小さい、NDIS は、[次へ] の NET の開始時のデータには、このようなデータを結合していない\_バッファーの構造体。

NDIS ドライバー呼び出し、 [ **NdisFreeFragmentNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff561847) 、NET の解放関数\_バッファー\_リスト構造とすべての関連する NET\_バッファーの構造体以前の呼び出しによって割り当てられた MDL チェーン[ **NdisAllocateFragmentNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff560707)します。

## <a name="related-topics"></a>関連トピック


[NET の派生\_バッファー\_リストの構造体](derived-net-buffer-list-structures.md)

 

 






