---
title: ユーザー モード ドライバー フレームワークのデバッグ
description: ユーザー モード ドライバー フレームワークのデバッグ
ms.assetid: f59a420e-57d3-4ae0-84e3-58ec6e088b63
keywords:
- ユーザー モード ドライバー フレームワークのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6982feb6288937c5cf25dd7fbebab39603cf50b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559783"
---
# <a name="user-mode-driver-framework-debugging"></a>ユーザー モード ドライバー フレームワークのデバッグ


この種のデバッグ セッションを開始する方法に関する情報など、ユーザー モード ドライバー フレームワーク (UMDF) ドライバーをデバッグする方法の概要については、、 [UMDF ドライバーのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=153578)Windows Driver Kit (WDK) ドキュメントの「を参照してください。

### <a name="span-idumdfdebuggingextensionsspanspan-idumdfdebuggingextensionsspanumdf-debugging-extensions"></a><span id="umdf_debugging_extensions"></span><span id="UMDF_DEBUGGING_EXTENSIONS"></span>UMDF デバッグ拡張機能

ユーザー モード ドライバー フレームワーク (UMDF) デバッグ拡張機能は、拡張機能モジュール Wudfext.dll で実装されます。 これらの拡張機能を使用して、使用して、UMDF ドライバーをデバッグすることができます。

Wudfext.dll 内の拡張機能コマンドの詳細については、[ユーザー モード ドライバー フレームワークの拡張機能 (Wudfext.dll)](user-mode-driver-framework-extensions--wudfext-dll-.md)を参照してください。

一部の拡張機能が必要です。 UMDF バージョン、Windows バージョンで追加の制限があります。これらの制限は、個々 のリファレンス ページに記載されています。

**注**  新しい KMDF または UMDF ドライバーを作成するときに、32 文字のあるドライバー名を選択する必要がありますまたはそれ以下。 この長さの制限は、wdfglobals.h で定義されています。 ドライバー名は、最大長を超えている場合、ドライバーは読み込みに失敗します。

 

この拡張機能ライブラリを使用するには、デバッガーに、ライブラリを読み込む必要があります。 デバッガーに拡張機能ライブラリを読み込む方法については、[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)を参照してください。

 

 





