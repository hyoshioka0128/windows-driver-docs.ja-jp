---
title: XPSDrv プリンター ドライバーのデバッグ
description: XPSDrv プリンター ドライバーのデバッグ
ms.assetid: 7193f007-de25-4b77-9133-9937b3d37db0
keywords:
- デバッグ XPSDrv ドライバー WDK を印刷します。
- XPSDrv ドライバーが WDK 印刷のデバッグ
- XPSDrv プリンター ドライバー WDK、デバッグ
- spoolsv.exe プロセス WDK の印刷
- printfilterpipelinesvc.exe プロセス WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 809e49f2afffe4ea4f77b2e78868f3b1515d7421
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537374"
---
# <a name="debugging-xpsdrv-printer-drivers"></a>XPSDrv プリンター ドライバーのデバッグ


印刷キューに XPSDrv プリンター ドライバーが spoolsv.exe プロセスでホストされています。 ただし、GDI ベースのプリンター ドライバーとは異なりは XPSDrv プリンター ドライバーのフィルターは spoolsv.exe 別 printfilterpipelinesvc.exe プロセスでホストされるは。 結果として、XPSDrv プリンター ドライバーのフィルターをデバッグする printfilterpipelinesvc.exe プロセスにデバッガーをアタッチする必要があります。

### <a href="" id="configuring-the-printfilterpipelinesvc-exe-process-time-out"></a>Printfilterpipelinesvc.exe プロセスのタイムアウトを構成します。

印刷キューに XPSDrv プリンター ドライバーを使用した印刷ジョブが送信されるときに、printfilterpipelinesvc.exe プロセスが開始します。 プロセスが終了されたアクティブなレジストリの値で定義されている時間の期間後。 Printfilterpipelinesvc.exe プロセスの断続的な性質によって、printfilterpipelinesvc.exe XPSDriv のプリンター ドライバーのフィルターをデバッグするデバッガーをアタッチする困難になります。

ただし、レジストリで、非アクティブ状態のタイムアウト期間を構成できます。 下の PipelineHostTimeout 値、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\印刷**サブキーで、レジストリは、printfilterpipelinesvc.exe プロセスのタイムアウトをミリ秒単位で定義します。 XPSDrv プリンター ドライバーをデバッグしやすくには、この値を増やすことができます。 ドライバーに定義されているフィルターがない場合でも、プロセスがまだ起動できるように、構成ファイルを解析する printfilterpipelinesvc.exe プロセスを開始することに注意してください。

### <a name="configuring-the-system-for-debugging"></a>デバッグ用のシステムを構成します。

XPSDrv プリンター ドライバーをデバッグするには、次の必要があります。

1.  ファイルのポートに出力をデバッグするドライバーを使用する印刷キューを割り当てます。

2.  PipelineHostTimeout 値は、問題をデバッグする十分な時間を提供する値に設定します。

3.  Printfilterpipelinesvc.exe プロセスを開始する手順 1. で作成した印刷キューに印刷ジョブを送信します。

4.  Printfilterpipelinesvc.exe プロセスにデバッガーをアタッチし、デバッグを開始します。

デバッガーをアタッチした後は、フィルター モジュールにブレークポイントを設定し、プリンター ドライバーのデバッグを開始できます。

プリンター ドライバーをデバッグするデバッガーをアタッチする前に終了する printfilterpipelinesvc.exe プロセス発生すると、次の操作を行うことができます。

1.  構成ファイルで定義されているすべてのフィルターがない XPSDrv プリンター ドライバーを作成します。

2.  前の手順で作成されたプリンター ドライバーを使用した印刷キューを作成します。

3.  ファイルのポートに出力をデバッグするドライバーを使用する印刷キューを割り当てます。

4.  PipelineHostTimeout 値は、問題をデバッグする十分な時間を提供する値に設定します。

5.  手順 2 で作成した印刷キューに印刷ジョブを送信します。

6.  Printfilterpipelinesvc.exe プロセスにデバッガーをアタッチします。

7.  プリンター ドライバーをデバッグするのには、ブレークポイントを設定します。

8.  デバッグするドライバーを使用した印刷キューに印刷します。

 

 




