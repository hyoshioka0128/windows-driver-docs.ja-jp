---
title: CM_PROB_FAILED_START
description: CM_PROB_FAILED_START
ms.assetid: a7759bcd-1806-4d7a-8ff0-3b03abcae08b
keywords:
- CM_PROB_FAILED_START
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1599ae52fad1d904672f561e66682b9f6387a82d
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279565"
---
# <a name="code-10---cm_prob_failed_start"></a>コード 10-CM_PROB_FAILED_START

このデバイスマネージャーエラーメッセージは、デバイスを起動できなかったことを示します。

## <a name="error-code"></a>エラー コード

10

### <a name="display-message"></a>メッセージの表示

デバイスの[ハードウェアキー](opening-a-device-s-hardware-key.md)に "Fail理由文字列" の値が含まれている場合は、値の文字列がエラーメッセージとして表示されます。 (ドライバーまたは列挙子は、このレジストリ文字列値を提供します)。ハードウェアキーに "Fail理由文字列" の値が含まれていない場合は、次の一般的なエラーメッセージが表示されます。

"このデバイスを開始できません。 (コード 10) "

"このデバイスのデバイスドライバーをアップグレードしてみてください。"

### <a name="recommended-resolution"></a>推奨される解決策

**[ドライバーの更新]** を選択すると、ハードウェアの更新ウィザードが起動します。

このエラーコードは、デバイスのドライバースタック内のいずれかのドライバーが IRP_MN_START_DEVICE に失敗した場合に設定されます。 スタック内に多数のドライバーがある場合は、失敗したドライバーを特定するのが困難な場合があります。

[開始 IRP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)に対して返されたエラーコードについては、デバイスの[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)プロパティを参照してください。

詳細については、「[デバイスインスタンスの状態と問題コードを取得](retrieving-the-status-and-problem-code-for-a-device-instance.md)する」を参照してください。

## <a name="for-driver-developers"></a>ドライバー開発者向け

デバイススタック内のいずれかのドライバーが[開始 IRP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)に失敗しました。 デバイスの[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)プロパティは、エラーコードを示している必要があります。
