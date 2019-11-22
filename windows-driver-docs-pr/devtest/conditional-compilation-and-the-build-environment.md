---
title: 条件付きコンパイルとビルド環境
description: 条件付きコンパイルとビルド環境
ms.assetid: 7879b6c6-4985-4817-a8bc-b287397df721
keywords:
- DBG プリプロセッサ定数
- コードのデバッグ WDK、条件付きコンパイル
- コードをデバッグする WDK、ビルド環境
- 条件付きコンパイルの WDK デバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 053e26b6b69656a7f4141045dda46e920d94e8f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840293"
---
# <a name="conditional-compilation-and-the-build-environment"></a>条件付きコンパイルとビルド環境


## <span id="ddk_conditional_compilation_and_the_build_environment_tools"></span><span id="DDK_CONDITIONAL_COMPILATION_AND_THE_BUILD_ENVIRONMENT_TOOLS"></span>


Windows Driver Kit (WDK) 8 を使用する場合は、[リリース (無料)] または [デバッグ] (チェック済み) の構成を選択することで、ドライバーのデバッグコードを条件付きでコンパイルできます。 選択した構成によって、 **DBG**プリプロセッサ定数が設定されます。

**DBG**の値は、ドライバーをビルドするために選択したビルド構成によって異なります。

-   デバッグ (チェック) 構成を使用してドライバーを作成した場合、 **DBG**は1と等しくなります。

-   リリース (無料) のビルド構成を使用してドライバーを作成した場合、 **DBG**は0に等しくなります (または、wdm も ntddk も含まれていない場合は未定義になります)。

デバッグルーチン[**ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))、 [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)、 [**KdBreakPoint**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))、 [**KdBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus)、 [**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)、および[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)は、実際には、 **DBG**の値に応じて条件付きで定義されるマクロです。 0の場合、これらのマクロは ops ではありません。 そのため、これらのマクロは、ドライバーのデバッグ (チェックされた) ビルドでのみアクティブになります。

  **メモ**"Kd" で始まるすべてのデバッグルーチンは、 **KdRefreshDebuggerNotPresent**を除いて、ドライバーの無償ビルドには影響しません。

 

Visual Studio と MSBuild を使用してドライバーのリリースバージョンとデバッグバージョンを作成する方法の詳細については、「[ドライバー](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)と[WDK および Visual Studio ビルド環境](wdk-and-visual-studio-build-environment.md)のビルド」を参照してください。

 

 





