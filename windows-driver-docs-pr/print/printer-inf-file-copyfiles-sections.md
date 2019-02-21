---
title: プリンターの INF ファイル CopyFiles セクション
description: プリンターの INF ファイル CopyFiles セクション
ms.assetid: 92c96019-d2dd-4b2c-818a-80ae091ec662
keywords:
- WDK の INF ファイルの印刷、CopyFiles セクション
- セクションでは WDK プリンター
- CopyFiles ディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f87a84631d1553f9780dd6134cb4881febf8f8da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530613"
---
# <a name="printer-inf-file-copyfiles-sections"></a>プリンターの INF ファイル CopyFiles セクション





によって参照されるファイル リスト セクションがプリンター INF ファイルに含まれているとき、 [ **INF CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)、次の形式を使用して、ファイルの一覧内の各ファイルを指定する必要があります。

**\[**<em>ファイルのセクション一覧</em>**\]**
*変換先ファイル名\[、およびフラグ\]* 
 *変換先ファイル名\[、およびフラグ\]*
*変換先ファイル名\[、およびフラグ\]* .*変換先ファイル名*フィールドは必須ですが、および*フラグ*フィールドは省略可能です。 ファイル指定を省略可能な含めないで*ソース ファイル名*または*一時ファイル名*ファイルに対して定義されているフィールド リストのセクションでは、INF CopyFiles ディレクティブと共に使用します。 この制限は、Web ページから印刷ドライバーをインストールする必要があります。

 

 




