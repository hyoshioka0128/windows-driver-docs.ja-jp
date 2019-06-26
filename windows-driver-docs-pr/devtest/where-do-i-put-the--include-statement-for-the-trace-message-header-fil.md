---
title: どこに配置します
description: どこに配置します
ms.assetid: 5d8a2bb7-efe1-4cf2-9424-b63d4f17805e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23fb5488167183124b672d172ed54cfcf81e1161
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372684"
---
# <a name="where-do-i-put-the-include-statement-for-the-trace-message-header-file"></a>どこに配置、\#ステートメント トレース メッセージのヘッダー ファイルにはが含まれますか?


**\#含める**のステートメント、[トレース メッセージのヘッダー ファイル](trace-message-header-file.md)の定義後にソース ファイルに表示する必要があります、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロ WPP マクロ呼び出しの前。

プロジェクト全体のヘッダー ファイルを使用している場合は、配置、 **\#含める**ステートメントの後にトレース メッセージのヘッダー ファイル、 **\#含める**プロジェクト全体のヘッダーのステートメントファイルです。

 

 





