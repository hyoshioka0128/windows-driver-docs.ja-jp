---
title: デバイス メタデータの取得クライアント
description: デバイス メタデータの取得クライアント
ms.assetid: fdcf3459-0fd4-4cf6-a9f5-13337fbd604b
keywords:
- DMRC WDK
- デバイス メタデータの取得クライアント WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f3ac1d6c5635e2553a62ef2b14c1fe58e2e5e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348210"
---
# <a name="device-metadata-retrieval-client"></a>デバイス メタデータの取得クライアント


デバイス メタデータの取得クライアント (DMRC) は、デバイス メタデータ パッケージをデバイスに一致するオペレーティング システム コンポーネントです。 デバイスのギャラリー ビュー ウィンドウを開くし、DMRC、プリンターのユーザー インターフェイスは、デバイスとプリンターを表示するデバイスのデバイス メタデータの取得を試みます。 まず、ローカル コンピューターを確認します[デバイス メタデータのキャッシュ](device-metadata-cache.md)と[デバイス メタデータ ストア](device-metadata-store.md)します。 デバイスが新しくインストールした場合、または DMRC クエリ メタデータの定期的な更新プログラムのデバイスがスケジュールされている場合、 [Windows メタデータとインターネット サービス](windows-metadata-and-internet-services.md)デバイス メタデータ パッケージが使用できるかどうかを判断する (WMIS) web サイト、デバイスです。 デバイス メタデータ パッケージを使用できる場合 DMRC 自動的に WMIS からダウンロードしたパッケージ、パッケージのデバイスのメタデータ コンポーネントを抽出およびデバイスのメタデータ キャッシュ内に保存します。

[PackageInfo XML ドキュメント](packageinfo-xml-document.md)(Packageinfo.xml)、デバイス メタデータ パッケージのコンポーネントである、DMRC がパッケージにデバイスを一致させるために必要な情報が含まれています。 ファイルが含まれています、 [ **MetadataKey** ](https://msdn.microsoft.com/library/windows/hardware/ff548740)はの次のソースのいずれかのデバイスに一致する情報を指定する XML 要素。

-   デバイスでサポートされているハードウェアの機能を識別する 1 つまたは複数のハードウェア Id の一覧。 ハードウェア Id の一覧がで指定された、 [ **HardwareIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff546121)子 XML 要素。

-   デバイスでサポートされているハードウェア関数を識別する 1 つまたは複数のモデル Id の一覧。 各モデル ID がグローバル一意識別子 (GUID)、およびモデル Id の一覧がで指定された、 [ **ModelIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff549303)子 XML 要素。

によって参照される XML スキーマの詳細については、 [PackageInfo XML ドキュメント](packageinfo-xml-document.md)を参照してください[XML スキーマの PackageInfo](https://msdn.microsoft.com/library/windows/hardware/ff549614)します。

 

 





