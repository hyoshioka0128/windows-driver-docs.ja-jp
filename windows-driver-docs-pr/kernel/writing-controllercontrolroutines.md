---
title: ControllerControl ルーチンの記述
description: ControllerControl ルーチンの記述
ms.assetid: 9330e0ff-c4bb-4aa6-985e-ef89791f74df
keywords:
- コントローラーオブジェクト WDK カーネル、コントローラー制御ルーチンの記述
- コントローラー制御ルーチン、書き込み
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 987eb4b8f3150ce4435a003aa7250c668f2c824e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835591"
---
# <a name="writing-controllercontrol-routines"></a>ControllerControl ルーチンの記述





コントローラーオブジェクトを使用するドライバーは、i/o 操作を開始するためのコントローラー[*制御*](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチンを提供する必要があります。

"AT" ディスクコントローラーなどの物理コントローラーを介して操作を同一のデバイスに同期する必要がある、最低レベルのデバイスドライバーは、コントローラー*制御*ルーチンを持つことができます。

ドライバーが[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)を呼び出すと、コントローラーオブジェクトによって表されるハードウェアを i/o 操作に使用できる場合は *、そのコントローラーのコントローラー*のコントローラーが直ちに実行されます。 それ以外の場合、コントローラーが解放されるまでコントローラーの*制御*ルーチンがキューに入れられます。

**  WDM**ドライバーでは、コントローラーオブジェクトとコントローラー*制御*ルーチンを使用できません。

 

 

 




