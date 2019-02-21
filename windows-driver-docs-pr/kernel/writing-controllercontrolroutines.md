---
title: 書き込み ControllerControl ルーチン
description: 書き込み ControllerControl ルーチン
ms.assetid: 9330e0ff-c4bb-4aa6-985e-ef89791f74df
keywords:
- コント ローラー オブジェクトの WDK カーネル、ControllerControl ルーチンを記述
- 書き込みの ControllerControl ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcec280f64accb304c28a3b0eee798b30f99d235
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539298"
---
# <a name="writing-controllercontrol-routines"></a>書き込み ControllerControl ルーチン





コント ローラー オブジェクトを使用するドライバーを指定する必要があります、 [ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049) I/O 操作を開始するルーチン。

最下位レベルのデバイス ドライバに類似するデバイスに"AT"ディスク コント ローラーなどの物理的なコント ローラーでの操作を同期する必要がありますを持つことができます、 *ControllerControl*ルーチン。

ドライバーを呼び出すと[ **IoAllocateController**](https://msdn.microsoft.com/library/windows/hardware/ff548224)その*ControllerControl*ルーチンがコント ローラー オブジェクトが使用可能な場合は、ハードウェアがによって表される直前に実行I/O 操作。 それ以外の場合、 *ControllerControl*ルーチンは、コント ローラーが無料になるまでキューに配置します。

**注**  WDM ドライバーは、コント ローラー オブジェクトを使用できないと*ControllerControl*ルーチン。

 

 

 




