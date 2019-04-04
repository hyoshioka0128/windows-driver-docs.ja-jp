---
title: フィルターは受信パケットの結合の変更
description: フィルターは受信パケットの結合の変更
ms.assetid: 082A969F-2977-482A-B060-ED8D353EC2E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be351199b52214ac3c72f8b07518bdecc2813a8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549140"
---
# <a name="modifying-packet-coalescing-receive-filters"></a>フィルターは受信パケットの結合の変更


パケットの結合をサポートしているミニポート ドライバーに対する受信フィルターを変更するに、上位のプロトコルまたはフィルター ドライバーは、次の手順を実行します。

1.  上にあるドライバーがの OID メソッド要求を発行するミニポート ドライバーにダウンロードされているフィルターをすべての受信パケットの結合の一覧を取得する[OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)構造体。

    **注**上にあるドライバーまたはアプリケーションを初期化するときに、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)設定する必要があります、構造、 **QueueId** NDIS メンバー\_既定\_受信\_キュー\_id。

    OID メソッド要求から正常に戻った後[OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造には、更新されたへのポインターが含まれる[ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)構造体が 1 つまたは複数続く[ **NDIS\_受信\_フィルター\_情報** ](https://msdn.microsoft.com/library/windows/hardware/ff567176)構造体。 各**NDIS\_受信\_フィルター\_情報**構造体は、ネットワーク アダプターに設定されているフィルターの識別子 (ID) を指定します。

2.  特定のパケットのパラメーターを取得する結合フィルターの上にあるドライバーの問題 OID メソッド要求のミニポート ドライバーにダウンロードされたを受信[OID\_受信\_フィルター\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569792). **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。 上にあるドライバーまたはアプリケーションの初期化、 **NDIS\_受信\_フィルター\_パラメーター**構造体を設定して、 **FilterId**メンバーを 0 以外の IDパラメーターが返されるフィルターの値。

    OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体バッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

    -   [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181) NDIS 受信フィルターのパラメーターを指定する構造体。

    -   配列の[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)フィルターを指定する構造体は、フィールドを 1 つの条件をテストします。ネットワーク パケットのヘッダー。

3.  上にあるドライバーは、追加、削除、またはテスト条件のフィルターのセットを変更するには、受信フィルターを変更します。 ドライバーは追加、削除、または個々 の変更によって[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)から構造体指定されたフィールド パラメーターの配列、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。

    メンバーを更新する必要があります、上にあるドライバーには、テスト条件への変更が完了したら、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)受信フィルターに加えられた変更を反映するように構造体。 たとえば、上にあるドライバーを更新する必要があります、 **FieldParametersArrayNumElements**メンバーを含む新しい配列の要素数。

    詳細については、[パケット結合受信フィルターを指定する](specifying-a-packet-coalescing-receive-filter.md)を参照してください。

4.  上にあるドライバーの OID メソッド要求を発行する[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)ミニポート ドライバーに変更された受信フィルターをダウンロードします。

    詳細については、[パケット結合受信フィルターを設定](setting-a-packet-coalescing-receive-filter.md)を参照してください。









