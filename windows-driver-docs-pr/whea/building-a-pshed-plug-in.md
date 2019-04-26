---
title: PSHED プラグインの構築
description: PSHED プラグインの構築
ms.assetid: 2d4dc052-af8b-4ee1-a8e7-4dbbb3817616
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9b63ef90318f0b2d69feb1ec0625b241dc56cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355032"
---
# <a name="building-a-pshed-plug-in"></a>PSHED プラグインの構築


プラグインの PSHED がカーネルとハードウェア アブストラクション レイヤー (HAL) にリンクするだけでなく、PSHED プラグインする必要がありますも明示的にリンクすることを除いて、他の Windows Driver Model (WDM) デバイス ドライバーなど、WDK を使用して構築された*Pshed.lib*.

**注**  以降 Windows 7 では、さまざまな Windows ハードウェア エラー アーキテクチャ (WHEA) データ型は、WDK の以前のバージョンから変更されています。 これらの変更の詳細については、次を参照してください。 [WHEA データ型の名前を変更](renamed-whea-data-types.md)します。 既存の PSHED Windows 7 または以降のバージョンの WDK でプラグインを構築する場合は、WHEA データ型の名前は、前者を引き続き使用できます。 これを行うには、次の情報を追加、*ソース*プラグインをビルドするために使用するファイル。 `C_DEFINES = $(C_DEFINES) /DWHEA_DOWNLEVEL_TYPE_NAMES`

 

 

 




