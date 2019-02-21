---
title: 割り当てられているキューを列挙します。
description: 割り当てられているキューを列挙します。
ms.assetid: 4566314b-ea6b-49e2-bc85-946ed303bc6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d98d094b1ca254456dcd9ccda7194c1eafeca145
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552679"
---
# <a name="enumerating-the-allocated-queues"></a>割り当てられているキューを列挙します。





すべての受信キューの一覧を取得するに割り当てられたネットワーク アダプターでは、上位のドライバーの問題、 [OID\_受信\_フィルター\_ENUM\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569788)クエリ OID 要求。 OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_受信\_キュー\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567205)が続く構造体、 [**NDIS\_受信\_キュー\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567204)キューごとに構造体。

NDIS 処理 OID\_受信\_フィルター\_列挙\_ミニポート ドライバーのキュー クエリ OID 要求。 NDIS から受信したデータの内部キャッシュからの情報の取得、 [OID\_受信\_フィルター\_ALLOCATE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569784)と[OID\_受信\_フィルター\_キュー\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569794) OID 要求。

OID を使用できるドライバーとユーザー モード アプリケーションが重なって\_受信\_フィルター\_ENUM\_ネットワーク アダプターの受信キューを列挙するためにクエリ要求をキューの OID。

要求の種類のプロトコル ドライバーには、要求が発行した場合、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に設定されている**NdisRequestQueryInformation**し、この OID は、ネットワーク アダプターのプロトコル ドライバーに割り当てられているすべての受信キューの配列を返します。 ユーザー モード アプリケーションが要求を発行した場合、要求入力、NDIS\_OID\_要求に設定**NdisRequestQueryStatistics**、この OID が上のすべての受信キュー情報の配列を返しますミニポート アダプター。

 

 





