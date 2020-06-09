---
title: Windows Vista のデバッグ
description: WinDbg を使用して Windows Vista をデバッグするには、windows 7 用の windows 7 デバッグツールを入手します。このパッケージは、SDK for Windows 7 に含まれています。
ms.assetid: 1E4FC9D9-7F84-4F67-8FBC-4283C69AB0AC
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08c750e38a44e9623c8e34927e238aeb30bec36c
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534779"
---
# <a name="debugging-windows-vista"></a>Windows Vista のデバッグ


WinDbg を使用して Windows Vista をデバッグするには、windows 7 用の[Microsoft Windows ソフトウェア開発キット (SDK) および .NET Framework 4.0](https://www.microsoft.com/download/details.aspx?id=8279)に含まれている Windows 7 デバッグツールの windows パッケージを入手してください。

Windows 用のデバッグツールのみをダウンロードする場合は、SDK をインストールし、インストール中に [ **Windows 用のデバッグツール**] ボックスを選択して、その他のすべてのボックスをオフにします。

**メモ**   SDK をインストールする前に、Microsoft Visual C++ 2010 再頒布可能コンポーネントをアンインストールする必要がある場合があります。 詳細については、 [Microsoft サポート web サイト](https://support.microsoft.com/help/2717426/windows-sdk-fails-to-install-with-return-code-5100)を参照してください。

 

## <a name="span-iddebugging_tools__windbg__kd__cdb__ntsd__for_windows_windows_vistaspandebugging-tools-windbg-kd-cdb-ntsd-for-windows-vista"></a><span id="DEBUGGING_TOOLS__WINDBG__KD__CDB__NTSD__FOR_WINDOWS_WINDOWS_VISTA"></span>Windows Vista 用のデバッグツール (WinDbg、KD、CDB、NTSD)


Windows 用の Windows 7 デバッグツールは、x86 ベースまたは x64 ベースのプロセッサで実行でき、x86 ベースまたは x64 ベースのプロセッサで実行されているコードをデバッグできます。 デバッガーとデバッグ対象のコードは、同じコンピューター上で実行されることも、別々のコンピューターで実行されることもあります。 いずれの場合も、デバッガーが実行されるコンピューターは "*ホスト コンピューター*" と呼ばれ、デバッグ対象のコンピューターは "*ターゲット コンピューター*" と呼ばれます。 対象のコンピューターでこれらのオペレーティングシステムのいずれかが実行されている場合は、windows 用の Windows 7 デバッグツールを使用します。

|               |                     |
|---------------|---------------------|
| Windows Vista | Windows Server 2008 |
 

対象のコンピューターでより新しいバージョンの Windows が実行されている場合は、 [windows 用の現在のデバッグツール](index.md)を入手してください。


 

 





