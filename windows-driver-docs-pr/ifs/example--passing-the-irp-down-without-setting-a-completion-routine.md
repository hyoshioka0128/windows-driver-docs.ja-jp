---
title: 完了ルーチンを設定せず、IRP を渡す例
description: 完了ルーチンを設定せず、IRP を渡す例
ms.assetid: d18d3ead-2cec-4ea6-ac4c-b809ba985f23
keywords:
- IRP ディスパッチ ルーチン WDK ファイル システム、IRP を渡す
- デバイス スタック WDK ダウン Irp を渡す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 050059ea570a22973e415e8d4bfcfc6b398d47ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383849"
---
# <a name="example-passing-the-irp-down-without-setting-a-completion-routine"></a>以下に例を示します。完了ルーチンを設定せずに IRP を渡す


## <span id="ddk_example_passing_the_irp_down_without_setting_a_completion_routine_"></span><span id="DDK_EXAMPLE_PASSING_THE_IRP_DOWN_WITHOUT_SETTING_A_COMPLETION_ROUTINE_"></span>


完了ルーチンを設定せず、下位レベルのドライバーに IRP を渡すためディスパッチ ルーチンは、次の操作を行う必要があります。

-   呼び出す[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355) IRP が完了 IRP の処理を実行するときの完了のルーチンが I/O マネージャーを検索しませんようにの場所をスタックを現在の削除します。

-   呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)を次の下位レベルのドライバーに IRP を渡します。

この手法は、次のコード例に示します。

```cpp
IoSkipCurrentIrpStackLocation ( Irp ); 
return IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
```

または同等にします。

```cpp
IoSkipCurrentIrpStackLocation ( Irp ); 
status = IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
/* log or debugprint the status value here */
return status; 
```

これらの例では、呼び出しの最初のパラメーターで[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)下位レベルの次のフィルター ドライバーのデバイス オブジェクトへのポインターです。 2 番目のパラメーターは、IRP へのポインターです。

### <a name="span-idadvantagesofthisapproachspanspan-idadvantagesofthisapproachspanspan-idadvantagesofthisapproachspanadvantages-of-this-approach"></a><span id="Advantages_of_This_Approach"></span><span id="advantages_of_this_approach"></span><span id="ADVANTAGES_OF_THIS_APPROACH"></span>このアプローチの利点

前に示した手法 (呼び出し[ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)) を簡単かつ効率的と登録を行わずに、ドライバーが IRP がドライバー スタック ダウンを通過するすべてのケースで使用する必要があります、メモリを割り当てます。

### <a name="span-iddisadvantagesofthisapproachspanspan-iddisadvantagesofthisapproachspanspan-iddisadvantagesofthisapproachspandisadvantages-of-this-approach"></a><span id="Disadvantages_of_This_Approach"></span><span id="disadvantages_of_this_approach"></span><span id="DISADVANTAGES_OF_THIS_APPROACH"></span>このアプローチの欠点

後[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)を呼び出すに渡された IRP ポインター**保留**が無効にして、安全に逆参照することはできません。 を、ドライバーが IRP がドライバーの下位レベルで処理された後に、さらに処理するか、クリーンアップを実行する必要がある場合は、ドライバー スタック ダウン IRP を送信する前に完了ルーチンを設定があります。 書き込みと設定完了ルーチンの詳細については、次を参照してください。[完了ルーチンを使用して](using-irp-completion-routines.md)します。

呼び出す場合[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)の IRP では、その完了ルーチンを設定することはできません。

 

 




