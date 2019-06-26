---
title: C28126
description: IRP requestormode で]-> [警告 C28126、AccessMode パラメーター ObReferenceObject * がある必要があります。
ms.assetid: be8f909e-2d4a-4e22-b457-81a048d90df8
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28126
ms.openlocfilehash: 5e6de5f744051096a9fe99cde7a9e870c03cbd64
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364141"
---
# <a name="c28126"></a>C28126


C28126 を警告します。ObReferenceObject への AccessMode パラメーター\* IRP にする必要があります&gt;requestormode で

呼び出しで[ **ObReferenceObjectByHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)または[ **ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)、ドライバーを渡す**UserMode**または**kernelmode である**の*AccessMode*パラメーターを使用する代わりに**Irp -&gt;requestormode で**します。

ドライバーを使用する必要があります**Irp -&gt;requestormode で**を指定するのではなく**UserMode**または**kernelmode である**します。 これにより、カーネル モードのハンドルを安全に提供するカーネル モードの IRP の送信者ができます。

この警告はドライバー スタックの最上位レベルのドライバーの対象としています。 無視するか、その他のすべてのドライバーには、この警告を抑制します。

ドライバー スタックの最上位レベルのドライバーを使用する必要があります**Irp -&gt;requestormode で**を指定するのではなく**UserMode**または**kernelmode である**します。 これにより、カーネル モードのハンドルを安全に提供するカーネル モードの IRP の送信者ができます。 スタックの他のすべてのドライバーを指定する必要があります**kernelmode である**、アクセス チェックをスキップして、リーフ責任へのアクセスを最上位レベルのドライバーを確認します。

 

 





