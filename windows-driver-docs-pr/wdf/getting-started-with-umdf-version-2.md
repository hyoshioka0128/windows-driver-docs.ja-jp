---
title: UMDF の概要
description: このセクションでは、ユーザーモードドライバーフレームワーク (UMDF) について説明し、UMDF バージョン1と2の違いについて詳しく説明します。
ms.assetid: 2C4DAFA4-783C-4739-8D27-A417AC63B447
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b35820930d33e64b54e75d699c98b4165a97002d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845271"
---
# <a name="getting-started-with-umdf"></a>UMDF の概要


このセクションでは、ユーザーモードドライバーフレームワーク (UMDF) について説明し、UMDF バージョン1と2の違いについて詳しく説明します。 また、UMDF に関する高レベルのアーキテクチャ情報も提供します。 このセクションでは、必要に応じて UMDF ドライバーが適切に選択されているかどうかを確認し、使用する UMDF バージョンを決定します。

Windows Driver Framework (WDF) には、ユーザーモードドライバーを作成するためのフレームワークである UMDF が含まれています。 カーネルモードドライバーフレームワーク (KMDF) と同様に、UMDF は WDM から抽象化レイヤーを提供し、プラグアンドプレイ (PnP) と電源管理機能の大部分を処理し、ドライバーが特定の機能やイベント処理をオプトインできるようにします。

Windows 8.1 には、バージョン1と2の2つの主要なバージョンがあります。 Umdf version 1.11 (1 ドット 11) は、最新バージョンの UMDF バージョン1です。これは、UMDF 2 が登場する前の最終バージョンです。 完全なバージョン情報とオペレーティングシステムの関連性を示す表については、「 [UMDF Version History](umdf-version-history.md)」を参照してください。

UMDF version 1 を使用してドライバーを記述するには、COM C++プログラミングモデルを使用してコードを記述する必要があります。 UMDF バージョン1は KMDF と同じ概念ドライバープログラミングモデルに基づいていますが、UMDF 1 は、さまざまなコンポーネント、デバイスドライバーインターフェイス (DDIs)、およびデータ構造を持つモデルを実装します。

これに対し、UMDF バージョン2以降では、KMDF ドライバーで使用可能なメソッドの多くを呼び出す、C プログラミング言語で UMDF ドライバーを記述できます。 UMDF version 2 と KMDF 間で共有されるすべてのインターフェイスには、同じ名前、パラメーター、および構造体の定義があります。 ドライバーが共有機能のみを使用する場合、または1つのフレームワークでのみサポートされている呼び出しに関する条件付きマクロを使用する場合は、UMDF または KMDF でコンパイルできる1つのドライバーを記述できます。 詳細については、「 [KMDF ドライバーから UMDF ドライバーを生成する方法](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)」を参照してください。

UMDF 2 と KMDF の間には重要な共通点がありますが、1つのフレームワークでしか使用できない機能も少ししかありません。 詳細については、「 [UMDF 2 の機能と KMDF の比較](comparing-umdf-2-0-functionality-to-kmdf.md)」を参照してください。 すべての UMDF 2 および KMDF コールバックとメソッドの一覧と、それらが適用されるフレームワークについては、「 [WDF のコールバックとメソッドの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)」を参照してください。 場合によっては、メソッドの構造体メンバーまたはパラメーターが1つのフレームワークにのみ適用されます。 ドキュメントでは、これらの違いについて、対応するリファレンスページで説明しています。

どちらか一方を選択する必要があります。UMDF バージョン1と2の両方からメソッドを呼び出す UMDF ドライバーを作成することはできません。

UMDF version 2 ドライバーは Windows 8.1 以降でのみ実行されます。 Windows 8.1 より前のオペレーティングシステムで実行される UMDF ドライバーを作成する必要がある場合は、UMDF 1.x ドライバーを記述する必要があります。 バージョン1.11 を使用して、Windows Vista 以降で実行されるドライバーを構築することができます。 バージョン1の詳細については、「 [UMDF 1.X 設計ガイド](user-mode-driver-framework-design-guide.md)」を参照してください。 このセクションでは、UMDF version 2 について説明します。



 

 
