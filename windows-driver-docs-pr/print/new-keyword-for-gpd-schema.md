---
title: GPD スキーマの新しいキーワード
description: GPD スキーマの新しいキーワード
ms.assetid: 4814d019-0556-4e5a-8c55-c05454bafbd3
keywords:
- ルート レベルのキーワードの WDK プリンターの自動構成
- GPD ファイル WDK GDL 拡張機能、キーワード
- キーワードの WDK プリンターの自動構成
- ボックスの自動構成サポート WDK プリンター、キーワード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e10528d9b1ace6b2eb3d728973a12c823f6a05f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528254"
---
# <a name="new-keyword-for-gpd-schema"></a>GPD スキーマの新しいキーワード


以降では、Windows Vista は、する必要があります新しいルート レベルにキーワードを追加、GPD で GDL ファイルを指す GPD ファイル\* **BidiQueryFile**、bidi マッピング情報を含む GDL ファイルを識別するようです自動構成に必要です。 キーワードが不足している場合は、自動構成が GDL パーサーの呼び出しまたは GDL ファイルを検索するには、もう一度、ファイル システムにヒットする必要はありません。

Unidrv ベースのドライバーを作成する場合、ドライバーの主な GPD ファイルを使用して直接参照する別の GDL ファイルを使用する必要があります、 \* **BidiQueryFile**キーワード。

 

 




