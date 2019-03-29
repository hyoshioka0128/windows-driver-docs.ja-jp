---
title: フォールト挿入の有効化
description: フォールト挿入の有効化
ms.assetid: 451a5e9e-bc5c-4148-b475-7f38c535cf6a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78e47bd3171e3f0c05d8288962a6997010178e8b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579281"
---
# <a name="enabling-fault-injection"></a>フォールト挿入の有効化


WdfTester ツールでは、特定のドライバーに対して DDI フォールト インジェクションを構成するための WMI インターフェイスを提供します。 スクリプト (WdftesterScript.wsf) は、フォールト インジェクションを構成するのにはこの WMI インターフェイスを提供します。 独自のスクリプトを記述するか、提供されているスクリプトを使用して、フォールト インジェクションを有効にすることができます。 スクリプト (WdftesterScript.wsf) は、登録、構成、およびドライバーの登録を解除するには、コマンド プロンプト ウィンドウから実行できます。 スクリプトはというコマンド ライン オプションもあります**runtest**します。

### <a name="span-idwhattheruntestoptiondoesspanspan-idwhattheruntestoptiondoesspanwhat-the-runtest-option-does"></a><span id="what_the_runtest_option_does"></span><span id="WHAT_THE_RUNTEST_OPTION_DOES"></span>どのような runtest オプションでは

**Runtest**ドライバーでの操作を有効にして簡単な無効化を実行します。 このオプションでは、ツールを使用する方法を示します。 最初は、スクリプトは、指定されたドライバーを無効にし、され有効になります。 これにより、WdfTester を無効化中に行われたすべての DDI 呼び出しを監視し、操作を有効にできます。 スクリプトでは、WMI インターフェイスの 1 つを使用して、この期間中に呼び出された Ddi の一覧を取得します。 スクリプトを決定します (それらを返す NTSTATUS) のみこれら Ddi の失敗できます。 スクリプトは、一覧の最初の DDI が失敗する WdfTester を構成するための別の WMI インターフェイスを呼び出します。 スクリプトは無効にし、DDI 失敗し、WMI イベントが発生すると、ドライバーを使用します。 スクリプトは既に WMI の失敗イベントの DDI を待機しています。 イベントが正常に受信したし、原因が、コンピューターが応答しなくなるか (ドライバー開発者またはテスターによって決定される) としてのバグ チェックが発生する場合は、テストが成功したと見なされます。 スクリプトは、しの一覧で [次へ] DDI の次の手順を繰り返します。

**注**   、 **runtest**オプションは、コピーする必要があります、 [DevCon](devcon.md) (Devcon.exe) ツールし、その他の Wdftester ファイルと同じディレクトリに配置します。 Devcon.exe アプリケーションにある、 *%wdkroot*\\ツール\\*&lt;プラットフォーム&gt;* ディレクトリ。

 

**Runtest オプション:**

1.  WdfTester、ドライバーに登録します。 ドライバーをインストールしていない場合、runtest を使用する前にインストールする必要があります。

2.  このドライバーのドライバーの検証を有効に (Windows Vista を実行しているコンピューターまたは後で、再起動は必要ありません)。

3.  Devcon アプリケーションを使用して、ドライバーを無効にします。

4.  ドライバーを有効するには、Devcon アプリケーションを使用します。

5.  有効化中に呼び出された、操作を無効にして NTSTATUS およびを失敗でしたを返す関数を識別および関数の名前を取得します。

6.  非同期の WMI イベント通知を開始します。

7.  手順 5 で取得されたリストから失敗でしたした各 DDI: の
    1.  エラーの関数を構成します。
    2.  無効になり、Devcon.exe を使用して、ドライバーが有効になります。 関数を呼び出し、この操作と WdfTester 関数呼び出しが失敗します。
    3.  WMI イベントの発生を待機します。
    4.  WMI イベントが発生した場合は、 **runtest**オプションは、手順の一覧で次の関数の 7 を繰り返します。

8.  ドライバーの登録を解除します。

 

 





