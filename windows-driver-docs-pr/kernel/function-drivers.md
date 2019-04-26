---
title: ファンクション ドライバー
description: ファンクション ドライバー
ms.assetid: a6ac329b-ffb0-4bd3-9d54-195fa025d532
keywords:
- 機能ドライバー WDK WDM
- WDK WDM の raw モード
- WDM 関数ドライバー WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17397b0c68258dc7db5e6dd86a5c285c7af9a4f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359944"
---
# <a name="function-drivers"></a>ファンクション ドライバー





A*関数ドライバー*デバイス用のメイン ドライバーは、(可能なドライバーのレイヤーを参照してください)。 PnP マネージャーでは、デバイスの最大で 1 つ関数のドライバーを読み込みます。 関数のドライバーは、1 つまたは複数のデバイスに対応できます。

関数のドライバーでは、そのデバイスの運用上のインターフェイスを提供します。 通常、関数ドライバー読み取りの処理しデバイスに書き込み、電源ポリシーがデバイスを管理します。

デバイスの機能のドライバーは、ポート/ミニポート ドライバーのペアまたはクラス/miniclass ドライバー ペアなど、ドライバー/ミニドライバーのペアとして実装できます。 このようなドライバーのペアで、ミニドライバーは、2 つ目のドライバーは、dll にリンクされます。

デバイスは、raw モードで行われるが場合、ありません関数ドライバーとない上位または下位レベルのフィルター ドライバーがあります。 Raw モードのすべての I/O は、バス ドライバーと省略可能な bus フィルター ドライバーによって行われます。

 

 




