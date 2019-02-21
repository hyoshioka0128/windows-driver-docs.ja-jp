---
title: デバイス セットアップ クラスに対するレジストリ キーを開く
description: デバイス セットアップ クラスに対するレジストリ キーを開く
ms.assetid: B747EB2B-892C-4465-98E0-245FF7BC1E70
keywords:
- レジストリ WDK デバイスのインストール、デバイス セットアップ クラスに対するレジストリ キーを開く
- デバイス セットアップ クラス WDK デバイスのインストール、レジストリ キーを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4ff3cb7321ee1a0a15f164e8d47f9fa1ce3cb88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556735"
---
# <a name="opening-registry-keys-for-a-device-setup-class"></a>デバイス セットアップ クラスに対するレジストリ キーを開く


デバイス セットアップ クラスのレジストリ キーに直接アクセスできません。 レジストリ キーと同様にこれらのキーの名前と場所は、Windows の異なるバージョン間変更可能性があります。

安全のレジストリ キーを開くには、[デバイス セットアップ クラス](device-setup-classes.md)、次のいずれかを使用して、 [SetupAPI](setupapi.md)関数。

-   [**SetupDiOpenClassRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552065)
-   [**SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)で、*フラグ*パラメーター DIOCR_INSTALLER に設定

 

 





