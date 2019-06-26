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
ms.openlocfilehash: 08df0df5dd7ce393442a4bc1af60648c605b0fec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384225"
---
# <a name="life-cycle-of-an-object"></a>オブジェクトのライフ サイクル





このトピックで説明されるオブジェクトの「ライフ サイクル」、オブジェクトの参照しオブジェクト マネージャーによって追跡する方法。 このトピックでは、一時的または永続的なオブジェクトを作成する方法も説明します。

### <a name="object-reference-count"></a>オブジェクトの参照カウント

オブジェクト マネージャーは、オブジェクトへの参照の数のカウントを保持します。 オブジェクトが作成されると、オブジェクト マネージャーは、1 つに、オブジェクトの参照カウントを設定します。 そのカウンターがゼロになる、オブジェクトが解放されます。

ドライバーは、オブジェクト マネージャーが、正確な参照カウントのすべてのオブジェクトを操作することを確認する必要があります。 途中でリリースされているオブジェクトには、システムがクラッシュする可能性があります。 参照カウントが誤って高オブジェクトは解放されません。

ハンドルまたはポインターのいずれかのオブジェクトを参照できます。 だけでなく、参照カウントは、オブジェクト マネージャーは、オブジェクトを開いているハンドルの数を保持します。 ルーチンはハンドルを開いて、それぞれは、オブジェクトの参照カウントとオブジェクトのハンドル数の両方を 1 つずつ増加します。 このようなルーチンを呼び出すたびに対応する呼び出しと照合する必要があります[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)します。 詳細については、次を参照してください。[オブジェクトは処理](object-handles.md)します。

カーネル モードでは、オブジェクトへのポインターでオブジェクトを参照できます。 など、オブジェクトにポインターを返すルーチン[ **IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference)、参照カウントを 1 ずつ増加します。 ドライバーが完了すると、ポインターを使用して呼び出す必要があります[ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)をいずれかによって、参照カウントを減らします。

次のすべてのルーチンは、オブジェクトの参照カウントを 1 ずつ増加します。

[**ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excreatecallback)

[**IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference)

[**IoGetDeviceObjectPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)

[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)

[**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)

[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)

[**ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)

前のルーチンのいずれかに実行される各呼び出しに対応する呼び出しと一致する必要があります**ObDereferenceObject**します。

**ObReferenceObject**と**ObReferenceObjectByPointer**ルーチンが提供されるためのドライバーは、既知のオブジェクト ポインターの参照カウントを増やすことができますを 1 つ。 **ObReferenceObject**単に参照カウントが増加します。 **ObReferenceObjectByPointer**は参照カウントを増やす前に、アクセス チェックします。

**ObReferenceObjectByHandle**ルーチンは、オブジェクト ハンドルを受信し、基になるオブジェクトへのポインターを提供します。 1 つの参照カウントが増加します。

### <a name="temporary-and-permanent-objects"></a>一時的および永続的なオブジェクト

ほとんどのオブジェクトは*一時*;、使用されていると、オブジェクト マネージャーによって解放される限り存在します。 あるオブジェクトを作成できます*永続的な*します。 オブジェクトは、永続的に、オブジェクト マネージャー自体は、オブジェクトへの参照を保持します。 したがって、参照カウントが 0 より大きい間、使用中になったときに、オブジェクトが解放されません。

限りそのハンドルの数が 0 以外の場合、一時オブジェクトを名前でアクセスできます。 ハンドルの数をデクリメント 0、オブジェクトの名前には、オブジェクト マネージャーの名前空間から削除されるとします。 参照カウントが 0 より大きい限り、このようなオブジェクトはまだポインターによってアクセスできます。 存在する限り、永続的なオブジェクトを名前でアクセスできます。

オブジェクトにできる永続的な作成時に、OBJ を指定することによって\_で永続的な属性、 [**オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_object_attributes)オブジェクトの構造体。 詳細については、次を参照してください。 [ **InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/nf-wudfwdm-initializeobjectattributes)します。

永続的なオブジェクトを一時的にするために、使用、 [ **ZwMakeTemporaryObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwmaketemporaryobject)ルーチン。 このルーチンは、オブジェクトを使用してが自動的に削除します。 (開いているハンドル オブジェクトがない場合は、オブジェクトの名前は直ちに削除オブジェクト マネージャーの名前空間。 オブジェクト自体は、参照カウントがゼロになるまでです。)

 

 




