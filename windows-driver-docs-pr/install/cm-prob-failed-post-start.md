---
title: CM_PROB_FAILED_POST_START
description: CM_PROB_FAILED_POST_START
ms.assetid: 82d43c8b-d5de-4395-9ca0-34d2258b9772
keywords:
- CM_PROB_FAILED_POST_START
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 14e7bb470f3b1a92b512309a7dd89618d1a6fdeb
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279567"
---
# <a name="code-43---cm_prob_failed_post_start"></a>コード 43-CM_PROB_FAILED_POST_START

このデバイスマネージャーエラーメッセージは、ドライバーがデバイスの障害を報告したことを示します。

## <a name="error-code"></a>エラー コード

43

### <a name="display-message"></a>メッセージの表示

"問題が報告されたため、Windows はこのデバイスを停止しました。 (コード 43) "

### <a name="recommended-resolution"></a>推奨される解決策

デバイスをアンインストールして再インストールします。

デバイスを制御するドライバーの1つで、IRP_MN_QUERY_PNP_DEVICE_STATE に応答して何らかの方法でデバイスが失敗したことがオペレーティングシステムに通知されました。

## <a name="for-driver-developers"></a>ドライバー開発者向け

ドライバーはデバイスのデバイスの[状態を無効](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)にし、結果として生成されたクエリデバイスの状態を[PNP_DEVICE_FAILED](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state)します。

ドライバーが WDF ドライバーである場合、WDF ドライバーが[**Wdfdevicesetfailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)を呼び出したか、WDF コールバックからエラーを返すことによって、デバイスの報告が失敗したことが間接的に発生する可能性があります。 詳細については、「[デバイスの障害の報告](https://docs.microsoft.com/windows-hardware/drivers/wdf/reporting-device-failures)」を参照してください。
