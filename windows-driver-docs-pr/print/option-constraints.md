---
title: オプションの制約
description: オプションの制約
ms.assetid: dc399715-c238-4a6e-8ce0-3204aa0cca68
keywords:
- WDK Unidrv の制約
- プリンター オプション WDK Unidrv、制約
- 同時プリンター WDK Unidrv をオプションします。
- WDK Unidrv オプションのプリンターを組み合わせること
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50f8d391fc65573e6f37e76844e1f49852af27d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535828"
---
# <a name="option-constraints"></a>オプションの制約





インストールまたはプリンターの機能に関連付けられている特定のプリンター オプションを選択してユーザーの能力を制限する必要があります。 次の種類のオプションの制約を指定できます。

-   オプションは、競合するオプションが既に選択されている場合に選択できないように制限できます。 これらの制約が呼び出される[選択制約](selection-constraints.md)します。

-   インストール可能なオプションは、競合しているインストール可能なオプションが既にインストールされている場合はインストールできないように制限できます。 これらの制約が呼び出される[インストール制約](installation-constraints.md)します。

-   オプションは、競合しているインストール可能なオプションが既にインストールされている、または場合、必要なインストール可能なオプションを選択できないようにがインストールされていない場合に選択できないように制限できます。 これらの制約が呼び出される[選択とインストールの間の制約](constraints-between-selections-and-installations.md)します。

ユーザーが選択したときに、ドライバーのユーザー インターフェイスのコードが制約を強制、 **OK**プリンターのプロパティ シートのダイアログ ボックスのボタン。 ユーザーがプロパティ シートのページを変更して競合を修正するかを選択するかに基づいて、自動的に修正するドライバー試行できるようにすることオプションの無効な組み合わせが選択されている場合[機能の競合優先順位](feature-conflict-priority.md)します。

 

 




