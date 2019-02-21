---
title: Mbidgenerator.exe を使用して、ハードウェア Id を生成するには
description: Mbidgenerator.exe を使用して、ハードウェア Id を生成するには
ms.assetid: 2f2286e2-9300-4ef8-8e13-0851b60cd8eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96749ccbfa249efa6013812b67f95c9744c26747
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558526"
---
# <a name="using-mbidgeneratorexe-to-generate-hardware-ids"></a>Mbidgenerator.exe を使用して、ハードウェア Id を生成するには

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

サービス メタデータ パッケージのハードウェア ID の値を生成するには、Windows 8.1 および Windows 10 SDK の一部である MBIDGenerator.exe コマンド ライン ツールを使用できます。

**注**   Windows 8 MBIDGenerator.exe では、WDK に含まれていました。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>入力


MBIDGenerator.exe は、次のパラメーターを受け取ります。

``` syntax
MBIDGenerator.exe [/Test] <input file> [<output file>]
```

**注**   、*テスト*パラメーターはハッシュされていない出力を提供し、Windows デベロッパー センター ダッシュ ボードに送信するハードウェア Id を生成するのには使えません。

 

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>出力


MBIDGenerator.exe からの出力は、標準のコマンドライン出力の表示では。 必要に応じて、出力ファイルのパスとファイル名を指定することができます。 常に、コマンド プロンプトに戻るエラーが報告されます。

出力値は、次のように表示されます。

``` syntax
<HardwareIDList>
  <HardwareID>MBAE:0:hashednumber1</HardwareID>
  <HardwareID>MBAE:0:hashednumber2</HardwareID>
  <HardwareID>MBAE:0:hashednumber3</HardwareID>
</HardwareIDList>
```

MBIDGenerator.exe から出力を取得し、それを挿入できます、 [PackageInfo XML スキーマ](packageinfo-xml-schema.md)サービス メタデータ パッケージの。

 

 





