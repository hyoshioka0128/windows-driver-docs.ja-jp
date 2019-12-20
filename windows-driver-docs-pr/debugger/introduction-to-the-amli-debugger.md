---
title: AMLI Debugger の概要
description: AMLI Debugger の概要
ms.assetid: f210171c-2226-4bd6-bbb4-aee4b087e575
keywords:
- AMLI デバッガー、概要
- ACPI デバッグ、コンピューターの言語
- AML インタープリター
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: dd8d79b5d5c0f296b8dc36f19405b5f013c609ae
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209838"
---
# <a name="introduction-to-the-amli-debugger"></a>AMLI Debugger の概要


## <span id="ddk_introduction_to_the_amli_debugger_dbg"></span><span id="DDK_INTRODUCTION_TO_THE_AMLI_DEBUGGER_DBG"></span>


標準のカーネルモードコードのデバッグと ACPI (Advanced Configuration and Power Interface) BIOS のデバッグには大きな違いがあります。

Windows とそのドライバーは、特定のプロセッサ用にコンパイルされたバイナリマシンコードで構成されますが、ACPI BIOS のコアはコンピューターコードには含まれていません。 代わりに、ACPI コンピューター言語 (AML) として格納され、実行時に Microsoft AML インタープリターによって処理されます。

Microsoft AMLI デバッガーは、AML コードをデバッグできる特殊なデバッグツールのセットです。 

Windows 10 より前のバージョンの Windows では、バージョン1803のチェックを行った Windows ACPI ドライバー (Acpi) のビルドが使用されていました。 これは、チェックされたビルドが提供されなくなった場合のケースではなくなりました。

AMLI デバッガーは、完全に64ビットに対応しています。 ターゲットコンピューターまたはホストコンピューターで使用されているプロセッサに関係なく、AMLI デバッガーは正常に機能します。

 

 





