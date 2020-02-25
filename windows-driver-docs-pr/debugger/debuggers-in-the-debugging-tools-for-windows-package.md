---
title: デバッグ環境
description: Windows Driver Kit (WDK) 8.0 以降では、ドライバー開発環境と Windows デバッガーが Microsoft Visual Studio に統合されています。
ms.assetid: 13F9D82A-4C04-425A-A063-B349DB5C8E08
keywords:
- WinDbg
- KD
- CDB
- NTSD
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5bbaf80898d2007c2b898fa8a4c5db0a2da7f80b
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528964"
---
# <a name="debugging-environments"></a>デバッグ環境

使用できるデバッグ環境は6つあります。

- WinDbg プレビュー
- Windows デバッガー (WinDbg)
- カーネルデバッガー (KD)
- NTKD
- コンソールデバッガー (CDB)
- NT シンボリックデバッガー (NTSD)

以下のセクションでは、デバッグ環境について説明します。

### <a name="span-idwindbgpreviewspanspan-idwindbgpreviewspanspan-idwindbgpreviewspanwindbg-preview"></a><span id="WinDbgPreview"></span><span id="windbgpreview"></span><span id="WINDBGPREVIEW"></span>WinDbg プレビュー

WinDbg Preview は、最新バージョンの WinDbg で、拡張可能なデバッガーデータモデルの front と center を使用して構築された本格的なスクリプトエクスペリエンスである最新のビジュアルを備えています。 WinDbg プレビューは、現行の WinDbg と同じ基本エンジンを使用しているため、使い慣れたすべてのコマンド、拡張機能、ワークフローがこれまでどおり動作します。

詳細については、「 [WinDbg Preview を使用したデバッグ](debugging-using-windbg-preview.md)」を参照してください。

### <a name="span-idwindbgspanspan-idwindbgspanspan-idwindbgspanwindbg"></a><span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>WinDbg

Microsoft Windows デバッガー (WinDbg) は、ユーザーモードとカーネルモードの両方のデバッグ機能を備えた Windows ベースのデバッガーです。 WinDbg は、Windows カーネル、カーネルモードドライバー、およびシステムサービスに加え、ユーザーモードのアプリケーションとドライバーのデバッグを提供します。

WinDbg では、ソースレベルのデバッグに Visual Studio デバッグシンボル形式が使用されます。 このメソッドは、PDB シンボルファイルがあるモジュールから任意のシンボルや変数にアクセスでき、COFF シンボルファイル (Windows の dbg ファイルなど) でコンパイルされたモジュールによって公開されている任意のパブリック関数の名前にアクセスできます。

WinDbg では、ソースコードの表示、ブレークポイントの設定C++ 、変数 (オブジェクトを含む)、スタックトレース、メモリの表示を行うことができます。 デバッガーコマンドウィンドウを使用すると、ユーザーはさまざまなコマンドを発行できます。

カーネルモードのデバッグでは、通常、WinDbg に2台のコンピューター (ホストコンピューターとターゲットコンピューター) が必要です。 WinDbg では、ユーザーモードとカーネルモードの両方のターゲットに対して、さまざまなリモートデバッグオプションもサポートされています。

WinDbg は、CDB/NTSD および KD/NTKD に対応するグラフィカルインターフェイスです。

### <a name="span-idkdspanspan-idkdspankd"></a><span id="KD"></span><span id="kd"></span>KD

Microsoft カーネルデバッガー (KD) は、すべての NT ベースのオペレーティングシステムにおけるカーネルモードアクティビティの詳細な分析を可能にする、文字ベースのコンソールプログラムです。 KD を使用すると、カーネルモードのコンポーネントとドライバーをデバッグしたり、オペレーティングシステム自体の動作を監視したりできます。 KD では、マルチプロセッサデバッグもサポートされています。

通常、KD は、デバッグ中のコンピューターでは実行されません。 カーネルモードのデバッグには、2台のコンピューター (*ホストコンピューター*と*ターゲットコンピューター*) が必要です。

### <a name="span-idntkdspanspan-idntkdspanntkd"></a><span id="NTKD"></span><span id="ntkd"></span>NTKD

KD デバッガーには、NTKD という名前のバリエーションがあります。 これは、すべての方法で KD と同じです。ただし、開始時に新しいテキストウィンドウが生成される点が異なりますが、KD は呼び出されたコマンドプロンプトウィンドウを継承します。

### <a name="span-idcdbspanspan-idcdbspancdb"></a><span id="CDB"></span><span id="cdb"></span>CDB

Microsoft コンソールデバッガー (CDB) は、Windows ユーザーモードのメモリと構成体の低レベルの分析を可能にする、文字ベースのコンソールプログラムです。 名前*コンソールデバッガー*は、CDB がコンソールアプリケーションとして分類されるという事実を示すために使用されます。ターゲットアプリケーションがコンソールアプリケーションである必要はありません。 実際、CDB は、コンソールアプリケーションとグラフィカル Windows プログラムの両方を完全にデバッグできます。

CDB は、現在実行中または最近クラッシュしたプログラム (ライブ分析) をデバッグする場合に非常に強力ですが、セットアップは簡単です。 これは、動作中のアプリケーションの動作を調査するために使用できます。 アプリケーションのエラーが発生した場合は、CDB を使用してスタックトレースを取得したり、問題のあるパラメーターを調べたりすることができます。 これは文字ベースであるため、(リモートアクセスサーバーを使用して) ネットワーク全体で適切に動作します。

CDB では、プログラムコードの表示と実行、ブレークポイントの設定、メモリ内の値の確認と変更を行うことができます。 CDB は、バイナリコードを逆アセンブルし、アセンブリ命令を表示することで、バイナリコードを分析できます。 また、ソースコードを直接分析することもできます。

CDB はアドレスまたはグローバルシンボルを使用してメモリ位置にアクセスできるので、アドレスではなく名前でデータと命令を参照できます。これにより、コードの特定のセクションを簡単に見つけてデバッグすることができます。 CDB では、複数のスレッドとプロセスのデバッグがサポートされています。 拡張可能であり、ページングされたメモリと非ページメモリの両方の読み取りと書き込みが可能です。

ターゲットアプリケーション自体がコンソールアプリケーションである場合、ターゲットはコンソールウィンドウを CDB と共有します。 ターゲットコンソールアプリケーション用に別のコンソールウィンドウを生成するには、 *-2*コマンドラインオプションを使用します。

### <a name="span-idntsdspanspan-idntsdspanntsd"></a><span id="NTSD"></span><span id="ntsd"></span>NTSD

Microsoft NT シンボリックデバッガー (NTSD) という名前の CDB デバッガーのバリエーションがあります。 これは CDB と同じですが、開始時に新しいテキストウィンドウが生成されますが、CDB は呼び出されたコマンドプロンプトウィンドウを継承する点が異なります。

**Start**コマンドを使用して新しいコンソールウィンドウを生成することもできるため、次の2つの構造で同じ結果が得られます。

```console
start cdb parameters
ntsd parameters
```

NTSD (または CDB) からの入出力を、カーネルデバッガー (Visual Studio、WinDbg、または KD) から制御できるようにリダイレクトすることができます。 この手法を NTSD と共に使用すると、コンソールウィンドウはまったく表示されません。 このため、カーネルデバッガーからの NTSD の制御は特に便利です。これは、ターゲットアプリケーションを含むコンピューターにほとんど負担をかけない非常に軽量なデバッガーが生成されるためです。 この組み合わせを使用して、システムプロセスのデバッグ、シャットダウン、および起動の後の段階を行うことができます。 詳細については[、「カーネルデバッガーからのユーザーモードデバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[Windows のデバッグ](index.md)

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)
