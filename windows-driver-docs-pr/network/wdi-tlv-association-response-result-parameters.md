---
title: WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS では、アソシエーションの応答の結果のパラメーターを含む TLV です。
ms.assetid: 8BF2C8B4-207E-479A-9903-3FCDEED5BA2C
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8278c7e46002e0501a1c14073e46233f619335a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342267"
---
# <a name="wditlvassociationresponseresultparameters"></a>WDI\_TLV\_アソシエーション\_応答\_結果\_パラメーター


WDI\_TLV\_アソシエーション\_応答\_結果\_パラメーターは、アソシエーションの応答の結果のパラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x76

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926071" data-raw-source="[&lt;strong&gt;WDI_MAC_ADDRESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926071)"><strong>WDI_MAC_ADDRESS</strong></a></td>
<td>ピアのアダプターの MAC アドレス。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>ピアのステーションからの要求が、要求を再関連付けであるかどうかを示すビット値。
<p>有効な値とは、0 および 1 です。 1 の値では、再関連付け要求であることを示します。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>ピアのステーションからの応答が応答を再関連付けであるかどうかを示すビット値。
<p>有効な値とは、0 および 1 です。 1 の値では、再関連付け応答であることを示します。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897792" data-raw-source="[&lt;strong&gt;WDI_AUTH_ALGORITHM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897792)"><strong>WDI_AUTH_ALGORITHM</strong></a></td>
<td>アソシエーションの認証アルゴリズムです。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897802" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897802)"><strong>WDI_CIPHER_ALGORITHM</strong></a></td>
<td>アソシエーションのユニキャストの暗号アルゴリズム。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897802" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897802)"><strong>WDI_CIPHER_ALGORITHM</strong></a></td>
<td>アソシエーションのマルチキャストの暗号アルゴリズム。</td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




