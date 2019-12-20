---
title: UMDF での一般 I/O ターゲットに関する情報の取得
description: UMDF での一般 I/O ターゲットに関する情報の取得
ms.assetid: 306a7f46-423a-4647-846d-76f917ca0f7c
keywords:
- 一般的な i/o ターゲット WDK UMDF、情報
- ステータス情報 WDK i/o ターゲット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62398f46235f45c14acf3c1c4f720630a8a48307
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208915"
---
# <a name="obtaining-information-about-a-general-io-target-in-umdf"></a>UMDF での一般 I/O ターゲットに関する情報の取得


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

I/o ターゲットに関する情報を取得するために、UMDF ドライバーは、i/o ターゲットオブジェクトによって定義される次のメソッドを呼び出すことができます。

<a href="" id="iwdfiotarget--gettargetfile"></a>[**IWDFIoTarget:: GetTargetFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-gettargetfile)  
I/o ターゲットに関連付けられているフレームワークファイルオブジェクトを返します。

<a href="" id="iwdfiotargetstatemanagement--getstate"></a>[**IWDFIoTargetStateManagement:: GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)  
ローカル i/o ターゲットの状態情報を返します。

<a href="" id="iwdfremotetarget--getstate"></a>[**IWDFRemoteTarget:: GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-getstate)  
リモート i/o ターゲットの状態情報を返します。

 

 





