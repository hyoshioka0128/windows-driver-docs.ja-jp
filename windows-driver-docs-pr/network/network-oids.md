---
title: ネットワーク OID
description: ネットワーク OID
ms.assetid: a897ba37-7984-455f-9428-a74850f7e3b6
keywords:
- Oid WDK ネットワーク
- ネットワークの Oid WDK
- オブジェクト識別子の WDK ネットワーク
- Oid WDK ネットワー キングの Oid の詳細について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d522a11e461d65e3783798ef792160020ec30931
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331834"
---
# <a name="network-oids"></a>ネットワーク OID





ミニポート ドライバーでは、その機能と、現在の状態に関する情報と、管理している各ミニポート アダプターに関する情報を保持します。 各情報の種類は、オブジェクト識別子 (OID) によって識別されます。 Oid は、システム定義です。 NDIS ミニポート ドライバーの OID 要求の多くを処理し、NDIS ミニポート ドライバーには、このような要求を渡しません。 ミニポート ドライバーは、その機能は、初期化中にその属性での OID クエリへの応答で報告された以前の多くを報告します。 レポート属性の詳細については、次を参照してください。 [、アダプターの初期化](initializing-a-miniport-adapter.md)します。

NDIS とより高いレベルのドライバー クエリを実行でき、場合によっては、Oid を使用して情報を設定できます。

-   上位レベルのコネクションレス メディア呼び出し用のドライバー [ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)クエリまたはコネクションレス ミニポート ドライバーの情報を設定します。 NDIS ミニポート ドライバーの呼び出し、クエリまたはセットの操作を実行する[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数。

-   上位レベルの接続指向のメディアの呼び出し用のドライバー [ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)クエリまたは接続指向のミニポート ドライバーの情報を設定します。 両方のクエリを実行し、操作を設定、NDIS に呼び出し、ミニポート ドライバーの[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)関数。

NDIS は、多くのミニポート ドライバーのシステム定義の Oid をグローバル一意識別子 (Guid) にマップします。 NDIS は、これらの Guid と、カーネル モード Microsoft Windows Management Instrumentation (WMI) Web-based Enterprise Management (WBEM) アプリケーションのユーザー モードをサポートするを登録します。 WMI クライアントでは、クエリまたはこれらの Guid のいずれかを設定、ときに、NDIS がクエリの OID 操作または、必要に応じて、設定の OID 操作の要求を変換し、返された情報を渡します、状態が WMI に戻します。 カスタムの Guid は、カスタム Oid またはミニポート ドライバーの状態にマップできます。 ミニポート ドライバーする必要がありますカスタム GUID を OID または登録 GUID-状態マッピング NDIS の初期化中にします。

クエリを実行して、Oid、カスタムの Oid の作成の設定の詳細については、WMI の NDIS サポートを参照してくださいと[の取得と設定のミニポート ドライバーの情報と NDIS が WMI のサポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)します。

 

 





