---
title: ポインター DrvSetPointerShape を制御します。
description: ポインター DrvSetPointerShape を制御します。
ms.assetid: 14d782de-5da8-40e9-a3e3-91d2588146e0
keywords:
- 描画ポインター WDK Windows 2000 を表示します。
- ディスプレイ ドライバー WDK Windows 2000 では、ポインター
- Windows 2000 の WDK のポインターを表示します。
- DrvSetPointerShape
- Windows 2000 の WDK のポインターの表示の図形
- Windows 2000 の WDK のポインターの表示形状を変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f2cf9b4c63d0f0be27413b3790b0f04237087f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392657"
---
# <a name="controlling-the-pointer-drvsetpointershape"></a>ポインターの制御: DrvSetPointerShape


## <span id="ddk_controlling_the_pointer_drvsetpointershape_gg"></span><span id="DDK_CONTROLLING_THE_POINTER_DRVSETPOINTERSHAPE_GG"></span>


ディスプレイ ドライバーが、ポインターを制御する場合、ドライバーをサポートする必要があります[ **DrvSetPointerShape** ](https://msdn.microsoft.com/library/windows/hardware/ff556289)変更するポインターの形を許可します。 DrvSetPointerShape への呼び出しでは、次の結果が生成されます。

1.  関数は、ディスプレイ ドライバーが引かれている既存のポインターを削除します。

2.  関数は、図形を処理することがある場合を除き、新しい要求された図形を設定します。

3.  新しいポインターは、呼び出しのパラメーターで示された位置に表示されます。

ドライバーを呼び出すことができます[ **EngSetPointerShape** ](https://msdn.microsoft.com/library/windows/hardware/ff565017) GDI ソフトウェア カーソルを管理します。

 

 





