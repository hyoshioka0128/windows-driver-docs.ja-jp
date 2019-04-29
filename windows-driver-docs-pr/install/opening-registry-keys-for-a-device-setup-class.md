---
title: デバイス セットアップ クラス用のレジストリ キーを開く
description: デバイス セットアップ クラス用のレジストリ キーを開く
ms.assetid: B747EB2B-892C-4465-98E0-245FF7BC1E70
keywords:
- レジストリ WDK デバイスのインストール、デバイス セットアップ クラスに対するレジストリ キーを開く
- デバイス セットアップ クラス WDK デバイスのインストール、レジストリ キーを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4ff3cb7321ee1a0a15f164e8d47f9fa1ce3cb88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330238"
---
# <a name="opening-registry-keys-for-a-device-setup-class"></a>デバイス セットアップ クラス用のレジストリ キーを開く


デバイス セットアップ クラスのレジストリ キーに直接アクセスできません。 レジストリ キーと同様にこれらのキーの名前と場所は、Windows の異なるバージョン間変更可能性があります。

安全のレジストリ キーを開くには、[デバイス セットアップ クラス](device-setup-classes.md)、次のいずれかを使用して、 [SetupAPI](setupapi.md)関数。

-   [**SetupDiOpenClassRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552065)
-   [**SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)で、*フラグ*パラメーター DIOCR_INSTALLER に設定

 

 





