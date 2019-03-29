---
title: UMDF での一般 I/O ターゲットに関する情報の取得
description: UMDF での一般 I/O ターゲットに関する情報の取得
ms.assetid: 306a7f46-423a-4647-846d-76f917ca0f7c
keywords:
- 一般的な I/O に関する WDK UMDF、情報をターゲットします。
- 状態情報の WDK I/O ターゲット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd1432c0b732ff18af2a950f8bea2af0da8f7625
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572382"
---
# <a name="obtaining-information-about-a-general-io-target-in-umdf"></a>UMDF での一般 I/O ターゲットに関する情報の取得


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ドライバーは、I/O ターゲットに関する情報を取得するには、I/O のターゲット オブジェクトを定義する次のメソッドを呼び出すことができます。

<a href="" id="iwdfiotarget--gettargetfile"></a>[**IWDFIoTarget::GetTargetFile**](https://msdn.microsoft.com/library/windows/hardware/ff559243)  
I/O のターゲットに関連付けられている framework ファイル オブジェクトを返します。

<a href="" id="iwdfiotargetstatemanagement--getstate"></a>[**IWDFIoTargetStateManagement::GetState**](https://msdn.microsoft.com/library/windows/hardware/ff559202)  
状態のローカル I/O ターゲットの情報を返します。

<a href="" id="iwdfremotetarget--getstate"></a>[**IWDFRemoteTarget::GetState**](https://msdn.microsoft.com/library/windows/hardware/ff560265)  
状態の I/O ターゲットをリモートの情報を返します。

 

 





