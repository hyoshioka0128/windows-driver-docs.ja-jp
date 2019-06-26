---
title: 条件付きコンパイルとビルド環境
description: 条件付きコンパイルとビルド環境
ms.assetid: 7879b6c6-4985-4817-a8bc-b287397df721
keywords:
- DBG プリプロセッサ定数
- WDK、条件付きコンパイルのコードのデバッグ
- WDK ビルド環境のコードのデバッグ
- 条件付きコンパイル WDK のデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6550d4411052d1a90e7dd87871f245f46976ad4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371585"
---
# <a name="conditional-compilation-and-the-build-environment"></a>条件付きコンパイルとビルド環境


## <span id="ddk_conditional_compilation_and_the_build_environment_tools"></span><span id="DDK_CONDITIONAL_COMPILATION_AND_THE_BUILD_ENVIRONMENT_TOOLS"></span>


Windows Driver Kit (WDK) 8 を使用する場合は、リリース (無料) または (オン) デバッグ構成を選択してコードのデバッグには、ドライバーで条件付きでコンパイルできます。 セットを選択した構成、 **DBG**プリプロセッサ定数です。

値**DBG**ドライバーのビルドを選択するビルド構成によって異なります。

-   デバッグ (オン) 構成を使用して、ドライバーを作成する場合**DBG** 1 になります。

-   リリース ビルド (無料) の構成を使用して、ドライバーを作成する場合**DBG** 0 になります (または未定義になります wdm.h も ntddk.h が含まれている場合)。

デバッグ ルーチン[ **ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))、 [ **ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-assertmsg)、 [ **KdBreakPoint**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))、 [ **KdBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdbreakpointwithstatus)、 [ **KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprint)、および[ **KdPrintEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprintex)の値によって条件付きで定義されているマクロが実際に**DBG**します。 0 の場合、これらのマクロは操作不要にします。 そのため、これらのマクロは、ドライバーの (オン) デバッグ ビルドでのみアクティブです。

**注**  名前が"Kd"で始まるすべてのデバッグ ルーチンがある影響しない、ドライバーの無料のビルドで除く**KdRefreshDebuggerNotPresent**します。

 

Visual Studio および MSBuild を使用して、リリース バージョンとデバッグのドライバーのバージョンを作成する方法の詳細については、次を参照してください。[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)と[WDK と Visual Studio ビルド環境](wdk-and-visual-studio-build-environment.md)します。

 

 





