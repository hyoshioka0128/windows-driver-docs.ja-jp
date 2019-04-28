---
title: ミニポート アダプターの OID 要求の処理
description: ミニポート アダプターの OID 要求の処理
ms.assetid: 0819ef06-5715-4814-a1ed-ddc757728ec4
keywords:
- ミニポート ドライバー WDK ネットワーク、OID 要求
- Oid WDK ネットワー キング、ミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d35af0dd923aaa5c3e4d4cd6103b56a2d4aa5333
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379056"
---
# <a name="handling-oid-requests-in-a-miniport-adapter"></a>ミニポート アダプターの OID 要求の処理





NDIS ミニポート ドライバーを呼び出す[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)クエリまたはドライバーの情報を設定する OID 要求を送信する関数。 NDIS 呼び出し、 *MiniportOidRequest*関数自身が代理として、または呼び出される上位のドライバーの代わり、 [ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)または[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)関数。

NDIS 渡します*MiniportOidRequest*へのポインター、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)要求情報を含む構造体。 要求の構造には、OID が含まれています。\_要求データを定義するには、要求とその他のメンバーの種類を示す Xxx 識別子。

**タイムアウト**メンバーは、秒単位の要求で、タイムアウトを指定します。 NDIS は、ドライバーをリセットしたり、ドライバーは、要求を完了する前にタイムアウトに達すると、要求をキャンセルできます。

**RequestId**メンバーは、要求のオプションの識別子を指定します。 ミニポート ドライバーを設定できる、 **RequestId**から取得した値に状態表示のメンバー、 **RequestId**関連付けられている OID 要求のメンバー。 通常、ミニポート ドライバーでは、このメンバーを無視できます。 ドライバーは、このメンバーを設定する必要があります、特定の OID のリファレンス ページは、必要な値を提供します。 状態インジケーターの詳細については、次を参照してください。[アダプター状態のインジケーター](miniport-adapter-status-indications.md)します。

OID のセット要求を正常に処理するミニポート ドライバーを設定する必要があります、 **SupportedRevision**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)OID セットの要求からの戻り時に構造体。 **SupportedRevision**メンバーのリビジョン、ドライバーがサポートされている要求の発信側に通知します。 たとえば、ミニポート ドライバーが、Xxx を作成できます\_リビジョン\_2 構造、および、Xxx の適切な値を指定\_リビジョン\_1 の構造、およびゼロの構造体の残りの部分の塗りつぶし。 ミニポート ドライバーの Xxx は報告\_リビジョン\_で 1、 **SupportedRevision**メンバー。 ここで、Xxx をサポートできるプロトコル ドライバー\_リビジョン\_2 が Xxx を使用して\_リビジョン\_ミニポート ドライバーがサポートされている 1 つの情報。 NDIS 構造のバージョン情報の詳細については、次を参照してください。 [NDIS バージョン情報を指定する](specifying-ndis-version-information.md)します。

ミニポート ドライバーは、成功または失敗の状態を返すことによって、OID 要求を同期的に完了できます。

ミニポート ドライバーが NDIS を返すことによって、OID 要求を非同期的に実行できる\_状態\_保留します。 この場合、ミニポート ドライバーを呼び出す必要があります、 [ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)操作を完了する関数。

場合*MiniportOidRequest* NDIS を返します\_状態\_保留中、NDIS を呼び出すことがない*MiniportOidRequest*で別の要求を保留中の要求になるまでアダプター完了しました。

NDIS ミニポート ドライバーを呼び出すことができます[ *MiniportCancelOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559339) OID 要求をキャンセルする関数。

 

 





