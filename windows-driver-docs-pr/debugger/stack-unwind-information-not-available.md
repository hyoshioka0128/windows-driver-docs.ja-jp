---
title: Stack Unwind Information Not Available
description: Stack Unwind Information Not Available
ms.assetid: 82260f85-780b-4f30-bebd-62faed6efeeb
keywords:
- スタック アンワインド情報を利用できません (警告)
- コール スタック、スタック アンワインド情報を利用できません (警告)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16a3eafedf8830351550145b6724a2fbf509647f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335529"
---
# <a name="stack-unwind-information-not-available"></a>Stack Unwind Information Not Available


## <span id="ddk_stack_unwind_information_not_available_dbg"></span><span id="DDK_STACK_UNWIND_INFORMATION_NOT_AVAILABLE_DBG"></span>


デバッガーは、呼び出し履歴を調べることが、ときに、メッセージが表示"スタック アンワインド情報を利用できません。 次のフレームがありますが正しくありません。"

この警告は、デバッガーがない特定の後、このメッセージが正しいが、コール スタックのフレームに表示されていることを示します。

コール スタックをトレースするには、デバッガーは、スタックを検査し、スタックを使用している関数を分析します。 これにより、コール スタックを形成する戻り値のアドレスのチェーンを識別することができます。 ただし、この手順では、スタックを使用する関数が含まれる各モジュールのシンボル情報が必要です。

このシンボル情報が利用できない場合は、デバッガーを強制的に妥当などのフレームには戻り値のアドレス。 この警告の情報は、この時点より後の呼び出し履歴の不明な性質を示すために表示されます。

 

 





