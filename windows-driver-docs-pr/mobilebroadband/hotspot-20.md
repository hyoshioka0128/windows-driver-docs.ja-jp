---
title: Hotspot 2.0
description: Hotspot 2.0
ms.assetid: 4dbd242d-8745-4ab2-b1dc-9f9dd9a73b42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ba7481b0669a20179ea355c5e0fd9b3726abca3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580769"
---
# <a name="hotspot-20"></a>Hotspot 2.0


ホット スポット 2.0 は、ホット スポットにシームレスな認証の標準です。 ホット スポット 2.0 では、クライアントとアクセス ポイント間の暗号化接続を提供します。 IEEE 802.11u、接続を確立する前に、プロバイダーとの通信に使用します。 認証と暗号化は、いくつかの EAP メソッドのいずれかと共に/wpa2-エンタープライズを使用して提供されます。

次の表では、ホット スポット 2.0 で定義されている一般的な資格情報の種類について説明します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Credential</th>
<th>EAP メソッド</th>
<th>サポートされている EAP メソッド</th>
<th>ユーザーが資格情報を入力できます。</th>
<th>演算子は、資格情報をプロビジョニングできます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ユーザー名とパスワード</p></td>
<td><p>EAP-TTLS</p></td>
<td><p>はい</p></td>
<td><p>[はい]</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Certificate</p></td>
<td><p>EAP-TTLS</p></td>
<td><p>はい</p></td>
<td><p>うん<em></p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>SIM</p></td>
<td><p>EAP SIM または EAP AKA</p></td>
<td><p>はい</p></td>
<td><p>[はい]</em></p></td>
<td><p>はい</p></td>
</tr>
</tbody>
</table>

 

\*ユーザーが証明書から選択するか、SIM では既にシステムに存在します。

Windows 8 および Windows 8.1 のホット スポット 2.0 では、オンラインのサインアップ一部または検出をサポートはありませんが、WPA2-エンタープライズとホット スポット 2.0 仕様で必要なすべての EAP メソッドをサポートしています。 そのため、Windows 8 および Windows 8.1 は、ユーザーが既に資格情報とホット スポット 2.0 ネットワークに接続できます。

Windows 8 および Windows 8.1 は 802.11u をサポートしないため、探索演算子する必要がありますプロビジョニング Windows 8 または Windows 8.1 と、適用可能なネットワークの Ssid を含むワイヤレス プロファイルです。

Windows 10 には、ホット スポット 2.0 Release 1、検出およびプロファイルの作成を含む完全にサポートしています。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ホット スポット認証方法](hotspot-authentication-methods.md)

 

 






