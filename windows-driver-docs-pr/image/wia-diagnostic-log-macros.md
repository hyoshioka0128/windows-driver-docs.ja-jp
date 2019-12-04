---
title: WIA 診断ログのマクロ
description: WIA 診断ログのマクロ
ms.assetid: 8b544045-e9d7-422b-825c-f1a5531e0e11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82c1c8af3f3d7b4b3a14b30ab64a6f33de751bb8
ms.sourcegitcommit: 1585a52e762226b01c7369371727746487cc57bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74796644"
---
# <a name="wia-diagnostic-log-macros"></a>WIA 診断ログのマクロ

> [!NOTE]
> 最新の Windows オペレーティングシステムでの WIA エラー処理については、「 [Wia ドライバーエラー回復](wia-driver-error-recovery-for-windows-vista.md)」を参照してください。

診断ログマクロは、ミニドライバーがトレース、エラー、および警告メッセージを*Wiaservc*診断ログファイルに記録できるようにします。

| マクロ | 説明 |
| --- | --- |
|[WIAS_LERROR](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lerror) | 種類が ERROR の log ステートメントを Wiaservc 診断ログファイルに書き込みます。 |
| [WIAS_LHRESULT](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lhresult) | HRESULT 値を文字列に変換し、その文字列を Wiaservc 診断ログファイルに書き込みます。 |
| [WIAS_LTRACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_ltrace) | Wiaservc 診断ログファイルに TRACE 型の log ステートメントを書き込みます。 |
| [WIAS_LWARNING](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lwarning) | 種類が WARNING の log ステートメントを Wiaservc 診断ログファイルに書き込みます。 |
| [WIAS_ERROR](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_error) | 種類が ERROR の log ステートメントを Wiatrace ログファイルに書き込みます。 |
| [WIAS_TRACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_trace) | 種類が TRACE の log ステートメントを Wiatrace .log 診断ログファイルに書き込みます。 |
