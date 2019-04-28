---
title: AMLI Debugger の概要
description: AMLI Debugger の概要
ms.assetid: f210171c-2226-4bd6-bbb4-aee4b087e575
keywords:
- AMLI デバッガー, 概要
- ACPI は、コンピューター言語のデバッグ
- AML インタープリター
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5334a3161e53046fa48f8020bf03d90bdfe9213f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374344"
---
# <a name="introduction-to-the-amli-debugger"></a>AMLI Debugger の概要


## <span id="ddk_introduction_to_the_amli_debugger_dbg"></span><span id="DDK_INTRODUCTION_TO_THE_AMLI_DEBUGGER_DBG"></span>


標準のカーネル モード コードのデバッグと ACPI (Advanced Configuration and Power Interface) BIOS のデバッグの間に大きな違いがあります。

Windows とそのドライバーは、特定のプロセッサ用にコンパイルされたバイナリのマシン コードで構成されますが、ACPI BIOS のコアのマシン語コードにないです。 代わりに、ACPI 機械語 (AML) として格納し、それが実行されると、Microsoft AML インタープリターによって処理されます。

Microsoft AMLI デバッガーには、AML コードをデバッグできる特別なデバッグ ツールのセットです。 

Windows 10 より前に、の Windows のバージョンでは、Windows の ACPI ドライバー (Acpi.sys) のバージョン 1803 チェック ビルドが使用されました。 このケースではなくなりました。

AMLI デバッガーが完全には、64 ビットに注意してください。 どのようなプロセッサは、対象のコンピューターまたはホスト コンピューターで使用されているに関係なくは AMLI デバッガーが正しく機能します。

 

 





