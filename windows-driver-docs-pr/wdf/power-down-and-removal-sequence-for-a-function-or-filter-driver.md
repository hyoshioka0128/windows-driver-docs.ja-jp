---
title: 電源と関数、またはフィルター ドライバーの削除順序
description: 電源と関数、またはフィルター ドライバーの削除順序
ms.assetid: E5A22C91-5967-42D6-A991-42B46C72ED82
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b5a0af13f2c8bfdd379ebbcfa0a6aafe0abbbe9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559440"
---
# <a name="power-down-and-removal-sequence-for-a-function-or-filter-driver"></a>電源と関数、またはフィルター ドライバーの削除順序


次の図は、KMDF 関数または電源をオフのときに、フィルター ドライバーのイベント コールバック関数と、デバイスを削除するフレームワークが呼び出します順序を示します。 シーケンスは、図の上部にある作業の電源の状態 (D0) では、運用のデバイスで始まります。

![関数またはフィルター ドライバーの電源と削除のシーケンス](images/fdo-fido-powerdown3.png)

図に示す、KMDF 電源と削除のシーケンスは、呼び出し元は、デバイスの運用を行うにするフレームワークと呼ばれる関数を逆順で対応する「元に戻す」コールバックが関わります。 フレームワークは、デバイス オブジェクトのコンテキストの領域を削除した後にデバイス オブジェクトを削除します。

 

 





