---
title: デバイス セットアップ クラス用のレジストリ キーを開く
description: デバイス セットアップ クラス用のレジストリ キーを開く
ms.assetid: B747EB2B-892C-4465-98E0-245FF7BC1E70
keywords:
- レジストリ WDK デバイスのインストール、デバイス セットアップ クラスに対するレジストリ キーを開く
- デバイス セットアップ クラス WDK デバイスのインストール、レジストリ キーを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d6e67a92cc35506af4868f7477f07a9fe0156dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366646"
---
# <a name="opening-registry-keys-for-a-device-setup-class"></a>デバイス セットアップ クラス用のレジストリ キーを開く


デバイス セットアップ クラスのレジストリ キーに直接アクセスできません。 レジストリ キーと同様にこれらのキーの名前と場所は、Windows の異なるバージョン間変更可能性があります。

安全のレジストリ キーを開くには、[デバイス セットアップ クラス](device-setup-classes.md)、次のいずれかを使用して、 [SetupAPI](setupapi.md)関数。

-   [**SetupDiOpenClassRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)
-   [**SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)で、*フラグ*パラメーター DIOCR_INSTALLER に設定

 

 





