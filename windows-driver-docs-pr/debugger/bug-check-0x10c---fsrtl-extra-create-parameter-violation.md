---
title: バグ チェック 0x10C FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION
description: FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION のバグ チェックでは、0x0000010C FsRtl ECP パッケージで違反が検出されたことを示す値を持ちます。
ms.assetid: b702b182-696a-4233-8bd0-23a52ab2ddc4
keywords:
- バグ チェック 0x10C FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION
- FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c2100206135c058015ee1e95e2018f95869db059
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521421"
---
# <a name="bug-check-0x10c-fsrtlextracreateparameterviolation"></a>バグ チェック 0x10C:FSRTL\_余分な\_作成\_パラメーター\_違反


FSRTL\_余分な\_作成\_パラメーター\_違反のバグ チェックが 0x0000010C の値を持ちます。 これは、ファイル システムのランタイム ライブラリ (FsRtl) 余分な作成パラメーター (ECP) パッケージの違反が検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="fsrtlextracreateparameterviolation-parameters"></a>FSRTL\_余分な\_作成\_パラメーター\_違反パラメーター


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
<td align="left"><p>1</p></td>
<td align="left"><p>違反の型。 (参照次の表に、後でこのページの詳細)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>ECP のアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ECP リストの開始アドレス。</p></td>
</tr>
</tbody>
</table>

 

パラメーター 1 の値では、違反の種類を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">種類の違反</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>ECP 署名が有効で、無効なポインターまたはメモリの破損が原因です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>ECP のフラグのセットが定義されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>ECP、FsRtl によって割り当てられていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>ECP には、作成の呼び出し元によって渡されたパラメーターに対して有効でないフラグのセットがあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>ECP が破損しています。そのサイズは、ヘッダーのサイズより小さいです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>対象となる ECP が空でないリストのポインター。一部 ECP リストのある可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>ECP リスト署名が有効で、無効なポインターまたはメモリの破損が原因です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>ECP 一覧には、フラグのセットが定義されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>ECP 一覧は、FsRtl によって割り当てられていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ECP リストが、作成の呼び出し元によって渡されるパラメーターのリストに対して有効でないをフラグの設定にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>作成の呼び出し元によって渡される ECP 一覧が空です。</p></td>
</tr>
</tbody>
</table>

 

 

 




