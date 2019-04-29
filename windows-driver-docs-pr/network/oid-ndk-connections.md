---
title: OID_NDK_CONNECTIONS
description: クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーションはミニポート アダプターからのアクティブな直接ネットワーク接続の一覧を照会するのに OID_NDK_CONNECTIONS OID を使用します。
ms.assetid: 31A0BB2B-B571-4548-A9D1-BE44687DEA37
ms.date: 08/08/2017
keywords: -OID_NDK_CONNECTIONS ネットワークのドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9c15dd731ddd5dec5fb1d7d67b389fe4c4ffc1e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383599"
---
# <a name="oidndkconnections"></a>OID\_NDK\_接続


クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーション使用 OID\_NDK\_ミニポート アダプターからのアクティブな直接ネットワーク接続の一覧を照会する接続の OID。

NDIS 6.30 と以降のミニポート ドライバー NDK サービスを提供するには、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>注釈
-------

NDIS は、アダプターから Network Direct のアクティブな接続の一覧を取得するには、この OID を発行します。 アダプターとの接続の一覧を返す必要があります、 [ **NDIS\_NDK\_接続**](https://msdn.microsoft.com/library/windows/hardware/hh451561)で構造体、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。

この構造体には返される接続の数に基づく可変サイズです。 要素の数として、接続の配列のサイズがで指定された、**カウント**メンバー。

<a name="requirements"></a>要件
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


[**NDIS\_NDK\_接続**](https://msdn.microsoft.com/library/windows/hardware/hh451561)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




