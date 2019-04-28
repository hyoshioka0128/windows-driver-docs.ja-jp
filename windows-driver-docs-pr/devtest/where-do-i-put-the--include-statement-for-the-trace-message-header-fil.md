---
title: どこに配置します
description: どこに配置します
ms.assetid: 5d8a2bb7-efe1-4cf2-9424-b63d4f17805e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e99786e33559627d9e1e8d31096eb6e25792c22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379126"
---
# <a name="where-do-i-put-the-include-statement-for-the-trace-message-header-file"></a>どこに配置、\#ステートメント トレース メッセージのヘッダー ファイルにはが含まれますか?


**\#含める**のステートメント、[トレース メッセージのヘッダー ファイル](trace-message-header-file.md)の定義後にソース ファイルに表示する必要があります、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)マクロ WPP マクロ呼び出しの前。

プロジェクト全体のヘッダー ファイルを使用している場合は、配置、 **\#含める**ステートメントの後にトレース メッセージのヘッダー ファイル、 **\#含める**プロジェクト全体のヘッダーのステートメントファイルです。

 

 





