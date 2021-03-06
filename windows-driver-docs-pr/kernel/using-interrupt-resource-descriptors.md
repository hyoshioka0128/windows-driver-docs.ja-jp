---
title: 割り込みリソース記述子の使用
description: 割り込みリソース記述子の使用
ms.assetid: 0e9aa9a1-c1aa-42e1-9c0b-a91a2424ad1a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0632f480ef358fd7dec2dd81652225f7d09cf104
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381636"
---
# <a name="using-interrupt-resource-descriptors"></a>割り込みリソース記述子の使用


プラグ アンド プレイ (PnP) マネージャーは、割り込みメッセージを 2 つのパスを使用してデバイスに割り当てます。 PnP マネージャーを最初に、送信、 [ **IRP\_MN\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements) 、ハードウェア リソースの一覧で、ドライバーへの要求デバイスに割り当てる割り込みメッセージを含むです。 ドライバーは、いくつかのメッセージごとの設定と同様に、割り込みメッセージの数を変更するには、この一覧を変更できます。 次に後、PnP マネージャーは、実際には、リソースを割り当てる、送信、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を要求し、ハードウェアの完全な一覧を提供などのリソースは、ドライバーのデバイスに割り当てられているメッセージを中断します。

**IRP\_MN\_フィルター\_リソース\_要件**要求の一覧を提供する[ **IO\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_resource_descriptor)構造体。 デバイスが MSI (メッセージ シグナル割り込み) の機能構造 PCI 2.2 仕様で定義されている場合、PnP マネージャーは、1 つの割り込みメッセージ記述子を提供します。 デバイスが MSI X 機能の構造、PCI 3.0 仕様で定義されている場合、PnP マネージャーは、割り込みメッセージごとに 1 つの構造を提供します。 記述子が割り込みメッセージ**型** = **CmResourceTypeInterrupt**と**フラグ**= CM\_リソース\_中断\_LATCHED |CM\_リソース\_INTERRUPT\_メッセージ。 ドライバーでは、割り込みアフィニティなどの設定を変更しても変更できます、 **u.Interrupt**構造体のメンバー。 MSI を使用する場合すべて割り込みがある同じアフィニティは、さまざまな類似性を持つことができます MSI X を使用する場合に注意してください。 詳細については、次を参照してください。[割り込みアフィニティと優先順位](interrupt-affinity-and-priority.md)します。

PCI の 2.2 で定義されている、MSI の**u.Interrupt.MaximumVector** - **u.Interrupt.MinimumVector** + 1 がデバイスに割り当てられた割り込みメッセージの数。 ドライバーは、変更することにより割り込みメッセージの数を変更できます**u.Interrupt.MinimumVector**します。 MSI 割り込みメッセージ、 **u.Interrupt.MaximumVector** CM では常に\_リソース\_割り込み\_メッセージ\_トークンです。 割り当てる*MessageCount*中断メッセージは、設定**u.Interrupt.MinimumVector** CM と等しい\_リソース\_割り込み\_メッセージ\_トークン - *MessageCount* + 1 です。

MSI X、PCI 3.0 で定義されている、ドライバーは割り込みメッセージが追加または一覧からエントリを削除して割り当てられた数にできます変更します。 その割り込みメッセージをこの方法で追加のリソースはへの応答では、その後削除されませんする必要がありますに注意してください、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。 MSI x、PnP マネージャーがメッセージの割り込みあたり 1 つの記述子を提供し、 **u.Interrupt.MinimumVector**と**u.Interrupt.MaximumVector**この記述子のメンバーが両方とも cm設定\_リソース\_INTERRUPT\_メッセージ\_トークンです。

プラグ アンド プレイのマネージャーには、割り込みメッセージを含む、デバイスのすべてのハードウェア リソースが割り当てられて、送信、 **IRP\_MN\_開始\_デバイス**ドライバーに要求します。 この要求の 2 つのリストを提供する[ **CM\_部分\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_partial_resource_descriptor)生と翻訳されたリソースに対して 1 つずつの構造します。 割り当てられたメモリ アドレスごとに 1 つの構造を提供する PnP マネージャー、割り込みメッセージ**型** = **CmResourceTypeInterrupt**と**フラグ**= CM\_リソース\_INTERRUPT\_LATCHED |CM\_リソース\_INTERRUPT\_メッセージ。

MSI を使用して、ドライバーのみを受信する割り込みリソース記述子が 1 つ、すべてのメッセージが同じアドレスを共有するために注意してください。 **MessageCount**のメンバー **u.MessageInterrupt.Raw**割り当てられているメッセージの数を決定するために使用できます。 MSI X を使用する場合、ドライバーは、割り込みメッセージごとに個別のリソースの記述子を受信します。

Windows 8 のオペレーティング システムではデバイス関数あたり 2,048 個以下の割り込みメッセージ用のリソースの要求をできません。 Windows 7 および Windows Vista では、オペレーティング システムではデバイス関数あたり以上 910 割り込みメッセージ リソース要求をできません。 デバイス ドライバーは、この制限を超えている場合、デバイスが起動に失敗します。 多くの論理プロセッサを含むコンピューターで動作するためのドライバーを有効にするには、ドライバーは 1 プロセッサあたり 1 つ以上の割り込みを要求しないようにする必要があります。

システムは、割り込みのリソースの再分配、中に、PnP マネージャーは、リソース要件の一覧から別の割り込みのリソースの推奨セットを選択するためのドライバーを求められるあります。 ただし、PnP マネージャー割り当てることはできません常に、ドライバーをドライバーが希望しているリソース。 ドライバーする必要がありますので、しなくても許容エラー、任意のリソース要件の一覧から別の割り込みのリソース セットの割り当て。 たとえば、デバイスの割り当ては、要求のドライバーよりもメッセージの割り込みの数を減らしてに可能性があります。 最悪の場合は、行ベースの割り込みを 1 つだけでデバイスの動作にドライバーを準備する必要があります。

 

 




