---
title: PCL XL ミニドライバーで新しいデバイス フォントを指定する
description: PCL XL ミニドライバーで新しいデバイス フォントを指定する
ms.assetid: 395b9200-4514-4b05-b417-15d4896914f4
keywords:
- PCL XL ベクター グラフィックス WDK Unidrv、デバイス フォント
- デバイス フォント WDK PCL XL
- フォント WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90596e8d09a7a10edb939e19cf1063a392e81bc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570175"
---
# <a name="specifying-new-device-fonts-in-pcl-xl-minidrivers"></a>PCL XL ミニドライバーで新しいデバイス フォントを指定する





PCL XL ミニドライバーで新しいデバイス フォントをサポートする場合は、作成する必要があります*Unidrv フォント メトリック (UFM)* デバイス フォントのファイル。

UFM ファイルには、次の形式があります。

A [ **UNIFM\_HDR** ](https://msdn.microsoft.com/library/windows/hardware/ff563587) UFM ファイルのヘッダーとして機能する構造体

A [ **UNIDRVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff562872)構造体

[ **IFIMETRICS** ](https://msdn.microsoft.com/library/windows/hardware/ff567418)構造体

[ **EXTTEXTMETRIC** ](https://msdn.microsoft.com/library/windows/hardware/ff548801)構造体

文字幅の表

正しく書式設定されたフォントの選択コマンドは、UFM ファイル内の正しい位置に配置する必要があります。 フォントの選択コマンドのフォント選択、1 バイト文字のスペースを 16 バイトで構成され、記号の桁を保持するために必要なバイト数を設定します。

UFM ファイルでフォントの選択コマンドの表示と方法の例を次に示します。 (2 行目の数値を表示の各文字の位置のフォントの選択コマンド。)

```cpp
CG Omega    BdIt 629
12345678901234567890
```

フォント名とスタイル、CG オメガ BdIt (太字/斜体) 最初の 16 バイトを占有します。 その後、どの分離数を設定する、シンボルからフォント名、単一の空白文字があります。 シンボル セット番号、629 は、最後の 3 バイトを占有します。 Unidrv UFM ファイルでフォントの選択コマンドの解析し、フォントの選択コマンドを送信し、シンボルが個別に数を設定します。

フォント名とシンボル セット番号に必要な 3 つの属性の 2 つでは、前の例で説明した、 **SetFont**演算子で、ドライバーから出力データに表示されます。 次の例では、 **FontName**と**SymbolSet**この演算子の属性は、前の例のように同じ値に設定されます。 3 番目の属性**CharSize**100 の値に設定されます。

```cpp
ubyte_array (CG Omega    BdIt) FontName
real32 100 CharSize
uint16 629 SymbolSet
SetFont
```

詳細については、 **SetFont**フォント コマンドを参照してください、 *PCL XL 機能参照プロトコル クラス 2.0*ドキュメント。 (このリソースできない場合がありますのいくつかの言語および国。)

 

 




