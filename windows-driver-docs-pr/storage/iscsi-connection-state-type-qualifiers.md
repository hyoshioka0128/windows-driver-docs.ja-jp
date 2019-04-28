---
title: ISCSI\_接続\_状態\_型\_修飾子
description: ISCSI\_接続\_状態\_型\_修飾子
ms.assetid: 53242205-4fd3-471d-abe2-35474491b29d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: de5a7bebe25dc2c725ef2cd32e8b8078db200dff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372761"
---
# <a name="iscsiconnectionstatetypequalifiers"></a>ISCSI\_接続\_状態\_型\_修飾子


## <span id="ddk_iscsi_connection_state_type_qualifiers_kr"></span><span id="DDK_ISCSI_CONNECTION_STATE_TYPE_QUALIFIERS_KR"></span>


ISCSI\_接続\_状態\_型\_修飾子 WMI プロパティ修飾子は、接続状態を表す値のグループに対応します。

次の表に、ISCSI\_接続\_状態\_型\_修飾子の値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">接続状態の値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>ログオン要求フェーズでの接続です。 接続が確立されているが、引き続き、ターゲットは、最終的なビットが設定された有効なログオン応答送信されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>ターゲットが、最終的なビットが設定された有効なログオンの応答を送信接続が完全な機能のフェーズでは、イニシエーターがターゲットに SCSI コマンドとデータを送信できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>イニシエーターが有効なログオフのコマンドを送信しますが、接続がまだ終了していません。</p></td>
</tr>
</tbody>
</table>

 

 

 





