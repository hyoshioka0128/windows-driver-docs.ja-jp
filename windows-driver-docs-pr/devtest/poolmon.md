---
title: PoolMon
description: PoolMon
ms.assetid: 3cda6297-0e6f-48d5-b9d9-670ccf102c86
keywords:
- PoolMon WDK
- WDK のプール モニタ
- プール タグ WDK PoolMon
- WDK のメモリ プール モニタ
- ドライバー WDK、PoolMon のテスト
- ドライバー WDK、PoolMon のテスト
- 割り当てプール タグ WDK PoolMon
- メモリ割り当て WDK PoolMon
- メモリ割り当てデータを表示します。
- メモリ WDK PoolMon
- ターミナル サービス セッションの WDK PoolMon
- WDK PoolMon ファイルにタグ付け
- WDK PoolMon の統計情報
- WDK PoolMon のステータス情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36966ba65ca5d337e9af9808d990e8fb4ec93a39
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338709"
---
# <a name="poolmon"></a>PoolMon


## <span id="ddk_poolmon_tools"></span><span id="DDK_POOLMON_TOOLS"></span>


PoolMon (poolmon.exe)、メモリ プール モニタは、ページング システムからメモリの割り当てについて、オペレーティング システムで収集されるデータと非ページ カーネル プールの場合は、ターミナル サービス セッションに使用されるメモリ プールを表示します。 データは、プール割り当てタグでグループ化されます。

ドライバー開発者およびテスト担当者 PoolMon を使用して多くの場合、新しいドライバーを作成、ドライバーのコードを変更またはドライバーを強調したときのメモリ リークを検出する必要があります。 割り当ておよび解放操作は、ドライバーのパターンを表示して、ドライバーが特定の時点を使用してプール メモリの量を表示するは、テストの各ステージで PoolMon を使用することもできます。

このドキュメントで説明されている PoolMon のバージョンが記載されて、\\ツール\\の他のサブディレクトリ、 [Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=846744)します。

このトピックには次が含まれます。

[PoolMon の概要](poolmon-overview.md)

[PoolMon 要件](poolmon-requirements.md)

[PoolMon コマンド](poolmon-commands.md)

[PoolMon 表示](poolmon-display.md)

[PoolMon 例](poolmon-examples.md)

で Microsoft Windows XP およびそれ以前のシステムを PoolMon を使用する必要がありますを有効にした*プール タグ付け*します。 Windows Server 2003 および Windows の以降のバージョンでは、プールのタグ付けは完全に有効です。 詳細については、「プール タグ付け要件」を参照してください[PoolMon 要件](poolmon-requirements.md)します。

PoolMon は Windows コンポーネントの名前を表示することができ、通常各プール タグを割り当てることがドライバーを使用します。 この機能は、pooltag.txt、および Windows のツールをデバッグ パッケージ PoolMon と一緒にインストール ファイルからデータを使用します。 場合によっては、Microsoft は、このファイルを更新します。 更新プログラムを確認するには、 [Microsoft サポート](https://go.microsoft.com/fwlink/p/?linkid=8713)"pooltag.txt"を検索して web サイト。

 

 





