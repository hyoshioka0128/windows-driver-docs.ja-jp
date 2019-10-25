---
title: フレームワーク割り込みオブジェクト
description: フレームワーク割り込みオブジェクト
ms.assetid: FA2B8C11-69D2-4A9E-8F57-C7295DA4EE44
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b40691410ab820dc7df17235a40068c9540c251f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843167"
---
# <a name="framework-interrupt-object"></a>フレームワーク割り込みオブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークの interrupt オブジェクトは、 [**Iwdfinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfinterrupt)インターフェイスによってドライバーに公開されます。 これは、ハードウェアの割り込みを表します。 Interrupt オブジェクトは、 [UMDF デバイスオブジェクト](framework-device-object.md)の子です。 ドライバーは、 [**IWDFDevice3:: createinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)メソッドを呼び出して、interrupt オブジェクトを作成できます。

ドライバーが割り込みを作成するとき、インターフェイスに関連するイベントが発生したときに、そのドライバーに通知するためにフレームワークが呼び出すコールバック関数のインターフェイスを提供できます。 詳細については、「 [UMDF Interrupt Object イベントコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/)」を参照してください。

割り込みオブジェクトの詳細については、「[割り込みの処理](handling-interrupts.md)」を参照してください。

 

 





