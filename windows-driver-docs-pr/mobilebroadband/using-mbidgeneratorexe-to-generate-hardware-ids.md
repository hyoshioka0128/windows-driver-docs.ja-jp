---
title: mbidgenerator.exe を使用したハードウェア ID の生成
description: mbidgenerator.exe を使用したハードウェア ID の生成
ms.assetid: 2f2286e2-9300-4ef8-8e13-0851b60cd8eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96749ccbfa249efa6013812b67f95c9744c26747
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323654"
---
# <a name="using-mbidgeneratorexe-to-generate-hardware-ids"></a>mbidgenerator.exe を使用したハードウェア ID の生成

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

サービスメタデータパッケージのハードウェア ID 値を生成するには、Windows 8.1 と Windows 10 の SDK の一部である MBIDGenerator コマンドラインツールを使用できます。

Windows 8 MBIDGenerator**の   は**、WDK に含まれていました。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>代入


MBIDGenerator は、次のパラメーターを受け入れます。

``` syntax
MBIDGenerator.exe [/Test] <input file> [<output file>]
```

*テスト*パラメーターは、ハッシュされていない出力を提供**する  、** Windows デベロッパーセンターのダッシュボードに送信するためのハードウェア id の生成には使用しないでください。

 

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Output


MBIDGenerator からの出力は、標準のコマンドライン出力の表示によって行われます。 必要に応じて、出力ファイルのパスとファイル名を指定できます。 エラーは常にコマンドプロンプトに返されます。

出力値は次のように表示されます。

``` syntax
<HardwareIDList>
  <HardwareID>MBAE:0:hashednumber1</HardwareID>
  <HardwareID>MBAE:0:hashednumber2</HardwareID>
  <HardwareID>MBAE:0:hashednumber3</HardwareID>
</HardwareIDList>
```

MBIDGenerator の出力を取得し、サービスメタデータパッケージの[Packageinfo XML スキーマ](packageinfo-xml-schema.md)に挿入することができます。

 

 





