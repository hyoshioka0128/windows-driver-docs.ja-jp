---
title: ユーザーモード ドライバー フレームワークのデバッグ
description: ユーザーモード ドライバー フレームワークのデバッグ
ms.assetid: f59a420e-57d3-4ae0-84e3-58ec6e088b63
keywords:
- ユーザーモードドライバーフレームワークのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d92b09fc191ae298af3af6282ab6cd62b4e772e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533823"
---
# <a name="user-mode-driver-framework-debugging"></a>ユーザーモード ドライバー フレームワークのデバッグ

この種のデバッグセッションを開始する方法に関する情報など、ユーザーモードドライバーフレームワーク (UMDF) ドライバーをデバッグする方法の概要については、「 [Umdf ドライバーのデバッグを有効にする方法](https://docs.microsoft.com/windows-hardware/drivers/wdf/enabling-a-debugger)」を参照してください。

### <a name="umdf-debugging-extensions"></a>UMDF デバッグ拡張機能

ユーザーモードドライバーフレームワーク (UMDF) デバッグ拡張機能は、拡張モジュール Wudfext dll に実装されています。 これらの拡張機能を使用して、UMDF を使用するドライバーをデバッグできます。

Wudfext dll の拡張コマンドの詳細については、「[ユーザーモードドライバーフレームワーク拡張 (Wudfext .dll)](user-mode-driver-framework-extensions--wudfext-dll-.md)」を参照してください。

一部の拡張機能には、必要な Windows バージョンまたは UMDF バージョンに関する追加の制限があります。これらの制限については、個々の参照ページで説明されています。

**注**  新しい KMDF ドライバーか UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。 ドライバー名が最大長を超えていると、ドライバーの読み込みに失敗します。

この拡張ライブラリを使用するには、ライブラリをデバッガーに読み込む必要があります。 デバッガーに拡張ライブラリを読み込む方法については、「[デバッガー拡張 dll の読み込み](loading-debugger-extension-dlls.md)」を参照してください。
