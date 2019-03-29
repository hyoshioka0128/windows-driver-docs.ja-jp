---
title: OID_NDK_LOCAL_ENDPOINTS
description: クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーションはミニポート アダプターで Network Direct のアクティブなリスナーと共有のエンドポイントの一覧に OID_NDK_LOCAL_ENDPOINTS OID を使用します。
ms.assetid: 93F077AF-7FEA-4F92-9784-B65ADCC16564
ms.date: 08/08/2017
keywords: -OID_NDK_LOCAL_ENDPOINTS ネットワークのドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 38c933f3bb7d077d9676c79a6ac45661d8514fb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572283"
---
# <a name="oidndklocalendpoints"></a>OID\_NDK\_ローカル\_エンドポイント


クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーション使用 OID\_NDK\_ローカル\_Network Direct のアクティブなリスナーとミニポート アダプター上の共有のエンドポイントの一覧にエンドポイントの OID。

NDIS 6.30 と以降のミニポート ドライバー NDK サービスを提供するには、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>コメント
-------

NDIS は、アダプターから Network Direct のアクティブなリスナーと共有のエンドポイントの一覧を取得するには、この OID を発行します。 リスナーと共有のエンドポイントのリストを返すため、アダプターが必要な[ **NDIS\_NDK\_ローカル\_エンドポイント**](https://msdn.microsoft.com/library/windows/hardware/hh451563)で構造体**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。

この構造体には返されるローカル エンドポイントの数に基づく可変サイズです。 要素の数として、ローカル エンドポイントの配列のサイズがで指定された、**カウント**メンバー。

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
<td><p>サポートなし</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_NDK\_ローカル\_エンドポイント**](https://msdn.microsoft.com/library/windows/hardware/hh451563)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




