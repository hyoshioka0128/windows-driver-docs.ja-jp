---
title: カスタマイズされた OID と状態の表示
description: カスタマイズされた OID と状態の表示
ms.assetid: 675aff2c-8e4a-4a02-8d08-0f59b8fcd4a2
keywords:
- 状態インジケーターの WDK ネットワー キング、WMI
- WMI の WDK は、ネットワーク状態インジケーター
- Windows Management Instrumentation WDK ネットワー キング、状態インジケーター
- カスタム Oid WDK ネットワーク
- カスタム ステータス インジケーターの WDK ネットワーク
- WMI の WDK にネットワーク接続、OID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d18839c5b0d0f9bd094473c6446e05b5d1abcfef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364961"
---
# <a name="customized-oids-and-status-indications"></a>カスタマイズされた OID と状態の表示





NDIS は、作成したカスタムの GUID にマップするカスタム OID を作成することができます。 NDIS は、WMI クライアントがクエリまたは関連付けられている情報を設定するため、カスタム GUID を wmi、ミニポート ドライバーに登録します。

NDIS ミニポート ドライバーをカスタムの状態を示す値を提供する、NDIS を使用する必要があります\_状態\_メディア\_特定\_INDICATION\_EX 状態を示す値。 WMI クライアントでは、カスタム イベントを識別するために WMI イベントに含まれているデータを使用する必要があります。 NDIS は、状態インジケーターのカスタム Guid を登録できません。

ミニポート アダプタのカスタム Oid と WMI に関連付けられた Guid を取得するには、ミニポート ドライバーの初期化が完了した後、NDIS は、ミニポート ドライバーに OID 要求を発行します。 NDIS 問題、 [OID\_GEN\_サポートされている\_一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-list)ミニポート ドライバーがサポートするアルゴリズムの一覧を取得するクエリ。 ミニポート ドライバーには、その応答カスタム Oid と標準の Oid の両方が含まれます。 カスタム Oid、NDIS 問題に関連付けられている Guid を取得する、 [OID\_GEN\_サポートされている\_GUID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-guids)コネクションレス ミニポート ドライバーへのクエリまたは[OID\_GEN\_CO\_サポートされている\_GUID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-supported-guids)接続指向のミニポート ドライバーにクエリします。

Oid クエリ\_GEN\_サポートされている\_GUID または OID\_GEN\_CO\_サポートされている\_GUID の配列を返します[NDIS\_GUID](filling-in-an-ndis-guid-structure.md) NDIS する構造体。 各 NDIS\_GUID 構造体では、カスタム GUID をカスタム OID にマップします。

カスタム Oid と状態インジケーターをサポートする NDIS で入力する必要があります\_GUID 構造体。 GUID を記述する管理オブジェクト フォーマット (MOF) ファイルを作成して、ミニポート ドライバーでは、このファイルを構築する必要があります。

このセクションの内容:

[入力、NDIS\_GUID 構造体](filling-in-an-ndis-guid-structure.md)

[MOF ファイルを含む](including-a-mof-file.md)

 

 





