---
title: 複数ヘッド ハードウェアのサポート
description: 複数ヘッド ハードウェアのサポート
ms.assetid: ea618586-3649-405c-b1fd-78a11f14c742
keywords:
- 複数ヘッド ハードウェア WDK DirectX 9.0
- ハードウェアの複数ヘッド WDK DirectX 9.0 をサポートします。
- 複数ヘッドのハードウェアに関する複数ヘッド ハードウェア WDK DirectX 9.0 では、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5df8008ccbb6c650498d92ef55e6fb54798a88b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330684"
---
# <a name="supporting-multiple-head-hardware"></a>複数ヘッド ハードウェアのサポート


## <span id="ddk_supporting_multiple_head_hardware_gg"></span><span id="DDK_SUPPORTING_MULTIPLE_HEAD_HARDWARE_GG"></span>


DirectX 9.0 バージョンのドライバーでは、複数ヘッドのカードは、次の機能がある複数ヘッドのサポートを実装できます。

-   一般的なフレーム バッファーとすべてのアクセラレータは、カードのデバイス (ヘッド) を表示します。

-   アナログ コンバーター (DAC) およびモニターするデジタル独立の各ディスプレイ デバイス (head) を出力します。

-   使用可能なマルチ モニターのサポートのような異種ディスプレイ カード数よりもします。

-   1 つのヘッド コントロールまたは独立した操作。 1 台のデバイスは、アプリケーションに公開することができ、そのデバイスは、いくつかの全画面表示のスワップ チェーンを促進します。 その結果、すべてのリソースは、多くのヘッドで共有され、各ヘッドが正確に同じ機能です。 各ヘッドを独立した表示モードに設定することができます。アプリケーションを呼び出すことができますし、**存在**異なる時刻では、各ヘッド メソッド。 ヘッドの各スワップ チェーンは全画面表示である必要があります。 複数ヘッド モードに入ると、デバイス、全画面表示にする必要があります残ります。 ウィンドウ表示モードに切り替え (最小化の操作) を除く、デバイスの破棄が必要です。

DirectX 8.1 と以前のアプリケーションでは、DirectX 9.0 ドライバーする必要がありますも以前のメカニズムを使用ヘッド間のビデオ メモリを分割し、各ヘッドを完全に独立したアクセラレータとして扱うことに注意してください。 モードでは、アプリケーションが複数ヘッド DirectX 9.0 の機能をコード化された場合のみ、ドライバーは、これら複数ヘッドの新機能を使用します。 ドライバーに通知を 2 つの操作モードを切り替えるときにします。

次のセクションでは、ドライバーが複数ヘッドのハードウェアをサポートする方法について説明します。

[アダプター グループを識別して、機能を提供します。](identifying-adapter-group-and-providing-capabilities.md)

[ヘッドを作成します。](creating-heads.md)

[ハンドルの割り当ての例](example-of-handle-assignments.md)

[複数ヘッドのメモリを管理します。](managing-multiple-head-memory.md)

[レポートの複数ヘッド ビデオ メモリ](reporting-multiple-head-video-memory.md)

[複数のヘッドとプレゼンテーション](presentation-with-multiple-heads.md)

[複数ヘッドが複数のアダプターを使用します。](using-multiple-multiple-head-adapters.md)

 

 





