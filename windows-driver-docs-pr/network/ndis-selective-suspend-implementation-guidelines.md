---
title: 選択的 NDIS 中断実装ガイドライン
description: 選択的 NDIS 中断実装ガイドライン
ms.assetid: 70548C06-B944-4040-AEA2-4FB6098EBA9E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9494d87b5cc658bdb9f1c5db0787458e5403b89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535745"
---
# <a name="ndis-selective-suspend-implementation-guidelines"></a>選択的 NDIS 中断実装ガイドライン


このセクションでは、NDIS 選択的に実装するためのガイドラインは、ミニポート ドライバーの中断を提供します。 理解しておく必要があります、 [NDIS 選択の概要を中断](overview-of-ndis-selective-suspend.md)このセクションを読む前にします。

このセクションには、次のガイドラインが含まれます。

[選択的 NDIS のリソースを管理する IRP を中断します。](managing-irp-resources-for-ndis-selective-suspend.md)

[実装する、 *MiniportIdleNotification*ハンドラー関数](implementing-a-miniportidlenotification-handler-function.md)

[実装する、 *MiniportCancelIdleNotification*ハンドラー関数](implementing-a-miniportcancelidlenotification-handler-function.md)

 

 





