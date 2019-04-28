---
title: オブジェクトのライフ サイクル
description: オブジェクトのライフ サイクル
ms.assetid: e81bfce6-27c4-4916-adc8-9c014d02bee7
keywords:
- オブジェクトのライフ サイクルの WDK カーネル
- WDK オブジェクトのライフ サイクル
- オブジェクトを参照します。
- オブジェクト参照は、WDK のカーネルをカウントします。
- 一時オブジェクトの WDK カーネル
- 永続的なオブジェクトの WDK カーネル
- 参照カウントの WDK オブジェクト
- 解放されたオブジェクトの WDK カーネル
- オブジェクトの一時的な状態の WDK カーネル
- オブジェクトの永続的な状態の WDK カーネル
- 自動オブジェクトの削除の WDK カーネル
- WDK のカーネルを追跡するオブジェクト
- オブジェクト ハンドル WDK カーネルを開く
- WDK のオブジェクトの参照をカウント
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ee77d2900138b800722496dd6c4cc3128f6f295
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381366"
---
# <a name="life-cycle-of-an-object"></a>オブジェクトのライフ サイクル





このトピックで説明されるオブジェクトの「ライフ サイクル」、オブジェクトの参照しオブジェクト マネージャーによって追跡する方法。 このトピックでは、一時的または永続的なオブジェクトを作成する方法も説明します。

### <a name="object-reference-count"></a>オブジェクトの参照カウント

オブジェクト マネージャーは、オブジェクトへの参照の数のカウントを保持します。 オブジェクトが作成されると、オブジェクト マネージャーは、1 つに、オブジェクトの参照カウントを設定します。 そのカウンターがゼロになる、オブジェクトが解放されます。

ドライバーは、オブジェクト マネージャーが、正確な参照カウントのすべてのオブジェクトを操作することを確認する必要があります。 途中でリリースされているオブジェクトには、システムがクラッシュする可能性があります。 参照カウントが誤って高オブジェクトは解放されません。

ハンドルまたはポインターのいずれかのオブジェクトを参照できます。 だけでなく、参照カウントは、オブジェクト マネージャーは、オブジェクトを開いているハンドルの数を保持します。 ルーチンはハンドルを開いて、それぞれは、オブジェクトの参照カウントとオブジェクトのハンドル数の両方を 1 つずつ増加します。 このようなルーチンを呼び出すたびに対応する呼び出しと照合する必要があります[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。 詳細については、次を参照してください。[オブジェクトは処理](object-handles.md)します。

カーネル モードでは、オブジェクトへのポインターでオブジェクトを参照できます。 など、オブジェクトにポインターを返すルーチン[ **IoGetAttachedDeviceReference**](https://msdn.microsoft.com/library/windows/hardware/ff549145)、参照カウントを 1 ずつ増加します。 ドライバーが完了すると、ポインターを使用して呼び出す必要があります[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)をいずれかによって、参照カウントを減らします。

次のすべてのルーチンは、オブジェクトの参照カウントを 1 ずつ増加します。

[**ExCreateCallback**](https://msdn.microsoft.com/library/windows/hardware/ff544560)

[**IoGetAttachedDeviceReference**](https://msdn.microsoft.com/library/windows/hardware/ff549145)

[**IoGetDeviceObjectPointer**](https://msdn.microsoft.com/library/windows/hardware/ff549198)

[**IoWMIOpenBlock**](https://msdn.microsoft.com/library/windows/hardware/ff550453)

[**ObReferenceObject**](https://msdn.microsoft.com/library/windows/hardware/ff558678)

[**ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)

[**ObReferenceObjectByPointer**](https://msdn.microsoft.com/library/windows/hardware/ff558686)

前のルーチンのいずれかに実行される各呼び出しに対応する呼び出しと一致する必要があります**ObDereferenceObject**します。

**ObReferenceObject**と**ObReferenceObjectByPointer**ルーチンが提供されるためのドライバーは、既知のオブジェクト ポインターの参照カウントを増やすことができますを 1 つ。 **ObReferenceObject**単に参照カウントが増加します。 **ObReferenceObjectByPointer**は参照カウントを増やす前に、アクセス チェックします。

**ObReferenceObjectByHandle**ルーチンは、オブジェクト ハンドルを受信し、基になるオブジェクトへのポインターを提供します。 1 つの参照カウントが増加します。

### <a name="temporary-and-permanent-objects"></a>一時的および永続的なオブジェクト

ほとんどのオブジェクトは*一時*;、使用されていると、オブジェクト マネージャーによって解放される限り存在します。 あるオブジェクトを作成できます*永続的な*します。 オブジェクトは、永続的に、オブジェクト マネージャー自体は、オブジェクトへの参照を保持します。 したがって、参照カウントが 0 より大きい間、使用中になったときに、オブジェクトが解放されません。

限りそのハンドルの数が 0 以外の場合、一時オブジェクトを名前でアクセスできます。 ハンドルの数をデクリメント 0、オブジェクトの名前には、オブジェクト マネージャーの名前空間から削除されるとします。 参照カウントが 0 より大きい限り、このようなオブジェクトはまだポインターによってアクセスできます。 存在する限り、永続的なオブジェクトを名前でアクセスできます。

オブジェクトにできる永続的な作成時に、OBJ を指定することによって\_で永続的な属性、 [**オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff557749)オブジェクトの構造体。 詳細については、次を参照してください。 [ **InitializeObjectAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff547804)します。

永続的なオブジェクトを一時的にするために、使用、 [ **ZwMakeTemporaryObject** ](https://msdn.microsoft.com/library/windows/hardware/ff566477)ルーチン。 このルーチンは、オブジェクトを使用してが自動的に削除します。 (開いているハンドル オブジェクトがない場合は、オブジェクトの名前は直ちに削除オブジェクト マネージャーの名前空間。 オブジェクト自体は、参照カウントがゼロになるまでです。)

 

 




