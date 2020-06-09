---
title: OCA ミニダンプ ファイルのデバッグ
description: オンライン クラッシュ分析 (OCA) は、Windows エラー報告 (WER) の情報に関する報告機能です。 会社で OCA クラッシュ ダンプを使用すると、顧客の問題を分析することができます。
ms.assetid: 56F4202D-6A5F-4177-BBFD-70DA717FF24A
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1603fcbba40ea6557eed1416bea56046644e86b3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534459"
---
# <a name="debugging-oca-minidump-files"></a>OCA ミニダンプ ファイルのデバッグ

オンラインクラッシュ分析 (OCA) は、 [Windows エラー報告 (WER)](https://docs.microsoft.com/windows/desktop/wer/windows-error-reporting)情報のレポート機能です。 会社で OCA クラッシュ ダンプを使用すると、顧客の問題を分析することができます。

## <a name="analyze-dump-files"></a>ダンプファイルの分析

ダンプ ファイルは、クラッシュ時のコンピューター (またはプロセス) の状態をとらえたスナップショットです。

このデータを分析するには、開発者はユーザーのミニダンプ ファイルを読み取ることができるデバッガーを使う必要があります。 デバッガーはまた、ダンプ ファイルの内容と照合するイメージとシンボルの両方にアクセスできる必要があります。 ほとんどの開発者は、ライブクラッシュのデバッグ時に一致するシンボルを使用する必要があることを認識しています。 ただし、ミニダンプをデバッグする場合は、一致するイメージもデバッガーで使用できる必要があります。

ミニダンプ ファイルには情報がほとんど格納されないため、照合するイメージを使用できる必要があります。ミニダンプ ファイルに格納されるのは、クラッシュ時の揮発性情報の一部だけです。 コンピューターがメモリに読み込んだ基本コード ストリームは格納されません。 代わりに、領域を節約するため、ミニダンプ ファイルには、クラッシュしたコンピューターに読み込まれたイメージの名前とタイム スタンプのみが格納されます。

クラッシュしたコンピューターで実行されていたコードを調べるには、クラッシュしたコンピューターが実行していたのと同じバイナリに対するアクセスがデバッガーに許可されている必要があります。 デバッガーは、ミニダンプ ファイルに格納されている名前とタイム スタンプを使用して、開発者がクラッシュをデバッグするときにバイナリを一意に照合して読み込みます。

イメージとシンボルがデバッガーに読み込まれると、クラッシュが発生した後に保存されたデータを含めてクラッシュ時のシステムの状態を分析することができます。 ただし、ミニダンプでは特定の障害の原因となった手順は再現されません。 根本的な原因を調べるには、ドライバーのソース コードを分析し、どのコード パスが障害の原因となったのかを特定する必要があります。 経験的には、障害の大半はダンプ ファイルとソース コードを分析することによって解明して対処することができます。

## <a name="use-symbols-to-match-executable-code-with-source-code"></a>シンボルを使用して実行可能コードをソースコードと照合する

照合するイメージとシンボルにアクセスするのに最適な方法は、Microsoft シンボル サーバーを使用することです。 シンボルは、デバッガーが実行可能コードをソース コードにマップできるようにするデータです。 プログラムをビルドすると、プログラムのシンボルは通常、シンボル ファイルに格納されます。 デバッガーは、プログラムを分析するときにプログラムのシンボルにアクセスする必要があります。

シンボル ファイルには、次のいずれかまたはすべてを含めることができます。

- すべての関数の名前とアドレス
- すべてのデータ型、構造体、クラスの定義
- グローバル変数の名前、データ型、アドレス
- ローカル変数の名前、データ型、アドレス、スコープ
- ソース コードで、各バイナリ命令に対応する行番号

Windows Driver Kit (WDK) に含まれているツールを使用すると、シンボル ファイル内のシンボルの数を減らすことができます。 ソース レベルの情報をすべて含むシンボル ファイルは、フル シンボル ファイルと呼ばれます。 情報が減らされたシンボル ファイルは、ストリップ シンボル ファイルと呼ばれます。 詳細については、「 [Binplace](https://docs.microsoft.com/windows-hardware/drivers/devtest/binplace)」を参照してください。

シンボル データは Windows エラー報告 (WER) のデータから有益なクラッシュ情報を取得するうえで重要であるため、署名用にドライバーを提出するときはシンボルを提出することをお勧めします。 提出されたシンボルはサーバーに格納され、関連付けられた WER プロセスとシンボル データが同期されます。 このストレージ プロセスにより、ミニダンプ ファイルで報告されたクラッシュを容易に分類し、最終的に Microsoft からより適切なデータを受け取ることができます。

Microsoft はインターネット上でシンボル サーバーを提供しているため、ユーザーはこれを使用してミニダンプ ファイル内に示されている Windows モジュールを分析できます。 サーバーには、Windows とその他いくつかの製品用のストリップ シンボル ファイルが含まれています。 Microsoft は、Windows XP と Windows Server 2003 用のバイナリを追加しています。 インターネット シンボル サーバーと Debugging Tools for Windows を使用して、ミニダンプ ファイルを分析できます。

## <a name="integrate-wer-into-applications"></a>WER をアプリケーションに統合する

WER をアプリケーションに統合する場合の詳細については、「[Using WER](https://docs.microsoft.com/windows/desktop/wer/using-wer)」(WER の使用) を参照してください。

## <a name="related-topics"></a>関連トピック

[高度なドライバーのデバッグ \[ 336 KB の \] \[ PPT\]](https://download.microsoft.com/download/f/0/5/f05a42ce-575b-4c60-82d6-208d3754b2d6/adv-drv_debug.ppt)

[WDK および WinDbg ダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

[ドライバーデバッグの基礎 \[ : WinHEC 2007; 633 KB の \] \[ PPT\]](https://download.microsoft.com/download/a/f/d/afdfd50d-6eb9-425e-84e1-b4085a80e34e/dvr-t410_wh07.pptx)

[クラッシュが発生した場合に Windows によって作成された小さいメモリダンプファイルを読み取る方法](https://support.microsoft.com/help/315263/how-to-read-the-small-memory-dump-file-that-is-created-by-windows-if-a)

[リソース定義ステートメント](https://docs.microsoft.com/windows/desktop/menurc/resource-definition-statements)

[Windows エラー報告](https://docs.microsoft.com/windows/desktop/wer/windows-error-reporting)

[VERSIONINFO リソース](https://docs.microsoft.com/windows/desktop/menurc/versioninfo-resource)
