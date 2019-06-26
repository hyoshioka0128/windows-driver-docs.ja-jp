---
title: プリンター INF ファイル CopyFiles セクション
description: プリンター INF ファイル CopyFiles セクション
ms.assetid: 92c96019-d2dd-4b2c-818a-80ae091ec662
keywords:
- WDK の INF ファイルの印刷、CopyFiles セクション
- セクションでは WDK プリンター
- CopyFiles ディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d97d30dedc040951457687ea49408cd22730ba94
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356057"
---
# <a name="printer-inf-file-copyfiles-sections"></a>プリンター INF ファイル CopyFiles セクション





によって参照されるファイル リスト セクションがプリンター INF ファイルに含まれているとき、 [ **INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)、次の形式を使用して、ファイルの一覧内の各ファイルを指定する必要があります。

**\[** <em>ファイルのセクション一覧</em> **\]** 
*変換先ファイル名\[、およびフラグ\]* 
 *変換先ファイル名\[、およびフラグ\]* 
*変換先ファイル名\[、およびフラグ\]* .*変換先ファイル名*フィールドは必須ですが、および*フラグ*フィールドは省略可能です。 ファイル指定を省略可能な含めないで*ソース ファイル名*または*一時ファイル名*ファイルに対して定義されているフィールド リストのセクションでは、INF CopyFiles ディレクティブと共に使用します。 この制限は、Web ページから印刷ドライバーをインストールする必要があります。

 

 




