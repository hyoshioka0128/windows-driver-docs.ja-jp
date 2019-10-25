---
title: 正しいデバイス電源状態の判断
description: 正しいデバイス電源状態の判断
ms.assetid: 4acefe93-1d7a-4c12-8701-03c2a8929591
keywords:
- DEVICE_CAPABILITIES 構造体
- デバイスの電源状態の修正 WDK 電源管理
- デバイスの電源状態 WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f3891c9a4cb775be0a4071d402ec01f0719d4f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836939"
---
# <a name="determining-the-correct-device-power-state"></a>正しいデバイス電源状態の判断





電源ポリシーの所有者は、[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造の[**devicestate**](devicestate.md)配列を調べて、各システム電源状態のデバイスの電源状態の有効範囲を判断します。 配列には、基になるデバイスがシステムの電源状態ごとにサポートできるデバイスの最大電源状態が一覧表示されます。

この範囲から特定の状態を選択する場合は、次の点を考慮してください。

-   ほとんどのデバイスは、システムが S0 状態になったときに、D0 状態に入ります。

-   ほとんどのデバイスは、システムがスリープ状態になると D3 状態に入ります。 ただし、ウェイクアップが有効になっているデバイスでは、このような状態がサポートされている場合は、代わりに D1 または D2 を入力する必要があります。 詳細については、「[デバイスの電源機能の報告](reporting-device-power-capabilities.md)」を参照してください。

-   休止状態ファイルを保持するデバイスには、特別な規則が適用されます。 システムの IRP が**Powersystemhibernate**を要求する場合、休止状態ファイルを保持するデバイスの電源をオフにすることはできません。 このようなデバイスの電源ポリシーの所有者は、デバイスの電源状態 D3 を要求してコンテキストを保存する必要がありますが、デバイスのドライバーはデバイスの電源をオフにしないでください。

システムの IRP が**Powersystemshutdown**を要求した場合、ドライバーは、 **Irp-&gt;Parameters.-shutdowntype**の電源\_アクションの値をチェックして、状態変更の理由を判断する必要があります。 詳細については、「[システム電源動作](system-power-actions.md)」を参照してください。

デバイスの電源ポリシーの所有者は、デバイスが既に正しいデバイスの電源状態にある場合でも、各システムセット-電源 IRP に対してデバイスセット-電源 IRP を送信する必要があります。 ドライバーがクエリ-電源 IRP に応答してデバイスの操作を以前に中断した場合、set-power irp は、Irp Irp を停止し、現在の電源状態の通常の動作に戻るように通知します。 この例外は、デバイスが D3 状態にある場合にのみ発生します。この場合、ドライバーは、D3 の[**パワー要求\_\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された追加の IRP\_送信する必要はありません。

 

 




