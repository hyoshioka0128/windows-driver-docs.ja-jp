---
title: 開発とテスト ツール
description: 開発とテスト ツール
ms.assetid: 6cc81509-27e1-4d5b-996c-6a7bbfd0ddcf
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、ツール
- Fltmc.exe WDK ファイル システム ミニフィルター
- fltkd デバッガー拡張機能 WDK ファイル システム ミニフィルター
- Verifier WDK ファイル システム ミニフィルターをフィルター処理します。
- 検証ユーティリティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73737850d38bc3ddfb5e0f6fb38581e40d43fe10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359317"
---
# <a name="development-and-testing-tools"></a>開発とテスト ツール


IFS Kit for Windows Server 2003 SP1 とで、Windows Driver Kit (WDK) Windows Vista 以降、このセクションで説明されているフィルター マネージャー ツールが提供されます。

ミニフィルター ドライバー開発者向けに汎用のカーネル モード開発を使用することをお勧めもと、ドライバー固有のルールと PREfast などのツールをテストします。

### <a name="span-idfltmcexecontrolprogramspanspan-idfltmcexecontrolprogramspanspan-idfltmcexecontrolprogramspanfltmcexe-control-program"></a><span id="Fltmc.exe_Control_Program"></span><span id="fltmc.exe_control_program"></span><span id="FLTMC.EXE_CONTROL_PROGRAM"></span>Fltmc.exe コントロール プログラム

Fltmc.exe コントロール プログラムは、一般的なミニフィルター ドライバーの管理操作のコマンド ライン ユーティリティです。 開発者は、読み込みとミニフィルター ドライバーをアンロード、ミニフィルター ドライバーをボリュームにアタッチまたはボリュームからのデタッチに Fltmc.exe を使用して、ミニフィルター ドライバー、インスタンス、およびボリュームを列挙できます。

### <a name="span-idfltkddebuggerextensionspanspan-idfltkddebuggerextensionspanspan-idfltkddebuggerextensionspanfltkd-debugger-extension"></a><span id="_fltkd_Debugger_Extension"></span><span id="_fltkd_debugger_extension"></span><span id="_FLTKD_DEBUGGER_EXTENSION"></span>! fltkd デバッガー拡張機能

! で fltkd デバッガーの拡張機能の提供、 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)ツール。 よく使用されるコマンドを以下に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>!cbd</strong></p></td>
<td align="left"><p>フィルター マネージャーと同等の! irp</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! フィルター</strong></p></td>
<td align="left"><p>指定されたフィルターに関する詳細な情報を一覧表示</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! フィルター</strong></p></td>
<td align="left"><p>すべてのアタッチされたミニフィルター ドライバーを一覧します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! フレーム</strong></p></td>
<td align="left"><p>リストのすべてのマネージャーのフレームのフィルターし、ミニフィルター ドライバーの接続</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! インスタンス</strong></p></td>
<td align="left"><p>指定したインスタンスに関する詳細な情報を一覧表示</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>! ボリューム</strong></p></td>
<td align="left"><p>指定したボリュームに関する詳細な情報を一覧表示</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>! ボリューム</strong></p></td>
<td align="left"><p>すべてのボリュームを一覧表示し、ミニフィルター ドライバーのインスタンスに接続されています。</p></td>
</tr>
</tbody>
</table>

 

デバッグの詳細については、一般的なエラーをキャッチする多数のアサート ステートメントを含む、Fltmgr.sys のデバッグ バージョンとミニフィルター ドライバーをテストします。

### <a name="span-idfilterverifierspanspan-idfilterverifierspanspan-idfilterverifierspanfilter-verifier"></a><span id="Filter_Verifier"></span><span id="filter_verifier"></span><span id="FILTER_VERIFIER"></span>フィルターの検証方法

フィルターの検証ツールは、 [I/O の検証](https://msdn.microsoft.com/library/windows/hardware/ff548045)オプション[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)ミニフィルター ドライバーの使用状況のフィルター マネージャーの機能を検証します。 フィルター検証ツールは、フィルター マネージャーと共にインストールされます。 開発者は、Driver Verifier でミニフィルター ドライバーを開発常にする必要があり、フィルター検証機能を有効にします。

フィルター検証ツールを使用するには、ミニフィルター ドライバーの名前を指定し、Driver Verifier (Verifier.exe) で I/O の検証オプションを有効にします。 フィルター マネージャーとミニフィルター ドライバーの登録時に検証を開始します。

フィルター検証ツールは、ミニフィルター ドライバーでは次の使用法を検証します。

-   パラメーターと呼び出し元のコンテキストの正しい使用

-   Preoperation と postoperation コールバック ルーチンから適切な戻り値

-   コールバック データのパラメーターに、首尾一貫した変更

フィルター検証ツールは、次のフィルター マネージャー オブジェクトを追跡します。

-   コンテキスト

-   コールバックのデータ構造体

-   キューに置かれた作業項目

-   NameInformation 構造体

-   ファイル オブジェクト

-   フィルター オブジェクト

-   インスタンス オブジェクト

-   Volume オブジェクト

 

 




