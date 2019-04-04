---
title: WHEA 管理アプリケーションの概要
description: WHEA 管理アプリケーションの概要
ms.assetid: d0c487bd-dfa8-43f2-a494-0ed95d767bfb
keywords:
- 管理アプリケーションの WDK WHEA では、管理アプリケーションについて
- ユーザー モード アプリケーション WDK WHEA、管理アプリケーション
- WHEA WDK、管理アプリケーション
- Windows ハードウェア エラー アーキテクチャ WDK、管理アプリケーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c36e0b701118b92d54d526575d9053f73263a600
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528823"
---
# <a name="introduction-to-whea-management-applications"></a>WHEA 管理アプリケーションの概要


Windows ハードウェア エラー アーキテクチャ (WHEA) は、WHEA 管理操作を実行するユーザー モード アプリケーションを使用する Windows Management Instrumentation (WMI) インターフェイスを提供します。 WHEA の管理インターフェイスは、次の WMI プロバイダー クラスで構成されます。

<a href="" id="wheaerrorsourcemethods"></a>[WHEAErrorSourceMethods](https://msdn.microsoft.com/library/windows/hardware/ff559521)  
このクラスを管理するためのメソッドを実装、[エラー ソース](hardware-errors-and-error-sources.md)システム。

<a href="" id="wheaerrorinjectionmethods"></a>[WHEAErrorInjectionMethods](https://msdn.microsoft.com/library/windows/hardware/ff559513)  
このクラスは、ハードウェア プラットフォームにハードウェア エラーを挿入するためのメソッドを実装します。

ユーザー モード アプリケーション メソッドを呼び出しましていないこれらのクラスで直接呼び出すことによって、 **iwbemservices::execmethod**メソッド。 WMI プロバイダー クラスでメソッドを呼び出す方法の詳細については、、[プロバイダーのメソッドを呼び出す](https://go.microsoft.com/fwlink/p/?linkid=80945)、Microsoft Windows SDK ドキュメントのトピックを参照してください。

WMI の詳細については、、 [Windows Management Instrumentation](https://go.microsoft.com/fwlink/p/?linkid=80947) Windows SDK ドキュメントの「を参照してください。

**注**  WHEA WMI プロバイダー クラスは、Windows Server 2008、Windows Vista SP1 と以降のバージョンの Windows でサポートされています。

 

 

 




