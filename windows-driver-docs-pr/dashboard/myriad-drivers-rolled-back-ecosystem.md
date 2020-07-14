---
title: インストール後 2 日以内にロールバックまたは再インストールされた多数のドライバー
description: この測定値は、インストール後 2 日以内にロールバックまたは再インストールされた無数の個別のマシンとして、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4e6c0cf929fcb8ced4e7bcbaef10c51df478dd3e
ms.sourcegitcommit: cb5f370b867ceab28b6b6c64a3586b0bb3831b3d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86035998"
---
# <a name="myriad-of-drivers-that-were-rolled-back-or-re-installed-within-2-days-of-installation-ecosystem"></a>インストール後 2 日以内にロールバックまたは再インストールされた無数のドライバー (エコシステム)

## <a name="description"></a>説明

この測定値は、ドライバーがインストールされてから 2 日以内にロールバックまたは代わりに別のドライバーがインストール (WU によって開始されない) されたどうかを追跡します。 このようなアクションは、ユーザーが別のドライバーを使用する必要があるほどドライバーに関する重大な問題がユーザーにあることを示します。

[インストール後 2 日以内にロールバックまたは再インストールされた多数のドライバー](https://docs.microsoft.com/windows-hardware/drivers/dashboard/myriad-drivers-rolled-back-standard)の測定値のエコシステムに対応するものです。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|マシン数|
|**最小母集団**|5,000 台のデバイス|
|**合格基準**|<= ドライバーをインストールした 10,000 デバイスあたり 10 件のロールバック|
|**測定 ID**|26124773|

## <a name="calculation"></a>計算

この測定値は、ドライバーのロールバック/このドライバーをインストールした 10,000 デバイスあたりの別のドライバーインストールの比率として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです

ロールバックまたは別のドライバーがインストールされたデバイスの合計 = ドライバーのインストールから 2 日以内にロールバックまたは別のドライバーがインストールされたデバイスの数

合計デバイス数 = ドライバーをインストールして 2 日間使用したデバイスの数

### <a name="final-calculation"></a>最終的な計算

ドライバーのロールバック/別のドライバーのインストールの比率 = ロールバックまたは別のドライバーをインストールしたデバイスの合計 * 10,000/合計デバイス数
