---
title: 一般リリースのためのカーネル ドライバーへの構成証明署名
author: DOMARS
redirect_url: https://msdn.microsoft.com/library/windows/hardware/mt786448
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8ce89f77d3cba335aac24272226fed959a1e5bf
ms.sourcegitcommit: 4184cb3bb6737762b2768cd8b9b2233297fc64cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74820389"
---
# <a name="attestation-signing-a-kernel-driver-for-public-release"></a>一般リリースのためのカーネル ドライバーへの構成証明署名

このトピックでは、Windows ハードウェア デベロッパー センター ダッシュボード Web ポータルを利用し、構成証明署名を使ってドライバーに署名する方法について説明します。

**注**  構成証明署名には次の特徴があります。

 - 構成証明署名は、Windows 10 デスクトップのカーネル モード ドライバーとユーザー モード ドライバーをサポートしています。 Windows 10 では、ユーザー モード ドライバーは Microsoft による署名を必要としませんが、ユーザー モード ドライバーとカーネル モード ドライバーの両方で同じ構成証明プロセスを使うことができます。
 - 構成証明署名では、EV 証明書を使ってハードウェア デベロッパー センター ダッシュボードにドライバーを提出する必要があります。
 - 構成証明署名されたドライバーは、Windows 10 および Windows Server 2016 以降で動作します。 それより前のバージョンの Windows (Windows 8.1 や Windows 7 など) では機能しません。




## <a name="span-idattestation_signing_a_kernel_mode_driverspanspan-idattestation_signing_a_kernel_mode_driverspanspan-idattestation_signing_a_kernel_mode_driverspanattestation-signing-a-kernel-mode-driver"></a><span id="Attestation_Signing_a_Kernel_Mode_Driver"></span><span id="attestation_signing_a_kernel_mode_driver"></span><span id="ATTESTATION_SIGNING_A_KERNEL_MODE_DRIVER"></span>カーネル モード ドライバーへの構成証明署名


カーネル モード ドライバーに構成証明署名するには、次の手順を実行します。

1. EV コード署名証明書を取得する
2. Windows ハードウェア ダッシュボード サービスに会社を登録する
3. Windows Driver Kit をダウンロードしてインストールする
4. CAB ファイル提出を作成する
5. EV 証明書を使って CAB ファイル申請に署名する
6. ハードウェア デベロッパー センター ダッシュボードを使って、EV 署名された CAB ファイルを提出する
7. ドライバーが正しく署名されていることを検証する
8. デスクトップ用 Windows 10 でドライバーをテストする <span id="Acquire_an__EV_Code_Signing_Certificate"></span><span id="acquire_an__ev_code_signing_certificate"></span><span id="ACQUIRE_AN__EV_CODE_SIGNING_CERTIFICATE"></span>EV コード署名証明書を取得する


署名されるバイナリ ファイルをダッシュボードを使って提出する前に、デジタル情報を保護するための拡張検証 (EV) コード署名証明書を取得する必要があります。 この証明書は、提出するコードに対する会社の所有権を確立するための公認されている標準です。 .exe、.cab、.dll、.ocx、.msi、.xpi、.xap ファイルなどの PE バイナリにデジタル署名できます。

「[コード署名証明書の取得](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)」で説明されているプロセスに従って、必要な EV コード署名証明書を取得してください。

## <a name="span-idregister_your_company_for_windows_hardware_dashboard_servicesspanspan-idregister_your_company_for_windows_hardware_dashboard_servicesspanspan-idregister_your_company_for_windows_hardware_dashboard_servicesspanregister-your-company-for-windows-hardware-dashboard-services"></a><span id="Register_your_company_for_Windows_Hardware_Dashboard_Services"></span><span id="register_your_company_for_windows_hardware_dashboard_services"></span><span id="REGISTER_YOUR_COMPANY_FOR_WINDOWS_HARDWARE_DASHBOARD_SERVICES"></span>Windows ハードウェア ダッシュボード サービスに会社を登録する


ハードウェア デベロッパー センター ダッシュボードを使うと、ハードウェア認定を受けるためにデバイスとアプリを認定することができます。 ハードウェア デベロッパー センター ダッシュボードにアクセスするには、会社を登録し、コード署名証明書を取得する必要があります。

「[サインインする前に](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)」で説明されているプロセスに従って、ダッシュボードで必要となるアカウントをセットアップしてください。

## <a name="span-id_download_and_install_the_windows_driver_kitspanspan-id_download_and_install_the_windows_driver_kitspanspan-id_download_and_install_the_windows_driver_kitspan-download-and-install-the-windows-driver-kit"></a><span id="_Download_and_install_the_Windows_Driver_Kit"></span><span id="_download_and_install_the_windows_driver_kit"></span><span id="_DOWNLOAD_AND_INSTALL_THE_WINDOWS_DRIVER_KIT"></span>Windows Driver Kit をダウンロードしてインストールする


バイナリ ファイルへの署名に使うツールにアクセスするために、Windows Driver Kit (WDK) をダウンロードしてインストールする必要があります。

「[Windows 10 用のキットとツールのダウンロード](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)」で説明されているプロセスに従って、WDK をダウンロードしインストールしてください。

## <a name="span-idcreate_a_cab_files_submissionspanspan-idcreate_a_cab_files_submissionspanspan-idcreate_a_cab_files_submissionspancreate-a-cab-files-submission"></a><span id="Create_a_CAB_Files_Submission"></span><span id="create_a_cab_files_submission"></span><span id="CREATE_A_CAB_FILES_SUBMISSION"></span>CAB ファイルの申請を作成する


ダッシュボード用に CAB ファイル提出を作成するには、次の手順を実行します。

1. 署名のために提出するバイナリを 1 つのディレクトリにまとめます。 この例では、C:\\Echo を使います。 ここで説明されている手順では、GitHub の次の場所で利用可能な Echo ドライバーを参照します。

[https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf/driver/AutoSync](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf/driver/AutoSync)

  一般的な CAB ファイル提出には、以下のものが含まれます。

  -   ドライバー自体 (Echo.sys など)。
  -   ドライバー INF ファイル。署名プロセスを容易に実行するために、ダッシュボードで使われます。
  -   カタログ .CAT ファイルは必要ありません。 Microsoft では、カタログ ファイルを再生成し、提出されたカタログ ファイルを置き換えます。 Microsoft が提供する代替カタログも署名されています。

2. MakeCab.exe を使って DDF ファイルを処理し、CAB ファイルを作成します。

   管理者としてコマンド プロンプト ウィンドウを開きます。 次のコマンドを入力し、MakeCab のオプションを表示します。

   MakeCab /?

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; MakeCab /?
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
    /V[n]          Verbosity level (1..3).</code></pre></td>
   </tr>
   </tbody>
   </table>

3. CAB ファイルの DDF 入力ファイルを準備します。 ここで使う Echo ドライバーの場合は、次のようになります。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>; *** Echo.ddf example ***
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
   ; Specify file name for new cab file
   .Set CabinetNameTemplate=Echo.cab
   ; Specify the subdirectory for the files.  
   ; Your cab file should not have files at the root level, 
   ; and each driver package must be in a separate subfolder.
   .Set DestinationDir=Echo
   ; Specify files to be included in cab file
   C:\Echo\Echo.Inf
   C:\Echo\Echo.Sys</code></pre></td>
   </tr>
   </tbody>
   </table>

   **注**  CAB ファイル内のすべてのドライバー フォルダーは、同じアーキテクチャのセットをサポートする必要があります。たとえば、すべてのドライバーが x86 であるか、x64 であることが必要になります。また、x86 と x64 の両方をサポートしていることが必要になることもあります。

4. makecab ユーティリティを呼び出し、/f オプションを使って DDF ファイルを入力として指定します。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; MakeCab /f "C:\Echo\Echo.ddf</code></pre></td>
   </tr>
   </tbody>
   </table>

   makecab の出力には、例 2 で作成したキャビネット ファイル内のファイルの数が表示されます。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; MakeCab /f Echo.ddf
   Cabinet Maker - Lossless Data Compression Tool

   17,682 bytes in 2 files
   Total files:              2
   Bytes before:        17,682
   Bytes after:          7,374
   After/Before:            41.70% compression
   Time:                     0.20 seconds ( 0 hr  0 min  0.20 sec)
   Throughput:              86.77 Kb/second</code></pre></td>
   </tr>
   </tbody>
   </table>

5. Disk1 サブディレクトリにある CAB ファイルを探します。 エクスプローラーで CAB ファイルをクリックすると、必要なファイルが含まれているかどうかを確認できます。

## <a name="span-idsign_the_submission_cab_file__with_your_ev_certspanspan-idsign_the_submission_cab_file__with_your_ev_certspanspan-idsign_the_submission_cab_file__with_your_ev_certspansign-the-submission-cab-file-with-your-ev-cert"></a><span id="Sign_the_Submission_Cab_File__with_your_EV_Cert"></span><span id="sign_the_submission_cab_file__with_your_ev_cert"></span><span id="SIGN_THE_SUBMISSION_CAB_FILE__WITH_YOUR_EV_CERT"></span>EV 証明書を使って CAB ファイル提出に署名する


1. EV 証明書プロバイダーで推奨されるプロセスに従い、EV 証明書を使って CAB ファイルに署名します。たとえば、signtool を使う場合があります。また、Verisign を利用しているときは、タイムスタンプ サーバーを指定する場合もあります。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; SignTool sign /v /s MY /n "Subject Name of the Signing Certificate" /t http://timestamp.digicert.com "C:\Echo\Disk1\Echo.cab"</code></pre></td>
   </tr>
   </tbody>
   </table>

   **注**  業界のベスト プラクティスに従って、EV 証明書の署名プロセスのセキュリティを管理します。



## <a name="span-idsubmit_the_ev_signed_cab_file_using_the__windows_hardware_developer_center_dashboardspanspan-idsubmit_the_ev_signed_cab_file_using_the__windows_hardware_developer_center_dashboardspanspan-idsubmit_the_ev_signed_cab_file_using_the__windows_hardware_developer_center_dashboardspansubmit-the-ev-signed-cab-file-using-the-hardware-dev-center-dashboard"></a><span id="Submit_the_EV_signed_Cab_file_using_the__Windows_Hardware_Developer_Center_Dashboard"></span><span id="submit_the_ev_signed_cab_file_using_the__windows_hardware_developer_center_dashboard"></span><span id="SUBMIT_THE_EV_SIGNED_CAB_FILE_USING_THE__WINDOWS_HARDWARE_DEVELOPER_CENTER_DASHBOARD"></span>ハードウェア デベロッパー センター ダッシュボードを使用して、EV で署名された CAB ファイルを申請する


1. ハードウェア デベロッパー センター ダッシュボードを使って、EV 署名された CAB ファイルを提出します。 詳しくは、「[ドライバーの署名のプロパティ](driver-signing-properties.md)」と「[ファイル署名サービス](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)」をご覧ください。

提出プロセスの一環として、提出に含まれるすべてのドライバーがサポートするアーキテクチャを指定します。 チェック ボックスで 3 つのオプションを利用できます。

-   x86
-   x64
-   x86 または x64

CAB ファイル内のすべてのドライバー フォルダーは、同じアーキテクチャのセットをサポートする必要があります。たとえば、すべてのドライバーが x86 であるか、x64 であることが必要になります。また、x86 と x64 の両方をサポートしていることが必要になることもあります。 ドライバーが異なる組み合わせのアーキテクチャをサポートしている場合は、個別の提出を作成してください。

ユニバーサル ドライバーを提出するかどうかも指定します。 詳しくは、「[ユニバーサル Windows ドライバーの概要](getting-started-with-universal-drivers.md)」をご覧ください。

次のスクリーン ショットは、署名用に Echo ドライバーを提出するためのオプションを示しています。

![ドライバーの署名の提出オプション](images/attestation-driver-signing-submission-dashboard.png)

2. 署名プロセスが完了したら、ハードウェア デベロッパー センター ダッシュボードから署名されたドライバーをダウンロードします。
   ## <a name="span-idvalidate_that_the_driver_was_properly_signedspanspan-idvalidate_that_the_driver_was_properly_signedspanspan-idvalidate_that_the_driver_was_properly_signedspanvalidate-that-the-driver-was-properly-signed"></a><span id="Validate_that_the_driver_was_properly_signed"></span><span id="validate_that_the_driver_was_properly_signed"></span><span id="VALIDATE_THAT_THE_DRIVER_WAS_PROPERLY_SIGNED"></span>ドライバーが正しく署名されていることを検証する


次の手順を実行して、ドライバーが正しく署名されていることを検証します。

1. 申請ファイルをダウンロードした後で、ドライバー ファイルを抽出します。

2. 管理者としてコマンド プロンプト ウィンドウを開きます。 次のコマンドを入力して、ドライバーが適切に署名されていることを確認します。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; SignTool verify Echo.Sys</code></pre></td>
   </tr>
   </tbody>
   </table>

3. 追加の情報を表示し、Signtool で複数の署名に基づいてファイル内のすべての署名を確認するには、次のように入力します。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; SignTool verify /pa /ph /v /d Echo.Sys</code></pre></td>
   </tr>
   </tbody>
   </table>

4. ドライバーの EKU を確認するには、次の手順を実行します。

   a. エクスプローラーを開き、バイナリ ファイルを探します。 そのファイルを右クリックし、 **[プロパティ]** を選びます。

   b. **[デジタル署名]** タブの [署名の一覧] で、示されている項目を選びます。

   c. **[詳細]** ボタンを選び、 **[証明書の表示]** を選びます。

   d. **[詳細]** タブで、 **[拡張キー使用法]** フィールドを選びます。

ダッシュ ボードでドライバーが再署名される場合は、次のプロセスが実行されます。

-   Microsoft SHA2 埋め込み署名を追加します。
-   ドライバーのバイナリが顧客によって独自の証明書を使って埋め込み署名されている場合、それらの署名は上書きされません。
-   新しいカタログ ファイルを作成し、SHA2 Microsoft 証明書を使って署名します。 顧客が提供した既存のカタログは、このカタログに置き換えられます。

## <a name="span-idtest_your_driver_on_windows_10_for_desktopspanspan-idtest_your_driver_on_windows_10_for_desktopspanspan-idtest_your_driver_on_windows_10_for_desktopspantest-your-driver-on-windows-10-for-desktop"></a><span id="Test_your_driver_on_Windows_10_for_Desktop"></span><span id="test_your_driver_on_windows_10_for_desktop"></span><span id="TEST_YOUR_DRIVER_ON_WINDOWS_10_FOR_DESKTOP"></span>デスクトップ用 Windows 10 でドライバーをテストする


次の手順に従って、サンプル ドライバーをインストールします。

1. デバイス マネージャーを開き、コンピューター アイコンを右クリックして、[レガシ ハードウェアの追加] を選びます。 指示に従ってドライバーのインストールを完了します。

2. または、管理者としてコマンド プロンプト ウィンドウを開き、devcon を使ってドライバーをインストールします。 ドライバー パッケージのフォルダーに移動し、次のコマンドを入力します。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; devcon install echo.inf root\ECHO</code></pre></td>
   </tr>
   </tbody>
   </table>

3. ドライバーのインストール プロセスで、"ドライバー ソフトウェアの発行元を検証できません" というメッセージが表示されないことを確認します。 [Windows セキュリティ] ダイアログ ボックス

## <a name="span-idcreate_a_multiple_driver_submissionspanspan-idcreate_a_multiple_driver_submissionspanspan-idcreate_a_multiple_driver_submissionspancreate-a-multiple-driver-submission"></a><span id="Create_a_Multiple_Driver_Submission"></span><span id="create_a_multiple_driver_submission"></span><span id="CREATE_A_MULTIPLE_DRIVER_SUBMISSION"></span>複数のドライバーの申請を作成する


一度に複数のドライバーを提出するには、次に示すようにドライバーごとにサブディレクトリを作成します。

![CAB 提出のディレクトリ構造](images/b-wes-driversigning-v4.png)

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

ドライバー ファイルの署名、提出、テストを行うには、既に説明した手順に従ってください。
## 



## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ドライバーへの署名](signing-a-driver.md)





