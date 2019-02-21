---
title: SymProxy をインストールします。
description: SymProxy をインストールします。
ms.assetid: 63633de7-d254-415d-bf06-c0e81bd03e74
keywords:
- SymProxy のインストール
ms.date: 01/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 25fab2a9a40a858b4ff1e8820f5a31acaf06960b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530976"
---
# <a name="installing-symproxy"></a>SymProxy をインストールします。


## <a name="span-idsummaryofinstallationtasksspanspan-idsummaryofinstallationtasksspanspan-idsummaryofinstallationtasksspansummary-of-installation-tasks"></a><span id="Summary_of_installation_tasks"></span><span id="summary_of_installation_tasks"></span><span id="SUMMARY_OF_INSTALLATION_TASKS"></span>インストールのタスクの概要


次は、インストールして SymProxy を構成するタスクをまとめたものです。

-   %Windir% にコピーする必要があります SymProxy ファイル\\system32\\iis inetsrv フォルダー。 このタスクは以下で説明します。

-   レジストリは、SymProxy 用に構成する必要があります。 詳細については、次を参照してください。[レジストリを構成する](configuring-the-registry.md)します。

-   マニフェストは、パフォーマンス カウンターと ETW イベントとして登録する必要があるし、イベント ログを構成する必要があります。

-   IIS を構成する必要があります。 詳細については、次を参照してください。[ネットワーク セキュリティの資格情報を選択する](choosing-network-security-credentials.md)と[SymProxy の IIS を構成する](configuring-iis-for-symproxy.md)します。

Install.cmd ファイルを使用して、次の手順を自動化できます。 詳細については、次を参照してください。 [SymProxy Automated Installation](symproxy-automated-installation.md)します。

## <a name="span-idcopythesymproxyfilestoiisspanspan-idcopythesymproxyfilestoiisspanspan-idcopythesymproxyfilestoiisspancopy-the-symproxy-files-to-iis"></a><span id="Copy_the_SymProxy_files_to_IIS"></span><span id="copy_the_symproxy_files_to_iis"></span><span id="COPY_THE_SYMPROXY_FILES_TO_IIS"></span>IIS に SymProxy ファイルをコピーします。


SymProxy ファイルは、Windows Driver Kit のデバッガーのディレクトリに含まれます。 たとえば、これは、Windows 10 のキット用の 64 ビット ファイルの場所です。 C:\\Program Files (x86)\\Windows キット\\10\\デバッガー\\x64\\symproxy します。

SymProxy をサーバーにインストールするには、%windir% symproxy.dll、symsrv.dll および symproxy.man をコピー\\system32\\inetsrv します。

Microsoft のシンボル ストアにアクセス中に発生する問題を回避するには、%windir% と呼ばれる新しいファイルを作成\\system32\\inetsrv\\symsrv.yes します。 このファイルの内容は重要ではありません。 Symsrv.yes ファイルが存在する場合は、Microsoft パブリック シンボル ストアの使用許諾契約書が自動的に受け入れます。

 

 





