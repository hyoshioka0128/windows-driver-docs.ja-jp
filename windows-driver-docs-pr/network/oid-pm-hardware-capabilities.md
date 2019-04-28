---
title: OID_PM_HARDWARE_CAPABILITIES
description: クエリとして関連ドライバーを使用できます OID_PM_HARDWARE_CAPABILITIES OID ネットワーク アダプターのハードウェアの電源の管理機能を照会します。
ms.assetid: 52446584-bb73-4cf4-bda9-bf92ef2488e3
ms.date: 08/08/2017
keywords: -OID_PM_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 46da6ba6459bb342712f07af1d5638cc307bfed0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377578"
---
# <a name="oidpmhardwarecapabilities"></a>OID\_PM\_ハードウェア\_機能


クエリとしてドライバーを重なってできます OID を使用\_PM\_ハードウェア\_ネットワーク アダプターのハードウェアの電源の管理機能のクエリを実行する機能の OID。 OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)構造体。

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーにクエリを処理します。 以降では、NDIS 6.20 が動作は、ミニポート ドライバーを指定のハードウェアの電源管理機能の初期化中に、 **PowerManagementCapabilitiesEx**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)構造体。

ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_PM\_機能\_変更**](https://msdn.microsoft.com/library/windows/hardware/ff567410)電源の変更の報告に状態の表示NDIS および上にあるドライバーをネットワーク アダプターのハードウェア機能を管理します。

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


[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)

[**NDIS\_状態\_PM\_機能\_変更**](https://msdn.microsoft.com/library/windows/hardware/ff567410)

 

 




