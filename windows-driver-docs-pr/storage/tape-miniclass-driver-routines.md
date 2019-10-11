---
title: Tape Miniclass Driver ルーチン
description: Tape Miniclass Driver ルーチン
ms.assetid: 7a641199-2607-4980-bd8b-ec3856b311ef
keywords:
- テープドライバー WDK storage、オプションのルーチン
- ストレージテープドライバー WDK、オプションのルーチン
- テープドライバー WDK storage、必須ルーチン
- ストレージテープドライバー WDK、必須ルーチン
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: fe4db0e49a5a171fcb42ca4a2453923068e240d5
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72256308"
---
# <a name="tape-miniclass-driver-routines"></a>Tape Miniclass Driver ルーチン

Tape miniclass ドライバーには、次のルーチンが必要です。

- [**Driverentry**](driverentry-of-tape-miniclass-driver.md)には、miniclass ドライバーを初期化するためにテープクラスドライバーが使用するドライバー固有のエントリポイントと定数が用意されています。

  Tape miniclass ドライバーの**Driverentry**ルーチンは、TAPE_INIT_DATA_EX 構造体を割り当て、その構造体にドライバー固有の定数とエントリポイントを設定し、tape クラスドライバーで**TapeClassInitialize**を呼び出します。

- TapeMiniGetPosition や TapeMiniGetMediaTypes などのデバイス制御要求に対してデバイス固有の処理を実装するルーチン。

  Tape クラスドライバーは、デバイス制御ディスパッチルーチンからこのようなルーチンを呼び出します。 詳細については、「[テープデバイス制御要求の処理](processing-tape-device-control-requests.md)」を参照してください。

Tape miniclass ドライバーには、次のオプションのルーチンを含めることができます。

- *TapeMiniExtensionInit*は、省略可能な minitape 拡張を初期化します。

  Minitape 拡張機能の詳細については、「 [Tape Miniclass Context をオプションの拡張機能に格納](storing-tape-miniclass-context-in-optional-extensions.md)する」を参照してください。

- *TapeMiniTapeError*は、テープクラスドライバーのエラー処理を補足します。

  ほとんどのデバイスでは、tape miniclass ドライバーからの入力なしでエラーが発生した場合に、テープクラスドライバーが適切な状態値を返すことができます。 ただし、一部のデバイスでは、テープクラスドライバーが適切な状態を返すために、tape miniclass ドライバーからのデバイス固有の情報を必要とします。 たとえば、4mm DAT テープドライブの miniclass ドライバーは、特定の状況では、TAPE_STATUS_BUS_RESET の状態が実際にドライブにメディアがないことが原因であると判断できます。 4mm DAT miniclass ドライバーの*TapeMiniTapeError*ルーチンは、このような状況を特定し、TAPE_ERROR_NO_MEDIA に返される状態を変更します。

Tape miniclass ドライバーの**Driverentry**ルーチンでは、オペレーティングシステムによって自動的に読み込まれるためには、その名前を正確に使用する必要があります。 *TapeMiniXxx*ルーチンは、ルーチンのエントリポイントが TAPE_INIT_DATA_EX 構造体で設定されている限り、ドライバーライターが選択した名前を付けることができます。 デバッグを支援するために、miniclass ドライバーは*TapeMiniXxx*ルーチンの前にいくつかの文字を付加して、それ自体を識別する必要があります。また、名前に含まれる残りの文字がルーチンの動作を反映していることを確認する必要があります。

Tape miniclass ドライバーが必要とするルーチン、構造体、定数は、 *minitape*で宣言されています。

テープクラスのルーチンの詳細については、「 [Tape Class Driver ルーチン](tape-class-driver-routines.md)」を参照してください。
