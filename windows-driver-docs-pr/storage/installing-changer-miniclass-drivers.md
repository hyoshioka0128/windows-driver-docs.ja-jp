---
title: チェンジャー ミニクラス ドライバーのインストール
description: チェンジャー ミニクラス ドライバーのインストール
ms.assetid: 923e1128-bacc-450b-b250-bc666951965d
keywords:
- チェンジャー ドライバー WDK ストレージ、miniclass ドライバー
- 記憶域チェンジャー ドライバー WDK、miniclass ドライバー
- miniclass ドライバー WDK チェンジャー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c95b2babd755e01bbe7d51bbd38d894b803669d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362280"
---
# <a name="installing-changer-miniclass-drivers"></a>チェンジャー ミニクラス ドライバーのインストール


## <span id="ddk_installing_changer_miniclass_drivers_kg"></span><span id="DDK_INSTALLING_CHANGER_MINICLASS_DRIVERS_KG"></span>


このセクションでは、インストールについては、Windows 2000 以降のオペレーティング システムでチェンジャー miniclass ドライバーに固有では。

独自のコント ローラー ミニドライバーを提供しているベンダー ミニドライバーを行う必要がありますで MediumChanger セットアップ クラスのメンバー、 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)ドライバーの INF ファイル。 次に、例を示します。

```cpp
[version]
Signature="$WINDOWS NT$"
Class=MediumChanger
ClassGuid={CE5939AE-EBDE-11d0-B181-0000F8753EC4}
```

チェンジャー miniclass ドライバーのインストールに関連付けられているその他の特別な要件はありません。

インストールの詳細については、Windows Driver Kit (WDK) で含まれているメディア チェンジャー サンプルに付属している INF ファイルを参照してください。

Windows 2000 以降のオペレーティング システムでデバイスのインストールの詳細については、次を参照してください。[デバイス インストールの概要](https://msdn.microsoft.com/library/windows/hardware/ff549455)します。

 

 




