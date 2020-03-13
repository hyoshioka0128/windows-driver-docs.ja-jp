---
title: ドライバー インストール プロセスが正常に完了したマシンの割合
description: この測定値は、ドライバーが正常にインストールされたマシンの割合として、30 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3f2f1868566b73cf4d65204bf302f58979d9f69d
ms.sourcegitcommit: 387de60712790691970924e059b0564325e211bc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2020
ms.locfileid: "79083126"
---
# <a name="percent-of-machines-where-the-driver-install-process-completes-successfully"></a>ドライバー インストール プロセスが正常に完了したマシンの割合

## <a name="description"></a>説明

ドライバーが正しくインストールされなかった場合、対象のコンポーネントの機能が失われ、ユーザーがコンポーネントの機能にアクセスできなくなる可能性があります。 機能を回復するには、ユーザーが問題のトラブルシューティングを行う必要があります。 PnP エラー コードの一覧については、「[デバイス マネージャーの問題コード](https://docs.microsoft.com/windows-hardware/drivers/install/device-manager-error-messages)」および [Windows サポート](https://support.microsoft.com/help/310123/error-codes-in-device-manager-in-windows)のページを参照してください。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|展開|
|**期間**|30 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|100 台のマシン|
|**合格基準**|ドライバーが正常にインストールされたマシンが 95% 以上|
|**測定 ID**|10042840|

## <a name="calculation"></a>計算

1. この測定値は、**ドライバーが正常にインストールされたマシンの割合**として、30 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*成功したインストールの数 = PnP イベントが成功したマシンの台数*"
3. "*総インストール数 = ドライバー インストール プロセスを開始したマシンの台数*"

### <a name="final-calculation"></a>最終的な計算

"*PnP 成功率 = 成功したインストールの数 / 総インストール数*"
