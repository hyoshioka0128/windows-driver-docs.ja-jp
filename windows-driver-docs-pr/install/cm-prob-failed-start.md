---
title: CM_PROB_FAILED_START
description: CM_PROB_FAILED_START
ms.assetid: a7759bcd-1806-4d7a-8ff0-3b03abcae08b
keywords:
- CM_PROB_FAILED_START
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 185621f49368d5e2ad85e3daf1531c3459a4ea4b
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558420"
---
# <a name="cm_prob_failed_start"></a>CM_PROB_FAILED_START

この関数は、システムで使用するために予約されています。

デバイスを起動できませんでした。

## <a name="error-code"></a>エラー コード

10

### <a name="display-message"></a>メッセージの表示

デバイスのハードウェアキーに "Fail理由文字列" の値が含まれている場合は、値の文字列がエラーメッセージとして表示されます。 (ドライバーまたは列挙子は、このレジストリ文字列値を提供します)。ハードウェアキーに "Fail理由文字列" の値が含まれていない場合は、次の一般的なエラーメッセージが表示されます。

"このデバイスを開始できません。 (コード 10) "

"このデバイスのデバイスドライバーをアップグレードしてみてください。"

### <a name="recommended-resolution"></a>推奨される解決策

**[ドライバーの更新]** を選択すると、ハードウェアの更新ウィザードが起動します。

このエラーコードは、デバイスのドライバースタック内のいずれかのドライバーが IRP_MN_START_DEVICE に失敗した場合に設定されます。 スタック内に多数のドライバーがある場合は、失敗したドライバーを特定するのが困難な場合があります。

開始 IRP に対して返されたエラーコードについては、デバイスの[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)プロパティを参照してください。

詳細については、「[デバイスインスタンスの状態と問題コードを取得](retrieving-the-status-and-problem-code-for-a-device-instance.md)する」を参照してください。
