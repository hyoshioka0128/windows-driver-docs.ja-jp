---
title: ソース コード ウィンドウ内のファイル
description: ソース コード ウィンドウ内のファイル
ms.assetid: 1bc248be-cdc8-4e6c-9eca-da2943daaf58
keywords:
- Static Driver Verifier レポート WDK、ソース コード ウィンドウ
- ソース コード ウィンドウ WDK Static Driver Verifier
- WDK Static Driver Verifier のファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81f18aed8e785ac522b5c42e8d2f1148f4e8fa55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531922"
---
# <a name="files-in-the-source-code-pane"></a>ソース コード ウィンドウ内のファイル


ファイルに表示されます、**ソース コード**ペインの含まれているコードが原因か、規則違反の検出に関係する場合にのみです。 その結果、さまざまなルール違反は、ウィンドウには、同じドライバーによって別のファイルが表示されます。

次の種類のファイルは、ソース コード ウィンドウに表示されます。

<span id="Driver_source_files"></span><span id="driver_source_files"></span><span id="DRIVER_SOURCE_FILES"></span>**ドライバーのソース ファイル**  
ドライバーの場合、規則違反に関連するライブラリを使用するは、ソース ファイル。 このファイル グループには、C のファイルとヘッダー ファイルが含まれています。

<span id="rule_source_file___________________.slic__"></span><span id="RULE_SOURCE_FILE___________________.SLIC__"></span>**規則のソース ファイル (\\*** **.slic** **)**  
ソース ファイル、 [Static Driver Verifier ルール](static-driver-verifier-rule.md)で検証します。 このコードは、インターフェイス チェック (SLIC)、この目的用に開発された単純な言語を仕様の言語で記述されます。

<span id="sdv-harness.c_"></span><span id="SDV-HARNESS.C_"></span>**sdv-harness.c**   
SDV のソース ファイル[オペレーティング システムのモデル](operating-system-model.md)の検証ルール。

 

 





