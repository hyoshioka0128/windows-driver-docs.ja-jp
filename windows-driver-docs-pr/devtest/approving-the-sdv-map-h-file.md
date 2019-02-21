---
title: Sdv map.h ファイルを承認します。
description: Sdv map.h ファイルを承認します。
ms.assetid: eb192eb2-7a2c-47eb-846e-3d641d5046a8
keywords:
- Sdv map.h WDK Static Driver Verifier を承認します。
- Sdv map.h を承認します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65e1ac75efd01e57684a09fd11ff386c47b46a26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536942"
---
# <a name="approving-the-sdv-maph-file"></a>Sdv map.h ファイルを承認します。


Sdv map.h ファイルには、ファイルを調べることと、すべてのエラーを修正した後、ファイルをおそらく承認した SDV を指示するテキストの行が含まれています。 作成されると、Sdv map.h ファイルには、語句が含まれます。"承認済み = false"。

### <a name="span-idtoapproveansdvmaphfilespanspan-idtoapproveansdvmaphfilespanto-approve-an-sdv-maph-file"></a><span id="to_approve_an_sdv_map_h_file"></span><span id="TO_APPROVE_AN_SDV_MAP_H_FILE"></span>Sdv map.h ファイルを承認するには

1.  Sdv map.h ファイルをメモ帳などのテキスト エディターで開きます。 SDV は、ドライバーのソース ディレクトリに Sdv map.h ファイルを作成します。 (これは、検証用のローカル ディレクトリです)。

2.  変更 **//Approved=false**に **//Approved=true**します。

### <a name="span-idwhenyoushouldapproveasdvmaphfilespanspan-idwhenyoushouldapproveasdvmaphfilespanwhen-you-should-approve-a-sdv-maph-file"></a><span id="when_you_should_approve_a_sdv_map_h_file"></span><span id="WHEN_YOU_SHOULD_APPROVE_A_SDV_MAP_H_FILE"></span>Sdv map.h ファイルを承認するとき

Sdv map.h 正確かつ完全な場合に、SDV:

-   すべてのために使用するエントリ ポイントが見つかりません。

-   エントリ ポイントに関連付けられているロールの適切な関数の種類。

### <a name="span-idwhenyoushouldcorrectasdvmaphfilespanspan-idwhenyoushouldcorrectasdvmaphfilespanwhen-you-should-correct-a-sdv-maph-file"></a><span id="when_you_should_correct_a_sdv_map_h_file"></span><span id="WHEN_YOU_SHOULD_CORRECT_A_SDV_MAP_H_FILE"></span>Sdv map.h ファイルを修正すると

Sdv map.h ファイルが正しくないか不完全な場合に SDV:

-   Driver では、すべてのエントリ ポイントが見つかりません役割タイプの宣言関数を見つけられないため、通常 (を参照してください[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md))。

-   重複するコールバック関数が関数のロールの種類に関連付けられます。

-   最大値よりも多くのコールバック関数は、関数のロールの種類のサポートします。

-   あることが検出または存在しない間違った関数名 Sdv map.h ファイルで、ファイルが承認されます。

SDV を分析できるすべてのエントリ ポイントには、ドライバーは必要はありません。 特定のルールの検証には、ドライバーがドライバーのエントリ ポイントが必要とする場合、SDV はそのルールの検証をキャンセルしの結果を返します**該当なし**します。 この結果は、障害が発生した結果であると見なされません。

SDV はドライバーで、エントリ ポイントが見つかりません、しない限りは、その分析を実行します。 分析で使用されるヘッダー ファイルが不完全なまたは正しくない場合は、検証結果は信頼できません。

SDV が検出または存在しない間違った関数名、Sdv map.h ファイルで、ファイルが承認された後、SDV は終了し、次の例のような警告メッセージが発行されます。

```
Warning 'driver' It appears that your sdv-map.h file has an incorrect entry at this line "#define fun_IRP_MJ_PNP DispatchPnpNotExist". Please regenerate your sdv-map.h file.
```

このエラーを修正するには、エラーが発生しますまたは、ファイルを再生成する Sdv.map ファイル内の行を削除します。

### <a name="span-idtoregeneratethesdvmaphfilespanspan-idtoregeneratethesdvmaphfilespanto-regenerate-the-sdv-maph-file"></a><span id="to_regenerate_the_sdv_map_h_file"></span><span id="TO_REGENERATE_THE_SDV_MAP_H_FILE"></span>Sdv map.h ファイルを再生成するには

1.  Sdv map.h ファイルを開き、変更 **//Approved=true**に **//Approved=false**します。

2.  使用して、 **staticdv/scan** 、マップ ファイルを再生成または使用するコマンド、 **staticdv/rule**または**staticdv/config** SDV 分析を実行するコマンド。

 

 





