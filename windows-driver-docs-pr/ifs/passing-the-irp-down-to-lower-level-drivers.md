---
title: 下位レベルのドライバーに IRP を渡す
description: 下位レベルのドライバーに IRP を渡す
ms.assetid: 9a8e72fb-b0a8-4026-8606-57fa03344146
keywords:
- IRP ディスパッチ ルーチン WDK ファイル システム、IRP を渡す
- デバイス スタック WDK ダウン Irp を渡す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6200c24666752c8ce20eda6e72cdfa407571b558
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552946"
---
# <a name="passing-the-irp-down-to-lower-level-drivers"></a>下位レベルのドライバーに IRP を渡す


## <span id="ddk_passing_the_irp_down_to_lower_level_drivers_if"></span><span id="DDK_PASSING_THE_IRP_DOWN_TO_LOWER_LEVEL_DRIVERS_IF"></span>


既定ですべてディスパッチ ルーチン IRP のターゲットのデバイス オブジェクトを確認した後渡す必要があります、下位レベルの次のデバイス ドライバーに IRP を呼び出して[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。 フィルター ドライバーが単に失敗することではなくは認識されない任意の Irp を渡すことが特に重要です。 未知の Irp が失敗すると、オペレーティング システム自体が予期しない方法で失敗する可能性があります。 たとえば、IRP を失敗\_MJ\_PNP システムの休止状態を防ぐことによって、ファイル システム フィルター ドライバーで要求できる電源管理に影響をします。 これは、ファイル システム フィルター ドライバーは電源管理に含まれないは受け取りませんという事実に関係なく当てはまります[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)要求。

 

 




