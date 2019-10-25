---
title: PCL XL ミニドライバーでの新しいデバイスフォントの指定
description: PCL XL ミニドライバーでの新しいデバイスフォントの指定
ms.assetid: 395b9200-4514-4b05-b417-15d4896914f4
keywords:
- PCL XL vector グラフィックス WDK Unidrv、デバイスフォント
- デバイスフォント WDK PCL XL
- フォント WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3def1c88b16dba522897be9525c6b0b169cfbbc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840406"
---
# <a name="specifying-new-device-fonts-in-pcl-xl-minidrivers"></a>PCL XL ミニドライバーでの新しいデバイスフォントの指定





PCL XL ミニドライバーで新しいデバイスフォントをサポートする場合は、それらのデバイスフォント用の*Unidrv フォントメトリック (UFM)* ファイルを作成する必要があります。

UFM ファイルの形式は次のとおりです。

[**Unifm\_HDR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_unifm_hdr)構造体。 ufm ファイルのヘッダーとして機能します。

[**UNIDRVINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_unidrvinfo)構造体

[**Ifimetrics**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_ifimetrics)構造体

[**Exttextmetric**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_exttextmetric)構造体

文字幅の表

正しく書式設定されたフォント選択コマンドを UFM ファイル内の正しい場所に配置する必要があります。 フォント選択コマンドは、フォント選択の場合は16バイト、空白文字の場合は1バイト、シンボルセット番号の桁数を保持するために必要なバイト数で構成されます。

次に、フォント選択コマンドが UFM ファイルにどのように表示されるかの例を示します。 (2 行目の数字は、フォント選択コマンドの各文字の位置を示しています)。

```cpp
CG Omega    BdIt 629
12345678901234567890
```

フォント名とスタイル、CG オメガ BdIt (太字/斜体) は、最初の16バイトを占有します。 その後、1つの空白文字があります。これにより、フォント名がシンボルセット番号と区別されます。 シンボルセット番号629は、最後の3バイトを取得します。 Unidrv は、UFM ファイル内のフォント選択コマンドを解析し、フォント選択コマンドとシンボルセット番号を個別に送信します。

前の例で説明したフォント名とシンボルセット番号は、 **SetFont**演算子に必要な3つの属性のうちの2つです。これは、ドライバーの出力データに表示されます。 次の例では、この演算子の**FontName**属性と**シンボルセット**属性が、前の例と同じ値に設定されています。 3番目の属性**Charsize**は、値100に設定されています。

```cpp
ubyte_array (CG Omega    BdIt) FontName
real32 100 CharSize
uint16 629 SymbolSet
SetFont
```

**SetFont**フォント選択コマンドの詳細については、 *PCL XL 機能リファレンスプロトコルクラス 2.0*のドキュメントを参照してください。 (このリソースは、一部の言語および国では使用できません。)

 

 




