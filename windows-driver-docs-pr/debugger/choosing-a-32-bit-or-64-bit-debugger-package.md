---
title: 32 ビットまたは 64 ビット デバッグ ツールの選択
description: Windows 用デバッグツールをインストールすると、32ビットのツールセットと64ビットのツールセットの両方が得られます。
ms.assetid: 26aaaf11-1005-4ae7-8f27-4ae0812faa81
keywords:
- 32-ビットデバッガーパッケージ
- 32ビットデバッグツール
- 64-ビットデバッガーパッケージ
- 64ビットデバッグツール
- 32ビットパッケージと64ビットパッケージのどちらかを選択してインストール
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01a3181caef4dc68f86e0fed79e1d3635463cbe1
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528972"
---
# <a name="choosing-the-32-bit-or-64-bit-debugging-tools"></a>32 ビットまたは 64 ビット デバッグ ツールの選択


Windows 用デバッグツールをインストールすると、32ビットのツールセットと64ビットのツールセットの両方が得られます。

他のデバッグ環境 (WinDbg、KD、CDB、NTSD) のいずれかを使用している場合は、自分で選択する必要があります。 使用するデバッグツールのセットを決定するには、ホストコンピューターで実行されているプロセッサの種類と、ホストコンピューターで32または64ビットバージョンの Windows が実行されているかどうかを確認する必要があります。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。

### <a name="span-idhost_computer_running_a_32-bit_version_of_windowsspanspan-idhost_computer_running_a_32-bit_version_of_windowsspanspan-idhost_computer_running_a_32-bit_version_of_windowsspanhost-computer-running-a-32-bit-version-of-windows"></a><span id="Host_computer_running_a_32-bit_version_of_Windows"></span><span id="host_computer_running_a_32-bit_version_of_windows"></span><span id="HOST_COMPUTER_RUNNING_A_32-BIT_VERSION_OF_WINDOWS"></span>32ビットバージョンの Windows を実行しているホストコンピューター

ホストコンピューターで32ビットバージョンの Windows が実行されている場合は、32ビットのデバッグツールを使用します。 (この状況は、x86 ベースと x64 ベースの両方のターゲットに適用されます)。

### <a name="span-idx64-based_host_computer_running_a_64-bit_version_of_windowsspanspan-idx64-based_host_computer_running_a_64-bit_version_of_windowsspanspan-idx64-based_host_computer_running_a_64-bit_version_of_windowsspanx64-based-host-computer-running-a-64-bit-version-of-windows"></a><span id="x64-based_host_computer_running_a_64-bit_version_of_Windows"></span><span id="x64-based_host_computer_running_a_64-bit_version_of_windows"></span><span id="X64-BASED_HOST_COMPUTER_RUNNING_A_64-BIT_VERSION_OF_WINDOWS"></span>64ビットバージョンの Windows を実行している x64 ベースのホストコンピューター

ホストコンピューターが x64 ベースのプロセッサを使用していて、64ビット版の Windows を実行している場合は、次の規則が適用されます。

- ダンプファイルを分析する場合は、32ビットのデバッグツールまたは64ビットのデバッグツールのいずれかを使用できます。 (ダンプファイルがユーザーモードのダンプファイルであるか、カーネルモードのダンプファイルであるかは重要ではなく、ダンプファイルが x86 ベースまたは x64 ベースのプラットフォームで作成されているかどうかは重要ではありません。

- カーネルモードのデバッグを実行している場合は、32ビットのデバッグツールまたは x64 デバッグツールのいずれかを使用できます。 (この状況は、x86 ベースと x64 ベースの両方のターゲットに適用されます)。

- デバッガーと同じコンピューターで実行されているライブユーザーモードコードをデバッグする場合は、64ビットツールを使用して、WOW64 で実行されている64ビットコードと32ビットコードをデバッグします。 デバッガーを32ビットまたは64ビットモードに設定するには、 [**effmach**](-effmach--effective-machine-.md)コマンドを使用します。

- 別のターゲットコンピューターで実行されている有効な32ビットユーザーモードコードをデバッグする場合は、32ビットのデバッグツールを使用します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[Windows のデバッグ](index.md)
