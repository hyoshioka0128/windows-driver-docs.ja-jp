---
title: 静的ドライバー検証ツールの結果の解釈
description: 静的ドライバー検証ツールの結果の解釈
ms.assetid: ec7e3b90-5d55-411a-8cfe-a1c9c4029694
keywords:
- 静的ドライバー検証ツール WDK、表示オプション
- StaticDV WDK、表示オプション
- SDV WDK、表示オプション
- 静的ドライバー検証ツール WDK、検証結果
- StaticDV WDK、検証結果
- SDV WDK、検証結果
- 検証結果 WDK 静的ドライバー検証ツール
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 228eab96c66f108732c50796a2dbea2dab77ffaf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839558"
---
# <a name="interpreting-static-driver-verifier-results"></a>静的ドライバー検証ツールの結果の解釈


Visual Studio から静的ドライバー検証ツールを起動し、ドライバーの分析を実行すると、結果は [メイン] タブの [**結果**の概要] に表示されます。

![静的ドライバー検証ツールを実行した後の結果の概要を示すスクリーンショット。](images/sdv-results-vs.png)

### <a name="span-idstatisticsspanspan-idstatisticsspanspan-idstatisticsspanstatistics"></a><span id="Statistics"></span><span id="statistics"></span><span id="STATISTICS"></span>値

**Entrypoints**ドライバーのソースコードで見つかったエントリポイントの数を報告します。 エントリポイントは、ドライバーによって提供されるコールバックまたはディスパッチルーチンです。 エントリポイントは、関数ロール型宣言を使用して定義します。 分析を実行するには、SDV が少なくとも1つのエントリポイントを処理する必要があります。 詳細については、「[関数ロール型宣言の使用](using-function-role-type-declarations.md)」を参照してください。

**欠陥が見つかりました**分析中に検出された欠陥の数を報告します。 欠陥は、DDI コンプライアンス規則の違反です。

**実行**されたテスト分析中にテストされたルールの数を報告します。 **[ルール]** タブで選択したルールが表示されます。

### <a name="span-idstatusspanspan-idstatusspanspan-idstatusspanstatus"></a><span id="Status"></span><span id="status"></span><span id="STATUS"></span>オンライン

分析の状態を報告します。 完了すると、見つかった結果を確認できます。

### <a name="span-idresultsspanspan-idresultsspanspan-idresultsspanresults"></a><span id="Results"></span><span id="results"></span><span id="RESULTS"></span>生じ

<span id="Completed__Rule_"></span><span id="completed__rule_"></span><span id="COMPLETED__RULE_"></span>**完了 (ルール)**  
SDV は、規則に違反するかドライバーをテストしましたが、規則違反を証明できませんでした。

この結果、ドライバーがエラーにならないという意味ではありません。 これは、SDV が検証パスの規則に違反していることを証明できなかったことを意味します。

<span id="Defect"></span><span id="defect"></span><span id="DEFECT"></span>**不具合**  
SDV が1つ以上の欠陥を報告した場合は、 **[欠陥]** リンクをクリックして、[静的ドライバー検証ツールレポートを使用](using-the-static-driver-verifier-report.md)してエラーのトレースを表示します。

<span id="Not_Applicable"></span><span id="not_applicable"></span><span id="NOT_APPLICABLE"></span>**該当なし**  
SDV は、規則に違反するかドライバーをテストしましたが、その分析に必要なエントリポイントをドライバーがサポートしていなかったか、またはドライバーがルールで監視する機能を呼び出しませんでした。

ルールが関数呼び出しの特定の引数 (通常はリソースへのポインター) を監視し、ドライバーが関数を呼び出していないか、またはその引数を参照していない場合、規則はドライバーに適用されません。

ドライバーがエントリポイントを指定し、ルールが監視する関数を呼び出す場合、この結果は、SDV がエントリポイントを見つけられなかったか、正しく解釈できなかったことを示している可能性があります。 この状況が発生したことを確認するには、を確認し、必要に応じて、 [sdv .h](sdv-map-h.md)ファイルを修正します。 この手順の詳細については、「[ドライバーのスキャン](scanning-the-driver.md)」を参照してください。

各ルールの詳細については、「[静的ドライバー検証規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のリファレンス」を参照してください。

ドライバーをさらに確認するには、さまざまな規則を使用して検証を実行します。

<span id="Timeouts"></span><span id="timeouts"></span><span id="TIMEOUTS"></span>**タイムアウト**  
SDV は、各ルールの検証の制限時間を超えたため、ルールの検証を停止しました。 制限時間は、[静的ドライバー検証ツールのオプションファイル](static-driver-verifier-options-file.md)、または **[構成]** タブの 最大時間 フィールドで設定します。

タイムアウトは、結果が不確定であると見なされます。 ドライバーエラーを示すものではありません。 SDV がタイムアウトを報告する場合は、確認のために許可されている時間を延長し (sdv-xmlfile の **\_Sdamconfig\_タイムアウト**値)、もう一度検証を実行します。

<span id="Completed__Property_"></span><span id="completed__property_"></span><span id="COMPLETED__PROPERTY_"></span>**完了 (プロパティ)**  
SDV は、指定されたドライバーのドライバープロパティルールを実行しました。 ドライバーのプロパティルールでは、ドライバーの機能やサポートされている機能が確認され、さらに分析するための準備があります。 たとえば、ドライバープロパティ rule **Cancelroutine**は、WDM ドライバーが[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを登録したかどうかを確認します。 *キャンセル*ルーチンが検出されない場合、特定の WDM 規則は適用されません。 これは、ドライバーのプロパティが満たされなかったことを意味します。

<span id="Satisfied__Property_"></span><span id="satisfied__property_"></span><span id="SATISFIED__PROPERTY_"></span>**満たされる (プロパティ)**  
SDV は、指定されたドライバーのドライバープロパティルールを実行しました。 ドライバーのプロパティルールでは、ドライバーの機能やサポートされている機能が確認され、さらに分析するための準備があります。 たとえば、ドライバープロパティ rule **Cancelroutine**は、WDM ドライバーが[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを登録したかどうかを確認します。 *キャンセル*ルーチンが検出されると、特定の WDM ルールが適用されます。 これは、ドライバーのプロパティが満たされたことを意味します。

<span id="Spaceouts"></span><span id="spaceouts"></span><span id="SPACEOUTS"></span>**スペースアウト**  
ルールを検証するためのメモリ制限を超えたため、SDV が検証を停止したルールの数。 メモリの制限は、[静的ドライバーの検証ツールのオプションファイル](static-driver-verifier-options-file.md)である sdv-default で設定されます。

スペースは、結果が不確定であると見なされます。 SDV が空白を報告する場合は、検証用に割り当てられた領域を拡張し (sdv-default ファイルの**sdv\_SlamConfig\_空間アウト**値)、もう一度検証を実行します。

<span id="Other"></span><span id="other"></span><span id="OTHER"></span>**他の**  

SDV が、回復できなかった内部エラーを検出した回数。  エラーとデバッグの詳細については、「[静的ドライバーの検証エラーメッセージ](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-error-messages)」ページを参照してください。

 

 





