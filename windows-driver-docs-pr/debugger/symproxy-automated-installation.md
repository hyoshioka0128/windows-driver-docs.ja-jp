---
title: SymProxy 自動インストール
description: 次のスクリプト Install.cmd と共に次の手順は、SymProxy の既定の IIS インストールへのインストールを自動化できます。
ms.assetid: 9E5433D8-D024-4E2B-AEAA-2271C133FD0E
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a269a3c44078c556b872d87ac18875102d2e8060
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549152"
---
# <a name="symproxy-automated-installation"></a>SymProxy 自動インストール


次のスクリプト Install.cmd と共に次の手順は、SymProxy の既定の IIS インストールへのインストールを自動化できます。 環境内の特定のニーズには、この手順を適用する必要があります。

1. D: を作成するには\\SymStore\\シンボル フォルダー。

   - すべてのユーザーに読み取り

   - 読み取り\\SymProxy アプリ プールのユーザー アカウントへの書き込み (ドメイン\\ユーザー)

2. 共有 d:\\SymStore\\シンボルとしてシンボル。

   - すべてのユーザーに読み取りを許可 (または詳細を指定)

3. (省略可能)D: index2.txt と呼ばれる空のファイルを作成する\\SymStore\\シンボル。
4. (省略可能)%Windir% と呼ばれる空のファイルを作成する\\system32\\inetsrv\\symsrv.yes します。 これは、Microsoft パブリック シンボル ストアの使用許諾契約書を受け入れます。
5. Install.cmd のパラメーターを特定し、それを実行します。
6. 作成したサーバー名を使用してクライアントのシンボル パスを構成します。
   ```dbgcmd
   SRV*\\MachineName\Symbols*https://MachineName/Symbols
   ```

Install.cmd スクリプトには、3 つのパラメーターが必要です。

-   仮想ディレクトリのパス (例: d:\\SymStore\\シンボル)
-   (アプリケーション プール) のユーザー名
-   (アプリケーション プール) のパスワード

MIME 型の継承をクリアするには、XML ファイルが関連付けられている AppCmd.exe コマンドをドライブに必要です。 この結果を実現するためには、Install.cmd スクリプトと同じフォルダーに、次に示す staticContentClear.xml ファイルを配置します。

Install.Cmd パラメーターの使用例:

```console
Install.cmd D:\SymStore\Symbols CONTOSO\SymProxyService Pa$$word
```

## <a name="span-idinstallcmdspanspan-idinstallcmdspaninstallcmd"></a><span id="install.cmd"></span><span id="INSTALL.CMD"></span>Install.cmd


```bat
@echo off

SET VirDirectory=%1
SET UserName=%2
SET Password=%3

::
::  SymProxy dll installation. 
::

copy symproxy.dll %windir%\system32\inetsrv
copy symproxy.man %windir%\system32\inetsrv
copy symsrv.dll %windir%\system32\inetsrv

lodctr.exe /m:%windir%\system32\inetsrv\symproxy.man
wevtutil.exe install-manifest %windir%\System32\inetsrv\symproxy.man
regedit.exe /s symproxy.reg

::
::  Web server Configuraiton
::

IF not exist %VirDirectory% mkdir %VirDirectory%

rem Make the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe add site -site.name:"Default Web Site" -bindings:"http/*:80:" -physicalPath:C:\inetpub\wwwroot

rem Enabled Directory Browsing on the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe set config "Default Web Site" -section:system.webServer/directoryBrowse /enabled:"True"

rem Make the 'SymProxy App Pool'
%windir%\system32\inetsrv\appcmd.exe add apppool -apppool.name:SymProxyAppPool -managedRuntimeVersion:
%windir%\system32\inetsrv\appcmd.exe set apppool -apppool.name:SymProxyAppPool -processModel.identityType:SpecificUser -processModel.userName:%UserName% -processModel.password:%Password% 

rem Make the 'Symbols' Virtual Directory and assign the 'SymProxy App Pool'
%windir%\system32\inetsrv\appcmd.exe add app -site.name:"Default Web Site" -path:/Symbols -physicalpath:%VirDirectory%
%windir%\system32\inetsrv\appcmd.exe set app -app.name:"Default Web Site/Symbols" -applicationPool:SymProxyAppPool

rem Disable 'web.config' for folders under virtual directories in the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe set config -section:system.applicationHost/sites "/[name='Default Web Site'].virtualDirectoryDefaults.allowSubDirConfig:false

rem Add the 'SymProxy ISAPI Filter'
%windir%\system32\inetsrv\appcmd.exe set config -section:system.webServer/isapiFilters /+"[name='SymProxy',path='%windir%\system32\inetsrv\SymProxy.dll',enabled='True']

rem Clear the MIME Types on the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe set config -in "Default Web Site" < staticContentClear.xml

rem Add * to the MIME Types of the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe set config "Default Web Site" -section:staticContent /+"[fileExtension='.*',mimeType='application/octet-stream']"
```

## <a name="span-idstaticcontentclearxmlspanspan-idstaticcontentclearxmlspanstaticcontentclearxml"></a><span id="staticcontentclear.xml"></span><span id="STATICCONTENTCLEAR.XML"></span>staticContentClear.xml


```xml
<?xml version="1.0" encoding="UTF-8"?>
<appcmd>
    <CONFIG CONFIG.SECTION="system.webServer/staticContent"                  path="MACHINE/WEBROOT/APPHOST">
        <system.webServer-staticContent>
            <clear />
        </system.webServer-staticContent>
    </CONFIG>
```

## <a name="span-idtestingthesymproxyinstallationspanspan-idtestingthesymproxyinstallationspanspan-idtestingthesymproxyinstallationspantesting-the-symproxy-installation"></a><span id="Testing_the_SymProxy_Installation_"></span><span id="testing_the_symproxy_installation_"></span><span id="TESTING_THE_SYMPROXY_INSTALLATION_"></span>SymProxy インストールのテスト


システムは、取得、ファイルを提供する準備完了になります。 これをテストするには、iisreset.exe を使用して、IISAdmin サービスを再起動することによって開始します。 これには、現在の IIS と SymProxy 構成で、ISAPI フィルターが再読み込みします。

このシンボル パスを使用するデバッガーを構成します。

```dbgcmd
srv*\\MachineName\Symbols*https://MachineName/Symbols
```

場合*MissTimeout*が有効になっている (これを 300 秒に既定で設定)、くらい高速で実行、2 回目の結果 .reload/f コマンドを 2 回実行する必要があります。

参照されている Pdb の場所を表示するには、lm (モジュールの一覧) のコマンドを使用します。 Pdb へのパスが始まります\\ \\MachineName\\シンボル。

Web サイト ディレクトリの参照が有効になっている場合を参照 https://MachineName/Symbolsにキャッシュされているファイルを参照してください。

パフォーマンス モニターを開くし、シンボルのプロキシのカウンターを表示します。

イベント ビューアーを開き、microsoft\\Windows\\SymProxy イベント。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SymProxy をインストールします。](installing-symproxy.md)

 

 






