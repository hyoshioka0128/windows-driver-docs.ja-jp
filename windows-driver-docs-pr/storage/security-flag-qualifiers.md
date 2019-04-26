---
title: セキュリティ\_フラグ\_修飾子
description: セキュリティ\_フラグ\_修飾子
ms.assetid: d5b4c3a6-1e05-497a-a0a6-be7908e61fec
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a7dfeebe177b90fbf5a0814b278b33e1d471f571
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356714"
---
# <a name="securityflagqualifiers"></a>セキュリティ\_フラグ\_修飾子


## <span id="ddk_security_flag_qualifiers_kr"></span><span id="DDK_SECURITY_FLAG_QUALIFIERS_KR"></span>


セキュリティ\_フラグ\_修飾子 WMI プロパティ修飾子がターゲットのセキュリティ要件を示すフラグ値に対応しています。 この情報は、IPsec 認証のネゴシエーションのインターネット キー交換 (IKE) で使用されます。 これらのフラグが記載されているポータルのセキュリティのビットマップ定義から派生した、*インターネット記憶域ネーム サービス (iSNS)* Internet Engineering Task Force (IETF) を発行する仕様。

次の表に、セキュリティに関連付けられている値\_フラグ\_修飾子プロパティ修飾子。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">シンボリック定数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_TUNNEL_MODE_PREFERRED</p></td>
<td align="left"><p>ターゲット要求トンネル モード。 HBA イニシエーターは、IPsec トンネル モードを使用して、ターゲットにログオンする必要があります。 この値が設定されていない場合は、IPsec トンネル モードは必要ありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_SECURITY_FLAG_TRANSPORT_MODE_PREFERRED</p></td>
<td align="left"><p>ターゲットは、トランスポート モードを要求します。 HBA イニシエーターは、IPsec トランスポート モードを使用してターゲットにログオンする必要があります。 この値が設定されていない場合は、IPsec トランスポート モードは必要ありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_PFS_ENABLED</p></td>
<td align="left"><p>HBA イニシエーターは、perfect forward secrecy () モードが有効なターゲットにログオンする必要があります。 この値が設定されていないときに、HBA イニシエーターは、PFS モードを無効になっているセッション接続を確立する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_SECURITY_FLAG_AGGRESSIVE_MODE_ENABLED</p></td>
<td align="left"><p>ターゲット、アグレッシブなモードが有効になり、積極的なモードが有効なターゲットに HBA イニシエーターにログオンする必要があります。 この値が設定されていないときに、HBA イニシエーターは、積極的なモードを無効になっているセッション接続を確立する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_MAIN_MODE_ENABLED</p></td>
<td align="left"><p>ターゲットのメイン モードが有効になり、メイン モードが有効なターゲットに HBA イニシエーターにログインする必要があります。 設定しない場合、HBA イニシエーターする必要があります、セッションの接続を使用してメイン モードを無効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_SECURITY_FLAG_IKE_IPSEC_ENABLED</p></td>
<td align="left"><p>ターゲット、IKE と IPsec が有効になり、HBA イニシエーターがターゲットにログオン Ike/ipsec プロトコルを有効にします。 この値が設定されていない Ike/ipsec は無効になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_VALID</p></td>
<td align="left"><p>このビットマスクで指定された iSCSI セキュリティのフラグは有効です。 この値が設定されていないときにセキュリティ フラグが指定されていません。</p></td>
</tr>
</tbody>
</table>

 

 

 





