---
title: Visual Studio を使用したユーザーモード プロセスのデバッグ
description: Microsoft Visual Studio では、Windows ユーザーモードのデバッガーを使用して、実行中のプロセスにアタッチしたり、新しいプロセスを生成してアタッチしたりすることができます。
ms.assetid: C19D1B6F-B97B-4C1B-AD84-AC974C5F5C8C
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3d628b1c2bf4d370733a2f215c1c9667c08872e7
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534423"
---
# <a name="span-iddebuggerdebugging_a_user-mode_process_using_visual_studiospandebugging-a-user-mode-process-using-visual-studio"></a><span id="debugger.debugging_a_user-mode_process_using_visual_studio"></span>Visual Studio を使用したユーザーモード プロセスのデバッグ

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>

Microsoft Visual Studio では、Windows ユーザーモードのデバッガーを使用して、実行中のプロセスにアタッチしたり、新しいプロセスを生成してアタッチしたりすることができます。 このプロセスは、デバッガーを実行しているのと同じコンピューターで実行することも、別のコンピューターで実行することもできます。

このトピックに記載されている手順では、Windows Driver Kit が Visual Studio に統合されている必要があります。 統合環境を入手するには、まず Visual Studio をインストールしてから、Windows Driver Kit (WDK) をインストールします。 詳細については、「 [Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/)」を参照してください。

## <a name="span-idattaching_to_a_running_process_on_the_same_computerspanspan-idattaching_to_a_running_process_on_the_same_computerspanspan-idattaching_to_a_running_process_on_the_same_computerspanattaching-to-a-running-process-on-the-same-computer"></a><span id="Attaching_to_a_running_process_on_the_same_computer"></span><span id="attaching_to_a_running_process_on_the_same_computer"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_ON_THE_SAME_COMPUTER"></span>同じコンピューターでの実行中のプロセスへのアタッチ


1.  Visual Studio で、[**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
2.  [**プロセスにアタッチ**] ダイアログボックスで、 **[トランスポート**] を [ **Windows ユーザーモードのデバッガー**] に設定し、[**修飾子**] を**Localhost**に設定します。
3.  [選択**可能なプロセス**] ボックスの一覧で、アタッチ先のプロセスを選択します。
4.  **[アタッチ]** をクリックします。

### <a name="span-idnoninvasive_debuggingspanspan-idnoninvasive_debuggingspanspan-idnoninvasive_debuggingspannoninvasive-debugging"></a><span id="Noninvasive_debugging"></span><span id="noninvasive_debugging"></span><span id="NONINVASIVE_DEBUGGING"></span>Noninvasive デバッグ

実行中のプロセスをデバッグし、その実行を最小限にする場合は、プロセス[noninvasively](noninvasive-debugging--user-mode-.md)をデバッグする必要があります。

## <a name="span-idspawning_a_new_process_on_the_same_computerspanspan-idspawning_a_new_process_on_the_same_computerspanspan-idspawning_a_new_process_on_the_same_computerspanspawning-a-new-process-on-the-same-computer"></a><span id="Spawning_a_new_process_on_the_same_computer"></span><span id="spawning_a_new_process_on_the_same_computer"></span><span id="SPAWNING_A_NEW_PROCESS_ON_THE_SAME_COMPUTER"></span>同じコンピューターで新しいプロセスを生成する


1.  Visual Studio の [**ツール**] メニューで、 **[デバッガー] の [起動**] を選択します。
2.  **[デバッガーで起動**] ダイアログボックスで、実行可能ファイルへのパスを入力します。 引数と作業ディレクトリを入力することもできます。
3.  [**起動] をクリックします。**

デバッガーによって作成されるプロセス ("生成されたプロセス" とも呼ばれます) の動作は、デバッガーが作成しないプロセスとは少し異なります。

デバッガーによって作成されるプロセスでは、標準のヒープ API を使用する代わりに、特殊なデバッグヒープを使用します。 デバッグヒープではなく標準ヒープを使用するように、生成されたプロセスに強制するには、 \_ NO \_ debug \_ heap 環境変数を使用します。

また、ターゲットアプリケーションはデバッガーの子プロセスであるため、デバッガーのアクセス許可を継承します。 このアクセス許可によって、対象アプリケーションは、それ以外の操作を実行できない特定のアクションを実行できる可能性があります。 たとえば、ターゲットアプリケーションが保護されたプロセスに影響を与える可能性があります。

## <a name="span-idattaching_to_a_running_process_on_a_separate_computerspanspan-idattaching_to_a_running_process_on_a_separate_computerspanspan-idattaching_to_a_running_process_on_a_separate_computerspanattaching-to-a-running-process-on-a-separate-computer"></a><span id="Attaching_to_a_running_process_on_a_separate_computer"></span><span id="attaching_to_a_running_process_on_a_separate_computer"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_ON_A_SEPARATE_COMPUTER"></span>別のコンピューターでの実行中のプロセスへのアタッチ


デバッガーとデバッグ対象のコードが別のコンピューターで実行されることがあります。 デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ対象のコードを実行するコンピューターは*ターゲットコンピューター*と呼ばれます。 ターゲットコンピューターは、ホストコンピューター上の Visual Studio から構成できます。 ターゲットコンピューターの構成は、ターゲットコンピューターの*プロビジョニング*とも呼ばれます。 詳しくは、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」をご覧ください。

対象のコンピューターをプロビジョニングした後、ホストコンピューターで Visual Studio を使用して、対象のコンピューターで実行されているプロセスにアタッチできます。

1.  ホストコンピューターの Visual Studio で、[**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
2.  [**プロセスにアタッチ**] ダイアログボックスで、 **[トランスポート**] を [ **Windows ユーザーモードのデバッガー**] に設定し、[**修飾子**] に対象のコンピューターの名前を設定します。
3.  [選択**可能なプロセス**] ボックスの一覧で、アタッチ先のプロセスを選択します。
4.  **[アタッチ]** をクリックします。

**メモ**   別のホストとターゲットコンピューターを使用している場合は、対象のコンピューターに Visual Studio と WDK をインストールしないでください。 Visual Studio と WDK がターゲットコンピューターにインストールされている場合、デバッグはサポートされません。

 

 

 





