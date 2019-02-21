---
title: 必須および省略可能なテープ Miniclass ルーチン
description: 必須および省略可能なテープ Miniclass ルーチン
ms.assetid: 7a641199-2607-4980-bd8b-ec3856b311ef
keywords:
- テープ ドライバー WDK 記憶域、省略可能なルーチン
- テープ記憶装置ドライバー WDK、省略可能なルーチン
- テープ ドライバー WDK のストレージが必要なルーチン
- 記憶域テープ ドライバー WDK、必要なルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f50eae3803f9297bf157153ed563e3f1cbad0cf3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538334"
---
# <a name="required-and-optional-tape-miniclass-routines"></a>必須および省略可能なテープ Miniclass ルーチン


## <span id="ddk_required_and_optional_tape_miniclass_routines_kg"></span><span id="DDK_REQUIRED_AND_OPTIONAL_TAPE_MINICLASS_ROUTINES_KG"></span>


テープ miniclass ドライバーは、次のルーチンで必要があります。

-   **DriverEntry**ドライバー固有のエントリ ポイントとテープ クラス ドライバーが miniclass ドライバーを初期化するために使用する定数を提供します。

    テープ miniclass ドライバーの**DriverEntry**ルーチンは、テープを割り当てる\_INIT\_データ\_EX 構造体、構造で、ドライバー固有の定数とエントリ ポイントを設定し、 **TapeClassInitialize**テープ クラス ドライバー。

-   TapeMiniGetPosition TapeMiniGetMediaTypes などのデバイス制御要求のデバイスに固有の処理を実装するルーチン。

    テープのクラス ドライバーは、そのデバイス制御ディスパッチ ルーチンからこのようなルーチンを呼び出します。 詳細については、次を参照してください。[テープ デバイス制御要求の処理](processing-tape-device-control-requests.md)します。

テープの miniclass ドライバーには、次の省略可能なルーチンがあります。

-   TapeMiniExtensionInit では、省略可能な minitape 拡張機能を初期化します。

    参照してください[省略可能な拡張機能を使用したテープ Miniclass コンテキストを格納する](storing-tape-miniclass-context-in-optional-extensions.md)minitape 拡張に関する情報。

-   TapeMiniTapeError は、テープ クラス ドライバーのエラー処理を補完します。

    ほとんどのデバイスのテープのクラス ドライバーは、テープ miniclass ドライバーからの入力エラーが発生したときに適切な状態値を返すことができます。 一部のデバイスでは、ただし、テープ クラス ドライバーが必要です、適切な状態を返すため、テープ miniclass ドライバーからデバイスに固有の情報。 たとえば、DAT テープ ドライブの 4 mm miniclass ドライバー判別されること、特定の状況では、テープで\_状態\_バス\_リセットの状態はドライブにメディアなしのために実際にします。 4 mm DAT miniclass ドライバー TapeMiniTapeError ルーチンは、このような状況を識別し、テープに返される状態を変更\_エラー\_いいえ\_メディア。

テープ miniclass ドライバーの**DriverEntry**ルーチンは、オペレーティング システムによって自動的に読み込まれるために正確にその名前を使用する必要があります。 TapeMini*Xxx*ルーチン名前を指定できますようにドライバー開発者が、ルーチンのエントリ ポイントがテープに設定されている限り\_INIT\_データ\_EX 構造体。 Miniclass ドライバーが、TapeMini をプレフィックス デバッグに役立つ、*Xxx*一部のルーチンで文字自体を識別するために、ルーチンが何名の文字の残りの部分の反映を確認してください。

テープ miniclass ルーチンの説明も参照してください。[テープ Miniclass ドライバー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff567970)します。

 

 




