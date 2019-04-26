---
title: OID_PM_CURRENT_CAPABILITIES
description: クエリとして重なってドライバーを使用できます OID_PM_CURRENT_CAPABILITIES OID ネットワーク アダプターの現在使用できる電源管理機能を照会します。
ms.assetid: b35ce325-a1aa-43e0-bf68-cb2ab89dff76
ms.date: 08/08/2017
keywords: -OID_PM_CURRENT_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6f4fd0cffb105e0fd6967d118f8e0c33df59f1ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349462"
---
# <a name="oidpmcurrentcapabilities"></a>OID\_PM\_現在\_機能


クエリとしてドライバーを重なってできます OID を使用\_PM\_現在\_ネットワーク アダプターの現在使用できる電源管理機能のクエリを実行する機能の OID。 OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)構造体。

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーにクエリを処理します。 以降では、NDIS 6.20 が動作は、ミニポート ドライバーは、初期化中に、ハードウェアの電源管理機能を指定します。 ただし、NDIS は、プロトコル ドライバーからいくつかの機能を非表示にすることができます。 たとえば、NDIS は、ユーザーは、電源管理機能の一部またはすべて無効にします。 ときに、さまざまな機能を報告する可能性があります。

プロトコル ドライバーに NDIS を報告する現在の電源管理機能できないが必ずしもに NDIS ミニポート ドライバーが報告されたハードウェアの機能と同じに注意してください。

NDIS プロトコル ドライバーに関連する、基になるネットワーク アダプターの電源管理機能の報告、 **PowerManagementCapabilitiesEx**のメンバー、 [ **NDIS\_のバインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)バインド操作中に構造体。 そのため、プロトコルのドライバーは、OID をクエリにはありません。

NDIS 問題、 [ **NDIS\_状態\_PM\_機能\_変更**](https://msdn.microsoft.com/library/windows/hardware/ff567410)電源管理での変更を報告する状態の表示ドライバーに関連する使用可能な機能です。

基になるネットワーク アダプターは、NDIS 6.1 または古いミニポート ドライバーは、NDIS に変換する基になるネットワーク アダプターの電源管理機能、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)構造体。

NDIS は、要求の次のステータス コードのいずれかを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **InformationBuffer**を指す、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)構造体。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS では、要求が完了した後、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡すは。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状態\_バッファー\_すぎます\_短い  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded** NDIS でメンバー\_OID\_構造体を最小バッファー サイズを要求が必要です。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
上記の理由以外の理由、要求が失敗しました。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。 ミニポート ドライバーには要求されません。 (「解説」の「」を参照).</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_バインド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)

[**NDIS\_状態\_PM\_機能\_変更**](https://msdn.microsoft.com/library/windows/hardware/ff567410)

 

 




