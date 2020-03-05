---
title: CM_PROB_DEVICE_NOT_THERE
description: CM_PROB_DEVICE_NOT_THERE
ms.assetid: 843afcc0-30ca-42f8-8c9b-3c4a56ec019d
keywords:
- CM_PROB_DEVICE_NOT_THERE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5d8931b6fe5790b466fdc042956ec706425fffd
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279591"
---
# <a name="code-24---cm_prob_device_not_there"></a>コード 24-CM_PROB_DEVICE_NOT_THERE

このデバイスマネージャーエラーメッセージは、デバイスが存在しないと思われることを示します。

## <a name="error-code"></a>エラー コード

24

### <a name="display-message"></a>メッセージの表示

"このデバイスは存在しないか、正常に動作していないか、またはすべてのドライバーがインストールされていません。 (コード 24) "

### <a name="recommended-resolution"></a>推奨される解決策

問題の原因はハードウェアに問題があるか、新しいドライバーが必要である可能性があります。 デバイスが削除用に準備されている場合、デバイスはこの状態のままです。 このエラーコードは、ドライバーの**Driverentry**ルーチンがデバイスを検出したが、後で**driverentry**ルーチンが失敗した場合に設定できます。

**注**  windows XP 以降のバージョンの windows では、 **driverentry**の問題に個別のエラーコードがあります。
