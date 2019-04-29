---
title: ライブラリの処理
description: ライブラリの処理
ms.assetid: 8ae9ae3b-885d-4eb5-b55b-415edcfc041a
keywords:
- WDK Static Driver Verifier のライブラリ、処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6b9e0aa920c28489b4638685868800fb29a5c35
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327356"
---
# <a name="processing-a-library"></a>ライブラリの処理


検証を実行する前に、ドライバーを必要とするライブラリを処理します。

 **ライブラリを処理するには**

1.  Static Driver Verifier を開始します。 **ドライバー** Visual Studio でメニュー **Static Driver Verifier を起動しています.**.
2.  をクリックして、**ライブラリ** タブでをクリックし、**ライブラリの追加**ライブラリを追加します。
3.  ライブラリのプロジェクト ファイルを格納するディレクトリに移動します。
4.  ドライバーを使用して各ライブラリの次の手順を繰り返します。

Static Driver Verifier は、追加したライブラリのキャッシュを保持します。 検証のため、ドライバーが必要なと、キャッシュに存在するライブラリのみが使用されます。 ライブラリは、ドライバーを使用する同じ構成とプラットフォームの設定で処理されます。

使用して Visual Studio コマンド プロンプト ウィンドウからのライブラリを処理することも、 **msbuild t: sdv/p:「/=/lib の入力」** *libraryproject.vcxproj*オプション。 コマンド オプションについては、次を参照してください。 [Static Driver Verifier のコマンド (MSBuild)](-static-driver-verifier-commands--msbuild-.md)します。

必要なライブラリを何らかの理由で処理されない場合は、それを使用するドライバーでも確認できます。 ただし、結果は、信頼性は低くなります。

 

 





