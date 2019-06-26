---
title: 必須およびオプションのテープ ミニクラス ルーチン
description: 必須およびオプションのテープ ミニクラス ルーチン
ms.assetid: 7a641199-2607-4980-bd8b-ec3856b311ef
keywords:
- テープ ドライバー WDK 記憶域、省略可能なルーチン
- テープ記憶装置ドライバー WDK、省略可能なルーチン
- テープ ドライバー WDK のストレージが必要なルーチン
- 記憶域テープ ドライバー WDK、必要なルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfe0638dd765e3e892c51c620ecd7b6b8dffb2da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360196"
---
# <a name="required-and-optional-tape-miniclass-routines"></a>必須およびオプションのテープ ミニクラス ルーチン


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

テープ miniclass ルーチンの説明も参照してください。[テープ Miniclass ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 




