---
title: UMDF ドライバーが過度にメモリを消費する理由
description: Wudfext.dll を使用して、バージョン 1 の UMDF ドライバーが大量のメモリを消費する理由を判断する方法について説明します。
ms.assetid: 01316c4e-24e8-467c-af52-900b3fe042db
keywords:
- UMDF ドライバー WDK UMDF のシナリオをデバッグするには、過剰なメモリを消費します。
- UMDF デバッグ シナリオでは、WDK UMDF ドライバーが過剰なメモリを消費します。
- UMDF WDK、過剰なメモリを消費する UMDF ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b3bf4f5cf10096e5ab756084414a0e5c98eac80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578827"
---
# <a name="determining-why-a-umdf-driver-consumes-an-excessive-amount-of-memory"></a>UMDF ドライバーが大量にメモリを消費する理由の特定

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) バージョン 1 のドライバーと組み合わせて Wudfext.dll デバッガー拡張機能を使用して UMDF ドライバーが大量のメモリを消費する理由を判断する方法について説明します。

以降 UMDF バージョン 2 では、代わりに、Wdfkd.dll デバッガー拡張機能を使用する必要があります。 詳細については、[Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)](https://msdn.microsoft.com/library/windows/hardware/ff551876)を参照してください。

メモリ使用量を調査するには、次の手順を使用します。

1.  使用してオブジェクト ツリー内の未処理のオブジェクトを表示、 **! wudfext.wudfobject** UMDF デバッガー拡張機能。

    **! Wudfext.wudfobject**拡張機能は、その親と子のリレーションシップが含まれています、WDF のオブジェクトに関する情報を表示します。 ビットの 0 が設定した場合、*フラグ*パラメーターを 1 (0x01) **! wudfext.wudfobject**が渡されるオブジェクトをルートとするオブジェクト ツリーの再帰的なダンプを実行します。 完全なオブジェクトのツリーを表示するには、次のコマンドの例を使用します。

    **!wudfext.wudfobject &lt;IWDFDriver\*&gt; 1**

2.  予想より優れた物体を見るかどうかを決定します。

    ドライバーが最終的にこれらのオブジェクトをリークする可能性があります (WDF オブジェクトのリークについての詳細については、次を参照してください。 [Determining If ドライバー リークのフレームワーク オブジェクト](determining-if-a-driver-leaks-framework-objects.md))。

    これらのオブジェクトは、オブジェクト ツリー内にあり、、最終的に解放されるためです。 ただし、それらが累積されているが不必要にします。 これらのオブジェクトが必要です。

    -   親オブジェクトを修正します。
    -   明示的な削除を使用して、 [ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)メソッド。

 

 





