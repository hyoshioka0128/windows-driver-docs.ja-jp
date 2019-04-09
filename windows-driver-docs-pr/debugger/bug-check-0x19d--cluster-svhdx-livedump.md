---
title: バグ チェック 0x19D CLUSTER_SVHDX_LIVEDUMP
description: CLUSTER_SVHDX_LIVEDUMP のバグ チェックでは、0x0000019D の値を持ちます。 これは、SVHDX に一貫性のない状態をデバッグする際にこの livedump が開始されたことを示します。
ms.assetid: E261617D-E84A-4644-8854-53A189395637
keywords:
- バグ チェック 0x19D CLUSTER_SVHDX_LIVEDUMP
- CLUSTER_SVHDX_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CLUSTER_SVHDX_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 180e322a24959e17b677e7da7c5c63bc1a56fea9
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239513"
---
# <a name="bug-check-0x19d-clustersvhdxlivedump"></a>バグ チェック 0x19D:クラスター\_SVHDX\_LIVEDUMP


クラスター\_SVHDX\_LIVEDUMP バグ チェックが 0x0000019D の値を持ちます。 これは、SVHDX に一貫性のない状態をデバッグする際にこの livedump が開始されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="clustersvhdxlivedump-parameters"></a>クラスター\_SVHDX\_LIVEDUMP パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>理由コード</p>
<p>0x1:マウントの共有仮想ディスクが失敗しました</p>
2-アドレスの Svhdxflt! _SVHDX_VIRTUALDISK_CONTEXT 3 - nt のアドレス _FILE_OBJECT 4 - NTSTATUS。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

SVHDX を検出する現在の状態では、なんらかの不整合が発生すると、この状態コードのライブのダンプが生成されます。 パラメーター 1 がコードの作成はこのライブ ダンプをどのようなシナリオをポイントします。 その他のパラメーターは、理由コードのコンテキストで解釈する必要があります。

 

 




