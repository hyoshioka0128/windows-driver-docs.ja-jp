---
title: PoolMon
description: PoolMon
ms.assetid: 3cda6297-0e6f-48d5-b9d9-670ccf102c86
keywords:
- PoolMon WDK
- プールモニター WDK
- プールタグ WDK PoolMon
- メモリプールモニタ WDK
- ドライバーテスト WDK、PoolMon
- ドライバーのテスト WDK、PoolMon
- 割り当てプールタグ WDK PoolMon
- メモリ割り当ての WDK PoolMon
- メモリ割り当てデータの表示
- メモリ WDK PoolMon
- ターミナルサービスセッション WDK PoolMon
- タグファイル WDK PoolMon
- 統計 WDK PoolMon
- ステータス情報 WDK PoolMon
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea468b00148cccd81e57c392fbc4faa8d47fb92a
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769526"
---
# <a name="poolmon"></a>PoolMon


## <span id="ddk_poolmon_tools"></span><span id="DDK_POOLMON_TOOLS"></span>


PoolMon (poolmon)、メモリプールモニターには、オペレーティングシステムによって収集されたデータがシステムページングおよび非ページカーネルプールからのメモリ割り当て、およびターミナルサービスセッションに使用されるメモリプールと共に表示されます。 データはプール割り当てタグによってグループ化されます。

ドライバーの開発者やテスト担当者は、多くの場合、PoolMon を使用して、新しいドライバーを作成するときにメモリリークを検出したり、ドライバーコードを変更したり、ドライバーをストレスしたりします。 また、テストの各ステージで PoolMon を使用して、ドライバーの割り当てと解放操作のパターンを確認したり、特定の時点でドライバーが使用しているプールメモリの量を表示したりすることもできます。

このドキュメントで説明されている PoolMon のバージョンは \\ 、 \\ [Windows DRIVER Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)の Tools Other サブディレクトリに含まれています。

このトピックには次が含まれます。

[PoolMon の概要](poolmon-overview.md)

[PoolMon の要件](poolmon-requirements.md)

[PoolMon のコマンド](poolmon-commands.md)

[PoolMon の表示](poolmon-display.md)

[PoolMon の例](poolmon-examples.md)

Microsoft Windows XP およびそれ以前のシステムで PoolMon を使用するには、*プールのタグ付け*を有効にする必要があります。 Windows Server 2003 以降のバージョンの Windows では、プールのタグ付けは完全に有効になっています。 詳細については、「 [PoolMon の要件](poolmon-requirements.md)」の「プールタグ付けの要件」を参照してください。

PoolMon では、各プールタグを割り当てる Windows コンポーネントと一般的に使用されるドライバーの名前を表示できます。 この機能では、PoolMon および Windows パッケージ用デバッグツールと共にインストールされたファイルである pooltag .txt のデータを使用します。

 





