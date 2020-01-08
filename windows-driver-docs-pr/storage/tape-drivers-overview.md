---
title: テープドライバーの概要
description: テープ ドライバー
ms.assetid: d6d8ac92-0713-401c-9551-fc8e08e903f4
keywords:
- テープドライバー WDK ストレージ
- 記憶域テープドライバー WDK
- ストレージドライバー WDK、テープドライバー
- テープドライバー WDK 記憶域、テープドライバーについて
- 記憶域テープドライバー WDK、テープドライバーについて
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: de07e2a92d9414754a338f173fd72baf96d70a05
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606554"
---
# <a name="introduction-to-tape-drivers"></a>テープドライバーの概要

NT ベースのオペレーティングシステムには、オペレーティングシステム固有およびデバイスに依存しないテープタスクを処理する汎用テープクラスドライバーが用意されています。 Tape クラスドライバーは、カーネルモードの DLL として提供されています。 新しいテープデバイスまたはテープデバイスのファミリをサポートするために、ドライバーライターは、システム提供のテープクラスドライバーに動的にリンクするデバイス固有の tape miniclass ドライバーを作成します。

Tape miniclass ドライバーが tape クラスドライバーのルーチンのみを呼び出す場合、miniclass ドライバーは、Win32 アプリケーションをサポートする Microsoft オペレーティングシステム間で移植でき、tape miniclass インターフェイスを使用するテープクラスドライバーを提供します。 Tape miniclass driver には、ヘッダーファイル*minitape*が含まれています。

Windows 2000 以降のオペレーティングシステムでビルドして実行するには、新しいエントリポイント*TapeMiniGetMediaTypes*を1つサポートするために、既存の tape miniclass ドライバーを変更する必要があります。 その他の変更は必要ありません。 システム提供のテープクラスドライバーは、システムによって提供される記憶域ポートドライバーと共に、テープ miniclass ドライバーの代わりに、プラグアンドプレイおよび電源管理要求を処理します。

このセクションでは、オペレーティングシステム固有のテープクラスドライバーによって提供されるサポートについて説明し、新しい tape miniclass ドライバーの作成に関するガイドラインを提供します。

- Tape クラスと tape Miniclass ドライバーのルーチンの詳細については、「 [Tape Class Driver ルーチン](tape-class-driver-routines.md)」および「 [Tape Miniclass driver ルーチン](tape-miniclass-driver-routines.md)」を参照してください。

- ストレージデバイスドライバーレイヤーの説明については、「[デバイス構成とレイヤードドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-configurations-and-layered-drivers) 」を参照してください。
