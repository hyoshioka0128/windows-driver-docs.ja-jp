---
title: EFI_CHECKSIG_PROTOCOL.EfiCheckSignatureAndHash
description: EFI_CHECKSIG_PROTOCOL.EfiCheckSignatureAndHash
ms.assetid: 7c6d1756-a3db-4754-9edb-af6ba1ecf65b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1957ac140db9ba79a90297385a8523e074fbbeec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571775"
---
# <a name="efichecksigprotocolefichecksignatureandhash"></a>EFI\_CHECKSIG\_プロトコル。EfiCheckSignatureAndHash


この関数は、デバイス上の主キーに対して FFU でカタログ ファイルの署名を確認します。 ハッシュ テーブルのハッシュが、カタログ ファイルで指定されたハッシュと一致することも確認します。

## <a name="syntax"></a>構文


```cpp
typedef EFI_STATUS
(EFIAPI * EFI_CHECK_SIG_AND_HASH) (
  IN EFI_CHECKSIG_PROTOCOL *This,
  IN UINT8 *pbCatalogData,
  IN UINT32 cbCatalogData,
  IN UINT8 *pbHashTableData,
  IN UINT32 cbHashTableData
);
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
\[\]へのポインター、 **EFI\_CHECKSIG\_プロトコル**インスタンス。

<a href="" id="pbcatalogdata"></a>*pbCatalogData*  
\[\]カタログ データへのポインター。

<a href="" id="cbcatalogdata"></a>*cbCatalogData*  
\[\] (バイト単位)、カタログ データのサイズ。

<a href="" id="pbhashtabledata"></a>*pbHashTableData*  
\[\]ハッシュ テーブルのデータへのポインター。

<a href="" id="cbhashtabledata"></a>*cbHashTableData*  
\[\] (バイト単位)、ハッシュ テーブルのデータのサイズ。

## <a name="return-value"></a>戻り値


次のステータス コードのいずれかを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リターン コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p></td>
<td><p>関数が正常に返され、ハッシュ テーブルのカタログ署名が無効です。</p></td>
</tr>
<tr class="even">
<td><p>EFI_SECURITY_VIOLATION</p></td>
<td><p>カタログ署名またはハッシュ テーブルが無効です。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>パラメーターが無効です。</p></td>
</tr>
<tr class="even">
<td><p>EFI_NO_MAPPING</p></td>
<td><p>内部エラーが発生しました。たとえば、PK はしないが正常にプロビジョニングします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>コメント


この関数の呼び出しは同期です。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




