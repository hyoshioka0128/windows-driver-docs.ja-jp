---
title: 一般リリースのためのカーネル ドライバーへの構成証明署名
description: このトピックでは、構成証明署名を使ってドライバーに署名する方法について説明します。
ms.assetid: A292B15D-37FD-407E-998C-728D9423E712
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcf71a3bf01640c99fadd035e5ea41b6ea3ade91
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "78180970"
---
# <a name="attestation-signing-a-kernel-driver-for-public-release"></a>一般リリースのためのカーネル ドライバーへの構成証明署名

このトピックでは、構成証明署名を使ってドライバーに署名する方法について説明します。

> [!Note]
> 構成証明署名には次の特徴があります。
> - 構成証明署名は、Windows 10 デスクトップのカーネル モード ドライバーとユーザー モード ドライバーをサポートしています。 Windows 10 では、ユーザー モード ドライバーは Microsoft による署名を必要としませんが、ユーザー モード ドライバーとカーネル モード ドライバーの両方で同じ構成証明プロセスを使うことができます。
> - 構成証明署名は、**ELAM** または **Windows Hello** PE バイナリについて、適切な PE レベルを返しません。  これらは、追加の署名属性を受け取るために、テストして .hlkx パッケージとして提出する必要があります。
> - 構成証明署名では、EV 証明書を使ってパートナー センターでドライバーを申請する必要があります。
> - **構成証明署名されたドライバーは、Windows 10 で動作します。Windows 8.1 や Windows 7 など、より古いバージョンの Windows では動作せず、Windows Server 2016 以降ではサポートされていません。サポート ポリシーの詳細については、[Windows の構成証明プロセスを使用して署名されたサードパーティ製のカーネルレベル ソフトウェアのサポート ポリシー](https://support.microsoft.com/help/4519013/support-policy-3rd-party-kernel-level-attestation-signed-software)** をご覧ください。
> - 構成証明署名を行うには、ドライバー フォルダー名に特殊文字や UNC ファイル共有パスを使用せず、 40 文字未満のフォルダー名にする必要があります。

## <a name="attestation-signing-a-kernel-mode-driver"></a>カーネル モード ドライバーへの構成証明署名

カーネル モード ドライバーに構成証明署名するには、次の手順を実行します。

1. EV コード署名証明書を取得する
2. パートナー センターに会社を登録する
3. Windows Driver Kit をダウンロードしてインストールする
4. CAB ファイル提出を作成する
5. EV 証明書を使って CAB ファイル申請に署名する
6. パートナー センターを使って、EV 署名された CAB ファイルを提出する
7. ドライバーが正しく署名されていることを検証する
8. デスクトップ用 Windows 10 でドライバーをテストする

## <a name="acquire-an-ev-code-signing-certificate"></a>EV コード署名証明書を取得する

署名対象のバイナリをダッシュボードに提出する前に、デジタル情報を保護するための[拡張検証 (EV) コード署名証明書](get-a-code-signing-certificate.md)を取得する必要があります。 EV 証明書は、提出するコードに対する会社の所有権を確立するための公認されている標準です。

## <a name="allowable-pe-signatures-and-binaries"></a>許容される PE 署名とバイナリ

次の PE レベルとバイナリは、構成証明を介して処理できます。

- **PeTrust**
- **DrmLevel**
- **HAL**
- .exe
- .cab
- .dll
- .ocx
- .msi
- .xpi
- .xap

## <a name="register-your-company-for-partner-center-services"></a>パートナー センター サービスに会社を登録する

パートナー センターでドライバーに署名するには、まず組織を登録し、コード署名証明書を取得する必要があります。

「[ハードウェア プログラムの登録](register-for-the-hardware-program.md)」に記載されているプロセスに従って、ハードウェア ダッシュボードで使用するアカウントをセットアップします。

## <a name="download-and-install-the-windows-driver-kit"></a>Windows Driver Kit をダウンロードしてインストールする

ドライバーのバイナリ ファイルへの署名に使うツールにアクセスするために、Windows Driver Kit (WDK) をダウンロードしてインストールする必要があります。

「[Windows 10 用のキットとツールのダウンロード](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)」で説明されているプロセスに従って、WDK をダウンロードしインストールしてください。

## <a name="create-a-cab-files-submission"></a>CAB ファイル提出を作成する

ダッシュボードで申請できる CAB ファイルを作成するには、次の手順を実行します。

1. 署名のために提出するバイナリを 1 つのディレクトリにまとめます。 この例では、C:\\Echo を使います。 ここで説明する手順では、GitHub で入手可能な [Echo ドライバー サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf/driver/AutoSync)を参照します。

一般的な CAB ファイル申請には、以下のものが含まれます。

- ドライバー自体 (Echo.sys など)。
- ドライバー INF ファイル。署名プロセスを容易に実行するために、ダッシュボードで使われます。
- シンボル ファイル。デバッグ情報用に使用されます。 たとえば、Echo.pdb などです。
- カタログ .CAT ファイルは必須で、会社の検証用にのみ使用されます。 Microsoft では、カタログ ファイルを再生成し、提出されたカタログ ファイルを置き換えます。

  > [!NOTE]
  > CAB ファイル内の各ドライバー フォルダーは、同じアーキテクチャのセットをサポートする必要があります。 たとえば、これらが x86 または x64 をサポートしているか、x86 と x64 の両方をサポートしている必要があります。
  > - ドライバーの場所を参照する際には、UNC ファイル共有パス (\\\server\share) は使わないでください。  CAB を検証するには、マップ済みのドライブ文字を使用する必要があります。 

2. MakeCab.exe を使って DDF ファイルを処理し、CAB ファイルを作成します。

管理者としてコマンド プロンプト ウィンドウを開きます。 次のコマンドを入力し、MakeCab のオプションを表示します。

MakeCab /?

```cpp
C:\Echo> MakeCab /?
Cabinet Maker - Lossless Data Compression Tool

MAKECAB [/V[n]] [/D var=value ...] [/L dir] source [destination]
MAKECAB [/V[n]] [/D var=value ...] /F directive_file [...]

  source         File to compress.
  destination    File name to give compressed file.  If omitted, the
                 last character of the source file name is replaced
                 with an underscore (_) and used as the destination.
  /F directives  A file with MakeCAB directives (may be repeated). Refer to
                 Microsoft Cabinet SDK for information on directive_file.
  /D var=value   Defines variable with specified value.
  /L dir         Location to place destination (default is current directory).
  /V[n]          Verbosity level (1..3).
```

3. CAB ファイルの DDF 入力ファイルを準備します。 ここで使う Echo ドライバーの場合は、次のようになります。

```cpp
;*** Echo.ddf example
;
.OPTION EXPLICIT     ; Generate errors
.Set CabinetFileCountThreshold=0
.Set FolderFileCountThreshold=0
.Set FolderSizeThreshold=0
.Set MaxCabinetSize=0
.Set MaxDiskFileCount=0
.Set MaxDiskSize=0
.Set CompressionType=MSZIP
.Set Cabinet=on
.Set Compress=on
;Specify file name for new cab file
.Set CabinetNameTemplate=Echo.cab
; Specify the subdirectory for the files.  
; Your cab file should not have files at the root level,
; and each driver package must be in a separate subfolder.
.Set DestinationDir=Echo
;Specify files to be included in cab file
C:\Echo\Echo.Inf
C:\Echo\Echo.Sys
```
 

4. makecab ユーティリティを呼び出し、/f オプションを使って DDF ファイルを入力として指定します。

```cpp
C:\Echo> MakeCab /f "C:\Echo\Echo.ddf
```

makecab の出力には、例 2 で作成したキャビネット ファイル内のファイルの数が表示されます。

```cpp
C:\Echo> MakeCab /f Echo.ddf
Cabinet Maker - Lossless Data Compression Tool

17,682 bytes in 2 files
Total files:              2
Bytes before:        17,682
Bytes after:          7,374
After/Before:            41.70% compression
Time:                     0.20 seconds ( 0 hr  0 min  0.20 sec)
Throughput:              86.77 Kb/second
```

5. Disk1 サブディレクトリにある CAB ファイルを探します。 エクスプローラーで CAB ファイルをクリックすると、必要なファイルが含まれているかどうかを確認できます。

## <a name="sign-the-submission-cab-file-with-your-ev-certificate"></a>EV 証明書を使って申請の CAB ファイルに署名する

1. EV 証明書プロバイダーで推奨されるプロセスに従い、EV 証明書を使って CAB ファイルに署名します。たとえば、SHA256 Certificate/Digest Algorithm/Timestamp を使用して .CAB に署名するには、次のようにします  

```cpp
C:\Echo> SignTool sign /ac "C:\MyEVCert.cer" /s MY /n "Company Name" /fd sha256 /tr http://sha256timestamp.ws.symantec.com/sha256/timestamp /td sha256 /v "C:\Echo\Disk1\Echo.cab"
```

> [!IMPORTANT]
> 業界のベスト プラクティスに従って、EV コード署名プロセスのセキュリティを管理します。

## <a name="submit-the-ev-signed-cab-file-using-the-partner-center"></a>パートナー センターを使って、EV 署名された CAB ファイルを提出する

1. パートナー センターを使って、EV 署名された CAB ファイルを提出します。 詳しくは、「[ドライバーの署名のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/develop/driver-signing-properties)」をご覧ください。

   * 構成証明の申請プロセスの一環として、以下で強調表示されているどの [テスト署名] ボックスもオンにしないでください。  これらはオフのままにしておきます。

   * 次のスクリーン ショットは、署名用に Echo ドライバーを提出するためのオプションを示しています。
    ![署名用に Echo ドライバーを提出するためのオプションを示すスクリーン ショット](images/Attestation-Flow.PNG)

2. 署名プロセスが完了したら、ハードウェア ダッシュボードから署名されたドライバーをダウンロードします。

## <a name="validate-that-the-driver-was-properly-signed"></a>ドライバーが正しく署名されていることを検証する

次の手順を実行して、ドライバーに正しく署名されていることを確認します。

1. 申請ファイルをダウンロードした後で、ドライバー ファイルを抽出します。

2. 管理者としてコマンド プロンプト ウィンドウを開きます。 次のコマンドを入力して、ドライバーが適切に署名されていることを確認します。

```cpp
C:\Echo> SignTool verify Echo.Sys
```

3. 追加の情報を表示し、signtool で複数の署名に基づいてファイル内のすべての署名を確認するには、次のように入力します。

```cpp
C:\Echo> SignTool verify /pa /ph /v /d Echo.Sys
```

4. ドライバーの EKU を確認するには、次の手順を実行します。
a。 エクスプローラーを開き、バイナリ ファイルを探します。 そのファイルを右クリックし、 **[プロパティ]** を選びます。
b. **[デジタル署名]** タブの [署名の一覧] で、示されている項目を選びます。
c. **[詳細]** ボタンを選び、 **[証明書の表示]** を選びます。
d. **[詳細]** タブで、 **[拡張キー使用法]** フィールドを選びます。
ダッシュ ボードでドライバーが再署名される場合は、次のプロセスが実行されます。

- Microsoft SHA2 埋め込み署名を追加します。
- ドライバーのバイナリが顧客によって独自の証明書を使って埋め込み署名されている場合、それらの署名は上書きされません。
- 新しいカタログ ファイルを作成し、SHA2 Microsoft 証明書を使って署名します。 顧客が提供した既存のカタログは、このカタログに置き換えられます。

## <a name="test-your-driver-on-windows-10"></a>Windows 10 でドライバーをテストする

次の手順に従って、サンプル ドライバーをインストールします。

1. デバイス マネージャーを開き、コンピューター アイコンを右クリックして、[レガシ ハードウェアの追加] を選びます。 指示に従ってドライバーのインストールを完了します。

2. または、管理者としてコマンド プロンプト ウィンドウを開き、devcon を使ってドライバーをインストールします。 ドライバー パッケージのフォルダーに移動し、次のコマンドを入力します。

```cpp
C:\Echo> devcon install echo.inf root\ECHO
```

3. ドライバーのインストール プロセスで、"ドライバー ソフトウェアの発行元を検証できません" というメッセージが表示されないことを確認します。 [Windows セキュリティ] ダイアログ ボックス

## <a name="create-a-submission-with-multiple-drivers"></a>複数のドライバーで申請を作成する

一度に複数のドライバーを提出するには、次に示すようにドライバーごとにサブディレクトリを作成します。

![ドライバー署名のディレクトリ構造の例を示す画像。](images/multiple-driversigning.png)

サブディレクトリを参照する CAB ファイルの DDF 入力ファイルを準備します。 次のようになります。

```cpp
;*** Submission.ddf multiple driver example
;
.OPTION EXPLICIT     ; Generate errors
.Set CabinetFileCountThreshold=0
.Set FolderFileCountThreshold=0
.Set FolderSizeThreshold=0
.Set MaxCabinetSize=0
.Set MaxDiskFileCount=0
.Set MaxDiskSize=0
.Set CompressionType=MSZIP
.Set Cabinet=on
.Set Compress=on
;Specify file name for new cab file
.Set CabinetNameTemplate=Echo.cab
;Specify files to be included in cab file
; First Driver
.Set DestinationDir=DriverPackage1
C:\DriverFiles\DriverPackage1\Driver1.sys
C:\DriverFiles\DriverPackage1\Driver1.inf
; Second driver
.Set DestinationDir=DriverPackage2
C:\DriverFiles\DriverPackage2\Driver2.sys
C:\DriverFiles\DriverPackage2\Driver2.inf
```

この手順に従い、申請する他のドライバー ファイルの署名、提出、テストも行うことができます。
