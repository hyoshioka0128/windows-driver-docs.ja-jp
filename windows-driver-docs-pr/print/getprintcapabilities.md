---
title: GetPrintCapabilities
description: IPrintTicketProvider GetPrintCapabilities ルーチンでは、有効な PrintCapabilities ドキュメントを返す必要があります。
ms.assetid: 9c9bd387-5ea2-4758-a967-190a711cd8c3
keywords:
- GetPrintCapabilities
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2c50be04253a076c730986ec24ceca8fdb563d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369002"
---
# <a name="getprintcapabilities"></a>GetPrintCapabilities


[ **IPrintTicketProvider::GetPrintCapabilities** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554365(v=vs.85))ルーチンは、有効な PrintCapabilities ドキュメントを返す必要があります。 基本的な実装では、使用できる非常に単純なただし印刷ドライバーは、PrintCapabilities ドキュメントで公開されていない印刷チケットでの機能をサポートできません。 プリンター ドライバーに印刷チケットのサポートを追加すると、このルーチンに戻って PrintCapabilities ドキュメントをそれらの機能を追加する必要があります。

システムでは、システムが、DEVMODE-PrintTicket を変換で提供される機能の場合でも、既定の PrintCapabilities ドキュメントは提供されません。 印刷ドライバーは、作成し、対応する PrintCapabilities ドキュメントを返す必要があります。

 

 




