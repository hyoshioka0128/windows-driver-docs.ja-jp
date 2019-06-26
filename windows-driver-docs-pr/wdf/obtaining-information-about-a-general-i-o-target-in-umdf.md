---
title: UMDF での一般 I/O ターゲットに関する情報の取得
description: UMDF での一般 I/O ターゲットに関する情報の取得
ms.assetid: 306a7f46-423a-4647-846d-76f917ca0f7c
keywords:
- 一般的な I/O に関する WDK UMDF、情報をターゲットします。
- 状態情報の WDK I/O ターゲット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5b28de8a49820c4fad51b2dfb29859d506ccb24
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375089"
---
# <a name="obtaining-information-about-a-general-io-target-in-umdf"></a>UMDF での一般 I/O ターゲットに関する情報の取得


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ドライバーは、I/O ターゲットに関する情報を取得するには、I/O のターゲット オブジェクトを定義する次のメソッドを呼び出すことができます。

<a href="" id="iwdfiotarget--gettargetfile"></a>[**IWDFIoTarget::GetTargetFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-gettargetfile)  
I/O のターゲットに関連付けられている framework ファイル オブジェクトを返します。

<a href="" id="iwdfiotargetstatemanagement--getstate"></a>[**IWDFIoTargetStateManagement::GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)  
状態のローカル I/O ターゲットの情報を返します。

<a href="" id="iwdfremotetarget--getstate"></a>[**IWDFRemoteTarget::GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-getstate)  
状態の I/O ターゲットをリモートの情報を返します。

 

 





