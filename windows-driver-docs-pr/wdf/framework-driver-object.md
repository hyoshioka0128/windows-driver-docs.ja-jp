---
title: Framework ドライバー オブジェクト
description: Framework ドライバー オブジェクト
ms.assetid: 6e9e568c-7e4f-48bd-b351-4be0e12cc15b
keywords:
- UMDF オブジェクト WDK、ドライバー オブジェクト
- framework オブジェクト WDK UMDF、ドライバー オブジェクト
- WDK UMDF ドライバーのオブジェクト
- IWDFDriver
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 263c5b5005fbc9d99c28ffca6b179306a60c35ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551295"
---
# <a name="framework-driver-object"></a>Framework ドライバー オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーによってフレームワーク ドライバー オブジェクトが公開されている、 [IWDFDriver](https://msdn.microsoft.com/library/windows/hardware/ff558893)インターフェイス。 ドライバーのホスト プロセスで読み込まれるドライバー イメージの framework 表現することをお勧めします。 フレームワークは、ドライバーのホスト プロセスに読み込まれた各ドライバーの新しいドライバー オブジェクトを作成します。 **IWDFDriver**インターフェイスは、ドライバーに渡される、 [ **IDriverEntry::OnInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff554900)メソッドで、ユーザー モード ドライバーのメイン エントリ ポイントです。

 

 





