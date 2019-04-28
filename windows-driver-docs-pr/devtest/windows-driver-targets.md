---
title: Windows ドライバーのターゲット
description: WindowsDriver.Common.targets、WindowsDriver.masm.targets、WindowsDriver.arm.targets ファイルは、ドライバーをビルドするために必要なターゲットを提供します。
ms.assetid: 9D04792B-2736-4871-A53E-6B90509133A7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc8363e8df2f936b7b9fcad0b31579b86d88abda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379117"
---
# <a name="windows-driver-targets"></a>Windows ドライバーのターゲット


WindowsDriver.Common.targets、WindowsDriver.masm.targets、WindowsDriver.arm.targets ファイルは、ドライバーをビルドするために必要なターゲットを提供します。

WindowsDriver.masm.targets と WindowsDriver.arm.targets、具体的には、アセンブリ ファイルを構築するためのターゲットを定義します。

これらのターゲットは、それらを直接変更することがなく、Cpp ターゲットを拡張します。 MSBuild は、拡張機能間の順序を保証するために使用される元のメカニズムを維持しながら、動作を挿入するための元のプロジェクトの構造に依存しないメカニズムを提供します。

 

 





