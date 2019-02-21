---
title: 事後のデバッグ中のセキュリティ
description: 事後のデバッグ中のセキュリティ
ms.assetid: 59c411c4-d829-4d1c-9820-e58188f0656c
keywords:
- セキュリティに関する考慮事項、事後検証のデバッグ
- 事後分析のデバッグ、セキュリティの考慮事項
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea002c275df1969aa466579345bb3c543ca95b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532005"
---
# <a name="security-during-postmortem-debugging"></a>事後のデバッグ中のセキュリティ


## <span id="ddk_security_during_postmortem_debugging_dbg"></span><span id="DDK_SECURITY_DURING_POSTMORTEM_DEBUGGING_DBG"></span>


管理者のみが有効にできます[事後デバッグ](enabling-postmortem-debugging.md)します。

ただし、事後のデバッグは 1 人のユーザーのだけでなく、システム全体に対して有効にします。 したがって、有効になっている、任意のアプリケーション クラッシュ アクティブになりますが選択されている - デバッガー、現在のユーザーに管理者特権がない場合でも。

また、事後分析のデバッガーは、クラッシュしたアプリケーションと同じ権限を継承します。 したがって、CSRSS、LSASS などの Windows サービスがクラッシュした場合、デバッガーは非常に高度な特権があります。

事後分析のデバッグを有効にするを選択する際のアカウントを考慮する必要があります。

 

 





