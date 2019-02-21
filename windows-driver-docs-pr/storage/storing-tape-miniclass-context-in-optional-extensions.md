---
title: 省略可能な拡張機能でテープ Miniclass コンテキストを格納します。
description: 省略可能な拡張機能でテープ Miniclass コンテキストを格納します。
ms.assetid: 9b259403-2fae-4708-8765-2d998a535620
keywords:
- テープ ドライバー WDK 記憶域、記憶域のコンテキスト
- テープ記憶装置ドライバー WDK、コンテキストのストレージ
- WDK の記憶域のコンテキスト
- コンテキストの格納域 WDK テープ
- ドライバー固有の minitape 拡張機能の WDK テープ
- コマンド固有のコマンド拡張機能の WDK テープ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9a3330ca4ee4770a4bb3bfbb47c45e103b9f217
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529030"
---
# <a name="storing-tape-miniclass-context-in-optional-extensions"></a>省略可能な拡張機能でテープ Miniclass コンテキストを格納します。


## <span id="ddk_storing_tape_miniclass_context_in_optional_extensions_kg"></span><span id="DDK_STORING_TAPE_MINICLASS_CONTEXT_IN_OPTIONAL_EXTENSIONS_KG"></span>


テープの miniclass ドライバーでは、2 つの省略可能な拡張機能にコンテキストを格納できます。

1.  ドライバー固有の minitape 拡張機能

    使用すると、この拡張機能は通常、デバイスの機能 (SCSI 問い合わせデータまたは同等) の情報を格納します。 複数のデバイスをサポートしているドライバーは、各デバイスについての詳細を格納できる繰り返し、デバイスのクエリではなく。

    Miniclass ドライバー minitape 拡張機能のサイズを指定します、 **MinitapeExtensionSize**テープのメンバー\_INIT\_データ\_EX 構造に渡す**TapeClassInitialize**からその**DriverEntry**ルーチン。 テープのクラス ドライバーは、miniclass ドライバーに代わって、要求されたストレージを割り当てます。 Miniclass ドライバーでは、TapeMiniExtensionInit ルーチンの省略可能な拡張機能を初期化します。 Minitape 拡張機能は、ドライバーがロードされるまで有効です。

2.  コマンド固有のコマンド拡張機能

    使用すると、この拡張機能は、1 つの要求を処理する 2 回以上呼び出さ可能性のあるテープ miniclass ルーチンへの呼び出しの間でのコマンド固有のコンテキストを格納します。 たとえば、テープ miniclass ドライバーの TapeMiniGetStatus ルーチンはテストの状態を格納可能性があります\_単位\_決定かどうか、テープ ドライブもクリーニングが必要なときに、コマンドの拡張機能のコマンドを準備します。

    Miniclass ドライバーでコマンド拡張機能のサイズを指定する、 **CommandExtensionSize**テープのメンバー\_INIT\_データ\_EX 構造に渡す**TapeClassInitialize**からその**DriverEntry**ルーチン。

    デバイス制御要求のデバイスに固有の機能を処理するすべてのテープ miniclass ルーチンは、呼び出されると、コマンド拡張機能へのポインターを与えられます。 テープ クラス ドライバーは、このような miniclass ルーチンを呼び出す前に、コマンド拡張機能のストレージを割り当てます。 Miniclass ルーチンが特定の要求を処理する最初の呼び出しで、コマンド拡張機能を初期化しますつまり、 *CallNumber*ルーチン パラメーターは 0 になります。 テープ miniclass ルーチンがいずれかのテープに戻るまでコマンド拡張機能の有効なまま\_状態\_成功またはエラー状態です。

 

 




