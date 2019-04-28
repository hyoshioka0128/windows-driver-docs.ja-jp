---
title: WdfTester のインストール
description: WdfTester のインストール
ms.assetid: 39645ca4-3f4e-4a1f-bf62-7b44856ce58e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec2a443b5c2bc39cbd11d26157e92bad8f4008c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378582"
---
# <a name="wdftester-installation"></a>WdfTester のインストール


WdfTester ツールを実行するには、ドライバーで、前に最初 WdfTester ファイルを作業ディレクトリにコピーして、インストール スクリプトを実行します。

**WdfTester をインストールするには**

1.  WDK から次のファイルの一覧をコピー (*%wdkroot*\\ツール\\*&lt;プラットフォーム&gt;*) には、ドライバーのコピーを含むローカル フォルダーにバイナリ。
    Wdftester.sys Wdftester.inf Wdftester.ctl Wdftester.tmf WdftesterScript.wsf
2.  コマンド プロンプト ウィンドウを開きます (必ず**管理者として実行**Windows Vista で)、し、次のコマンド: cscript WdfTesterScript.wsf インストールを入力

    このコマンドは、Wdftester.sys ドライバーをインストールし、サービスを開始します。

3.  Enter キーを押します。

 

 





