---
title: ControllerControl ルーチンの記述
description: ControllerControl ルーチンの記述
ms.assetid: 9330e0ff-c4bb-4aa6-985e-ef89791f74df
keywords:
- コント ローラー オブジェクトの WDK カーネル、ControllerControl ルーチンを記述
- 書き込みの ControllerControl ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4835a144472bc9f80019630ff64fd76a8996e51c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374117"
---
# <a name="writing-controllercontrol-routines"></a>ControllerControl ルーチンの記述





コント ローラー オブジェクトを使用するドライバーを指定する必要があります、 [ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049) I/O 操作を開始するルーチン。

最下位レベルのデバイス ドライバに類似するデバイスに"AT"ディスク コント ローラーなどの物理的なコント ローラーでの操作を同期する必要がありますを持つことができます、 *ControllerControl*ルーチン。

ドライバーを呼び出すと[ **IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)その*ControllerControl*ルーチンがコント ローラー オブジェクトが使用可能な場合は、ハードウェアがによって表される直前に実行I/O 操作。 それ以外の場合、 *ControllerControl*ルーチンは、コント ローラーが無料になるまでキューに配置します。

**注**  WDM ドライバーは、コント ローラー オブジェクトを使用できないと*ControllerControl*ルーチン。

 

 

 




