---
title: NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE を使用して、OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE によって送信された AP アソシエーションの応答に関する情報を示します。
ms.assetid: c8bfa3b3-5d22-4831-9355-94c62fed7fd4
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 461b34d968899f5a354edadc68e60afad9b9d014
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361030"
---
# <a name="ndisstatuswdiindicationsendapassociationresponsecomplete"></a>NDIS\_状態\_WDI\_INDICATION\_送信\_AP\_アソシエーション\_応答\_完了


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_送信\_AP\_アソシエーション\_応答\_についての情報を示す完了、アジア太平洋アソシエーションの応答で送信される[OID\_WDI\_タスク\_送信\_AP\_アソシエーション\_応答](oid-wdi-task-send-ap-association-response.md)します。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- |
| [**WDI\_TLV\_アソシエーション\_応答\_結果\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn926138) |   |   | アソシエーションの応答パラメーター。 |
| [**WDI\_TLV\_アソシエーション\_応答\_フレーム**](https://msdn.microsoft.com/library/windows/hardware/dn926135) |   |   | 受信したアソシエーションの応答です。 これは、802.11 MAC ヘッダーには含まれません。 |
| [**WDI\_TLV\_BEACON\_IES**](https://msdn.microsoft.com/library/windows/hardware/dn926148) |   |   | アソシエーションからビーコン IEs します。 |
| [**WDI\_TLV\_PHY\_型\_一覧**](https://msdn.microsoft.com/library/windows/hardware/dn898029) |   |   | PHY 型のリスト。 |
 

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
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




