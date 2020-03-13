---
title: ドライバーの更新プログラムがインストールされ、インストールから 2 日以内に PnP エラー コードが報告されたマシンの割合
description: この測定値は、ドライバーが正常にインストールされ、インストールから 2 日以内に PnP エラーが発生したマシンの割合として、30 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 416a0b8984055663d6fbedc8eb9b56b55ca482c5
ms.sourcegitcommit: 387de60712790691970924e059b0564325e211bc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2020
ms.locfileid: "79083137"
---
# <a name="percent-of-machines-that-installed-a-driver-update-and-reported-a-pnp-error-code-within-two-days-of-install"></a>ドライバーの更新プログラムがインストールされ、インストールから 2 日以内に PnP エラー コードが報告されたマシンの割合

## <a name="description"></a>説明

正常にインストールされても、インストール後にマシンで PnP エラーが発生して、ユーザー エクスペリエンスに悪影響を及ぼす可能性があります (デバイスが正常に機能しない、予期せず再起動するなど)。 PnP エラー コードの一覧については、「[デバイス マネージャーの問題コード](https://docs.microsoft.com/windows-hardware/drivers/install/device-manager-error-messages)」および [Windows サポート](https://support.microsoft.com/help/310123/error-codes-in-device-manager-in-windows)のページを参照してください。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|展開|
|**期間**|30 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|100 台のマシン|
|**合格基準**|インストール後に PnP エラーが発生したマシンが 5% 以下|
|**測定 ID**|10042784|

## <a name="calculation"></a>計算

1. この測定値は、**ドライバーが正常にインストールされ、インストールから 2 日以内に PnP エラーが発生したマシンの割合**として、30 日間のスライディング ウィンドウからのテレメトリを集計したものです

   a。 30日間のウィンドウ外におけるインストールに関連する PnP エラーはすべてカウントされません

2. "*インストール後の PnP エラーの数 = ドライバーのインストールから 2 日以内に PnP エラーが発生したマシンの台数*"
3. "*インストール後のエラーの総数 = ドライバーが正常にインストールされたマシンの総数*"

### <a name="final-calculation"></a>最終的な計算

"*インストール後の PnP エラー率 = インストール後の PnP エラーの数 / インストール後のエラーの総数*"
