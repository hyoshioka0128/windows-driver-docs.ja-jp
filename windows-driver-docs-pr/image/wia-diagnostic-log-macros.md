---
title: WIA 診断ログのマクロ
description: WIA 診断ログのマクロ
ms.assetid: 8b544045-e9d7-422b-825c-f1a5531e0e11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a47699622edd7b2cb5116fc338796a8189efd641
ms.sourcegitcommit: 67aadd2adef4c338b703464c377ae8c910f1f5f9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2019
ms.locfileid: "67622669"
---
# <a name="wia-diagnostic-log-macros"></a>WIA 診断ログのマクロ

> [!NOTE]
> WIA エラーは、最新の Windows オペレーティング システムで処理を参照してください。 [WIA ドライバー エラー回復](wia-driver-error-recovery-for-windows-vista.md)します。

診断ログのマクロには、ログ トレース、エラー、警告メッセージをミニドライバーが有効にする、 *Wiaservc.log*診断のログ ファイル。

| マクロ | 説明 |
| --- | --- |
|[WIAS_LERROR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lerror) | エラーの種類のログ ステートメントを Wiaservc.log 診断ログ ファイルに書き込みます。 |
| [WIAS_LHRESULT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lhresult) | HRESULT 値を文字列に変換し、Wiaservc.log 診断ログ ファイルに文字列を書き込みます。 |
| [WIAS_LTRACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_ltrace) | トレースの種類のログ ステートメントを Wiaservc.log 診断ログ ファイルに書き込みます。 |
| [WIAS_LWARNING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lwarning) | Wiaservc.log 診断ログ ファイルに警告の種類のログ ステートメントを書き込みます。 |
| [WIAS_ERROR](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_error) | エラーの種類のログ ステートメントを Wiatrace.log 診断ログ ファイルに書き込みます。 |
| [WIAS_TRACE](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_trace) | トレースの種類のログ ステートメントを Wiatrace.log 診断ログ ファイルに書き込みます。 |
