---
title: OID_GEN_HD_SPLIT_PARAMETERS
description: セットとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーションは、現在のヘッダー データ ミニポート アダプターの分割の設定を設定するのに OID_GEN_HD_SPLIT_PARAMETERS OID を使用します。
ms.assetid: 1b33c601-4302-4f63-8265-b75889b42d42
ms.date: 08/08/2017
keywords: -OID_GEN_HD_SPLIT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b593f58e8f3b110ece32602633eccd773de2540c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573175"
---
# <a name="oidgenhdsplitparameters"></a>OID\_GEN\_HD\_分割\_パラメーター


セットとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーションで、OID が使用\_GEN\_HD\_分割\_を現在のヘッダー データを設定するパラメーターの OID がミニポート アダプターの設定を分割します。 NDIS 6.1 と以降のミニポート ドライバー ヘッダー データの分割サービスを提供するには、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>コメント
-------

**InformationBuffer**のメンバー [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [ **NDIS\_HD\_分割\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565701)構造体。

NDIS 設定 OID\_GEN\_HD\_分割\_、NDIS 5 時にパラメーターの OID *。x*プロトコル ドライバーは、NDIS 6.1 ミニポートにバインドします。 ミニポート アダプターの更新の NDIS ミニポート ドライバーに渡す前にこの OID を処理および **\*HeaderDataSplit**必要な場合は、キーワードを標準化します。 ヘッダー データの分割が無効になっている場合は、NDIS はミニポート アダプターにこの OID を送信しません。

NDIS この OID に送付ミニポート ドライバーで NDIS ヘッダー データの分割が有効になっている場合にのみ\_HD\_分割\_を有効にする\_ヘッダー\_データ\_分割フラグ、 [**NDIS\_HD\_分割\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565694)ミニポートの初期化中に構造体。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.1 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_HD\_分割\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565694)

[**NDIS\_HD\_分割\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff565701)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




