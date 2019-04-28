---
title: 暗号化\_型\_修飾子
description: 暗号化\_型\_修飾子
ms.assetid: a1caedb8-18ab-4810-ac46-691925df250e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5f5b6b6e139ed6eacb8df1b1712b909ecdbeb7ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380650"
---
# <a name="encryptiontypesqualifiers"></a>暗号化\_型\_修飾子


## <span id="ddk_encryption_types_qualifiers_kr"></span><span id="DDK_ENCRYPTION_TYPES_QUALIFIERS_KR"></span>


暗号化\_型\_修飾子 WMI プロパティ修飾子がどのような形式の暗号化、HBA をサポートしているかを示す値のグループに対応します。

次の表に、暗号化に関連付けられている値\_型\_修飾子プロパティ修飾子。

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
<td align="left"><p>ISCSI_ENCRYPT_NONE</p></td>
<td align="left"><p>ホスト バス アダプター (HBA) は、すべての暗号化や認証をサポートしていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_ENCRYPT_3DES_HMAC_SHA1</p></td>
<td align="left"><p>HBA には、3 des SHA1 HMAC/暗号化がサポートしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_ENCRYPT_AES_CTR</p></td>
<td align="left"><p>HBA には、AES CTR/CBC-MAC XCBC 暗号化がサポートしています。</p></td>
</tr>
</tbody>
</table>

 

 

 





