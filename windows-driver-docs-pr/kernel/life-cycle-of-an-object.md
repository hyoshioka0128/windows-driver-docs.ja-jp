---
title: オブジェクトのライフサイクル
description: オブジェクトのライフサイクル
ms.assetid: e81bfce6-27c4-4916-adc8-9c014d02bee7
keywords:
- オブジェクトのライフサイクル WDK カーネル
- ライフサイクル WDK オブジェクト
- オブジェクトの参照
- オブジェクト参照カウント WDK カーネル
- 一時オブジェクト WDK カーネル
- パーマネントオブジェクト WDK カーネル
- 参照カウント WDK オブジェクト
- 解放されたオブジェクト WDK カーネル
- オブジェクトの一時的な状態 WDK カーネル
- オブジェクト永続的ステータス WDK カーネル
- 自動オブジェクト削除の WDK カーネル
- オブジェクト追跡 WDK カーネル
- open オブジェクトは WDK カーネルを処理します
- カウント参照 WDK オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18bfcd5585e2046f31db3b741014704093be1220
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838559"
---
# <a name="life-cycle-of-an-object"></a>オブジェクトのライフサイクル





このトピックでは、オブジェクトの "ライフサイクル" について説明します。つまり、オブジェクトマネージャーによってオブジェクトが参照および追跡される方法について説明します。 このトピックでは、オブジェクトを一時的または永続的にする方法についても説明します。

### <a name="object-reference-count"></a>オブジェクト参照カウント

オブジェクトマネージャーは、オブジェクトへの参照の数を保持します。 オブジェクトが作成されると、オブジェクトマネージャーによってオブジェクトの参照カウントが1に設定されます。 このカウンターがゼロになると、オブジェクトが解放されます。

ドライバーは、オブジェクトマネージャーが操作するオブジェクトに対して正確な参照カウントを持っていることを確認する必要があります。 オブジェクトが途中で解放されると、システムがクラッシュする可能性があります。 参照カウントが誤って高いオブジェクトは解放されません。

オブジェクトは、ハンドルまたはポインターによって参照できます。 オブジェクトマネージャーは、参照カウントに加えて、オブジェクトに対して開いているハンドルの数を保持します。 ハンドルを開く各ルーチンは、オブジェクト参照カウントとオブジェクトハンドル数の両方を1つ増やします。 このようなルーチンを呼び出すたびに、 [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)への対応する呼び出しが一致している必要があります。 詳細については、「[オブジェクトハンドル](object-handles.md)」を参照してください。

カーネルモードでは、オブジェクトへのポインターによってオブジェクトを参照できます。 [**IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)などのオブジェクトへのポインターを返すルーチンは、参照カウントを1つ増やします。 ポインターを使用してドライバーが終了したら、 [**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出して参照カウントを1つ減らす必要があります。

次のルーチンはすべて、オブジェクトの参照カウントを1つ増やします。

[**ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)

[**IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)

[**Plxntb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)

[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiopenblock)

[**Obreferenceobject へ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)

[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)

[**ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)

上記のいずれかのルーチンに対して行われる各呼び出しは、対応する**ObDereferenceObject**への呼び出しと一致している必要があります。

ドライバーが既知のオブジェクトポインターの参照カウントを1つ増やすことができるように、 **Obreferenceobject**と**Obreferenceobjectbypointer**ルーチンが用意されています。 **Obreferenceobject**は単に参照カウントを増やします。 **Obreferenceobjectbypointer**は、参照カウントを増やす前にアクセスチェックを行います。

**Obreferenceobjectbyhandle**ルーチンは、オブジェクトハンドルを受け取り、基になるオブジェクトへのポインターを提供します。 参照カウントが1つ増えすぎます。

### <a name="temporary-and-permanent-objects"></a>一時オブジェクトとパーマネントオブジェクト

ほとんどのオブジェクトは*一時的*です。これらは、使用されている限り存在するので、オブジェクトマネージャーによって解放されます。 *永続的*なオブジェクトを作成できます。 オブジェクトが永続的な場合、オブジェクトマネージャー自体はオブジェクトへの参照を保持します。 そのため、参照カウントは0よりも大きくなり、オブジェクトは使用されなくなったときに解放されません。

一時オブジェクトには、そのハンドルカウントが0以外の場合にのみ、名前を使用してアクセスできます。 ハンドル数が0に減少すると、オブジェクトの名前がオブジェクトマネージャーの名前空間から削除されます。 そのようなオブジェクトは、参照カウントが0よりも大きい限り、ポインターによって引き続きアクセスできます。 パーマネントオブジェクトには、存在する限り名前でアクセスできます。

オブジェクトのオブジェクト[ **\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_object_attributes)構造に OBJ\_パーマネント属性を指定することにより、オブジェクトを作成時に永続的にすることができます。 詳細については、「 [**Initializeobjectattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)」を参照してください。

永続的なオブジェクトを一時的に作成するには、 [**Zwmake一時オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmaketemporaryobject)ルーチンを使用します。 このルーチンは、使用されなくなったオブジェクトを自動的に削除します。 (オブジェクトに開いているハンドルがない場合、オブジェクトの名前は、オブジェクトマネージャーの名前空間から直ちに削除されます。 オブジェクト自体は、参照カウントがゼロになるまで残ります)。

 

 




