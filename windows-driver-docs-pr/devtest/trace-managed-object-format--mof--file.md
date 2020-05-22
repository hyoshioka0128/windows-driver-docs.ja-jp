---
title: トレース管理オブジェクト フォーマット (MOF) ファイル
description: トレース管理オブジェクト フォーマット (MOF) ファイル
ms.assetid: e0ef452b-042d-42d0-be0f-b36e7bf47285
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0de160d0af0595a07fe826cf0f4a859791ab66d7
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769650"
---
# <a name="trace-managed-object-format-mof-file"></a>トレース管理オブジェクト フォーマット (MOF) ファイル


トレース[管理オブジェクトフォーマット](https://docs.microsoft.com/windows/win32/wmisdk/managed-object-format--mof-)(MOF) ファイルは、PDB ファイルで表される各[トレースプロバイダー](trace-provider.md)のコントロール GUID を含むテキストファイルです。 MOF ファイルの名前は、トレースプロデューサーのモジュール名と、その後に .mof ファイル名拡張子を付けたものです。

[Tracepdb](tracepdb.md)と[BINPLACE](binplace.md)は、PDB ファイルの書式設定手順からトレースメッセージ形式 (tmf) ファイルを作成するときに、各トレースプロバイダーの MOF ファイルを作成します。

トレース MOF ファイルには、次の情報も含まれています。

-   PDB ファイルのパスとファイル名。

-   PDB ファイルが作成された日付と時刻。

-   各トレースプロバイダーのコントロール GUID。

-   トレースプロバイダーによって定義されたトレースフラグ。

Logman と Perfmon は、MOF ファイルを使用して、各プロバイダーのトレースフラグを見つけることができます。 MOF ファイルは、トレースプロバイダーのコントロール GUID のクイックリファレンスとして使用できます。
