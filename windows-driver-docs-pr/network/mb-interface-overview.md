---
title: MB インターフェイスの概要
description: MB インターフェイスの概要
ms.assetid: fcb79029-4225-4759-a130-6ef8b3f2d25d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b71c30c87057ae7544f0170288948ca92ba831
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343388"
---
# <a name="mb-interface-overview"></a>MB インターフェイスの概要


このドキュメントでは、モバイル ブロード バンド (MB) ドライバー モデルについて説明します。 MB ドライバー モデルは、Windows 7 および Windows の以降のバージョンで提供されるソフトウェア アーキテクチャです。 ネットワーク CDMA ベース (1 xrtt/1xEV-DO/1xEV-DO RevA/1xEvDO RevB) と、GSM ベース (GPRS/エッジ/UMTS/HSDPA/TD-SCDMA) 携帯電話テクノロジに基づく機能の統合セットのフレームワークを提供します。

Windows 8 MB のミニポート ドライバーがに基づいて、 [NDIS 6.30](introduction-to-ndis-6-30.md)インターフェイス。 Windows 7 MB のミニポート ドライバーがに基づいて、 [NDIS 6.20](introduction-to-ndis-6-20.md)インターフェイス。 MB のミニポート ドライバーは、適切なに従う必要があります"NDIS 6.x 仕様"に加えて、このドキュメント全体で説明されているデバイス ドライバー インターフェイス (Ddi)。

次の図は、MB ドライバー モデルのアーキテクチャを表します。

![モバイル ブロード バンド ドライバー モデルのアーキテクチャを示す図](images/wwanarchitecture.png)

### <a name="terminology"></a>用語

注意してくださいを条項*ワイヤレス ワイド エリア ネットワーク*(WWAN) と*モバイル ブロード バンド*(MB) モバイル ブロード バンド技術を表すためにこのドキュメント全体で同じ意味で使用します。

条件*アクティブ化*と*アクティベーション*このドキュメントでは 2 つの異なる意味を持ちます。 用語*アクティブ化*などと、ネットワーク プロバイダーする必要があります明示的に有効に MB サブスクリプション サービス プロバイダーのサービスを使用する前に、サービスのアクティブ化に関連します。 用語*アクティベーション*GSM ベース (GPRS/エッジ/UMTS/HSDPA/TD-SCDMA) テクノロジでの接続の設定に固有です。 たとえば、 *PDP コンテキストのアクティブ化*PDP コンテキストで指定したパラメーターに従って MB の接続の設定を参照します。

*SIM アクセス*Subscriber Identity Module (SIM とも呼ばれる、R-UIM) へのアクセスを参照します。 MB デバイスには、SIM/R-UIM として物理エンティティがない場合は、代わりには、論理的に相当に埋め込まれているデバイスにはこの用語はその論理回路を同等に適用できます。 SIM のアクセスは必要ありません、ミニポート ドライバーでは、要求を完了するには、SIM から情報を取得する必要はありません。

### <a name="semantics"></a>セマンティクス

ユーザー モードで MB サービス コンポーネントは、カーネル モードで MB ミニポート ドライバーを使用してデータを交換直接ことはできません。 WMI などの中継ぎ局または[NDIS フィルター ドライバー](ndis-filter-drivers2.md)が必要です。 わかりやすくするため、これらの中継ぎ局は、このドキュメントで明示的にについて説明しません。 ただし、この省略しないわけでは MB サービスと MB ミニポート ドライバーは、直接データ交換に取り組むことができます。

次のトピックでは、NDIS 6.20 が動作と MB OID のセマンティクスのミニポート ドライバーの同期および非同期の操作を実行する必要があります手順の概要と、モバイル ブロード バンド ドライバー モデルでサポートされる操作の概要を入力します。

[MB/NDIS 6.20 が動作インターフェイスの概要](mb---ndis-6-20-interfacing-overview.md)

[MB のデータ モデル](mb-data-model.md)

[MB 演算のセマンティクス](mb-operational-semantics.md)

[MB ドライバー モデルのバージョン管理](mb-driver-model-versioning.md)

[MB ミニポート ドライバーの INF の要件](mb-miniport-driver-inf-requirements.md)

[MB ミニポート ドライバーの種類](mb-miniport-driver-types.md)

[MB アダプターの一般的な属性の必要条件](mb-adapter-general-attribute-requirements.md)

[MB Raw IP パケット処理のサポート](mb-raw-ip-packet-processing-support.md)

[MB ミニポート ドライバー IP アドレスの通知のガイドライン](guidelines-for-mb-miniport-driver-ip-address-notifications.md)

[MB ミニポート ドライバーのエラーのログ記録](mb-miniport-driver-error-logging.md)

[MB ミニポート ドライバー パフォーマンスの要件](mb-miniport-driver-performance-requirements.md)

 

 





