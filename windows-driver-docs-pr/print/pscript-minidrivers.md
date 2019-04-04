---
title: Pscript ミニドライバー
description: Pscript ミニドライバー
ms.assetid: b1108a6b-e0cc-413c-b3ea-53a1aa3156c0
keywords:
- PostScript プリンター ドライバー WDK の印刷、ミニドライバー
- Pscript WDK の印刷、ミニドライバー
- ミニドライバー WDK Pscript
- ミニドライバー WDK Pscript、Pscript ミニドライバーについて
- WDK の PPD ファイルを印刷します。
- .ppd ファイル
- NTF ファイル
- .ntf ファイル
- WDK の東アジア言語フォントを印刷します。
- WDK のアジア言語フォントを印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcac1bd853231bcb038c174216d8d6e87f08908c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578058"
---
# <a name="pscript-minidrivers"></a>Pscript ミニドライバー





Pscript ミニドライバーは、.ppd ファイルと .ntf ファイルから作成されます。

### <a href="" id="ddk-ppd-files-gg"></a>PPD ファイル

PostScript プリンターの説明テキスト ベースのファイル (.ppd ファイル) には、PostScript プリンターの特性について説明します。 Microsoft Windows 2000 以降、Pscript ドライバーは、Adobe Systems, Inc. から PPD 仕様のバージョン 4.3 と互換性がある .ppd ファイルをサポートします。Pscript は、プリンターの .ppd ファイルをテキスト .ppd ファイルが変更されるたびに再生成される .bpd ファイルとしてローカルに格納されている、バイナリ形式を変換します。

### <a href="" id="ddk-ntf-files-gg"></a>NTF ファイル

Windows 2000 およびそれ以降のフォント ファイル (.ntf ファイル) は、Pscript でサポートされているプリンターのデバイスのフォントを記述するために使用されるバイナリ ファイルです。

Microsoft では、よく生じる米国デバイス フォントの説明を含む、pscript.ntf という名前の既定の .ntf ファイルを提供します。 東アジア言語のプリンターの Microsoft も提供します、よく生じる東アジア言語の説明を含む pscrptfe.ntf という名前の既定の .ntf ファイル デバイス フォント。

さらに、ハードウェア ベンダーは pscript.ntf でサポートされていないフォントをデバイス フォントの説明を指定できます。 これらのフォントの記述を作成できる[してを NTF ファイルに変換する](converting-afm-files-to-ntf-files.md)します。 カスタマイズすると、プリンターのモデルに固有の .ntf ファイル インストールできるに依存しているファイルを一覧表示することによって、[プリンター INF ファイル](printer-inf-files.md)します。 詳細については、[Pscript ミニドライバーをインストールする](installing-a-pscript-minidriver.md)を参照してください。

Pscript 最初チェック プリンターのモデルに固有の .ntf ファイルによって、pscript.ntf を確認し、見つかった最初のフォントの説明を使用してフォント メトリックを検索します。

このセクションでは、次のトピックについて説明します。

[NTF ファイルに変換します。](converting-afm-files-to-ntf-files.md)

[東アジアしてを NTF ファイルに変換します。](converting-east-asian-afm-files-to-ntf-files.md)

[Pscript ミニドライバーをインストールします。](installing-a-pscript-minidriver.md)

[PostScript プリンターの標準機能](postscript-printer-driver-standard-features.md)

[Pscript プリンター ミニドライバーのバージョン管理](pscript-printer-minidriver-versioning.md)

[ホチキス止め Pscript のサポート](pscript-support-for-stapling.md)

[AddEuro](addeuro.md)

[TrueGray](truegray.md)

 

 




