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
ms.openlocfilehash: 01d7fddd58f0f6660af7e8ef44960367963ce962
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570139"
---
# <a name="conditional-compilation-and-the-build-environment"></a>条件付きコンパイルとビルド環境


## <span id="ddk_conditional_compilation_and_the_build_environment_tools"></span><span id="DDK_CONDITIONAL_COMPILATION_AND_THE_BUILD_ENVIRONMENT_TOOLS"></span>


Windows Driver Kit (WDK) 8 を使用する場合は、リリース (無料) または (オン) デバッグ構成を選択してコードのデバッグには、ドライバーで条件付きでコンパイルできます。 セットを選択した構成、 **DBG**プリプロセッサ定数です。

値**DBG**ドライバーのビルドを選択するビルド構成によって異なります。

-   デバッグ (オン) 構成を使用して、ドライバーを作成する場合**DBG** 1 になります。

-   リリース ビルド (無料) の構成を使用して、ドライバーを作成する場合**DBG** 0 になります (または未定義になります wdm.h も ntddk.h が含まれている場合)。

デバッグ ルーチン[ **ASSERT**](https://msdn.microsoft.com/library/windows/hardware/ff542107)、 [ **ASSERTMSG**](https://msdn.microsoft.com/library/windows/hardware/ff542113)、 [ **KdBreakPoint**](https://msdn.microsoft.com/library/windows/hardware/ff548063)、 [ **KdBreakPointWithStatus**](https://msdn.microsoft.com/library/windows/hardware/ff548065)、 [ **KdPrint**](https://msdn.microsoft.com/library/windows/hardware/ff548092)、および[ **KdPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548100)の値によって条件付きで定義されているマクロが実際に**DBG**します。 0 の場合、これらのマクロは操作不要にします。 そのため、これらのマクロは、ドライバーの (オン) デバッグ ビルドでのみアクティブです。

**注**  名前が"Kd"で始まるすべてのデバッグ ルーチンがある影響しない、ドライバーの無料のビルドで除く**KdRefreshDebuggerNotPresent**します。

 

Visual Studio および MSBuild を使用して、リリース バージョンとデバッグのドライバーのバージョンを作成する方法の詳細については、次を参照してください。[ドライバーをビルド](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)と[WDK と Visual Studio ビルド環境](wdk-and-visual-studio-build-environment.md)します。

 

 





