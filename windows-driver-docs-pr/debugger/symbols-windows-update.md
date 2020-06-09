---
title: Windows Update のオフライン シンボル
description: このトピックでは、Windows Update に対してオフラインシンボルを操作する方法について説明します。
keywords:
- シンボル
- セットアップ、シンボル
- シンボル、セットアップ
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ee63ce37645064ef43c49317f71edf5b536f0118
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534297"
---
# <a name="offline-symbols-for-windows-update"></a>Windows Update のオフライン シンボル

このトピックでは、Windows Update のオフラインシンボルを操作する方法について説明します。 ここでは、Microsoft シンボルサーバーにアクセスできないコンピューター上の Windows Update ログをデコードするために使用できる手順について説明します。 

これを頻繁に行う必要がある場合は、シンボルプロキシサーバーの設定がネットワーク構成に対して有効かどうかを確認する必要があります。 詳細については、「 [Symproxy](symproxy.md)」を参照してください。

以下のすべてのオプションでは、Microsoft のシンボルサーバーに接続できる1台のコンピューターが必要です。また、ログが保存されているコンピューターとの間でファイルをコピーすることもできます。 シンボルサーバーへのアクセス権がないコンピューターは、*オフライン*コンピューターと呼ばれ、*オンライン*コンピューターとしてアクセスできるコンピューターになります。

 WU シンボルキャッシュが月単位でビルドされ、複数の更新プログラムリリースの WU シンボルが含まれるように、OS ビルドバージョンごとに1つのオンラインマシンを使用することをお勧めします。 
 
オフラインコンピューターと同じ正確なパッチレベルを持つオンラインマシンにアクセスできる場合は、次の2つの方法があります。

- [オプション 1: ETL イベントログをオンラインコンピューターにコピーする](#ETL)

- [オプション 2: オフラインコンピューターにシンボルをコピーする](#OFFLINE)

`winver`両方のコンピューターでまたはを実行して、オンラインおよびオフラインの pc が同じバージョンレベルであることを確認し `ver` ます。

```console
C:\>ver

Microsoft Windows [Version 10.0.17134.167]
```

同じバージョンのオンラインマシンにアクセスできない場合は、追加の手順を実行して SymChk マニフェストファイルを作成する必要があります。詳細については、このトピックで後述する「[オプション 3: SymChk マニフェストファイルを作成](#SYMCHK)する」を参照してください。


## <a name="span-idetlspanspan-idetlspanoption-1-copy-the-etl-event-log-to-the-online-machine"></a><span id="etl"></span><span id="ETL"></span>オプション 1: ETL イベントログをオンラインコンピューターにコピーする

1. すべてのある windowsupdate.log ETL ファイルをから `C:\Windows\logs\WindowsUpdate\` オンラインコンピューターにコピーします。

2. オンラインコンピューターで PowerShell プロンプトを開き、次の[WindowsUpdateLog](https://docs.microsoft.com/powershell/module/windowsupdate/get-windowsupdatelog?view=win10-ps) powershell コマンドを実行します。 

   ```powershell
   Get-WindowsUpdateLog -ETLPath <path to ETLs>
   ```
   これにより、ログ分析に必要なシンボルがダウンロードされます。


## <a name="span-idofflinespanspan-idofflinespanoption-2-copy-the-symbols-to-the-offline-machine"></a><span id="offline"></span><span id="OFFLINE"></span>オプション 2: オフラインコンピューターにシンボルをコピーする

1. オンラインコンピューターで、PowerShell プロンプトを開き、"WindowsUpdateLog" を実行します。 これにより、ログ分析に必要なシンボルがキャッシュされます。

2. %Temp%\WindowsUpdateLog\SymCache のすべてのファイルをオンラインコンピューターからオフラインコンピューターのにコピーし `%temp%\WindowsUpdateLog\SymCache` ます。

3. オフラインコンピューターで、PowerShell プロンプトを開き、"WindowsUpdateLog" を実行してログを分析します。


## <a name="span-idsymchkspanspan-idsymchkspanoption-3-create-a-symchk-manifest-file"></a><span id="symchk"></span><span id="SYMCHK"></span>オプション 3: SymChk マニフェストファイルを作成する

1.  オフラインコンピューターで、「 [SymChk でマニフェストファイルを使用](using-a-manifest-file-with-symchk.md)する」の手順に従って、system32 ディレクトリにこれらのファイルのマニフェストを作成します。

    ```console
    storewuauth.dll
    wuapi.dll
    wuauclt.exe
    wuaueng.dll
    wuautoappupdate.dll
    wuuhext.dll
    wuuhmobile.dll
    ```

2.  マニフェストをオンラインコンピューターにコピーします。

3.  マニフェストファイルで、SymChk を使用して、オンライン PC にシンボルをローカルでダウンロードします。 

4.  SymChk に渡されたフォルダーとシンボルを、オフライン PC の%temp%\WindowsUpdateLog\SymCache にコピーします。
 
5. オフラインコンピューターで、PowerShell プロンプトを開き、"WindowsUpdateLog" を実行してログを分析します。

 



## <a name="see-also"></a>参照

[シンボルサーバーを使用](using-a-symbol-server.md)します。

[シンボルパス](symbol-path.md) 

[デバッグ用シンボルへのアクセス](accessing-symbols-for-debugging.md)

[デバッグ中のシンボルに関する問題](symbol-problems-while-debugging.md)
 





