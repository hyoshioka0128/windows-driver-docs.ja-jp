---
ms.assetid: DAD531B1-2308-481F-841B-450EEEDA1BB1
title: ユーザー モード ドライバーとデスクトップ アプリでの Microsoft C ランタイムの使用
description: このトピックでは、Windows 8 および Windows 8.1 用のアプリケーションとドライバーを使って C ランタイム ライブラリを配布する方法について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16fef7a8ac858884e1be68e5b0fc7f61ca014d2e
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "63344031"
---
# <a name="using-the-microsoft-c-runtime-with-user-mode-drivers-and-desktop-apps"></a>ユーザー モード ドライバーとデスクトップ アプリでの Microsoft C ランタイムの使用
[このトピックはデスクトップ ドライバーのみに適用され、ユニバーサル ドライバーには適用されません。]

このトピックでは、Windows 8 および Windows 8.1 用のアプリケーションとドライバーを使って C ランタイム ライブラリを配布する方法について説明します。 ユーザー モード ドライバーとデスクトップ アプリケーションの作成者がコードをコンパイルし、必要な C ランタイム ライブラリと共に再頒布できるようにパッケージ化するためのガイドラインを示します。

## <a name="span-idthe_c_runtime_libraries__crt__are_no_longer_shipped_as_a_windows_shared_componentspanspan-idthe_c_runtime_libraries__crt__are_no_longer_shipped_as_a_windows_shared_componentspanspan-idthe_c_runtime_libraries__crt__are_no_longer_shipped_as_a_windows_shared_componentspanthe-c-runtime-libraries-crt-are-no-longer-shipped-as-a-windows-shared-component"></a><span id="The_C_runtime_libraries__CRT__are_no_longer_shipped_as_a_Windows_shared_component"></span><span id="the_c_runtime_libraries__crt__are_no_longer_shipped_as_a_windows_shared_component"></span><span id="THE_C_RUNTIME_LIBRARIES__CRT__ARE_NO_LONGER_SHIPPED_AS_A_WINDOWS_SHARED_COMPONENT"></span>C ランタイム ライブラリ (CRT) の Windows 共有コンポーネントへの付属停止


以前は、C ランタイム ライブラリ (CRT) が Window 共有システム コンポーネントとして配布されていました。 以前のバージョンの WDK では、ドライバーや従来型の Windows アプリをビルドするときに、コードを Windows システム バージョンの CRT とリンクできました。 Windows 8 リリースでは、C ランタイム ライブラリがシステム コンポーネントとは見なされなくなったため、ユーザー モード ドライバーやデスクトップ アプリケーションと共に再頒布可能バージョンの CRT を出荷する必要があります。 このトピックでは、この変更の理由、C ランタイムの新しいコンポーネント、デスクトップ アプリやドライバーをビルドして CRT を再頒布するための戦略について説明します。

## <a name="span-idwhy_did_microsoft_make_this_change_spanspan-idwhy_did_microsoft_make_this_change_spanspan-idwhy_did_microsoft_make_this_change_spanwhy-did-microsoft-make-this-change"></a><span id="Why_did_Microsoft_make_this_change_"></span><span id="why_did_microsoft_make_this_change_"></span><span id="WHY_DID_MICROSOFT_MAKE_THIS_CHANGE_"></span>Microsoft がこの変更を行った理由


C ランタイムのバージョンは、2 つになりました。 1 つは内部 Windows コンポーネントです。もう 1 つはアプリケーション開発者とドライバー開発者が使うバージョンで、Visual Studio に付属します。 この変更を行った主な理由は、一貫性を保ち、顧客への CRT の提供をサポートするためです。

以前、アプリケーションは、適切なバージョンの CRT DLL がインストールされていないコンピューターの CRT バージョンにリンクされていることがありました。 共通公開バージョンの CRT を使うことは、この問題を解消するのに役立ちます。

加えて、CRT の提供は複雑な場合があります。 Visual C チームは、Visual Studio に付属する CRT の更新プログラムを定期的に提供する予定です。 推奨される再頒布戦略を使うことで、これらの変更の中からアプリケーションに合うものを簡単に選ぶことができます。 さらに、Windows システム バージョンの CRT に加えられた変更によってアプリケーションが停止することを心配する必要はありません。

msvcrt.dll は、Windows によって所有およびビルドされるシステム コンポーネントになりました。 これは、システム レベルのコンポーネントだけが使います。 msvcr110.dll ファイル (Visual Studio 2012) や msvcr120.dll ファイル (Microsoft Visual Studio 2013) は、新しい公開バージョンの CRT であり、デスクトップ アプリケーションとユーザー モード ドライバーの開発者が使います。

## <a name="span-idbuilding_your_code_with_the_c_runtimespanspan-idbuilding_your_code_with_the_c_runtimespanspan-idbuilding_your_code_with_the_c_runtimespanbuilding-your-code-with-the-c-runtime"></a><span id="Building_your_code_with_the_C_runtime"></span><span id="building_your_code_with_the_c_runtime"></span><span id="BUILDING_YOUR_CODE_WITH_THE_C_RUNTIME"></span>C ランタイムを使ったコードのビルド


Visual C++ は、最新バージョンの CRT を開発システム上の System32 ディレクトリにインストールします。 これは、開発者の利便性のためにインストールされます。 インストールされていないと、Visual C++ を使ってビルドされ、共有 CRT とリンクされたすべてのプロジェクトをデバッグして実行するために、DLL のコピーがビルド ディレクトリに必要になります。 msvcr120.dll は、Windows 8.1 および Windows 8 と以前のバージョンの Windows (Windows Vista 以降) を対象とするドライバーに使うことができます。

## <a name="span-idredistributing_the_c_runtime_spanspan-idredistributing_the_c_runtime_spanspan-idredistributing_the_c_runtime_spanredistributing-the-c-runtime"></a><span id="Redistributing_the_C_Runtime_"></span><span id="redistributing_the_c_runtime_"></span><span id="REDISTRIBUTING_THE_C_RUNTIME_"></span>C ランタイムの再頒布


Microsoft Visual Studio でユーザー モード ドライバーや従来型のデスクトップ アプリケーションをビルドするときに、アプリケーションによって C ランタイム ライブラリ (CRT) が使われる場合、適切な CRT ダイナミック リンク ライブラリを配布する必要があります。

推奨される CRT 再頒布戦略は、ビルドするアプリケーションやドライバーの種類によって異なります。 Windows 8 と Windows 8.1 には、Visual C++ の再頒布可能パッケージ (VCRedist\_x86.exe、VCRedist\_x64.exe、VCRedist\_arm.exe) が用意されており、Visual Studio に付属しています。 開発者は、再頒布可能パッケージを他のバイナリと結び付けることができます。 再頒布可能パッケージを使う場合、顧客のコンピューター側で自動的に C/C++ ランタイムを提供できます。 分離する場合は、静的にリンクするか、他のバイナリと同時に特定の Visual C/C++ DLL を "*アプリケーション ローカル フォルダー*" にコピーすることができます。 *アプリケーション ローカル フォルダー*とは、アプリケーションの実行可能ファイルが存在するフォルダーのことです。 DLL は、アプリケーション ローカル フォルダーに展開する必要があります。

Visual C/C++ の再頒布可能パッケージ (VCRedist\_\*.exe) は、アプリケーションとして提供されます。 インストールに再頒布可能パッケージが含まれている場合、初期セットアップ時に最新バージョンが System32 にインストールされ、通常のパッケージのように Microsoft Update サービスを使って更新が有効になります。 Visual C/C++ の再頒布可能パッケージのすべてのコンポーネントは、単一のユニットとして更新されます。

再頒布可能パッケージを使わずに個々の CRT コンポーネントを System32 にコピーした場合、これらのコンポーネントは自動的に提供されないため、誤って上書きしてしまう可能性があります。

ドライバーが CRT コンポーネントを System32 にコピーして、別のプログラムが再頒布パッケージを実行した場合、問題が発生する可能性があります (ドライバーによってインストールされたバージョンが上書きされます)。 逆の場合も問題となります。 プログラムが再頒布可能パッケージを実行して、ドライバーがそれより前のバージョンの CRT コンポーネントを System32 にコピーした場合、アプリケーションが停止する可能性があります。 INF のインストール プロセスでは、インストールするライブラリのバージョン番号と、System32 に既に存在するライブラリのバージョン番号が比較されるだけのため、異なる場合は上書きされます。

## <a name="span-idrecommended_strategiesspanspan-idrecommended_strategiesspanspan-idrecommended_strategiesspanrecommended-strategies"></a><span id="Recommended_Strategies"></span><span id="recommended_strategies"></span><span id="RECOMMENDED_STRATEGIES"></span>推奨される戦略


ドライバーやアプリケーションと共に C/C++ ランタイム コンポーネントを再頒布する場合は、次の戦略を使います。

Program Files にインストールされるアプリケーションの場合

-   System32 の下に CRT を展開する Visual C++ の再頒布可能パッケージ (VCRedist\_x86.exe、VCRedist\_x64.exe、VCRedist\_arm.exe) を使います。 この場合、再頒布可能パッケージを自動的に更新できます。
-   あるいは、DLL をアプリケーション ローカル ディレクトリにインストールするか (アプリケーションがインストールされているディレクトリに直接コピーされます)、CRT に静的にリンクします。 この場合、CRT を手動で提供する必要があります。

プリンター ドライバーの場合

-   これらのドライバーの場合、必要な CRT ファイルが INF に含まれているため、CRT ファイルがドライバーのペイロードの一部としてドライバー ストアにコピーされます。
-   V4 プリンター ドライバーは、セットアップに共同インストーラーを使うことができないため、INF は C/C++ ランタイム ライブラリの関連バイナリをドライバー ストアにコピーする必要があります。 これを行うには、ドライバー パッケージの **\[COPY\_FILES\]** セクションにある該当ファイルを参照する必要があります。
-   V3 プリンター ドライバーは、セットアップに共同インストーラーを使いません。ポイント アンド プリント接続中には実行されないためです。 これらのドライバーは、ドライバー パッケージの **\[COPY\_FILES\]** セクションにある該当ファイルを参照する必要があります。

CRT バイナリを INF の **\[COPY\_FILES\]** セクションに含める方法の例を次に示します。
```Text
[COPY_FILES]
;CRT
Msvcr120.dll
; other files

* [SourceDisksFiles]
Msvcr120.dll = 2 
; other files

* [SourceDisksNames.amd64]
1 = %Location%,,,
2 = %Location%,,,"amd64"
```

UMDF ドライバーの場合

-   ドライバーを CRT に静的にリンクして、ランタイムをライブラリに含めます。 この場合、CRT を再頒布する必要はありません。

## <a name="span-idlinking_your_code_with_the_c_runtime_librariesspanspan-idlinking_your_code_with_the_c_runtime_librariesspanspan-idlinking_your_code_with_the_c_runtime_librariesspanlinking-your-code-with-the-c-runtime-libraries"></a><span id="Linking_your_code_with_the_C_Runtime_libraries"></span><span id="linking_your_code_with_the_c_runtime_libraries"></span><span id="LINKING_YOUR_CODE_WITH_THE_C_RUNTIME_LIBRARIES"></span>C ランタイム ライブラリとのコードのリンク


次のライブラリには、C ランタイム ライブラリ関数が含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Msvcr120.dll"></span><span id="msvcr120.dll"></span><span id="MSVCR120.DLL"></span>Msvcr120.dll</p></td>
<td align="left"><p>C ランタイム。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Msvcp120.dll"></span><span id="msvcp120.dll"></span><span id="MSVCP120.DLL"></span>Msvcp120.dll</p></td>
<td align="left"><p>C++ ランタイム。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Msvcr120d.dll"></span><span id="msvcr120d.dll"></span><span id="MSVCR120D.DLL"></span>Msvcr120d.dll</p></td>
<td align="left"><p>C ランタイムのデバッグ バージョン。 再頒布できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Msvcp120d.dll_"></span><span id="msvcp120d.dll_"></span><span id="MSVCP120D.DLL_"></span>Msvcp120d.dll</p></td>
<td align="left"><p>C++ ランタイムのデバッグ バージョン。 再頒布できません。</p></td>
</tr>
</tbody>
</table>

 

アプリケーションと共に再頒布する必要がある DLL を特定するには、アプリケーションが依存している DLL の一覧を収集する必要があります。 一覧を収集する 1 つの方法として、Dependency Walker (depends.exe) を実行できます。

依存関係の一覧を持っている場合、「[Visual Studio 2013 Preview および Visual Studio 2013 SDK Preview 用再頒布可能コード](https://go.microsoft.com/fwlink/p/?linkid=320999)」で説明されているファイルの一覧と比較します。 詳しくは、[再頒布する DLL の特定に関するページ](https://go.microsoft.com/fwlink/p/?linkid=321001)と[展開方法の選択に関するページ](https://go.microsoft.com/fwlink/p/?linkid=321651)をご覧ください。

Visual Studio に含まれているすべてのファイルを再頒布することはできません。[Visual Studio 2013 Preview および Visual Studio 2013 SDK Preview 用再頒布可能コードに関するページ](https://go.microsoft.com/fwlink/p/?linkid=320999)に記載されているファイルのみ再頒布することができます。 アプリケーションのデバッグ バージョンと各種 Visual C++ ダイナミック リンク ライブラリは、再頒布できません。

## <a name="span-idsummary_-_what_you_need_to_dospanspan-idsummary_-_what_you_need_to_dospanspan-idsummary_-_what_you_need_to_dospansummary---what-you-need-to-do"></a><span id="Summary_-_What_you_need_to_do"></span><span id="summary_-_what_you_need_to_do"></span><span id="SUMMARY_-_WHAT_YOU_NEED_TO_DO"></span>まとめ: 必要な作業


可能であれば、インストール プロセスの一部として Visual C++ の再頒布可能パッケージ (VCRedist\_x86.exe、VCRedist\_x64.exe、VCRedist\_arm.exe) の VCRedist.msi を使います。

プリンター ドライバーの場合、デスクトップ アプリケーションのローカルで CRT をドライバー ストアに展開します。

UMDF ドライバーの場合、CRT をドライバー コードに静的にリンクします。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [再頒布する DLL の特定](https://go.microsoft.com/fwlink/p/?linkid=321001)
* [Visual Studio 2013 Preview および Visual Studio 2013 SDK Preview 用再頒布可能コード](https://go.microsoft.com/fwlink/p/?linkid=320999)
* [展開方法の選択](https://go.microsoft.com/fwlink/p/?linkid=321651)
 

 






