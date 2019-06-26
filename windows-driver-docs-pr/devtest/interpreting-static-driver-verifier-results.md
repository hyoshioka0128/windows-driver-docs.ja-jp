---
title: 静的ドライバー検証ツールの結果の解釈
description: 静的ドライバー検証ツールの結果の解釈
ms.assetid: ec7e3b90-5d55-411a-8cfe-a1c9c4029694
keywords:
- Static Driver Verifier WDK、表示オプション
- StaticDV WDK、オプションが表示されます。
- SDV の WDK オプションが表示されます。
- 静的ドライバー検証ツールの WDK、検証結果
- StaticDV WDK、検証結果
- SDV の WDK、検証結果
- 検証結果の WDK Static Driver Verifier
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: f85f9192aefb7d79f4eed1a29923d4a7a37685bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373704"
---
# <a name="interpreting-static-driver-verifier-results"></a>静的ドライバー検証ツールの結果の解釈


Visual Studio からの Static Driver Verifier を起動して、ドライバーの分析を実行するで結果が表示されます、**結果**メイン タブの概要。

![スクリーン ショット、静的ドライバー検証ツールを実行した後、結果をサマリー表示します。](images/sdv-results-vs.png)

### <a name="span-idstatisticsspanspan-idstatisticsspanspan-idstatisticsspanstatistics"></a><span id="Statistics"></span><span id="statistics"></span><span id="STATISTICS"></span>統計情報

**Entrypoints**ドライバーのソース コード内で見つかったエントリ ポイントの数を報告します。 エントリ ポイントは、ドライバーによって提供されるコールバックまたはディスパッチ ルーチンです。 関数の役割の種類の宣言を使用してエントリ ポイントを定義します。 分析を実行する fiind SDV する必要があります。 少なくとも 1 つのエントリ ポイント。 詳細については、「[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。

**欠陥の見つかった**分析中に見つかった欠陥数を報告します。 欠陥は、DDI 準拠規則の違反です。

**実行されたテスト**分析中にテストされたルールの数を報告します。 選択したルールが、**ルール**タブ。

### <a name="span-idstatusspanspan-idstatusspanspan-idstatusspanstatus"></a><span id="Status"></span><span id="status"></span><span id="STATUS"></span>状態

分析のステータスを報告します。 完了したら、結果が見つかりませんでしたを確認できます。

### <a name="span-idresultsspanspan-idresultsspanspan-idresultsspanresults"></a><span id="Results"></span><span id="results"></span><span id="RESULTS"></span>結果

<span id="Completed__Rule_"></span><span id="completed__rule_"></span><span id="COMPLETED__RULE_"></span>**完了した (ルール)**  
SDV は、規則違反のドライバーをテストしますが、ルールの違反を証明する可能性がありますされません。

この結果では、ドライバーがエラーを回避することは限りません。 のみの検証パス ルールに違反したことを証明でしたいない SDV を意味します。

<span id="Defect"></span><span id="defect"></span><span id="DEFECT"></span>**欠陥**  
SDV には、1 つまたは複数の欠陥が報告されている場合は、クリックして、**欠陥**へのリンク[静的ドライバー検証ツールのレポートを使用して](using-the-static-driver-verifier-report.md)エラーのトレースを表示します。

<span id="Not_Applicable"></span><span id="not_applicable"></span><span id="NOT_APPLICABLE"></span>**該当なし**  
SDV は、規則違反のドライバーをテストまたはドライバーでは、分析のために必要なエントリ ポイントがサポートされていませんでしたが、ドライバーは、ルールを監視する関数を呼び出さなかったです。

場合、規則が関数呼び出し (通常は、リソースへのポインター) で特定の引数を監視し、ドライバーは、関数を呼び出しませんまたはその引数を参照していません、ルールは、ドライバーには適用されません。

ドライバーは、エントリ ポイントを指定するルール モニターでは、この結果ことを示しています、SDV が見つかりませんでしたエントリ ポイントが正しく解釈されませんでした関数を呼び出すことが場合。 このような状況が発生したことを確認するを調べ、必要に応じて、修正、 [Sdv map.h](sdv-map-h.md)ファイル。 この手順については、次を参照してください。[ドライバーをスキャン](scanning-the-driver.md)します。

各ルールの詳細については、次を参照してください。、[静的ドライバー検証規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)参照。

さらに、ドライバーを確認するには、さまざまな規則を使用して検証を実行します。

<span id="Timeouts"></span><span id="timeouts"></span><span id="TIMEOUTS"></span>**タイムアウト**  
SDV は、各ルールの検証の制限時間を超えたため、ルールの検証を停止します。 制限時間設定されて、[静的ドライバー検証ツールのオプション ファイル](static-driver-verifier-options-file.md)、または最大時間 フィールドで、**構成** タブ。

タイムアウトは、結果が不確定の結果と見なされます。 ドライバーのエラーは示されません。 SDV は、タイムアウトを報告する場合は、検証が許可された期間を拡張 (、 **SDV\_SlamConfig\_タイムアウト**sdv default.xmlfile 内の値) もう一度検証を実行します。

<span id="Completed__Property_"></span><span id="completed__property_"></span><span id="COMPLETED__PROPERTY_"></span>**完了した (プロパティ)**  
SDV は、指定されたドライバーのドライバーのプロパティ規則を実行します。 ドライバーのプロパティ規則は、ドライバーの機能を確認しますまたはサポートされる機能、さらに詳しい分析の準備をいます。 ドライバーのプロパティ規則など**CancelRoutine**、WDM ドライバーが登録されているかどうかにチェックを[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチン。 場合、*キャンセル*ルーチンが検出されない、特定の WDM ルールは適用されません。 これは、ドライバーのプロパティが満たされていないことを意味します。

<span id="Satisfied__Property_"></span><span id="satisfied__property_"></span><span id="SATISFIED__PROPERTY_"></span>**満足 (プロパティ)**  
SDV は、指定されたドライバーのドライバーのプロパティ規則を実行します。 ドライバーのプロパティ規則は、ドライバーの機能を確認しますまたはサポートされる機能、さらに詳しい分析の準備をいます。 ドライバーのプロパティ規則など**CancelRoutine**、WDM ドライバーが登録されているかどうかにチェックを[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチン。 場合、*キャンセル*ルーチンが検出されると、特定の WDM 規則が適用されます。 つまり、ドライバーのプロパティが満たされていること

<span id="Spaceouts"></span><span id="spaceouts"></span><span id="SPACEOUTS"></span>**Spaceouts**  
SDV は、検証ルールを検証するためのメモリ制限を超えたために停止ルールの数。 メモリの制限が設定されて、[静的ドライバー検証ツールのオプション ファイル](static-driver-verifier-options-file.md)、sdv default.xml します。

Spaceout は結果が不確定の結果と見なされます。 SDV は、spaceout を報告する場合は、検証用に割り当てられる領域を拡張 (、 **SDV\_SlamConfig\_Spaceout** sdv default.xml ファイル内の値) もう一度検証を実行します。

<span id="Other"></span><span id="other"></span><span id="OTHER"></span>**その他**  

SDV 元となることを復旧できませんでした内部エラーの発生回数。  参照してください、[静的ドライバー検証ツールのエラー メッセージ](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-error-messages)ページ エラーの詳細については、デバッグします。

 

 





