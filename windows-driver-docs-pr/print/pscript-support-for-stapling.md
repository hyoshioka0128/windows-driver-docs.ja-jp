---
title: Pscript のホチキス止めサポート
description: Pscript のホチキス止めサポート
ms.assetid: 75fc11e1-5cd9-4e95-b062-989fe493fdb5
keywords:
- ミニドライバー WDK Pscript、ホチキス止め
- ホチキス止めの WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69b6de9fd7c58fd6e8a94b1eea42017fc783c626
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359018"
---
# <a name="pscript-support-for-stapling"></a>Pscript のホチキス止めサポート





Microsoft Pscript ドライバーは、ホチキス止め機能で、次の標準をサポートしている*PPD*ファイル。

-   \*StapleLocation

-   \*StapleOrientation

-   \*StapleWhen

-   \*StapleX

-   \*StapleY

これらの標準機能をホチキス止めについての詳細については、次を参照してください。 *PostScript プリンター説明ファイル形式の仕様*、バージョン 4.3、1996 年 2 月 9 です。 (このリソースできない場合がありますのいくつかの言語および国。)

デバイスがホチキス止めをサポートしているかどうかを確認するのには、Pscript ドライバーは、次のロジックを使用します。

1.  上記に示した標準の機能をホチキス止めが定義されていない PPD ファイルで、ホチキス止めはサポートされません。

2.  場合\*StapleOrientation は PPD ファイルで定義されている唯一のホチキス止め機能し、ホチキス止めがサポートされています。

3.  上記に示した標準のホチキス止め機能の 1 つ以上の場合 (以外の\*StapleOrientation) PPD で定義されたファイルと、インストール可能な機能の現在の構成によって制限が定義されている機能のいずれかの場合は、ホチキス止めサポートされていません。 DuplexerUnit インストール可能な機能の NotInstalled オプションに制約を配置する場合など、 \*StapleLocation、および DuplexerUnit のプリンターの現在の構成は NotInstalled、し、ホチキス止めがサポートされていません。

 

 




