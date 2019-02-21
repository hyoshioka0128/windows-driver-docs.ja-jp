---
title: ファイルから証明書のインポート
description: ファイルから証明書のインポート
ms.assetid: 17596119-6b31-4a69-b83c-cec1dfd55572
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c565d3e753cc44abdc7af9879411a89295007aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556580"
---
# <a name="importing-certificates-from-a-file"></a>ファイルから証明書のインポート


記憶域証明書の管理の強化されたツールを使用して、ファイルから証明書をインポートすることができます。 ファイルは Distinguished Encoding Rules (DER) のバイナリ形式でエンコードされた X.509 証明書を含める必要があります。

このファイルを作成するには、次の方法のいずれかを使用します。

-   IEEE 1667 準拠 USB ストレージ デバイスから拡張記憶域証明書管理ツールでは、証明書をエクスポートできます。 ツールでは、ツールが実行されたときに指定されているファイルに証明書を保存します。

    詳細についてを参照してください、 [ **/Export スイッチ**](-export-switch.md)の記憶域証明書の管理の強化されたツールです。

-   使用して証明書を作成することができます、 [ **MakeCert** ](makecert.md)ユーティリティと、ファイルに保存します。

-   DER バイナリ形式でエンコードされた X.509 証明書を生成できる任意のアプリケーションを使用して、証明書を作成できます。 証明書は、ファイルに保存されます。

IEEE 1667 準拠 USB 記憶装置に、ファイルから証明書をインポートする方法の詳細については、次を参照してください、 **-ファイル**のパラメーター、 [ **/add** ](enhstor-add-switch.md)と[。**置換/** ](-replace-switch.md)拡張記憶域証明書管理ツールのスイッチ。

 

 





