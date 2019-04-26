---
title: フィルター ドライバー サービス
description: フィルター ドライバー サービス
ms.assetid: 72ee00c6-0887-46bd-a329-ee7bf0dd2c06
keywords:
- フィルター ドライバー WDK ネットワー キング、サービス
- NDIS フィルター ドライバー WDK、サービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49042f38727998439dbdbaa008363740a0f7dc8c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350021"
---
# <a name="filter-driver-services"></a>フィルター ドライバー サービス





フィルター ドライバーは、次のサービスを提供できます。

-   送信要求を発信および受信表示します。

-   データ バッファーの順序付けまたは送信でタイミングを変更し、データ パスを受信します。

-   追加、変更、送信の両方でネットワーク データ バッファーを削除およびドライバー スタックのデータ パスを受信します。 フィルター処理の詳細については送信および受信データを参照してください[フィルター モジュールの送信と受信操作](filter-module-send-and-receive-operations.md)します。

-   クエリを送信し、OID 要求を基になるドライバーに設定します。

-   クエリをフィルター処理し、OID 要求を基になるドライバーに設定します。

-   基になるドライバーから OID 要求の応答をフィルター処理します。 OID 要求の詳細については、次を参照してください。[フィルター モジュールの OID 要求](filter-module-oid-requests.md)します。

-   上にあるドライバーに状態インジケーターを生成します。

-   基になるドライバーからの状態インジケーターのフィルターを適用します。 詳細については、次を参照してください。[フィルター モジュールの状態インジケーター](filter-module-status-indications.md)します。

-   そのインターフェイスを各ミニポート アダプター用にレジストリの構成パラメーターを管理します。 詳細については、次を参照してください。[フィルター ドライバーの構成の情報にアクセスする](accessing-configuration-information-for-a-filter-driver.md)します。

 

 





