---
title: Windows ドライバーのターゲット
description: WindowsDriver.Common.targets、WindowsDriver.masm.targets、WindowsDriver.arm.targets ファイルは、ドライバーをビルドするために必要なターゲットを提供します。
ms.assetid: 9D04792B-2736-4871-A53E-6B90509133A7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc8363e8df2f936b7b9fcad0b31579b86d88abda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559066"
---
# <a name="windows-driver-targets"></a>Windows ドライバーのターゲット


WindowsDriver.Common.targets、WindowsDriver.masm.targets、WindowsDriver.arm.targets ファイルは、ドライバーをビルドするために必要なターゲットを提供します。

WindowsDriver.masm.targets と WindowsDriver.arm.targets、具体的には、アセンブリ ファイルを構築するためのターゲットを定義します。

これらのターゲットは、それらを直接変更することがなく、Cpp ターゲットを拡張します。 MSBuild は、拡張機能間の順序を保証するために使用される元のメカニズムを維持しながら、動作を挿入するための元のプロジェクトの構造に依存しないメカニズムを提供します。

 

 





