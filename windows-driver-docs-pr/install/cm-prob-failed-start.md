---
title: CM_PROB_FAILED_START
description: CM_PROB_FAILED_START
ms.assetid: a7759bcd-1806-4d7a-8ff0-3b03abcae08b
keywords:
- CM_PROB_FAILED_START
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 957882d0ee0ae0e60c03742becd233ea83baf2a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391481"
---
# <a name="cmprobfailedstart"></a>CM_PROB_FAILED_START

この関数は、システムの使用に予約されています。

デバイスは、開始できませんでした。

## <a name="error-code"></a>エラー コード

10

### <a name="display-message"></a>メッセージを表示します。

デバイスのハードウェア キーに「ドライバー」値が含まれている場合、値の文字列は、エラー メッセージとして表示されます。 (ドライバーまたは列挙子を提供このレジストリ文字列値。)ハードウェア キーに「ドライバー」値が含まれていない場合は、次の一般的なエラー メッセージが表示されます。

"このデバイスを起動できません。 (コードは 10)"

「このデバイスのデバイス ドライバーのアップグレードを再試行してください。」

### <a name="recommended-resolution"></a>推奨される解決方法

選択**ドライバーの更新**ハードウェアの更新ウィザードを開始します。

このエラー コードは、IRP_MN_START_DEVICE 失敗した場合、デバイスのドライバー スタック内のドライバーのいずれかに設定されます。 スタックに多くのドライバーがある場合は、失敗した 1 つの特定が困難ができます。
