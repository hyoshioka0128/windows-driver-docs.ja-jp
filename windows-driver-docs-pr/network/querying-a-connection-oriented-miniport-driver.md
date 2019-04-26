---
title: 接続指向ミニポート ドライバーのクエリ
description: 接続指向ミニポート ドライバーのクエリ
ms.assetid: 9e9926f6-cf90-48af-885f-59725721948d
keywords:
- 接続指向のドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b4de30e3ab57303a48b608173335fa4931e8c71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349436"
---
# <a name="querying-a-connection-oriented-miniport-driver"></a>接続指向ミニポート ドライバーのクエリ





バインドされているプロトコルを呼び出す接続指向のミニポート ドライバーを保持するオブジェクトの情報を照会する[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)渡します、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)を照会して、バッファーに NDIS 最終的に書き込み、必要な情報を提供するオブジェクト (OID) を指定します。 呼び出し**NdisCoOidRequest** NDIS ミニポート ドライバーを呼び出すと、 [ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362) NDIS に要求された情報を返す関数。 *MiniportCoOidRequest*への呼び出しでの同期または非同期で完了できます[ **NdisCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561716)します。

NDIS ミニポート ドライバーを呼び出すことも[ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)自身が代理としての関数-たとえば、ミニポート ドライバーの後[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数が NDIS を返しました\_状態\_成功: ミニポート ドライバーの機能、状態、または統計情報を照会します。 次の図は、接続指向のミニポート ドライバーにクエリを実行します。

![接続指向のミニポート ドライバーのクエリを実行するかを示す図](images/fig5-3.png)

接続指向のミニポート ドライバーでは、仮想とすべての接続 (VCs) の特定の NIC も VC あたりの単位でのグローバル ベースに関する情報を提供できる必要があります。 たとえば、以外の場合**NULL** *NdisVcHandle*に渡されます[ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)のクエリの[OID\_GEN\_CO\_受信\_CRC\_エラー](https://msdn.microsoft.com/library/windows/hardware/ff569562)、指定の vc ミニポート ドライバー返します CRC エラーが発生したすべてのエラーが数を受け取ります。 同じ要求で、 **NULL** *NdisVcHandle*、ミニポート ドライバーが発生した NIC が受け取るすべての受信の CRC エラーの合計数を返します

次の一覧には、接続指向のミニポート ドライバーに必須の一般的な運用 Oid のセットが含まれています。

[OID\_GEN\_CO\_サポートされている\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569567)

[OID\_GEN\_CO\_ハードウェア\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569452)

[OID\_GEN\_CO\_メディア\_サポートされています。](https://msdn.microsoft.com/library/windows/hardware/ff569558)

[OID\_GEN\_CO\_メディア\_IN\_使用](https://msdn.microsoft.com/library/windows/hardware/ff569557)

[OID\_GEN\_CO\_リンク\_速度](https://msdn.microsoft.com/library/windows/hardware/ff569453)

[OID\_GEN\_CO\_ベンダー\_ID](https://msdn.microsoft.com/library/windows/hardware/ff569571)

[OID\_GEN\_CO\_ベンダー\_の説明](https://msdn.microsoft.com/library/windows/hardware/ff569569)

[OID\_GEN\_CO\_ベンダー\_ドライバー\_バージョン](https://msdn.microsoft.com/library/windows/hardware/ff569570)

[OID\_GEN\_CO\_ドライバー\_バージョン](https://msdn.microsoft.com/library/windows/hardware/ff569449)

[OID\_GEN\_CO\_MAC\_オプション](https://msdn.microsoft.com/library/windows/hardware/ff569454)

[OID\_GEN\_CO\_メディア\_CONNECT\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569455)

[OID\_GEN\_CO\_最小\_リンク\_速度](https://msdn.microsoft.com/library/windows/hardware/ff569559)

ミニポート ドライバーの[ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)クエリまたは前の Oid のいずれかに、必要に応じて、セットに応答する関数を準備する必要があります。

ときに[ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362) OID を使用して呼び出した\_GEN\_CO\_MAC\_オプション、そのオプションを指定するビットマスクを返す必要がありますミニポート ドライバーを実行する操作です。 フラグのセットが含まれます。

-   NDIS\_MAC\_オプション\_いいえ\_ループバックします。 このフラグを設定するとに渡されるパケットにミニポート ドライバーがないループバック[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)は同じコンピューター上の受信者に送られますミニポート ドライバーNDIS ループバックを実行する必要があります。 NDIS は、パケットのループバックを実行する場合、パケットは渡されませんミニポート ドライバーに。 ミニポート ドライバーは、NIC がハードウェア ループバックを実行しない限り、常にこのフラグを設定します。

-   NDIS\_MAC\_ETOX\_を示す値。 このフラグが設定されている場合、ミニポート ドライバーでは、NIC は、パケットを送信した後にのみ、送信が完了したことを示します。

ミニポート ドライバーは、NDIS を使用しないでください必要があります\_MAC\_オプション\_予約済みフラグは、NDIS 内部使用のために予約されています。

[*MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)は、NIC の現在のアドレスを決定するメディア固有の OID を照会することもできます。

詳細については、次を参照してください。 [Connection-Oriented 呼び出す管理者とクライアントの Oid](https://msdn.microsoft.com/library/windows/hardware/ff569067)と[全般オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff546510)します。

 

 





