---
title: Windows Update のオフラインのシンボル
description: このトピックでは、操作する方法で行のシンボルを Windows Update のについて説明します。
keywords:
- シンボル
- シンボルの設定
- シンボル、セットアップ
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8e861b78408f3a1fb5ef19c9e46d58fe09865c29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550717"
---
# <a name="offline-symbols-for-windows-update"></a>Windows Update のオフラインのシンボル

このトピックでは、Windows 更新プログラムをオフラインのシンボルを使用する方法について説明します。 これには、Microsoft シンボル サーバーへのアクセス権がないコンピューターで Windows Update ログのデコードに使用できる手順について説明します。 

多くの場合、これを実行する必要がある場合は、シンボル サーバーのプロキシ設定が、ネットワークの構成可能な状態が表示されます。 詳細については、次を参照してください。 [SymProxy](https://docs.microsoft.com/windows-hardware/drivers/debugger/symproxy)します。

以下のオプションでは、Microsoft のシンボル サーバーに接続し、ログがあるコンピューターからファイルをコピーすることを 1 つのマシンがある必要があります。 シンボル サーバーにアクセスできないコンピューターとして参照される、*オフライン*マシン、およびマシンとしてへのアクセスが、*オンライン*マシン。

 WU シンボルのキャッシュは、月ごとを作成し、複数の更新プログラムのリリースから WU シンボルが含まれているために、OS ビルド バージョンごとに 1 つのオンライン マシンを使用することをお勧めします。 
 
オフラインのマシンと同じ正確なパッチ レベルでのオンラインのマシンへのアクセスがある場合は、2 つのオプションを設定します。

•[オプション 1。ETL のイベント ログをオンラインのマシンにコピーします。](#ETL)

•[オプション 2。オフラインのコンピューターにシンボルをコピーします。](#OFFLINE)

オンラインおよびオフラインの Pc を実行して、同じバージョン レベル確認`winver`または`ver`両方のコンピューターにします。

```console
C:\>ver

Microsoft Windows [Version 10.0.17134.167]
```

このトピックの後半で説明、SymChk マニフェスト ファイルを作成する特別な手順を経由する必要があります、同じバージョンのオンラインのマシンへのアクセスを持っていない場合[オプション 3。SymChk マニフェスト ファイルを作成](#SYMCHK)です。


## <a name="span-idetlspanspan-idetlspanoption-1-copy-the-etl-event-log-to-the-online-machine"></a><span id="etl"></span><span id="ETL"></span>オプション 1:ETL のイベント ログをオンラインのマシンにコピーします。

1. Windows Update の ETL ファイルからすべてコピー`C:\Windows\logs\WindowsUpdate\`オンラインのコンピューターにします。

2. オンラインのマシンでは、PowerShell プロンプトを開き、次の実行[Get WindowsUpdateLog](https://docs.microsoft.com/powershell/module/windowsupdate/get-windowsupdatelog?view=win10-ps) PowerShell コマンド。 

   ```powershell
   Get-WindowsUpdateLog -ETLPath <path to ETLs>
   ```
   これにより、ログ分析に必要なシンボルがダウンロードされます。


## <a name="span-idofflinespanspan-idofflinespanoption-2-copy-the-symbols-to-the-offline-machine"></a><span id="offline"></span><span id="OFFLINE"></span>オプション 2:オフラインのコンピューターにシンボルをコピーします。

1. オンラインのマシンでは、PowerShell プロンプトを開き、"Get WindowsUpdateLog"を実行します。 これにより、ログ分析に必要なシンボルをキャッシュします。

2. オンラインのマシンから %temp%\WindowsUpdateLog\SymCache ですべてのファイルをコピー`%temp%\WindowsUpdateLog\SymCache`オフラインのコンピューター。

3. オフラインのコンピューターで PowerShell プロンプトを開き、"Get WindowsUpdateLog"ログの分析を実行します。


## <a name="span-idsymchkspanspan-idsymchkspanoption-3-create-a-symchk-manifest-file"></a><span id="symchk"></span><span id="SYMCHK"></span>オプション 3:SymChk マニフェスト ファイルを作成します。

1.  オフラインのコンピューター上にある手順に従います[SymChk でマニフェスト ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-a-manifest-file-with-symchk)system32 ディレクトリにこれらのファイルのマニフェストを作成します。

    ```console
    storewuauth.dll
    wuapi.dll
    wuauclt.exe
    wuaueng.dll
    wuautoappupdate.dll
    wuuhext.dll
    wuuhmobile.dll
    ```

2.  オンラインのコンピューターに、マニフェストをコピーします。

3.  マニフェストのファイルを使用して、オンラインの PC にローカル シンボルをダウンロードするのに SymChk を使用します。 

4.  フォルダーと %temp%\WindowsUpdateLog\SymCache オフライン PC で SymChk に渡すシンボルをコピーします。
 
5. オフラインのコンピューターで PowerShell プロンプトを開き、"Get WindowsUpdateLog"ログの分析を実行します。

 



## <a name="see-also"></a>参照

[シンボル サーバーを使用して](using-a-symbol-server.md)します。

[シンボル パス](symbol-path.md) 

[デバッグのシンボルへのアクセス](accessing-symbols-for-debugging.md)

[デバッグ中にシンボルに関する問題](symbol-problems-while-debugging.md)
 





