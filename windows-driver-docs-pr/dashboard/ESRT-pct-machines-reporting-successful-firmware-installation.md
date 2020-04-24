---
title: ESRT から正常にファームウェアがインストールされたことを報告しているマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、インストールの試行に対する成功の割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6a9e4b1c9fe858e37ab4559ba4090638010f61c0
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "74097526"
---
# <a name="percent-of-machines-reporting-successful-firmware-installation-from-esrt"></a>ESRT から正常にファームウェアがインストールされたことを報告しているマシンの割合

## <a name="description"></a>説明

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、インストールの試行に対する成功の割合に集計したものです。
次のイベントが発生した場合、正常なインストールであると定義されます。

1. UEFI で始まるデバイス インスタンスのファームウェアが drvinst 経由でインストールされている
2. マシンの再起動とファームウェアが適用されている
3. ブート時に UEFI.sys によって、インストールが成功したことが報告されます。


マシンが一時的なエラー (UEFI.SYS からの一時的なエラーは以下の一覧に示します) を報告している場合、それは母集団に含まれません

|エラー コード|値|
|----|----|
|3221225659| STATUS_NOT_SUPPORTED|
|3221226195| STATUS_POWER_STATE_INVALID|
|3221226206| STATUS_INSUFFICIENT_POWER|
|3221225506| STATUS_ACCESS_DENIED|
|3221225473| STATUS_UNSUCCESSFUL|
|3221225517| STATUS_NOT_COMMITTED|
|3221225560| STATUS_UNKNOWN_REVISION|
|3221225626| STATUS_INSUFFICIENT_RESOURCES|
|3221226194| STATUS_PNP_REBOOT_REQUIRED|
|3221225659| STATUS_NOT_SUPPORTED|
|3221226195| STATUS_POWER_STATE_INVALID|
|3221226206| STATUS_INSUFFICIENT_POWER|
|3221225862| STATUS_DEVICE_PROTOCOL_ERROR|
|3221226681| STATUS_UNSATISFIED_DEPENDENCIES|
|3221226029| STATUS_RETRY|

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|200|
|**合格基準**|95% 以上|
|**測定 ID**|20116729|

## <a name="calculation"></a>計算

成功したマシンの数 / ファームウェア デバイスを試行したマシンのうち、一時的な状態のマシンを除外したマシンの数

