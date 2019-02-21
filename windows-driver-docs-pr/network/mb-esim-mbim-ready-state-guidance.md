---
title: MB eSIM MBIM 準備完了状態のガイダンス
description: MB eSIM MBIM 準備完了状態のガイダンス
ms.assetid: E7EB5E6D-1858-4B94-AF91-05333CC93D8B
ms.date: 08/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a74ff0333adb8772a2b355e4c43819cf34ff738
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552489"
---
# <a name="mb-esim-mbim-ready-state-guidance"></a>MB eSIM MBIM 準備完了状態のガイダンス

このトピックでは、Windows 10 バージョン 1709 以降の eSIM シナリオの予期される MBIM 準備完了状態でガイダンスを示します。 OS が正しくシナリオのすべての変更を処理することにより、正しい準備完了状態に準拠しています。 

> [!IMPORTANT]
> すべてのシナリオとこのトピックの状態は、eSIM 対応カードは executor 0 の場合、既定のエグゼキュータにマップされ、電源が入っていることを想定しています。

| シナリオ | MBIM_MS_UICCSLOT_STATE | MBIM_SUBSCRIBER_READY_STATE |
| --- | --- | --- |
| MF のみ (プロファイルがありません) と eSIM | MBIMMsUICCSlotStateActiveEsimNoProfiles | MBIMSubscriberReadyStateNoEsimProfile |
| esim 状で有効になっているプロファイルがありません。 | MBIMMsUICCSlotStateActiveEsimNoProfiles | MBIMSubscriberReadyStateNoEsimProfile |
| 有効になっているプロファイルと eSIM | MBIMMsUICCSlotStateActiveEsim | MBIMSubscriberReadyStateInitialized |
| パススルー モードで eSIM | MBIMMsUICCSlotStateActiveEsimNoProfiles | MBIMSubscriberReadyStateNotInitialized |

MBIM_MS_UICCSLOT_STATE と MBIM_SUBSCRIBER_READY_STATE の両方での変更が必要なときにスロットの状態の変更の準備完了状態の変更前にする必要があります。 

ときに、新しいプロファイルを有効にするプロファイル間の切り替え、準備完了状態を持つ必要が次のフローします。

![eSIM MBIM プロファイルを切り替えるときにフローの状態が準備完了](images/esim_mbim_ready_state_flow.png "eSIM MBIM プロファイルを切り替えるときにフローの状態が準備完了")

MBIM_MS_UICCSLOT_STATE に関する詳細については、MBIM_MS_UICCSLOT_STATE 表を参照して[MB マルチ SIM 操作 (MBIM_CID_MS_SLOT_INFO_STATUS)](mb-multi-sim-operations.md)します。

MBIM_SUBSCRIBER_READY_STATE に関する詳細については、の 10.5.2.3」セクションを参照してください。[パブリック USB MBIM 標準](https://go.microsoft.com/fwlink/p/?linkid=842064)します。

