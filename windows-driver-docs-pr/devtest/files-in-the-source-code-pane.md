---
title: '[Source Code] (ソース コード) ウィンドウでのファイル'
description: '[Source Code] (ソース コード) ウィンドウでのファイル'
ms.assetid: 1bc248be-cdc8-4e6c-9eca-da2943daaf58
keywords:
- Static Driver Verifier レポート WDK、ソース コード ウィンドウ
- ソース コード ウィンドウ WDK Static Driver Verifier
- WDK Static Driver Verifier のファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81f18aed8e785ac522b5c42e8d2f1148f4e8fa55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378816"
---
# <a name="files-in-the-source-code-pane"></a>[Source Code]\(ソース コード\) ウィンドウでのファイル


ファイルに表示されます、**ソース コード**ペインの含まれているコードが原因か、規則違反の検出に関係する場合にのみです。 その結果、さまざまなルール違反は、ウィンドウには、同じドライバーによって別のファイルが表示されます。

次の種類のファイルは、ソース コード ウィンドウに表示されます。

<span id="Driver_source_files"></span><span id="driver_source_files"></span><span id="DRIVER_SOURCE_FILES"></span>**ドライバーのソース ファイル**  
ドライバーの場合、規則違反に関連するライブラリを使用するは、ソース ファイル。 このファイル グループには、C のファイルとヘッダー ファイルが含まれています。

<span id="rule_source_file___________________.slic__"></span><span id="RULE_SOURCE_FILE___________________.SLIC__"></span>**規則のソース ファイル (\\*** **.slic** **)**  
ソース ファイル、 [Static Driver Verifier ルール](static-driver-verifier-rule.md)で検証します。 このコードは、インターフェイス チェック (SLIC)、この目的用に開発された単純な言語を仕様の言語で記述されます。

<span id="sdv-harness.c_"></span><span id="SDV-HARNESS.C_"></span>**sdv-harness.c**   
SDV のソース ファイル[オペレーティング システムのモデル](operating-system-model.md)の検証ルール。

 

 





