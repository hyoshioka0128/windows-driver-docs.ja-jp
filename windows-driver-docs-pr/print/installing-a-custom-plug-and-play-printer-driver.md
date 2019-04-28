---
title: カスタムのプラグ アンド プレイ プリンター ドライバーをインストールする
description: カスタムのプラグ アンド プレイ プリンター ドライバーをインストールする
ms.assetid: 0269afbe-c7d1-4227-ad77-b921852d6a0c
keywords:
- プリンター ドライバー WDK をカスタマイズするには、プラグ アンド プレイします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd3124b506928018a113461baae3bb1b197431bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362754"
---
# <a name="installing-a-custom-plug-and-play-printer-driver"></a>カスタムのプラグ アンド プレイ プリンター ドライバーをインストールする





Windows xp では、プラグ アンド プレイ マネージャーは、(最も低い優先順位に最上位から順に) この順序でドライバーを読み込みます。

1.  署名付きの IHV ドライバー

2.  「ボックス」ドライバー

3.  符号なしの IHV ドライバー

Windows 2000 では、ボックスで、符号付きの IHV ドライバーの間の違いはありません: ドライバーのいずれかの型が符号なしの IHV ドライバー方が優先的に読み込まれます。 ドライバーと「ボックス」ドライバーを置換する INF ファイルをインストールするためのアプリケーションの詳細については、次を参照してください。[デバイス インストール アプリケーションを記述して](https://msdn.microsoft.com/library/windows/hardware/ff554015)します。

Windows 2000 のインボックス ドライバーを置換するドライバーを開発している場合、以下のことを確認、*ハードウェア Id*で、 [ **INF モデル セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456) INF ファイルが含まれます、。適切なポートの列挙子。 Ntprint.inf の Windows 2000 バージョンには、モデルの INF セクションでは、エントリにはポートの列挙子が含まれます。 INF ファイルで同じエントリは、ポートの列挙子を省略、プラグ アンド プレイは皆さん方が優先的、インボックス Windows 2000 のドライバーを選択します。 場合、ドライバーは Windows XP のインボックス ドライバーにハードウェア ID で、ポートの列挙子を含める必要はありません。

IHV は、次の例のように、各モデルのモデルの INF セクション内の 2 行を提供することでクライアント側のインストールでユーザーの操作を求めるダイアログ ボックスを回避できます。

```cpp
; Models section

[OEM Company Name]
"XYZ PScript Printer" = OEMXYZ.PPD, LPTENUM\OEM_Company_NameXYZ_F84F, XYZ_PScript_Printer
"XYZ PScript Printer" = OEMXYZ.PPD, OEM_Company_NameXYZ_F84F, XYZ_PScript_Printer
.
.
.
```

この例では、2 つの行はほぼ同じで最初の行で、ハードウェア ID (LPTENUM) バスの列挙子を含めることのみが異なります。 行ごとに 2 番目と 3 番目のエントリの値は、ハードウェア ID および互換性 ID、それぞれします。 特定のバス (ここではパラレル ポート) 経由でインストールされているプリンター、最初の行で、ハードウェア ID には最適な候補は、ハードウェア ID の一致が生成されます。 その他の任意のバス経由でインストールされているプリンター、2 行目で、ハードウェア ID に一致するハードウェア ID も生成されます。

いずれの場合も、セットアップでは、応答を確認するダイアログ ボックスを表示しないようにドライバーをインストールするかどうかをユーザーからの応答は必要ありません。 ただしを一致するハードウェア ID の一致でない場合ではなく、*互換性 ID*一致、およびインストールが発生したクライアント側では、セットアップには、ユーザーの介入を要求するダイアログ ボックスが表示されます。

 

 




