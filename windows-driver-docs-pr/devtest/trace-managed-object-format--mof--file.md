---
title: トレース管理オブジェクト フォーマット (MOF) ファイル
description: トレース管理オブジェクト フォーマット (MOF) ファイル
ms.assetid: e0ef452b-042d-42d0-be0f-b36e7bf47285
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c59746b7db6531087f94418e8ebefb17a612a5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527721"
---
# <a name="trace-managed-object-format-mof-file"></a>トレース管理オブジェクト フォーマット (MOF) ファイル


トレース[マネージ オブジェクト形式](https://go.microsoft.com/fwlink/p/?linkid=74565)(MOF) ファイルは、各コントロールの GUID を含むテキスト ファイル[トレース プロバイダー](trace-provider.md) PDB ファイルで表されます。 MOF ファイルの名前は、.mof ファイル名拡張子を続けて、トレースのプロデューサーのモジュールの名前です。

[Tracepdb](tracepdb.md)と[BinPlace](binplace.md) PDB ファイルに書式設定の手順からトレース メッセージの形式 (.tmf) ファイルを作成するときに、各トレース プロバイダーの MOF ファイルを作成します。

トレースの MOF ファイルには、次の情報も含まれています。

-   PDB ファイルのパスとファイル名。

-   日付と PDB ファイルが作成された時刻。

-   トレース プロバイダーごとにコントロールの GUID。

-   トレース プロバイダーによって定義されているトレース フラグ。

Logman やパフォーマンス モニターは、各プロバイダーのトレース フラグを検索するのに MOF ファイルを使用できます。 MOF ファイルは、コントロールのトレース プロバイダーの GUID のクイック リファレンスとして使用できます。
