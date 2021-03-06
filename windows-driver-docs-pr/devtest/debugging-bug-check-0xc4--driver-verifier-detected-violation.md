---
title: バグ チェック 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION のデバッグ
description: Driver Verifier に違反が検出される場合は、コンピューターを停止させるバグ チェックが生成されます。
ms.assetid: 4B957C57-9095-4C81-9EBC-C92C620C5824
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2007bad7c6b0e5b69199f9e21565cf24610aabb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371564"
---
# <a name="debugging-bug-check-0xc4-driververifierdetectedviolation"></a>バグ チェック 0xC4 のデバッグ: ドライバー\_VERIFIER\_検出\_違反


場合[Driver Verifier](driver-verifier.md)違反が検出される、コンピューターを停止するバグ チェックが生成されます。 これは、問題をデバッグ可能なほとんどの情報を提供します。 Driver Verifier の生成より頻繁にバグのいずれかを確認しますが[ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)します。 このセクションでは、これらの違反をデバッグするため、いくつかの戦略の例について説明します。

ときに[Driver Verifier](driver-verifier.md)問題、 [ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)違反の具体的な原因を指定するパラメーター 1 の値 (またはサブコード) を使用します。 **バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**200 を超える違反を検出します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [ドライバーのメモリ リークのデバッグ\_VERIFIER\_検出\_違反 (C4)。0x62](debugging-memory-leaks---driver-verifier-detected-violation--c4---0x62.md)
-   [デッドロックのドライバーをデバッグ\_VERIFIER\_検出\_違反 (C4)。0x1001](debugging-deadlocks---driver-verifier-detected-violation--c4---0x1001.md)
-   [DDI 準拠のバグのドライバーをデバッグ\_VERIFIER\_検出\_違反 (C4)。0x20002 - 0x20022](debugging-ddi-compliance-bugs----driver-verifier-detected-violation--c4---0x000200--.md)
-   [ドライバーの NDIS/WiFi タイムアウト エラーをデバッグ\_VERIFIER\_検出\_違反 (C4)](debugging-ndis-wifi-timeouts---driver-verifier-detected-violation--c4---0x92003--etc-.md)

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件


-   実行[Driver Verifier](driver-verifier.md)コンピューターをテストするために予約されています。
-   テスト コンピューターでのカーネル デバッグを有効にします。

詳細については、次を参照してください。 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)と[をバグ チェック時にドライバーの検証ツールの処理が有効になっている](https://docs.microsoft.com/windows-hardware/drivers/debugger/handling-a-bug-check-when-driver-verifier-is-enabled)します。

 

 





