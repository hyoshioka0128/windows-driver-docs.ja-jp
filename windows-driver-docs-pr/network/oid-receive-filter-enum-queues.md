---
title: OID_RECEIVE_FILTER_ENUM_QUEUES
description: 上にあるドライバーとユーザー モード アプリケーションは、オブジェクト識別子 OID_RECEIVE_FILTER_ENUM_QUEUES のネットワーク アダプターに割り当てられているすべての受信キューの一覧を取得する (OID) のクエリを要求を発行します。
ms.assetid: e8a946a2-9ee9-42a0-8175-fbc592d404d1
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_ENUM_QUEUES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e6f81be0b7e2db312be29601ce16a8f1fda2f07b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380888"
---
# <a name="oidreceivefilterenumqueues"></a>OID\_受信\_フィルター\_ENUM\_キュー


上にあるドライバーとユーザー モード アプリケーション発行オブジェクト識別子 (OID) のクエリ要求の OID\_受信\_フィルター\_ENUM\_ネットワーク上に割り当てられたすべての受信キューの一覧を取得するキューアダプター。

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_受信\_キュー\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567205)が続く構造体、 [**NDIS\_受信\_キュー\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567204)各フィルターの構造体。

<a name="remarks"></a>注釈
-------

NDIS から受信したデータの内部キャッシュからの情報の取得、 [OID\_受信\_フィルター\_ALLOCATE\_キュー](oid-receive-filter-allocate-queue.md)と[OID\_受信\_フィルター\_キュー\_パラメーター](oid-receive-filter-queue-parameters.md) OID 要求。

上にあるドライバーとユーザー モード アプリケーションは、OID の OID クエリ要求を発行\_受信\_フィルター\_ENUM\_ネットワーク アダプターの受信キューを列挙するキュー。

内で、要求の入力プロトコル ドライバーには、要求が発行した場合、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に設定されている**NdisRequestQueryInformation**この OID は、ネットワーク アダプターのプロトコル ドライバーに割り当てられているすべての受信キューの配列を返します。 内で、要求の種類、ユーザー モード アプリケーションが要求を発行した場合、 **NDIS\_OID\_要求**構造に設定されている**NdisRequestQueryStatistics**、し、この OID を返しますネットワーク アダプターに、すべての受信キューに関する情報の配列。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_受信\_フィルター\_ENUM\_ミニポート ドライバー、および次のステータス コードを返します。 1 つのキュー。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>要求は正常に完了しました。 <strong>InformationBuffer</strong>を指す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567205" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_INFO_ARRAY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567205)"> <strong>NDIS_RECEIVE_QUEUE_INFO_ARRAY</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>完了待ちになっています。 NDIS では、要求が完了した後、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡すは。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ</strong>.<strong>METHOD_INFORMATION</strong>.<strong>BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_受信\_キュー\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567204)

[**NDIS\_受信\_キュー\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567205)

[OID\_受信\_フィルター\_ALLOCATE\_キュー](oid-receive-filter-allocate-queue.md)

[OID\_受信\_フィルター\_キュー\_パラメーター](oid-receive-filter-queue-parameters.md)

 

 




