---
title: CM_PROB_FAILED_DRIVER_ENTRY
description: CM_PROB_FAILED_DRIVER_ENTRY
ms.assetid: e1345892-69db-4135-be5b-1d182a2a1d66
keywords:
- CM_PROB_FAILED_DRIVER_ENTRY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c105dedf0bee0d2caf7e9ec929e96e7cb3db017e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358974"
---
# <a name="cmprobfaileddriverentry"></a>CM_PROB_FAILED_DRIVER_ENTRY

この関数は、システムの使用に予約されています。
ドライバーからエラーが返されますその**DriverEntry**ルーチン。

## <a name="error-code"></a>エラー コード

37

### <a name="display-message"></a>メッセージを表示します。

"Windows は、このハードウェアのデバイス ドライバーを初期化できません。 (コード 37)"

### <a name="recommended-resolution"></a>推奨される解決方法

再インストールするか、新しいドライバーを入手します。

**注**  場合、 **DriverEntry**ルーチン返します STATUS_INSUFFICIENT_RESOURCES、デバイス マネージャーのレポート、 [CM_PROB_OUT_OF_MEMORY](cm-prob-out-of-memory.md)エラー コード。
