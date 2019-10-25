---
title: C28126
description: 警告 C28126 ObReferenceObject * への AccessMode パラメーターは、IRP-> Irp->requestormode である必要があります。
ms.assetid: be8f909e-2d4a-4e22-b457-81a048d90df8
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28126
ms.openlocfilehash: 904e604b9ba135027ceda031a1101b852e6920bc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839600"
---
# <a name="c28126"></a>C28126


警告 C28126: ObReferenceObject\* への AccessMode パラメーターは&gt;Irp->requestormode である必要があります

[**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)または[**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)への呼び出しでは、ドライバーは kernelmode で**irp->requestormode&gt;** を使用する代わりに、 *accessmode*パラメーターの**ためにモード**またはを渡しています。

このドライバーでは、**モード**または**kernelmode で**を指定するのではなく、 **Irp&gt;irp->requestormode**を使用する必要があります。 これにより、カーネルモードの IRP の送信者はカーネルモードハンドルを安全に渡すことができます。

この警告は、ドライバースタックの最上位のドライバーを対象としています。 他のすべてのドライバーについては、この警告を無視するか非表示にすることができます。

ドライバースタックの最上位レベルのドライバーでは、**モード**または**kernelmode で**を指定するのではなく、 **Irp&gt;irp->requestormode**を使用する必要があります。 これにより、カーネルモードの IRP の送信者はカーネルモードハンドルを安全に渡すことができます。 スタック内の他のすべてのドライバーは**kernelmode で**を指定する必要があります。これにより、アクセスチェックがスキップされ、トップレベルドライバーへのアクセスチェックの責任が残ります。

 

 





