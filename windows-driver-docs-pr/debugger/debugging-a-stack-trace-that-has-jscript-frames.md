---
title: JScript フレームがあるスタック トレースのデバッグ
description: JScript スタック ダンプの作成と使用の機能は、JScript のフレームを収集して、デバッガーの物理的なフレームに対しての結合で動作します。
ms.assetid: A470809F-55AA-4A49-B181-EC8D22C84F31
keywords:
- JScript
- jscript9diagdump.dll
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bdcca140685e6173392cd5fecc5ba0e60fd7621
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324554"
---
# <a name="debugging-a-stack-trace-that-has-jscript-frames"></a>JScript フレームがあるスタック トレースのデバッグ


JScript スタック ダンプの作成と使用の機能は、JScript のフレームを収集して、デバッガーの物理的なフレームに対しての結合で動作します。 時に x86 プラットフォーム、スタックは正しくトレース デバッガーの構成要素。

スタックには、正しくない可能性がありますと思われる JScript フレームが含まれている場合は、デバッガーで、次のコマンドを入力します。

**.stkwalk\_強制\_フレーム\_ポインター 1**

 

 





