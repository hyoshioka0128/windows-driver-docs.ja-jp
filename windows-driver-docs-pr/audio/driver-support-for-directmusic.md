---
title: DirectMusic のドライバー サポート
description: DirectMusic のドライバー サポート
ms.assetid: 48f6245e-0911-46b6-9cf9-ea4db8875021
keywords:
- DirectMusic WDK オーディオ
- オーディオ ドライバー WDK、DirectMusic
- シンセサイザー WDK オーディオ
- wave オーディオの WDK をシンクします。
- WDM オーディオ ドライバー WDK、DirectMusic
- Dmu WDK オーディオ
- シンセサイザー シンク WDK オーディオ
- シンク WDK オーディオをレンダリングします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75c3a4b60205a85ca4432980cede12c02c874ca8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333741"
---
# <a name="driver-support-for-directmusic"></a>DirectMusic のドライバー サポート


## <span id="driver_support_for_directmusic"></span><span id="DRIVER_SUPPORT_FOR_DIRECTMUSIC"></span>


このドキュメントは、設計のガイド Microsoft DirectMusic シンセサイザー (シンセサイザー) 用のドライバーを実装して、wave シンクします。

-   シンセサイザー、MIDI メッセージのタイムスタンプ付きのストリームの入力し、出力のアナログ オーディオ信号または定期的にサンプリングされた wave デジタル オーディオ ストリームをデバイスです。

-   Wave シンクは、シンセサイザーから wave オーディオ サンプルを取得し、ターゲット オーディオ デバイスにそれらをフィードするストリーミング wave デバイスです。

ユーザー モードでは、ソフトウェアのシンセサイザーと wave シンクを実装できます。 カーネル モードでは、同じ機能を提供するソフトウェアまたはハードウェアのコンポーネントを実装できます。 シンセサイザーと wave シンク間のリレーションシップの詳細については、次を参照してください。[シンセサイザーと Wave シンク](synthesizers-and-wave-sinks.md)します。 DirectMusic API については、Microsoft Windows SDK のドキュメントを参照してください。

この設計のガイドには、次のセクションが含まれています。

[DirectMusic DDI の概要](directmusic-ddi-overview.md)

[ユーザー モードでカスタムの表示](custom-rendering-in-user-mode.md)

[カーネル モードのハードウェア アクセラレータ DDI](kernel-mode-hardware-acceleration-ddi.md)

 

 




