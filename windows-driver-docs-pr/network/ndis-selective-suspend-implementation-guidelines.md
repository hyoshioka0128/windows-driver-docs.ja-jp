---
title: NDIS セレクティブ サスペンド実装ガイドライン
description: NDIS セレクティブ サスペンド実装ガイドライン
ms.assetid: 70548C06-B944-4040-AEA2-4FB6098EBA9E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9494d87b5cc658bdb9f1c5db0787458e5403b89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387151"
---
# <a name="ndis-selective-suspend-implementation-guidelines"></a>NDIS セレクティブ サスペンド実装ガイドライン


このセクションでは、NDIS 選択的に実装するためのガイドラインは、ミニポート ドライバーの中断を提供します。 理解しておく必要があります、 [NDIS 選択の概要を中断](overview-of-ndis-selective-suspend.md)このセクションを読む前にします。

このセクションには、次のガイドラインが含まれます。

[選択的 NDIS のリソースを管理する IRP を中断します。](managing-irp-resources-for-ndis-selective-suspend.md)

[実装する、 *MiniportIdleNotification*ハンドラー関数](implementing-a-miniportidlenotification-handler-function.md)

[実装する、 *MiniportCancelIdleNotification*ハンドラー関数](implementing-a-miniportcancelidlenotification-handler-function.md)

 

 





