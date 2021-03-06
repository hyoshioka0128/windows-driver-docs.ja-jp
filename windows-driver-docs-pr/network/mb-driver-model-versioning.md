---
title: MB ドライバー モデルのバージョン管理
description: MB ドライバー モデルのバージョン管理
ms.assetid: f5778b36-4f84-4cfe-965c-36af225ac0dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e545f7ca9e8b4a94208fdccfad4e3ba48da0bee8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377989"
---
# <a name="mb-driver-model-versioning"></a>MB ドライバー モデルのバージョン管理


MB ドライバー モデルのバージョン管理は、モデルのドライバーのバージョンとリビジョンを構造体、個々 の OID データによって実現されます。 これは、NDIS で使用されるバージョン管理のパラダイムで一貫性のある 6.x します。

ドライバー モデルのバージョンでは、MB サービスと MB ミニポート ドライバーの間のインターフェイスの進化を定義します。 個々 の OID リビジョンは保持 Oid にさまざまな MB ドライバー モデルのバージョンで加えられた変更の追跡します。 つまり、ドライバー モデルのバージョンでは、一連の Oid のデータ構造は、特定のリビジョン番号によって識別されますが定義されます。

一貫性のある、 *NDIS 仕様*、MB ドライバー モデルの進化は*加法*します。 つまり、新しい Oid と新しいメンバーのみ追加できます OID の既存のデータ構造体。 これにより、ミニポート ドライバー MB サービスが旧バージョンとの互換性をサポートできること。

**重要な**  非常にまれな状況でのみ、既存の Oid は非推奨となるまたは既存の OID データ構造体のメンバーは、次のバージョンで使用するされません。 そのような場合は、これらの変更と旧バージョンとの互換性に影響を与えないことは明確に文書化する MB ドライバー モデルの仕様の新しいバージョンの後続のドキュメント。

 

このドキュメントでは、MB ドライバー モデルの Windows 8 のリリースについて説明します。 ドライバー モデルのバージョンはバージョン 2.0 にインクリメントされていた。 一部の OID リビジョンは引き続きリビジョン 2 に更新される一部のリビジョン番号 1 をします。 それぞれの Oid を使用するには、どのリビジョンに関する詳細については、次を参照してください。 [MB のデータ モデル](mb-data-model.md)します。

このドキュメントではため、モデルのドライバーのバージョンと個々 のリビジョンを OID を起動リビジョン番号が 1 MB、ドライバー モデルの最初のリリースについて説明します。

ドライバー モデルは、次のバージョンに移動、そのバージョン番号は 1 ずつ増加します。 ドライバー モデルに追加され、新しい Oid は、リビジョン 1; に開始されます。構造が変更されているデータは、対応するリビジョンを 1 増や、既存の Oid と、既存の Oid が変更されない、それぞれのリビジョン番号が保持されます。

ドライバー モデルのバージョンがによって伝えられる[OID\_WWAN\_ドライバー\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)します。 MB サービスに送信 OID\_WWAN\_ドライバー\_CAP クエリ要求中に、ミニポート ドライバーに[MB ミニポート ドライバーの初期化](mb-miniport-driver-initialization.md)します。 個々 のリビジョンを OID が説明されている、**リビジョン**のメンバー、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)構造体に含まれる各個々 の OID のデータ構造体。

 

 





