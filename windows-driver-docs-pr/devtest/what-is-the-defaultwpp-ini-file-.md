---
title: Defaultwpp.ini ファイルとは
description: Defaultwpp.ini ファイルとは
ms.assetid: 7e2673a3-5a01-498a-a2af-e5d8ff3e088b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9fdefbd78b6e6c5c4593cc0633b9168e8a0edef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573780"
---
# <a name="what-is-the-defaultwppini-file"></a>Defaultwpp.ini ファイルとは


Defaultwpp.ini ファイルは、ソフトウェア トレースをサポートするデータ型を定義する構成ファイルを示します。 Defaultwpp.ini ファイルは、箱にある\\wppconfig\\リビジョン 1 サブディレクトリの Windows Driver Kit (WDK)。

Defaultwpp.ini ファイルには、次の項目が含まれます。

-   UBYTE XINT64 などの算術データ型

-   SLONGPTR などのアーキテクチャに依存するデータ型

-   定義済みの COMPNAME (コンピューター名) などの定数--% です。FUNC! (関数名)、%、!レベル。 (プロバイダー レベル)--に含めること、[トレース メッセージのプレフィックス](trace-message-prefix.md)% トレースを編集して\_形式\_%path% 環境変数のプレフィックス

-   使用する形式の仕様の定数では、書式指定を使用して、トレース メッセージで使用されているように**printf**ステートメント。

-   IPADDR、HRESULT、GUID などのトレースでよく使用される型の特殊な種類。

-   日付、タイムスタンプなどの時間に関連する型、締め切りとデルタ。

-   B1 などの列挙型 (8 バイトのセット) と bool (Boolean)。

-   Irql、pnpmn、sysctrl などのカスタム型。

Defaultwpp.ini ファイルで、データ型を使用し、単純または複雑なデータ型を持つ独自のカスタム構成ファイルを作成できます。 詳細については、[カスタム データ型を定義する方法でしょうか。](how-do-you-define-custom-data-types-.md)と[定義の種類の複雑な構文とは何ですか?](what-is-the-syntax-of-the-complex-types-definition-.md)を参照してください。
