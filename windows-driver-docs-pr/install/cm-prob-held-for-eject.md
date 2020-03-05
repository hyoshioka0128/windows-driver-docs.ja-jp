---
title: CM_PROB_HELD_FOR_EJECT
description: CM_PROB_HELD_FOR_EJECT
ms.assetid: 8d67ad71-276d-4dea-b3fb-61fedcfba789
keywords:
- CM_PROB_HELD_FOR_EJECT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b76724cf14058e890ce97094a5ad460b4d36073a
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279547"
---
# <a name="code-47---cm_prob_held_for_eject"></a>コード 47-CM_PROB_HELD_FOR_EJECT

このデバイスマネージャーエラーメッセージは、デバイスが取り出し用に準備されたことを示します。

## <a name="error-code"></a>エラー コード

47

### <a name="display-message"></a>メッセージの表示

"安全な削除の準備ができていますが、コンピューターから削除されていないため、Windows はこのハードウェアデバイスを使用できません。 (コード 47) "

"この問題を解決するには、このデバイスをコンピューターから取り外してから、もう一度接続してください。"

### <a name="recommended-resolution"></a>推奨される解決策

デバイスを取り外してから、もう一度接続してください。 または、 **[コンピューターの再起動]** を選択すると、コンピューターが再起動され、デバイスが使用できるようになります。

このエラーが発生するのは、ユーザーがホットプラグプログラムを呼び出して、デバイスを削除用に準備する場合 ( [**CM_Request_Device_Eject**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_request_device_ejectw)を呼び出す場合)、またはユーザーが物理取り出しボタン ( [**IoRequestDeviceEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdeviceeject)を呼び出す) を押した場合のみです。 ユーザーは、ラップトップとドッキングステーショントレイとの間でトラップされた CD-ROM など、現在リムーバブルではないデバイスを準備できます。
