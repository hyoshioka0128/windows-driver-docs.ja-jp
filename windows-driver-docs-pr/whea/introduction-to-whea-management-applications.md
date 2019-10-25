---
title: WHEA 管理アプリケーションの概要
description: WHEA 管理アプリケーションの概要
ms.assetid: d0c487bd-dfa8-43f2-a494-0ed95d767bfb
keywords:
- 管理アプリケーション WDK WHEA、管理アプリケーションについて
- ユーザーモードアプリケーション WDK WHEA、管理アプリケーション
- WHEA WDK、管理アプリケーション
- Windows ハードウェアエラーアーキテクチャ WDK、管理アプリケーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83059d3bd9ef0b279fb85fb4d966c1f0f6926560
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843133"
---
# <a name="introduction-to-whea-management-applications"></a>WHEA 管理アプリケーションの概要


Windows ハードウェアエラーアーキテクチャ (WHEA) には、ユーザーモードアプリケーションが WHEA 管理操作を実行できるようにする Windows Management Instrumentation (WMI) インターフェイスが用意されています。 WHEA 管理インターフェイスは、次の WMI プロバイダークラスで構成されています。

<a href="" id="wheaerrorsourcemethods"></a>[WHEAErrorSourceMethods](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)  
このクラスは、システム内の[エラーソース](hardware-errors-and-error-sources.md)を管理するためのメソッドを実装します。

<a href="" id="wheaerrorinjectionmethods"></a>[WHEAErrorInjectionMethods](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)  
このクラスは、ハードウェアのエラーをハードウェアプラットフォームに挿入するためのメソッドを実装します。

ユーザーモードアプリケーションは、 **IWbemServices:: ExecMethod**メソッドを呼び出すことによって、これらのクラスのメソッドを間接的に呼び出します。 WMI プロバイダークラスのメソッドを呼び出す方法の詳細については、Microsoft Windows SDK のドキュメントの「[プロバイダーメソッドの呼び出し](https://go.microsoft.com/fwlink/p/?linkid=80945)」を参照してください。

WMI の詳細については、Windows SDK のドキュメントの「 [Windows Management Instrumentation](https://go.microsoft.com/fwlink/p/?linkid=80947) 」セクションを参照してください。

**  Windows** Server 2008、WINDOWS Vista SP1、およびそれ以降のバージョンの windows では、WHEA WMI プロバイダークラスがサポートされています。

 

 

 




